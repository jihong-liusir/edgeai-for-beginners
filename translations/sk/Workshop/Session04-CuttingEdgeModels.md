<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "d1b3c0fecfd713c2df903a0633249dc9",
  "translation_date": "2025-10-08T15:15:19+00:00",
  "source_file": "Workshop/Session04-CuttingEdgeModels.md",
  "language_code": "sk"
}
-->
# Session 4: Preskúmajte najmodernejšie modely – LLM, SLM a inferencia na zariadení

## Abstrakt

Porovnajte veľké jazykové modely (LLM) a malé jazykové modely (SLM) v scenároch lokálnej a cloudovej inferencie. Naučte sa vzory nasadenia využívajúce akceleráciu ONNX Runtime, vykonávanie WebGPU a hybridné RAG skúsenosti. Súčasťou je ukážka Chainlit RAG s lokálnym modelom a voliteľné preskúmanie OpenWebUI. Prispôsobíte štartér WebGPU inferencie a vyhodnotíte schopnosti Phi vs GPT-OSS-20B a kompromisy medzi nákladmi a výkonom.

## Ciele vzdelávania

- **Porovnať** SLM a LLM z hľadiska latencie, pamäte a kvality
- **Nasadiť** modely pomocou ONNXRuntime a (kde je podporované) WebGPU
- **Spustiť** inferenciu v prehliadači (interaktívna ukážka zachovávajúca súkromie)
- **Integrovať** pipeline Chainlit RAG s lokálnym backendom SLM
- **Vyhodnotiť** pomocou ľahkých heuristík kvality a nákladov

## Predpoklady

- Dokončené relácie 1–3
- Nainštalovaný `chainlit` (už zahrnutý v `requirements.txt` pre Module08)
- Prehliadač podporujúci WebGPU (Edge / Chrome najnovší na Windows 11)
- Spustený Foundry Local (`foundry status`)

### Poznámky k multiplatformovosti

Windows zostáva primárnym cieľovým prostredím. Pre vývojárov na macOS, ktorí čakajú na natívne binárne súbory:
1. Spustite Foundry Local vo Windows 11 VM (Parallels / UTM) ALEBO na vzdialenej pracovnej stanici Windows.
2. Zverejnite službu (predvolený port 5273) a nastavte na macOS:
```bash
export FOUNDRY_LOCAL_ENDPOINT=http://<windows-host>:5273/v1
```
3. Použite rovnaké kroky pre virtuálne prostredie Python ako v predchádzajúcich reláciách.

Inštalácia Chainlit (obe platformy):
```bash
pip install chainlit
```

## Priebeh ukážky (30 min)

### 1. Porovnanie Phi (SLM) vs GPT-OSS-20B (LLM) (6 min)

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

Sledujte: hĺbku odpovede, faktickú presnosť, bohatstvo štýlu, latenciu.

### 2. Akcelerácia ONNX Runtime (5 min)

```powershell
foundry config set compute.onnx.enable_gpu true
# Re-run Python benchmark script for quantitative latency / throughput after enabling GPU
#   set BENCH_MODELS=phi-4-mini
#   python Workshop\samples\session03\benchmark_oss_models.py
```

Pozorujte zmeny priepustnosti po zapnutí GPU oproti iba CPU.

### 3. Inferencia WebGPU v prehliadači (6 min)

Prispôsobte štartér `04-webgpu-inference` (vytvorte `samples/04-cutting-edge/webgpu_demo.html`):

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

Otvorte súbor v prehliadači; pozorujte nízku latenciu lokálneho spracovania.

### 4. Aplikácia Chainlit RAG Chat (7 min)

Minimálny `samples/04-cutting-edge/chainlit_app.py`:

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

Spustite:

```powershell
chainlit run samples/04-cutting-edge/chainlit_app.py -w
```

### 5. Štartovací projekt: Prispôsobte `04-webgpu-inference` (6 min)

Výstupy:
- Nahraďte logiku načítania zástupného textu streamovaním tokenov (použite variant endpointu `stream=True`, keď bude povolený)
- Pridajte graf latencie (na strane klienta) pre prepínanie medzi phi a gpt-oss-20b
- Vložte kontext RAG inline (textové pole pre referenčné dokumenty)

## Heuristiky hodnotenia

| Kategória | Phi-4-mini | GPT-OSS-20B | Pozorovanie |
|----------|------------|-------------|-------------|
| Latencia (studený štart) | Rýchla | Pomalšia | SLM sa rýchlo zahrieva |
| Pamäť | Nízka | Vysoká | Realizovateľnosť na zariadení |
| Dodržiavanie kontextu | Dobré | Silné | Väčší model môže byť výrečnejší |
| Náklady (lokálne) | Minimálne | Vyššie (zdroje) | Kompromis energie/času |
| Najlepšie použitie | Aplikácie na okraji | Hlboké uvažovanie | Možná hybridná pipeline |

## Validácia prostredia

```powershell
# List catalog (no --running flag; loaded models are those you have previously run)
foundry model list

# For runtime metrics use the Python benchmark script (Session 3) and OS tools (Task Manager / nvidia-smi) instead of 'model stats'
# Example:
#   set BENCH_MODELS=phi-4-mini,gpt-oss-20b
#   python Workshop\samples\session03\benchmark_oss_models.py
```

## Riešenie problémov

| Príznak | Príčina | Akcia |
|---------|-------|--------|
| Zlyhanie načítania webovej stránky | CORS alebo služba nefunguje | Použite `curl` na overenie endpointu; povolte CORS proxy, ak je potrebné |
| Prázdny Chainlit | Prostredie nie je aktívne | Aktivujte venv a preinštalujte závislosti |
| Vysoká latencia | Model práve načítaný | Zahrievajte malou sekvenciou promptov |

## Referencie

- Foundry Local SDK: https://github.com/microsoft/Foundry-Local/tree/main/sdk/python
- Dokumentácia Chainlit: https://docs.chainlit.io
- Hodnotenie RAG (Ragas): https://docs.ragas.io

---

**Trvanie relácie**: 30 min  
**Náročnosť**: Pokročilá

## Ukážkový scenár a mapovanie workshopu

| Artefakty workshopu | Scenár | Cieľ | Zdroj údajov / promptov |
|--------------------|----------|-----------|----------------------|
| `samples/session04/model_compare.py` / `notebooks/session04_model_compare.ipynb` | Tím architektúry hodnotí SLM vs LLM pre generátor výkonných zhrnutí | Kvantifikovať rozdiel v latencii + používaní tokenov | Jedna premenná prostredia `COMPARE_PROMPT` |
| `chainlit_app.py` (ukážka RAG) | Prototyp interného asistenta znalostí | Zakotviť krátke odpovede s minimálnym lexikálnym vyhľadávaním | Inline zoznam `DOCS` v súbore |
| `webgpu_demo.html` | Futuristický náhľad inferencie v prehliadači na zariadení | Ukázať nízku latenciu lokálneho spracovania + UX naratívu | Iba živý prompt používateľa |

### Scenár naratívu
Produktová organizácia chce generátor výkonných zhrnutí. Ľahký SLM (phi‑4‑mini) vytvára návrhy zhrnutí; väčší LLM (gpt‑oss‑20b) môže upravovať iba správy s vysokou prioritou. Skripty relácie zachytávajú empirické metriky latencie a tokenov na odôvodnenie hybridného dizajnu, zatiaľ čo ukážka Chainlit ilustruje, ako zakotvené vyhľadávanie udržuje odpovede malého modelu faktické. Konceptová stránka WebGPU poskytuje víziu plne klientského spracovania, keď sa zrýchlenie prehliadača vyvinie.

### Minimálny kontext RAG (Chainlit)
```python
DOCS = [
  "Foundry Local enables local model execution with OpenAI-compatible APIs.",
  "RAG combines retrieval and generation for grounded answers.",
  "SLMs provide efficiency advantages on constrained hardware."
]
```

### Hybridný tok Návrh→Úprava (Pseudo)
```python
draft, _ = chat_once('phi-4-mini', messages=[{"role":"user","content":prompt}], max_tokens=280)
if len(draft) < 600:  # heuristic: escalate only for longer briefs or flagged topics
    final = draft
else:
    final, _ = chat_once('gpt-oss-20b', messages=[{"role":"user","content":f"Refine and polish:\n{draft}"}], max_tokens=220)
```

Sledujte obe komponenty latencie na hlásenie zmiešaných priemerných nákladov.

### Voliteľné vylepšenia

| Zameranie | Vylepšenie | Prečo | Náznak implementácie |
|-------|------------|-----|---------------------|
| Porovnávacie metriky | Sledujte používanie tokenov + latenciu prvého tokenu | Holistický pohľad na výkon | Použite vylepšený skript benchmarku (Relácia 3) s `BENCH_STREAM=1` |
| Hybridná pipeline | Návrh SLM → Úprava LLM | Zníženie latencie a nákladov | Generujte pomocou phi-4-mini, upravte zhrnutie pomocou gpt-oss-20b |
| Streaming UI | Lepší UX v Chainlit | Postupná spätná väzba | Použite `stream=True`, keď bude lokálne streamovanie povolené; akumulujte časti |
| WebGPU caching | Rýchlejšia JS inicializácia | Zníženie režijných nákladov na rekompiláciu | Ukladajte artefakty skompilovaných shaderov (budúca schopnosť runtime) |
| Deterministická sada QA | Férové porovnanie modelov | Odstránenie variability | Fixný zoznam promptov + `temperature=0` pre hodnotiace behy |
| Skórovanie výstupov | Štruktúrovaný pohľad na kvalitu | Prekročenie anekdot | Jednoduchá rubrika: koherencia / faktickosť / stručnosť (1–5) |
| Poznámky k energii / zdrojom | Diskusia v triede | Ukázať kompromisy | Použite monitory OS (`foundry system info`, Task Manager, `nvidia-smi`) + výstupy skriptu benchmarku |
| Simulácia nákladov | Pred-cloudová odôvodnenie | Plánovanie škálovania | Mapujte tokeny na hypotetické cloudové ceny pre naratív TCO |
| Rozklad latencie | Identifikácia úzkych miest | Cielené optimalizácie | Merajte prípravu promptu, odoslanie požiadavky, prvý token, úplné dokončenie |
| RAG + LLM fallback | Bezpečnostná sieť kvality | Zlepšenie náročných otázok | Ak je dĺžka odpovede SLM < prahová hodnota alebo nízka dôvera → eskalácia |

#### Príklad hybridného vzoru Návrh/Úprava

```python
draft, _ = chat_once('phi-4-mini', messages=[{"role":"user","content":task}], max_tokens=300, temperature=0.4)
refine, _ = chat_once('gpt-oss-20b', messages=[{"role":"user","content":f"Improve clarity but keep facts:\n{draft}"}], max_tokens=220, temperature=0.3)
```

#### Náčrt rozkladu latencie

```python
import time
t0 = time.time(); # build messages
prep_ms = (time.time()-t0)*1000
t1 = time.time(); text,_ = chat_once(alias, messages=msgs, max_tokens=180)
full_ms = (time.time()-t1)*1000
print({"prep_ms": prep_ms, "full_gen_ms": full_ms})
```

Použite konzistentné meracie štruktúry naprieč modelmi pre férové porovnania.

---

**Upozornenie**:  
Tento dokument bol preložený pomocou služby AI prekladu [Co-op Translator](https://github.com/Azure/co-op-translator). Hoci sa snažíme o presnosť, upozorňujeme, že automatizované preklady môžu obsahovať chyby alebo nepresnosti. Pôvodný dokument v jeho pôvodnom jazyku by mal byť považovaný za autoritatívny zdroj. Pre kritické informácie sa odporúča profesionálny ľudský preklad. Nenesieme zodpovednosť za akékoľvek nedorozumenia alebo nesprávne interpretácie vyplývajúce z použitia tohto prekladu.