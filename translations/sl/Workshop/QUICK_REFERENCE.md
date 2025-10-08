<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a887b7e85782dadd3fd1216cd63b6c23",
  "translation_date": "2025-10-08T12:18:10+00:00",
  "source_file": "Workshop/QUICK_REFERENCE.md",
  "language_code": "sl"
}
-->
# Vzorci delavnice - Hitri referenčni karton

**Zadnja posodobitev**: 8. oktober 2025

---

## 🚀 Hiter začetek

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

## 📂 Pregled vzorcev

| Seja | Vzorec | Namen | Čas |
|------|--------|-------|-----|
| 01 | `chat_bootstrap.py` | Osnovni klepet + pretakanje | ~30s |
| 02 | `rag_pipeline.py` | RAG z vdelavami | ~45s |
| 02 | `rag_eval_ragas.py` | Ocena RAG | ~60s |
| 03 | `benchmark_oss_models.py` | Primerjava modelov | ~2m |
| 04 | `model_compare.py` | SLM proti LLM | ~45s |
| 05 | `agents_orchestrator.py` | Sistem več agentov | ~60s |
| 06 | `models_router.py` | Usmerjanje namer | ~45s |
| 06 | `models_pipeline.py` | Večstopenjski cevovod | ~60s |

---

## 🛠️ Spremenljivke okolja

### Osnovne
```bash
# Choose model
set FOUNDRY_LOCAL_ALIAS=phi-4-mini

# Override endpoint (optional)
set FOUNDRY_LOCAL_ENDPOINT=http://localhost:8000

# Show token usage
set SHOW_USAGE=1
```

### Specifične za sejo
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

## ✅ Validacija in testiranje

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

## 🐛 Odpravljanje težav

### Napaka povezave
```bash
# Check Foundry Local
foundry service status

# Start if needed
foundry service start
foundry model run phi-4-mini
```

### Napaka uvoza
```bash
# Install missing dependencies
pip install sentence-transformers ragas datasets

# Or install all
pip install -r Workshop/requirements.txt
```

### Model ni najden
```bash
# List available models
foundry model ls

# Download model
foundry model download phi-4-mini
```

### Počasno delovanje
```bash
# Use smaller model
set FOUNDRY_LOCAL_ALIAS=qwen2.5-0.5b

# Reduce benchmark rounds
set BENCH_ROUNDS=1
```

---

## 📖 Pogosti vzorci

### Osnovni klepet
```python
from workshop_utils import chat_once

text, usage = chat_once(
    'phi-4-mini',
    messages=[{"role": "user", "content": "Hello"}],
    max_tokens=100,
    temperature=0.7
)
```

### Pridobitev odjemalca
```python
from workshop_utils import get_client

manager, client, model_id = get_client(
    alias='phi-4-mini',
    endpoint=None  # Auto-detect
)
```

### Obvladovanje napak
```python
try:
    manager, client, model_id = get_client(alias)
except Exception as e:
    print(f"[ERROR] Failed: {e}")
    print("[INFO] Check: foundry service status")
    sys.exit(1)
```

### Pretakanje
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

## 📊 Izbira modela

| Model | Velikost | Najboljše za | Hitrost |
|-------|----------|--------------|---------|
| `qwen2.5-0.5b` | 0.5B | Hitro razvrščanje | ⚡⚡⚡ |
| `qwen2.5-coder-0.5b` | 0.5B | Hitro generiranje kode | ⚡⚡⚡ |
| `gemma-2-2b` | 2B | Kreativno pisanje | ⚡⚡ |
| `phi-3.5-mini` | 3.5B | Koda, prestrukturiranje | ⚡⚡ |
| `phi-4-mini` | 4B | Splošno, povzetki | ⚡⚡ |
| `qwen2.5-7b` | 7B | Kompleksno razmišljanje | ⚡ |

---

## 🔗 Viri

- **SDK dokumentacija**: https://github.com/microsoft/Foundry-Local/tree/main/sdk/python
- **Hitri referenčni vodič**: `Workshop/FOUNDRY_SDK_QUICKREF.md`
- **Povzetek posodobitev**: `Workshop/SAMPLES_UPDATE_SUMMARY.md`
- **Opombe o migraciji**: `Workshop/SDK_MIGRATION_NOTES.md`

---

## 💡 Nasveti

1. **Predpomnite odjemalce**: `workshop_utils` to naredi namesto vas
2. **Uporabljajte manjše modele**: Za testiranje začnite z `qwen2.5-0.5b`
3. **Omogočite statistiko uporabe**: Nastavite `SHOW_USAGE=1` za sledenje žetonom
4. **Obdelava v serijah**: Obdelajte več pozivov zaporedno
5. **Znižajte max_tokens**: Zmanjša zakasnitve za hitre odgovore

---

## 🎯 Delovni tokovi vzorcev

### Testirajte vse
```bash
python scripts/validate_samples.py
python scripts/test_samples.py --quick
```

### Primerjava modelov
```bash
cd samples/session03
set BENCH_MODELS=phi-4-mini,qwen2.5-0.5b,gemma-2-2b
set BENCH_ROUNDS=3
python benchmark_oss_models.py
```

### RAG cevovod
```bash
cd samples/session02
set RAG_QUESTION="What is RAG?"
python rag_pipeline.py
```

### Sistem več agentov
```bash
cd samples/session05
set AGENT_QUESTION="Why edge AI for healthcare?"
python agents_orchestrator.py
```

---

**Hitra pomoč**: Zaženite kateri koli vzorec z `--help` ali preverite docstring:
```bash
python chat_bootstrap.py --help
# or
python -c "import chat_bootstrap; help(chat_bootstrap)"
```

---

**Vsi vzorci posodobljeni oktobra 2025 z najboljšimi praksami Foundry Local SDK** ✨

---

**Izjava o omejitvi odgovornosti**:  
Ta dokument je bil preveden z uporabo storitve za strojno prevajanje [Co-op Translator](https://github.com/Azure/co-op-translator). Čeprav si prizadevamo za natančnost, vas prosimo, da upoštevate, da lahko avtomatizirani prevodi vsebujejo napake ali netočnosti. Izvirni dokument v njegovem izvirnem jeziku je treba obravnavati kot avtoritativni vir. Za ključne informacije priporočamo profesionalni človeški prevod. Ne prevzemamo odgovornosti za morebitne nesporazume ali napačne razlage, ki izhajajo iz uporabe tega prevoda.