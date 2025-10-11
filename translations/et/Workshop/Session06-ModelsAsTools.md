<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "94b65d49961cabc07f76062d09a5d09c",
  "translation_date": "2025-10-11T11:59:50+00:00",
  "source_file": "Workshop/Session06-ModelsAsTools.md",
  "language_code": "et"
}
-->
# Sessioon 6: Foundry Local – Mudelid kui Tööriistad

## Kokkuvõte

Käsitle mudelid kombineeritavate tööriistadena lokaalses AI operatsioonikihis. Selles sessioonis õpid, kuidas ühendada mitmeid spetsialiseeritud SLM/LLM-kõnesid, suunata ülesandeid valikuliselt ja pakkuda rakendustele ühtset SDK-liidest. Sa lood kergekaalulise mudelite suunaja + ülesande planeerija, integreerid selle rakenduse skripti ja visandad skaleerimistee Azure AI Foundry jaoks tootmiskoormuste haldamiseks.

## Õpieesmärgid

- **Mõtesta** mudelid kui iseseisvad tööriistad koos määratletud võimekustega
- **Suunamine** taotluste põhjal kavatsuse/heuristilise skoori järgi
- **Ühendamine** väljundite kaudu mitmeastmelistes ülesannetes (lahutamine → lahendamine → täpsustamine)
- **Integreerimine** ühtse kliendi API rakenduste jaoks
- **Skaleerimine** disain pilvele (sama OpenAI-ühilduv leping)

## Eeltingimused

- Sessioonid 1–5 läbitud
- Mitmed lokaalsed mudelid vahemällu salvestatud (nt `phi-4-mini`, `deepseek-coder-1.3b`, `qwen2.5-0.5b`)

### Platvormideülene keskkonna koodinäide

Windows PowerShell:
```powershell
py -m venv .venv
 .\.venv\Scripts\Activate.ps1
pip install --upgrade pip
pip install foundry-local-sdk openai
```

macOS / Linux:
```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install foundry-local-sdk openai
```

Remote/VM teenuse ligipääs macOS-ist:
```bash
export FOUNDRY_LOCAL_ENDPOINT=http://<windows-host>:5273/v1
```


## Demo Kava (30 min)

### 1. Tööriistade võimekuse määratlemine (5 min)

Loo `samples/06-tools/models_catalog.py`:

```python
CATALOG = {
  "phi-4-mini": {
    "capabilities": ["general", "reasoning", "summarize"],
    "priority": 2
  },
  "deepseek-coder-1.3b": {
    "capabilities": ["code", "refactor", "explain_code"],
    "priority": 1
  },
  "qwen2.5-0.5b": {
    "capabilities": ["fast", "classification", "lightweight"],
    "priority": 3
  }
}
```


### 2. Kavatsuse tuvastamine ja suunamine (8 min)

Loo `samples/06-tools/router.py`:

```python
#!/usr/bin/env python3
"""Model-as-tool router using Foundry Local OpenAI-compatible endpoint."""
from openai import OpenAI
from models_catalog import CATALOG
import re

client = OpenAI(base_url="http://localhost:5273/v1", api_key="not-needed")

INTENT_RULES = [
  (re.compile(r"code|function|refactor|bug|optimi", re.I), "code"),
  (re.compile(r"summari|abstract|tl;dr", re.I), "summarize"),
  (re.compile(r"classif|label|category", re.I), "classification"),
]

def detect_intent(prompt: str) -> str:
    for pat, intent in INTENT_RULES:
        if pat.search(prompt):
            return intent
    return "general"

def select_model(intent: str) -> str:
    # Score catalog: capability match first, then priority
    scored = []
    for name, meta in CATALOG.items():
        caps = meta["capabilities"]
        match = intent in caps
        scored.append((name, match, meta["priority"]))
    # Sort: match True first, then lowest priority value
    scored.sort(key=lambda t: (not t[1], t[2]))
    return scored[0][0]

def run(prompt: str):
    intent = detect_intent(prompt)
    model = select_model(intent)
    resp = client.chat.completions.create(
        model=model,
        messages=[{"role": "user", "content": prompt}],
        max_tokens=400,
        temperature=0.5
    )
    return {"intent": intent, "model": model, "output": resp.choices[0].message.content}

if __name__ == "__main__":
    tests = [
        "Refactor this Python function for readability",
        "Summarize the importance of local AI governance",
        "Classify this feedback: 'The UI is slow and confusing'"
    ]
    for t in tests:
        r = run(t)
        print(f"Prompt: {t}\nModel: {r['model']} (intent={r['intent']})\nOutput: {r['output'][:160]}...\n")
```


### 3. Mitmeastmeline ülesande ühendamine (7 min)

Loo `samples/06-tools/pipeline.py`:

```python
#!/usr/bin/env python3
"""Multi-step pipeline: plan -> solve -> refine using specialized models."""
from openai import OpenAI
from router import detect_intent, select_model

client = OpenAI(base_url="http://localhost:5273/v1", api_key="not-needed")

def chat(model, content, temp=0.4):
    r = client.chat.completions.create(
        model=model,
        messages=[{"role": "user", "content": content}],
        max_tokens=350,
        temperature=temp
    )
    return r.choices[0].message.content

def pipeline(task: str):
    plan_model = select_model("general")
    plan = chat(plan_model, f"Break the task into 3 ordered steps. Task: {task}")
    steps = [s for s in plan.split('\n') if s.strip()][:3]
    outputs = []
    for step in steps:
        intent = detect_intent(step)
        model = select_model(intent)
        out = chat(model, step)
        outputs.append((step, model, out))
    refine_model = select_model("summarize")
    combined = '\n'.join(o[2] for o in outputs)
    refined = chat(refine_model, f"Condense results into a cohesive answer:\n{combined}")
    return {"plan": plan, "steps": outputs, "final": refined}

if __name__ == '__main__':
    result = pipeline("Generate a refactored version of a slow Python loop and summarize performance gains.")
    print("PLAN:\n", result['plan'])
    print("FINAL:\n", result['final'][:400])
```


### 4. Algprojekt: Kohanda `06-models-as-tools` (5 min)

Täiendused:
- Lisa voogedastuse tokeni tugi (progressiivne UI uuendus)
- Lisa usaldusväärsuse skoorimine: leksikaalne kattuvus või prompti rubriik
- Ekspordi jälgimise JSON (kavatsus → mudel → latentsus → tokeni kasutus)
- Rakenda vahemälu korduvkasutust alamsammude jaoks

### 5. Skaleerimistee Azure'ile (5 min)

| Kiht | Kohalik (Foundry) | Pilv (Azure AI Foundry) | Üleminekustrateegia |
|------|-------------------|-------------------------|---------------------|
| Suunamine | Heuristiline Python | Püsiv mikroteenus | Konteineriseeri ja juuruta API |
| Mudelid | SLM-id vahemällu salvestatud | Hallatud juurutused | Kaardista kohalikud nimed juurutuse ID-dele |
| Jälgitavus | CLI statistika/käsitsi | Keskne logimine ja mõõdikud | Lisa struktureeritud jälgimise sündmused |
| Turvalisus | Ainult kohalik host | Azure autentimine / võrgustik | Lisa võtmehoidla saladuste jaoks |
| Kulu | Seadme ressursid | Tarbimispõhine arveldus | Lisa eelarvepiirangud |

## Valideerimise Kontrollnimekiri

```powershell
foundry model run phi-4-mini
foundry model run deepseek-coder-1.3b
python samples/06-tools/router.py
python samples/06-tools/pipeline.py
```

Oota kavatsusepõhist mudeli valikut ja lõplikku täpsustatud väljundit.

## Tõrkeotsing

| Probleem | Põhjus | Lahendus |
|----------|--------|---------|
| Kõik ülesanded suunatakse samale mudelile | Nõrgad reeglid | Rikasta INTENT_RULES regex komplekti |
| Toru ebaõnnestub keskel | Puuduv mudel laaditud | Käivita `foundry model run <model>` |
| Madal väljundi ühtsus | Puudub täpsustamise faas | Lisa kokkuvõtte/valideerimise samm |

## Viited

- Foundry Local SDK: https://github.com/microsoft/Foundry-Local/tree/main/sdk/python
- Azure AI Foundry dokumentatsioon: https://learn.microsoft.com/azure/ai-foundry
- Prompti kvaliteedimustrid: Vaata Sessiooni 2

---

**Sessiooni kestus**: 30 min  
**Raskusaste**: Ekspert

## Näidistsenaarium ja Töötuba

| Töötuba skriptid / märkmikud | Stsenaarium | Eesmärk | Andmestik / Kataloogi allikas |
|-----------------------------|-------------|---------|------------------------------|
| `samples/session06/models_router.py` / `notebooks/session06_models_router.ipynb` | Arendaja assistent, mis käsitleb segakavatsusega prompti (refaktor, kokkuvõte, klassifitseerimine) | Heuristiline kavatsus → mudeli alias suunamine koos tokeni kasutusega | Inline `CATALOG` + regex `RULES` |
| `samples/session06/models_pipeline.py` / `notebooks/session06_models_pipeline.ipynb` | Mitmeastmeline planeerimine ja täpsustamine keeruka koodiabi ülesande jaoks | Lahutamine → spetsialiseeritud täitmine → kokkuvõtte täpsustamise samm | Sama `CATALOG`; sammud tuletatud plaani väljundist |

### Stsenaariumi Narratiiv
Inseneri produktiivsuse tööriist saab heterogeenseid ülesandeid: koodi refaktorimine, arhitektuuriliste märkmete kokkuvõte, tagasiside klassifitseerimine. Latentsuse ja ressursikasutuse minimeerimiseks planeerib ja teeb kokkuvõtte väike üldine mudel, koodispetsialiseeritud mudel tegeleb refaktorimisega ja kerge klassifitseerimisvõimeline mudel märgistab tagasisidet. Toru skript demonstreerib ühendamist + täpsustamist; suunaja skript isoleerib kohanduva ühe prompti suunamise.

### Kataloogi Hetktõmmis
```python
CATALOG = {
    "phi-4-mini": {"capabilities": ["general", "summarize"], "priority": 2},
    "deepseek-coder-1.3b": {"capabilities": ["code", "refactor"], "priority": 1},
    "qwen2.5-0.5b": {"capabilities": ["classification", "fast"], "priority": 3}
}
```


### Näidistest Promptid
```json
[
    "Refactor this Python function for readability",
    "Summarize the importance of small language models",
    "Classify this feedback: The UI is slow but pretty",
    "Generate a refactored version of a slow Python loop and summarize performance gains."
]
```


### Jälgimise Laiendus (Valikuline)
Lisa sammupõhised jälgimise JSON read `models_pipeline.py` jaoks:
```python
trace.append({
    "step": step_idx,
    "intent": intent,
    "alias": alias,
    "latency_ms": round((end-start)*1000,2),
    "tokens": getattr(usage,'total_tokens',None)
})
```


### Eskaleerimise Heuristika (Idee)
Kui plaan sisaldab märksõnu nagu "optimeeri", "turvalisus" või sammu pikkus > 280 tähemärki → eskaleeri suuremale mudelile (nt `gpt-oss-20b`) ainult selle sammu jaoks.

### Valikulised Täiendused

| Valdkond | Täiendus | Väärtus | Vihje |
|----------|----------|---------|------|
| Vahemälu | Korduvkasuta halduri + kliendi objekte | Madalam latentsus, vähem koormust | Kasuta `workshop_utils.get_client` |
| Kasutusmõõdikud | Püüa tokenid ja sammupõhine latentsus | Profileerimine ja optimeerimine | Ajasta iga suunatud kõne; salvesta jälgimise nimekirja |
| Kohanduv Suunamine | Usaldusväärsuse/kulu teadlik | Parem kvaliteedi-kulu tasakaal | Lisa skoorimine: kui prompt > N tähemärki või regex vastab domeenile → eskaleeri suuremale mudelile |
| Dünaamiline Võimekuse Register | Kataloogi kuum laadimine | Ei vaja taaskäivitust ega uuesti juurutamist | Laadi `catalog.json` käitusajal; jälgi faili ajatemplit |
| Tagavarastrateegia | Tõrgete korral vastupidavus | Suurem saadavus | Proovi esmalt → erandi korral tagavaraliides |
| Voogedastuse Toru | Varajane tagasiside | UX-i parandus | Voogedasta iga samm ja puhverda lõplik täpsustamise sisend |
| Vektorkavatsuse Embeddings | Täpsem suunamine | Kõrgem kavatsuse täpsus | Embed prompt, klasterda ja kaardista centroid → võimekus |
| Jälgimise Ekspordi | Auditeeritav ühendus | Vastavus/aruandlus | Emit JSON read: samm, kavatsus, mudel, latentsus_ms, tokenid |
| Kulusimulatsioon | Pilve-eelne hinnang | Eelarve planeerimine | Määra mudeli kohta notionaalsed kulud/token ja koonda ülesande kohta |
| Deterministlik Režiim | Reprodutseeritavus | Stabiilne võrdlusalus | Keskkond: `temperature=0`, fikseeritud sammude arv |

#### Jälgimise Struktuuri Näide

```python
trace.append({
  "step": idx,
  "intent": intent,
  "alias": alias,
  "latency_ms": round((end-start)*1000,2),
  "tokens": getattr(usage,'total_tokens',None)
})
```


#### Kohanduva Eskaleerimise Visand

```python
if len(prompt) > 280 or 'compliance' in prompt.lower():
    # escalate to larger reasoning model if available
    alias = 'gpt-oss-20b'
```


#### Mudelikataloogi Kuum Laadimine

```python
import json, time, os
CATALOG_PATH = 'catalog.json'
last_mtime = 0
def get_catalog():
    global last_mtime, CATALOG
    m = os.path.getmtime(CATALOG_PATH)
    if m != last_mtime:
        CATALOG = json.load(open(CATALOG_PATH))
        last_mtime = m
    return CATALOG
```


Iteratsiooni järk-järgult—väldi varajaste prototüüpide üleliigset inseneritööd.

---

**Lahtiütlus**:  
See dokument on tõlgitud AI tõlketeenuse [Co-op Translator](https://github.com/Azure/co-op-translator) abil. Kuigi püüame tagada täpsust, palume arvestada, et automaatsed tõlked võivad sisaldada vigu või ebatäpsusi. Algne dokument selle algses keeles tuleks pidada autoriteetseks allikaks. Olulise teabe puhul soovitame kasutada professionaalset inimtõlget. Me ei vastuta selle tõlke kasutamisest tulenevate arusaamatuste või valesti tõlgenduste eest.