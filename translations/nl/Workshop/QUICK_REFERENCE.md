<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a887b7e85782dadd3fd1216cd63b6c23",
  "translation_date": "2025-10-09T16:56:53+00:00",
  "source_file": "Workshop/QUICK_REFERENCE.md",
  "language_code": "nl"
}
-->
# Workshop Voorbeelden - Snel Referentiekaart

**Laatst Bijgewerkt**: 8 oktober 2025

---

## 🚀 Snelle Start

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

## 📂 Overzicht Voorbeelden

| Sessie | Voorbeeld | Doel | Tijd |
|--------|-----------|------|------|
| 01 | `chat_bootstrap.py` | Basis chat + streaming | ~30s |
| 02 | `rag_pipeline.py` | RAG met embeddings | ~45s |
| 02 | `rag_eval_ragas.py` | RAG evaluatie | ~60s |
| 03 | `benchmark_oss_models.py` | Model benchmarking | ~2m |
| 04 | `model_compare.py` | SLM vs LLM | ~45s |
| 05 | `agents_orchestrator.py` | Multi-agent systeem | ~60s |
| 06 | `models_router.py` | Intent routing | ~45s |
| 06 | `models_pipeline.py` | Multi-stap pipeline | ~60s |

---

## 🛠️ Omgevingsvariabelen

### Essentieel
```bash
# Choose model
set FOUNDRY_LOCAL_ALIAS=phi-4-mini

# Override endpoint (optional)
set FOUNDRY_LOCAL_ENDPOINT=http://localhost:8000

# Show token usage
set SHOW_USAGE=1
```

### Sessie-specifiek
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

## ✅ Validatie & Testen

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

## 🐛 Problemen Oplossen

### Verbindingsfout
```bash
# Check Foundry Local
foundry service status

# Start if needed
foundry service start
foundry model run phi-4-mini
```

### Importfout
```bash
# Install missing dependencies
pip install sentence-transformers ragas datasets

# Or install all
pip install -r Workshop/requirements.txt
```

### Model Niet Gevonden
```bash
# List available models
foundry model ls

# Download model
foundry model download phi-4-mini
```

### Trage Prestaties
```bash
# Use smaller model
set FOUNDRY_LOCAL_ALIAS=qwen2.5-0.5b

# Reduce benchmark rounds
set BENCH_ROUNDS=1
```

---

## 📖 Veelvoorkomende Patronen

### Basis Chat
```python
from workshop_utils import chat_once

text, usage = chat_once(
    'phi-4-mini',
    messages=[{"role": "user", "content": "Hello"}],
    max_tokens=100,
    temperature=0.7
)
```

### Client Ophalen
```python
from workshop_utils import get_client

manager, client, model_id = get_client(
    alias='phi-4-mini',
    endpoint=None  # Auto-detect
)
```

### Foutafhandeling
```python
try:
    manager, client, model_id = get_client(alias)
except Exception as e:
    print(f"[ERROR] Failed: {e}")
    print("[INFO] Check: foundry service status")
    sys.exit(1)
```

### Streaming
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

## 📊 Modelselectie

| Model | Grootte | Beste Voor | Snelheid |
|-------|---------|------------|----------|
| `qwen2.5-0.5b` | 0.5B | Snelle classificatie | ⚡⚡⚡ |
| `qwen2.5-coder-0.5b` | 0.5B | Snelle code generatie | ⚡⚡⚡ |
| `gemma-2-2b` | 2B | Creatief schrijven | ⚡⚡ |
| `phi-3.5-mini` | 3.5B | Code, refactoring | ⚡⚡ |
| `phi-4-mini` | 4B | Algemeen, samenvatting | ⚡⚡ |
| `qwen2.5-7b` | 7B | Complexe redenering | ⚡ |

---

## 🔗 Bronnen

- **SDK Documentatie**: https://github.com/microsoft/Foundry-Local/tree/main/sdk/python
- **Snelle Referentie**: `Workshop/FOUNDRY_SDK_QUICKREF.md`
- **Update Samenvatting**: `Workshop/SAMPLES_UPDATE_SUMMARY.md`
- **Migratienotities**: `Workshop/SDK_MIGRATION_NOTES.md`

---

## 💡 Tips

1. **Cache clients**: `workshop_utils` cachet automatisch voor je
2. **Gebruik kleinere modellen**: Begin met `qwen2.5-0.5b` voor testen
3. **Schakel gebruiksstatistieken in**: Stel `SHOW_USAGE=1` in om tokens bij te houden
4. **Batchverwerking**: Verwerk meerdere prompts achter elkaar
5. **Verlaag max_tokens**: Vermindert latentie voor snelle antwoorden

---

## 🎯 Voorbeeld Workflows

### Test Alles
```bash
python scripts/validate_samples.py
python scripts/test_samples.py --quick
```

### Benchmark Modellen
```bash
cd samples/session03
set BENCH_MODELS=phi-4-mini,qwen2.5-0.5b,gemma-2-2b
set BENCH_ROUNDS=3
python benchmark_oss_models.py
```

### RAG Pipeline
```bash
cd samples/session02
set RAG_QUESTION="What is RAG?"
python rag_pipeline.py
```

### Multi-Agent Systeem
```bash
cd samples/session05
set AGENT_QUESTION="Why edge AI for healthcare?"
python agents_orchestrator.py
```

---

**Snelle Hulp**: Voer een voorbeeld uit met `--help` of bekijk de docstring:
```bash
python chat_bootstrap.py --help
# or
python -c "import chat_bootstrap; help(chat_bootstrap)"
```

---

**Alle voorbeelden bijgewerkt in oktober 2025 met Foundry Local SDK best practices** ✨

---

**Disclaimer**:  
Dit document is vertaald met behulp van de AI-vertalingsservice [Co-op Translator](https://github.com/Azure/co-op-translator). Hoewel we streven naar nauwkeurigheid, dient u zich ervan bewust te zijn dat geautomatiseerde vertalingen fouten of onnauwkeurigheden kunnen bevatten. Het originele document in de oorspronkelijke taal moet worden beschouwd als de gezaghebbende bron. Voor cruciale informatie wordt professionele menselijke vertaling aanbevolen. Wij zijn niet aansprakelijk voor misverstanden of verkeerde interpretaties die voortvloeien uit het gebruik van deze vertaling.