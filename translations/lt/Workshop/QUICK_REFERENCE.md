<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a887b7e85782dadd3fd1216cd63b6c23",
  "translation_date": "2025-10-09T21:38:01+00:00",
  "source_file": "Workshop/QUICK_REFERENCE.md",
  "language_code": "lt"
}
-->
# Seminaro Pavyzdžiai - Greitos Nuorodos Kortelė

**Paskutinį kartą atnaujinta**: 2025 m. spalio 8 d.

---

## 🚀 Greitas Pradėjimas

```bash
# 1. Ensure Foundry Local is running
foundry service status
foundry model run phi-4-mini

# 2. Install dependencies
pip install -r Workshop/requirements.txt

# 3. Run a sample
cd Workshop/samples/session01
python chat_bootstrap.py "What is edge AI?"
```

---

## 📂 Pavyzdžių Apžvalga

| Sesija | Pavyzdys | Tikslas | Laikas |
|--------|----------|---------|-------|
| 01 | `chat_bootstrap.py` | Pagrindinis pokalbis + transliacija | ~30s |
| 02 | `rag_pipeline.py` | RAG su įterpimais | ~45s |
| 02 | `rag_eval_ragas.py` | RAG vertinimas | ~60s |
| 03 | `benchmark_oss_models.py` | Modelių palyginimas | ~2m |
| 04 | `model_compare.py` | SLM vs LLM | ~45s |
| 05 | `agents_orchestrator.py` | Daugiaveiksnių agentų sistema | ~60s |
| 06 | `models_router.py` | Ketinimų nukreipimas | ~45s |
| 06 | `models_pipeline.py` | Daugiapakopė sistema | ~60s |

---

## 🛠️ Aplinkos Kintamieji

### Esminiai
```bash
# Choose model
set FOUNDRY_LOCAL_ALIAS=phi-4-mini

# Override endpoint (optional)
set FOUNDRY_LOCAL_ENDPOINT=http://localhost:8000

# Show token usage
set SHOW_USAGE=1
```

### Sesijos Specifiniai
```bash
# Session 02: RAG
set RAG_QUESTION="What is local inference?"
set EMBED_MODEL=sentence-transformers/all-MiniLM-L6-v2

# Session 03: Benchmarking
set BENCH_MODELS=phi-4-mini,qwen2.5-0.5b
set BENCH_ROUNDS=3
set BENCH_STREAM=1

# Session 04: Comparison
set SLM_ALIAS=phi-4-mini
set LLM_ALIAS=qwen2.5-7b

# Session 05: Agents
set AGENT_MODEL_PRIMARY=phi-4-mini
set AGENT_QUESTION="Why use edge AI?"

# Session 06: Pipeline
set PIPELINE_TASK="Your task here"
```

---

## ✅ Validacija ir Testavimas

```bash
# Validate syntax and imports
python scripts/validate_samples.py

# Validate specific session
python scripts/validate_samples.py --session 01

# Run smoke tests
python scripts/test_samples.py --quick

# Verbose testing
python scripts/test_samples.py --verbose
```

---

## 🐛 Trikčių Šalinimas

### Ryšio Klaida
```bash
# Check Foundry Local
foundry service status

# Start if needed
foundry service start
foundry model run phi-4-mini
```

### Importavimo Klaida
```bash
# Install missing dependencies
pip install sentence-transformers ragas datasets

# Or install all
pip install -r Workshop/requirements.txt
```

### Modelis Nerastas
```bash
# List available models
foundry model ls

# Download model
foundry model download phi-4-mini
```

### Lėtas Veikimas
```bash
# Use smaller model
set FOUNDRY_LOCAL_ALIAS=qwen2.5-0.5b

# Reduce benchmark rounds
set BENCH_ROUNDS=1
```

---

## 📖 Dažniausi Šablonai

### Pagrindinis Pokalbis
```python
from workshop_utils import chat_once

text, usage = chat_once(
    'phi-4-mini',
    messages=[{"role": "user", "content": "Hello"}],
    max_tokens=100,
    temperature=0.7
)
```

### Gauti Klientą
```python
from workshop_utils import get_client

manager, client, model_id = get_client(
    alias='phi-4-mini',
    endpoint=None  # Auto-detect
)
```

### Klaidų Tvarkymas
```python
try:
    manager, client, model_id = get_client(alias)
except Exception as e:
    print(f"[ERROR] Failed: {e}")
    print("[INFO] Check: foundry service status")
    sys.exit(1)
```

### Transliacija
```python
stream = client.chat.completions.create(
    model=model_id,
    messages=messages,
    stream=True
)

for chunk in stream:
    if chunk.choices[0].delta.content:
        print(chunk.choices[0].delta.content, end="", flush=True)
```

---

## 📊 Modelių Pasirinkimas

| Modelis | Dydis | Geriausiai Tinka | Greitis |
|---------|-------|------------------|---------|
| `qwen2.5-0.5b` | 0.5B | Greita klasifikacija | ⚡⚡⚡ |
| `qwen2.5-coder-0.5b` | 0.5B | Greitas kodo generavimas | ⚡⚡⚡ |
| `gemma-2-2b` | 2B | Kūrybinis rašymas | ⚡⚡ |
| `phi-3.5-mini` | 3.5B | Kodas, refaktoringas | ⚡⚡ |
| `phi-4-mini` | 4B | Bendras, santrauka | ⚡⚡ |
| `qwen2.5-7b` | 7B | Sudėtingas samprotavimas | ⚡ |

---

## 🔗 Ištekliai

- **SDK Dokumentacija**: https://github.com/microsoft/Foundry-Local/tree/main/sdk/python
- **Greita Nuoroda**: `Workshop/FOUNDRY_SDK_QUICKREF.md`
- **Atnaujinimų Santrauka**: `Workshop/SAMPLES_UPDATE_SUMMARY.md`
- **Migracijos Pastabos**: `Workshop/SDK_MIGRATION_NOTES.md`

---

## 💡 Patarimai

1. **Kešuokite klientus**: `workshop_utils` tai padarys už jus
2. **Naudokite mažesnius modelius**: Pradėkite nuo `qwen2.5-0.5b` testavimui
3. **Įjunkite naudojimo statistiką**: Nustatykite `SHOW_USAGE=1`, kad stebėtumėte žetonus
4. **Apdorokite partijomis**: Apdorokite kelis užklausimus iš eilės
5. **Sumažinkite max_tokens**: Sumažina vėlavimą greitiems atsakymams

---

## 🎯 Pavyzdinės Darbo Eigos

### Testuokite Viską
```bash
python scripts/validate_samples.py
python scripts/test_samples.py --quick
```

### Modelių Palyginimas
```bash
cd samples/session03
set BENCH_MODELS=phi-4-mini,qwen2.5-0.5b,gemma-2-2b
set BENCH_ROUNDS=3
python benchmark_oss_models.py
```

### RAG Sistema
```bash
cd samples/session02
set RAG_QUESTION="What is RAG?"
python rag_pipeline.py
```

### Daugiaveiksnių Agentų Sistema
```bash
cd samples/session05
set AGENT_QUESTION="Why edge AI for healthcare?"
python agents_orchestrator.py
```

---

**Greita Pagalba**: Paleiskite bet kurį pavyzdį su `--help` arba peržiūrėkite docstring:
```bash
python chat_bootstrap.py --help
# or
python -c "import chat_bootstrap; help(chat_bootstrap)"
```

---

**Visi pavyzdžiai atnaujinti 2025 m. spalio mėn. pagal Foundry Local SDK geriausią praktiką** ✨

---

**Atsakomybės atsisakymas**:  
Šis dokumentas buvo išverstas naudojant AI vertimo paslaugą [Co-op Translator](https://github.com/Azure/co-op-translator). Nors siekiame tikslumo, prašome atkreipti dėmesį, kad automatiniai vertimai gali turėti klaidų ar netikslumų. Originalus dokumentas jo gimtąja kalba turėtų būti laikomas autoritetingu šaltiniu. Dėl svarbios informacijos rekomenduojama profesionali žmogaus vertimo paslauga. Mes neprisiimame atsakomybės už nesusipratimus ar neteisingus aiškinimus, kilusius dėl šio vertimo naudojimo.