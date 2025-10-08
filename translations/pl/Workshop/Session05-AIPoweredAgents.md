<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "aee170a832b8870fc6eea546aa544bdb",
  "translation_date": "2025-10-08T21:41:57+00:00",
  "source_file": "Workshop/Session05-AIPoweredAgents.md",
  "language_code": "pl"
}
-->
# Sesja 5: Szybkie tworzenie agentów AI z Foundry Local

## Abstrakt

Projektuj i organizuj wielorole agentów AI, korzystając z niskolatencyjnego, chroniącego prywatność środowiska wykonawczego Foundry Local. Zdefiniujesz role agentów, strategie pamięci, wzorce wywoływania narzędzi oraz grafy wykonawcze. Sesja wprowadza wzorce szkieletowe, które można rozszerzyć za pomocą Chainlit lub LangGraph. Projekt startowy rozszerza istniejący przykład architektury agenta o trwałość pamięci i haki ewaluacyjne.

## Cele nauki

- **Definiowanie ról**: Podpowiedzi systemowe i granice możliwości
- **Implementacja pamięci**: Krótkoterminowa (rozmowa), długoterminowa (wektor / plik), tymczasowe notatniki
- **Szkieletowanie przepływów pracy**: Kroki agentów sekwencyjne, rozgałęzione i równoległe
- **Integracja narzędzi**: Lekki wzorzec wywoływania funkcji narzędziowych
- **Ewaluacja**: Podstawowe śledzenie + ocena wyników oparta na rubryce

## Wymagania wstępne

- Ukończone sesje 1–4
- Python z `foundry-local-sdk`, `openai`, opcjonalnie `chainlit`
- Modele lokalne uruchomione (przynajmniej `phi-4-mini`)

### Fragment środowiska wieloplatformowego

Windows:
```powershell
py -m venv .venv
 .\.venv\Scripts\Activate.ps1
pip install --upgrade pip
pip install foundry-local-sdk openai
```

macOS:
```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install foundry-local-sdk openai
```

Jeśli uruchamiasz agentów z macOS na zdalnym hostingu Windows:
```bash
export FOUNDRY_LOCAL_ENDPOINT=http://<windows-host>:5273/v1
```


## Przebieg demonstracji (30 min)

### 1. Definiowanie ról agentów i pamięci (7 min)

Utwórz `samples/05-agents/agents_core.py`:

```python
#!/usr/bin/env python3
"""Minimal multi-agent scaffolding using Foundry Local (OpenAI-compatible)."""
from openai import OpenAI
from dataclasses import dataclass, field
from typing import List, Dict, Any, Callable
import time, json

client = OpenAI(base_url="http://localhost:5273/v1", api_key="not-needed")

@dataclass
class AgentMessage:
    role: str
    content: str
    meta: Dict[str, Any] = field(default_factory=dict)

@dataclass
class Agent:
    name: str
    system_prompt: str
    tools: Dict[str, Callable] = field(default_factory=dict)
    memory: List[AgentMessage] = field(default_factory=list)

    def remember(self, role: str, content: str, **meta):
        self.memory.append(AgentMessage(role=role, content=content, meta=meta))

    def context(self, window:int=8):
        recent = self.memory[-window:]
        msgs = [ {"role": "system", "content": self.system_prompt}]
        msgs += [ {"role": m.role, "content": m.content} for m in recent ]
        return msgs

    def act(self, user_input: str, model: str = "phi-4-mini", temperature: float=0.4):
        self.remember("user", user_input)
        resp = client.chat.completions.create(
            model=model,
            messages=self.context() + [{"role": "user", "content": user_input}],
            temperature=temperature,
            max_tokens=400
        )
        answer = resp.choices[0].message.content
        self.remember("assistant", answer, model=model)
        return answer

researcher = Agent(
    name="Researcher",
    system_prompt="You gather factual, structured insights concisely."
)
writer = Agent(
    name="Writer",
    system_prompt="You rewrite content for clarity and engagement while preserving facts."
)

def demo():
    q = "Explain why edge inference matters for privacy and latency."
    r = researcher.act(q)
    print("Researcher ->", r[:200], "...\n")
    w = writer.act(f"Rewrite more user-friendly: {r}")
    print("Writer ->", w[:200], "...")

if __name__ == "__main__":
    demo()
```


### 2. Wzorzec szkieletowania CLI (3 min)

```powershell
python samples/05-agents/agents_core.py
```


### 3. Dodanie wywoływania narzędzi (7 min)

Rozszerz za pomocą `samples/05-agents/tools.py`:

```python
from datetime import datetime
import math, json

def tool_time(_:str)->str:
    return f"Current UTC time: {datetime.utcnow().isoformat()}"

def tool_estimate_tokens(text:str)->str:
    approx = len(text.split()) * 1.35
    return f"Estimated tokens ~ {int(approx)}"

TOOLS = {
    "get_time": tool_time,
    "estimate_tokens": tool_estimate_tokens
}
```

Zmodyfikuj `agents_core.py`, aby umożliwić prostą składnię narzędzi: użytkownik wpisuje `#tool:get_time`, a agent rozwija wynik narzędzia w kontekście przed generowaniem.

### 4. Zorganizowany przepływ pracy (6 min)

Utwórz `samples/05-agents/orchestrator.py`:

```python
from agents_core import researcher, writer, Agent
from tools import TOOLS
from openai import OpenAI

client = OpenAI(base_url="http://localhost:5273/v1", api_key="not-needed")

def inject_tools(agent: Agent, user_input: str) -> str:
    if user_input.startswith('#tool:'):
        name = user_input.split(':',1)[1].strip()
        if name in TOOLS:
            out = TOOLS[name](../../../Workshop/"")
            agent.remember("tool", out, tool=name)
            return f"Tool[{name}] => {out}"
    return None

def pipeline(question: str):
    tool_note = inject_tools(researcher, '#tool:get_time')
    r = researcher.act(question)
    w = writer.act(f"Improve readability:\n{r}\nAdd a friendly summary line.")
    return {"raw": r, "refined": w, "tool": tool_note}

if __name__ == '__main__':
    result = pipeline("List three concrete benefits of local SLM inference for regulated industries.")
    for k,v in result.items():
        print(f"== {k.upper()} ==\n{v}\n")
```


### 5. Projekt startowy: Rozszerzenie `05-agent-architecture` (7 min)

Dodaj:
1. Warstwę trwałej pamięci (np. dopisywanie linii JSON rozmów)
2. Prosta rubryka ewaluacyjna: faktyczność / klarowność / styl
3. Opcjonalny front-end Chainlit (dwie zakładki: rozmowa i ślady)
4. Opcjonalna maszyna stanowa w stylu LangGraph (jeśli dodano zależność) dla decyzji rozgałęzionych

## Lista kontrolna walidacji

```powershell
foundry model run phi-4-mini
python samples/05-agents/orchestrator.py
```

Oczekuj strukturalnego wyniku potoku z notatką o wstrzyknięciu narzędzia.

## Przegląd strategii pamięci

| Warstwa       | Cel                 | Przykład               |
|---------------|---------------------|------------------------|
| Krótkoterminowa | Ciągłość dialogu   | Ostatnie N wiadomości  |
| Epizodyczna    | Przypomnienie sesji | JSON na sesję          |
| Semantyczna    | Długoterminowe wyszukiwanie | Magazyn wektorów podsumowań |
| Notatnik       | Kroki rozumowania  | Wbudowany łańcuch myśli (prywatny) |

## Haki ewaluacyjne (koncepcyjne)

```python
evaluation = {
  "factuality": None,  # manual or heuristic
  "clarity": None,
  "style": None,
  "latency_sec": generation_time,
  "model": model_used
}
```


## Rozwiązywanie problemów

| Problem            | Przyczyna                  | Rozwiązanie                  |
|--------------------|---------------------------|------------------------------|
| Powtarzające się odpowiedzi | Zbyt duże/małe okno kontekstu | Dostosuj parametr okna pamięci |
| Narzędzie nie wywołane | Nieprawidłowa składnia | Użyj formatu `#tool:tool_name` |
| Wolna orkiestracja | Wiele zimnych modeli      | Uruchom wstępne podpowiedzi |

## Źródła

- Foundry Local SDK: https://github.com/microsoft/Foundry-Local/tree/main/sdk/python
- LangGraph (opcjonalna koncepcja): https://github.com/langchain-ai/langgraph
- Chainlit: https://docs.chainlit.io

---

**Czas trwania sesji**: 30 min  
**Poziom trudności**: Zaawansowany

## Przykładowy scenariusz i mapowanie warsztatów

| Skrypt warsztatowy | Scenariusz | Cel | Przykładowa podpowiedź |
|--------------------|------------|-----|------------------------|
| `samples/session05/agents_orchestrator.py` / `notebooks/session05_agents_orchestrator.ipynb` | Bot badawczy wiedzy tworzący podsumowania przyjazne dla kadry kierowniczej | Potok dwóch agentów (badania → redakcja) z opcjonalnymi odrębnymi modelami | Wyjaśnij, dlaczego inferencja na krawędzi jest ważna dla zgodności. |
| (Rozszerzony) koncept `tools.py` | Dodaj narzędzia do szacowania czasu i tokenów | Zademonstruj lekki wzorzec wywoływania narzędzi | #tool:get_time |

### Narracja scenariusza
Zespół ds. dokumentacji zgodności potrzebuje szybkich wewnętrznych streszczeń opartych na lokalnej wiedzy, bez wysyłania szkiców do usług w chmurze. Agent badawczy zbiera zwięzłe faktyczne punkty; agent redakcyjny przepisuje je dla klarowności kierowniczej. Można przypisać odrębne aliasy modeli, aby zoptymalizować opóźnienia (szybki SLM) vs. stylistyczne dopracowanie (większy model tylko w razie potrzeby).

### Przykładowe środowisko wielomodelowe
```powershell
set AGENT_MODEL_PRIMARY=phi-4-mini
set AGENT_MODEL_EDITOR=gpt-oss-20b
python Workshop\samples\session05\agents_orchestrator.py
```


### Struktura śladów (opcjonalna)
```json
{
    "step": 1,
    "agent": "Researcher",
    "latency_ms": 412.3,
    "tokens_in": 22,
    "tokens_out": 168,
    "model": "phi-4-mini"
}
```

Zapisz każdy krok do pliku JSONL w celu późniejszego oceniania rubryki.

### Opcjonalne ulepszenia

| Temat             | Ulepszenie                 | Korzyść                     | Szkic implementacji         |
|-------------------|---------------------------|-----------------------------|-----------------------------|
| Role wielomodelowe | Odrębne modele na agenta (`AGENT_MODEL_PRIMARY`, `AGENT_MODEL_EDITOR`) | Specjalizacja i szybkość   | Wybierz aliasy zmiennych środowiskowych, wywołaj `chat_once` z aliasem dla roli |
| Strukturalne ślady | Ślad JSON każdego aktu (narzędzie, wejście, opóźnienie, tokeny) | Debugowanie i ewaluacja    | Dodaj słownik do listy; zapisz `.jsonl` na końcu |
| Trwałość pamięci   | Kontekst dialogu do ponownego załadowania | Ciągłość sesji             | Zapisz `Agent.memory` do `sessions/<ts>.json` |
| Rejestr narzędzi   | Dynamiczne odkrywanie narzędzi | Rozszerzalność             | Utrzymuj słownik `TOOLS` i introspekcję nazw/opisów |
| Ponowne próby i wycofanie | Solidne długie łańcuchy | Redukcja przejściowych błędów | Owiń `act` w try/except + wykładnicze wycofanie |
| Ocena rubryki      | Automatyczne etykiety jakościowe | Śledzenie ulepszeń         | Drugie wywołanie modelu: "Oceń klarowność 1-5" |
| Pamięć wektorowa   | Semantyczne wyszukiwanie | Bogaty kontekst długoterminowy | Osadź podsumowania, pobierz top-k do wiadomości systemowej |
| Strumieniowe odpowiedzi | Szybsza postrzegana reakcja | Poprawa UX                 | Użyj strumieniowania, gdy dostępne, i wypłucz częściowe tokeny |
| Testy deterministyczne | Kontrola regresji       | Stabilne CI                 | Uruchom z `temperature=0`, ustalonymi nasionami podpowiedzi |
| Rozgałęzienia równoległe | Szybsza eksploracja     | Przepustowość              | Użyj `concurrent.futures` dla niezależnych kroków agenta |

#### Przykład zapisu śladu

```python
trace.append({
    "agent": agent.name,
    "input": prompt,
    "output_tokens": getattr(usage,'completion_tokens',None),
    "latency_ms": round((end-start)*1000,2),
    "tools_used": list(tool_calls)
})
```


#### Prosta podpowiedź ewaluacyjna

```python
score_prompt = f"Rate clarity (1-5) ONLY as a number for this answer:\n{answer}"
rating, _ = chat_once(PRIMARY_ALIAS, messages=[{"role":"user","content":score_prompt}], max_tokens=4, temperature=0)
```

Zapisz pary (`answer`, `rating`), aby zbudować historyczny wykres jakości.

---

**Zastrzeżenie**:  
Ten dokument został przetłumaczony za pomocą usługi tłumaczenia AI [Co-op Translator](https://github.com/Azure/co-op-translator). Chociaż dokładamy wszelkich starań, aby tłumaczenie było precyzyjne, prosimy pamiętać, że automatyczne tłumaczenia mogą zawierać błędy lub nieścisłości. Oryginalny dokument w jego języku źródłowym powinien być uznawany za autorytatywne źródło. W przypadku informacji o kluczowym znaczeniu zaleca się skorzystanie z profesjonalnego tłumaczenia przez człowieka. Nie ponosimy odpowiedzialności za jakiekolwiek nieporozumienia lub błędne interpretacje wynikające z użycia tego tłumaczenia.