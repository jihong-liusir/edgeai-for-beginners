<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "d1b3c0fecfd713c2df903a0633249dc9",
  "translation_date": "2025-10-08T21:39:16+00:00",
  "source_file": "Workshop/Session04-CuttingEdgeModels.md",
  "language_code": "pl"
}
-->
# Sesja 4: Eksploracja Nowoczesnych Modeli – LLM, SLM i Inference na Urządzeniu

## Streszczenie

Porównaj Duże Modele Językowe (LLM) i Małe Modele Językowe (SLM) w scenariuszach lokalnych i chmurowych. Poznaj wzorce wdrożeniowe wykorzystujące przyspieszenie ONNX Runtime, wykonanie WebGPU oraz hybrydowe doświadczenia RAG. W programie demo Chainlit RAG z lokalnym modelem oraz opcjonalna eksploracja OpenWebUI. Zaadaptujesz starter inference WebGPU i ocenisz możliwości oraz kompromisy koszt/wydajność Phi vs GPT-OSS-20B.

## Cele nauki

- **Porównaj** SLM i LLM pod względem opóźnienia, pamięci i jakości
- **Wdróż** modele z ONNXRuntime i (gdzie obsługiwane) WebGPU
- **Uruchom** inference w przeglądarce (interaktywne demo z zachowaniem prywatności)
- **Zintegruj** pipeline Chainlit RAG z lokalnym backendem SLM
- **Oceń** za pomocą lekkich heurystyk jakości i kosztów

## Wymagania wstępne

- Ukończone sesje 1–3
- Zainstalowany `chainlit` (już w `requirements.txt` dla Module08)
- Przeglądarka obsługująca WebGPU (Edge / Chrome najnowsza wersja na Windows 11)
- Działający Foundry Local (`foundry status`)

### Uwagi dotyczące różnych platform

Windows pozostaje głównym środowiskiem docelowym. Dla deweloperów macOS oczekujących na natywne binaria:
1. Uruchom Foundry Local w maszynie wirtualnej Windows 11 (Parallels / UTM) LUB na zdalnej stacji roboczej Windows.
2. Udostępnij usługę (domyślny port 5273) i ustaw na macOS:
```bash
export FOUNDRY_LOCAL_ENDPOINT=http://<windows-host>:5273/v1
```
3. Użyj tych samych kroków dotyczących wirtualnego środowiska Python co w poprzednich sesjach.

Instalacja Chainlit (obie platformy):
```bash
pip install chainlit
```

## Przebieg demo (30 min)

### 1. Porównanie Phi (SLM) vs GPT-OSS-20B (LLM) (6 min)

```powershell
foundry model run phi-4-mini
foundry model run gpt-oss-20b

# Quick capability probes (one-shot non-interactive)
foundry model run phi-4-mini   --prompt "Summarize retrieval augmented generation in 2 sentences."
foundry model run gpt-oss-20b --prompt "Summarize retrieval augmented generation in 2 sentences."

# Basic token / latency test (repeat a few times for intuition)
foundry model run phi-4-mini   --prompt "List 5 creative IoT edge AI ideas."
foundry model run gpt-oss-20b --prompt "List 5 creative IoT edge AI ideas."
```

Śledź: głębokość odpowiedzi, dokładność faktów, bogactwo stylistyczne, opóźnienie.

### 2. Przyspieszenie ONNX Runtime (5 min)

```powershell
foundry config set compute.onnx.enable_gpu true
# Re-run Python benchmark script for quantitative latency / throughput after enabling GPU
#   set BENCH_MODELS=phi-4-mini
#   python Workshop\samples\session03\benchmark_oss_models.py
```

Obserwuj zmiany przepustowości po włączeniu GPU w porównaniu do tylko CPU.

### 3. Inference WebGPU w przeglądarce (6 min)

Zaadaptuj starter `04-webgpu-inference` (utwórz `samples/04-cutting-edge/webgpu_demo.html`):

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Foundry Local WebGPU Demo</title>
  <style>body{font-family:system-ui;margin:2rem;max-width:820px;} textarea{width:100%;height:120px;} pre{background:#111;color:#eee;padding:1rem;} .resp{white-space:pre-wrap;margin-top:1rem;border:1px solid #444;padding:1rem;border-radius:6px;}</style>
</head>
<body>
  <h1>WebGPU Inference (Experimental)</h1>
  <p>Demonstration placeholder for a WebGPU-backed transformer (concept). Replace with actual JS runtime once exposed by Foundry Local or associated runtime libs.</p>
  <textarea id="prompt" placeholder="Enter your prompt..."></textarea>
  <button id="run">Generate</button>
  <div id="out" class="resp"></div>
  <script>
    document.getElementById('run').onclick = async () => {
      const p = document.getElementById('prompt').value.trim();
      if(!p) return;
      document.getElementById('out').textContent = 'Running (simulated)...';
      // Placeholder: in a real implementation you'd call into a WASM/WebGPU pipeline or local gateway endpoint.
      const resp = await fetch('http://localhost:5273/v1/chat/completions', {
        method: 'POST', headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
          model: 'phi-4-mini',
          messages: [ { role: 'user', content: p } ],
          max_tokens: 200, temperature: 0.5
        })
      }).then(r=>r.json()).catch(e=>({error:e.toString()}));
      if(resp.error){
        document.getElementById('out').textContent = 'Error: '+resp.error;
      } else {
        document.getElementById('out').textContent = resp.choices?.[0]?.message?.content || JSON.stringify(resp,null,2);
      }
    };
  </script>
</body>
</html>
```

Otwórz plik w przeglądarce; obserwuj lokalny roundtrip o niskim opóźnieniu.

### 4. Aplikacja Chat Chainlit RAG (7 min)

Minimalny `samples/04-cutting-edge/chainlit_app.py`:

```python
#!/usr/bin/env python3
"""Chainlit RAG demo using Foundry Local SLM as backend."""
import chainlit as cl
from openai import OpenAI

DOCS = [
  "Foundry Local enables local model execution with OpenAI-compatible APIs.",
  "RAG combines retrieval and generation for grounded answers.",
  "SLMs provide efficiency advantages on constrained hardware."  
]

client = OpenAI(base_url="http://localhost:5273/v1", api_key="not-needed")

def build_context(query: str):
    # Naive lexical scoring
    scored = sorted(DOCS, key=lambda d: sum(w in d.lower() for w in query.lower().split()), reverse=True)
    return "\n".join(scored[:2])

@cl.on_message
async def main(message: cl.Message):
    ctx = build_context(message.content)
    resp = client.chat.completions.create(
        model="phi-4-mini",
        messages=[
            {"role": "system", "content": "Answer using ONLY the provided context. If insufficient, say so."},
            {"role": "user", "content": f"Context:\n{ctx}\n\nQuestion: {message.content}"}
        ],
        max_tokens=300,
        temperature=0.3
    )
    await cl.Message(content=resp.choices[0].message.content).send()
```

Uruchom:

```powershell
chainlit run samples/04-cutting-edge/chainlit_app.py -w
```

### 5. Projekt startowy: Adaptacja `04-webgpu-inference` (6 min)

Rezultaty:
- Zastąp logikę pobierania placeholder streamingiem tokenów (użyj wariantu endpointu `stream=True`, gdy będzie dostępny)
- Dodaj wykres opóźnienia (po stronie klienta) dla przełączania phi vs gpt-oss-20b
- Osadź kontekst RAG inline (textarea dla dokumentów referencyjnych)

## Heurystyki oceny

| Kategoria | Phi-4-mini | GPT-OSS-20B | Obserwacja |
|-----------|------------|-------------|------------|
| Opóźnienie (zimny start) | Szybkie | Wolniejsze | SLM szybko się rozgrzewa |
| Pamięć | Niska | Wysoka | Możliwość na urządzeniu |
| Zgodność z kontekstem | Dobra | Silna | Większy model może być bardziej rozwlekły |
| Koszt (lokalny) | Minimalny | Wyższy (zasoby) | Kompromis energia/czas |
| Najlepsze zastosowanie | Aplikacje brzegowe | Głębokie rozumowanie | Możliwy hybrydowy pipeline |

## Walidacja środowiska

```powershell
# List catalog (no --running flag; loaded models are those you have previously run)
foundry model list

# For runtime metrics use the Python benchmark script (Session 3) and OS tools (Task Manager / nvidia-smi) instead of 'model stats'
# Example:
#   set BENCH_MODELS=phi-4-mini,gpt-oss-20b
#   python Workshop\samples\session03\benchmark_oss_models.py
```

## Rozwiązywanie problemów

| Objaw | Przyczyna | Działanie |
|-------|-----------|-----------|
| Nieudane pobieranie strony | CORS lub usługa nie działa | Użyj `curl`, aby zweryfikować endpoint; włącz proxy CORS, jeśli potrzebne |
| Pusty Chainlit | Środowisko nieaktywne | Aktywuj venv i ponownie zainstaluj zależności |
| Wysokie opóźnienie | Model właśnie załadowany | Rozgrzej małą sekwencją promptów |

## Źródła

- Foundry Local SDK: https://github.com/microsoft/Foundry-Local/tree/main/sdk/python
- Dokumentacja Chainlit: https://docs.chainlit.io
- Ocena RAG (Ragas): https://docs.ragas.io

---

**Czas trwania sesji**: 30 min  
**Poziom trudności**: Zaawansowany

## Przykładowy scenariusz i mapowanie warsztatów

| Artefakty warsztatowe | Scenariusz | Cel | Źródło danych / promptów |
|-----------------------|------------|-----|--------------------------|
| `samples/session04/model_compare.py` / `notebooks/session04_model_compare.ipynb` | Zespół architektoniczny oceniający SLM vs LLM dla generatora podsumowań dla kadry zarządzającej | Ilościowe porównanie opóźnienia + użycia tokenów | Pojedyncza zmienna środowiskowa `COMPARE_PROMPT` |
| `chainlit_app.py` (demo RAG) | Prototyp asystenta wiedzy wewnętrznej | Ugruntowanie krótkich odpowiedzi przy minimalnym wyszukiwaniu leksykalnym | Lista `DOCS` inline w pliku |
| `webgpu_demo.html` | Futurystyczny podgląd inference w przeglądarce na urządzeniu | Pokaz lokalnego roundtrip o niskim opóźnieniu + narracja UX | Tylko prompt użytkownika na żywo |

### Narracja scenariusza
Organizacja produktowa chce generator briefingów dla kadry zarządzającej. Lekki SLM (phi‑4‑mini) tworzy szkice podsumowań; większy LLM (gpt‑oss‑20b) może dopracowywać tylko raporty o wysokim priorytecie. Skrypty sesji rejestrują empiryczne opóźnienia i metryki tokenów, aby uzasadnić hybrydowy projekt, podczas gdy demo Chainlit ilustruje, jak ugruntowane wyszukiwanie utrzymuje odpowiedzi małego modelu zgodne z faktami. Strona koncepcyjna WebGPU zapewnia wizję pełnego przetwarzania po stronie klienta, gdy akceleracja przeglądarki dojrzeje.

### Minimalny kontekst RAG (Chainlit)
```python
DOCS = [
  "Foundry Local enables local model execution with OpenAI-compatible APIs.",
  "RAG combines retrieval and generation for grounded answers.",
  "SLMs provide efficiency advantages on constrained hardware."
]
```

### Hybrydowy przepływ Szkic→Dopracowanie (Pseudo)
```python
draft, _ = chat_once('phi-4-mini', messages=[{"role":"user","content":prompt}], max_tokens=280)
if len(draft) < 600:  # heuristic: escalate only for longer briefs or flagged topics
    final = draft
else:
    final, _ = chat_once('gpt-oss-20b', messages=[{"role":"user","content":f"Refine and polish:\n{draft}"}], max_tokens=220)
```

Śledź oba komponenty opóźnienia, aby zgłosić średni koszt mieszany.

### Opcjonalne ulepszenia

| Fokus | Ulepszenie | Dlaczego | Wskazówka implementacyjna |
|-------|------------|----------|---------------------------|
| Metryki porównawcze | Śledź użycie tokenów + opóźnienie pierwszego tokenu | Holistyczny widok wydajności | Użyj ulepszonego skryptu benchmarkowego (Sesja 3) z `BENCH_STREAM=1` |
| Hybrydowy pipeline | Szkic SLM → Dopracowanie LLM | Redukcja opóźnienia i kosztów | Generuj z phi-4-mini, dopracuj podsumowanie za pomocą gpt-oss-20b |
| Streaming UI | Lepszy UX w Chainlit | Informacje zwrotne w czasie rzeczywistym | Użyj `stream=True`, gdy lokalny streaming będzie dostępny; kumuluj fragmenty |
| Cache WebGPU | Szybsza inicjalizacja JS | Redukcja kosztów rekompilacji | Cache skompilowanych artefaktów shaderów (przyszła funkcjonalność runtime) |
| Deterministyczny zestaw QA | Sprawiedliwe porównanie modeli | Eliminacja zmienności | Stała lista promptów + `temperature=0` dla ocen |
| Ocena wyników | Strukturalna perspektywa jakości | Wyjście poza anegdoty | Prosta rubryka: spójność / zgodność z faktami / zwięzłość (1–5) |
| Uwagi dotyczące energii / zasobów | Dyskusja w klasie | Pokaz kompromisów | Użyj monitorów OS (`foundry system info`, Task Manager, `nvidia-smi`) + wyniki skryptów benchmarkowych |
| Symulacja kosztów | Uzasadnienie przed chmurą | Planowanie skalowania | Mapuj tokeny na hipotetyczne ceny chmurowe dla narracji TCO |
| Rozkład opóźnienia | Identyfikacja wąskich gardeł | Cel optymalizacji | Mierz przygotowanie promptu, wysłanie żądania, pierwszy token, pełne zakończenie |
| RAG + LLM jako zapas | Sieć bezpieczeństwa jakości | Poprawa trudnych zapytań | Jeśli długość odpowiedzi SLM < próg lub niska pewność → eskalacja |

#### Przykładowy wzorzec Szkic/Dopracowanie Hybrydowe

```python
draft, _ = chat_once('phi-4-mini', messages=[{"role":"user","content":task}], max_tokens=300, temperature=0.4)
refine, _ = chat_once('gpt-oss-20b', messages=[{"role":"user","content":f"Improve clarity but keep facts:\n{draft}"}], max_tokens=220, temperature=0.3)
```

#### Szkic rozkładu opóźnienia

```python
import time
t0 = time.time(); # build messages
prep_ms = (time.time()-t0)*1000
t1 = time.time(); text,_ = chat_once(alias, messages=msgs, max_tokens=180)
full_ms = (time.time()-t1)*1000
print({"prep_ms": prep_ms, "full_gen_ms": full_ms})
```

Użyj spójnych ram pomiarowych dla modeli, aby zapewnić uczciwe porównania.

---

**Zastrzeżenie**:  
Ten dokument został przetłumaczony za pomocą usługi tłumaczenia AI [Co-op Translator](https://github.com/Azure/co-op-translator). Chociaż dokładamy wszelkich starań, aby tłumaczenie było precyzyjne, prosimy pamiętać, że automatyczne tłumaczenia mogą zawierać błędy lub nieścisłości. Oryginalny dokument w jego rodzimym języku powinien być uznawany za źródło autorytatywne. W przypadku informacji o kluczowym znaczeniu zaleca się skorzystanie z profesjonalnego tłumaczenia przez człowieka. Nie ponosimy odpowiedzialności za jakiekolwiek nieporozumienia lub błędne interpretacje wynikające z użycia tego tłumaczenia.