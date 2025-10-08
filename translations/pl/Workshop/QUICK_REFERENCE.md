<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a887b7e85782dadd3fd1216cd63b6c23",
  "translation_date": "2025-10-08T21:56:11+00:00",
  "source_file": "Workshop/QUICK_REFERENCE.md",
  "language_code": "pl"
}
-->
# Przykładowe Warsztaty - Karta Szybkiego Dostępu

**Ostatnia aktualizacja**: 8 października 2025

---

## 🚀 Szybki Start

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

## 📂 Przegląd Przykładów

| Sesja | Przykład | Cel | Czas |
|-------|----------|-----|------|
| 01 | `chat_bootstrap.py` | Podstawowy chat + streaming | ~30s |
| 02 | `rag_pipeline.py` | RAG z embeddingami | ~45s |
| 02 | `rag_eval_ragas.py` | Ocena RAG | ~60s |
| 03 | `benchmark_oss_models.py` | Benchmark modeli | ~2m |
| 04 | `model_compare.py` | SLM vs LLM | ~45s |
| 05 | `agents_orchestrator.py` | System multi-agentowy | ~60s |
| 06 | `models_router.py` | Routing intencji | ~45s |
| 06 | `models_pipeline.py` | Pipeline wieloetapowy | ~60s |

---

## 🛠️ Zmienne Środowiskowe

### Podstawowe
```bash
# Choose model
set FOUNDRY_LOCAL_ALIAS=phi-4-mini

# Override endpoint (optional)
set FOUNDRY_LOCAL_ENDPOINT=http://localhost:8000

# Show token usage
set SHOW_USAGE=1
```

### Specyficzne dla sesji
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

## ✅ Walidacja i Testowanie

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

## 🐛 Rozwiązywanie Problemów

### Błąd Połączenia
```bash
# Check Foundry Local
foundry service status

# Start if needed
foundry service start
foundry model run phi-4-mini
```

### Błąd Importu
```bash
# Install missing dependencies
pip install sentence-transformers ragas datasets

# Or install all
pip install -r Workshop/requirements.txt
```

### Model Nie Znaleziony
```bash
# List available models
foundry model ls

# Download model
foundry model download phi-4-mini
```

### Wolne Działanie
```bash
# Use smaller model
set FOUNDRY_LOCAL_ALIAS=qwen2.5-0.5b

# Reduce benchmark rounds
set BENCH_ROUNDS=1
```

---

## 📖 Wzorce Użycia

### Podstawowy Chat
```python
from workshop_utils import chat_once

text, usage = chat_once(
    'phi-4-mini',
    messages=[{"role": "user", "content": "Hello"}],
    max_tokens=100,
    temperature=0.7
)
```

### Pobierz Klienta
```python
from workshop_utils import get_client

manager, client, model_id = get_client(
    alias='phi-4-mini',
    endpoint=None  # Auto-detect
)
```

### Obsługa Błędów
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

## 📊 Wybór Modelu

| Model | Rozmiar | Najlepsze Zastosowanie | Szybkość |
|-------|---------|------------------------|----------|
| `qwen2.5-0.5b` | 0.5B | Szybka klasyfikacja | ⚡⚡⚡ |
| `qwen2.5-coder-0.5b` | 0.5B | Szybka generacja kodu | ⚡⚡⚡ |
| `gemma-2-2b` | 2B | Twórcze pisanie | ⚡⚡ |
| `phi-3.5-mini` | 3.5B | Kod, refaktoryzacja | ⚡⚡ |
| `phi-4-mini` | 4B | Ogólne, podsumowania | ⚡⚡ |
| `qwen2.5-7b` | 7B | Złożone rozumowanie | ⚡ |

---

## 🔗 Zasoby

- **Dokumentacja SDK**: https://github.com/microsoft/Foundry-Local/tree/main/sdk/python
- **Szybki Dostęp**: `Workshop/FOUNDRY_SDK_QUICKREF.md`
- **Podsumowanie Aktualizacji**: `Workshop/SAMPLES_UPDATE_SUMMARY.md`
- **Notatki Migracyjne**: `Workshop/SDK_MIGRATION_NOTES.md`

---

## 💡 Wskazówki

1. **Cache klientów**: `workshop_utils` automatycznie przechowuje dane
2. **Używaj mniejszych modeli**: Zacznij od `qwen2.5-0.5b` do testów
3. **Włącz statystyki użycia**: Ustaw `SHOW_USAGE=1`, aby śledzić tokeny
4. **Przetwarzanie wsadowe**: Przetwarzaj wiele promptów sekwencyjnie
5. **Obniż max_tokens**: Zmniejsza opóźnienia dla szybkich odpowiedzi

---

## 🎯 Przykładowe Przepływy Pracy

### Testuj Wszystko
```bash
python scripts/validate_samples.py
python scripts/test_samples.py --quick
```

### Benchmark Modeli
```bash
cd samples/session03
set BENCH_MODELS=phi-4-mini,qwen2.5-0.5b,gemma-2-2b
set BENCH_ROUNDS=3
python benchmark_oss_models.py
```

### Pipeline RAG
```bash
cd samples/session02
set RAG_QUESTION="What is RAG?"
python rag_pipeline.py
```

### System Multi-Agentowy
```bash
cd samples/session05
set AGENT_QUESTION="Why edge AI for healthcare?"
python agents_orchestrator.py
```

---

**Szybka Pomoc**: Uruchom dowolny przykład z `--help` lub sprawdź docstring:
```bash
python chat_bootstrap.py --help
# or
python -c "import chat_bootstrap; help(chat_bootstrap)"
```

---

**Wszystkie przykłady zaktualizowane w październiku 2025 zgodnie z najlepszymi praktykami Foundry Local SDK** ✨

---

**Zastrzeżenie**:  
Ten dokument został przetłumaczony za pomocą usługi tłumaczenia AI [Co-op Translator](https://github.com/Azure/co-op-translator). Chociaż staramy się zapewnić dokładność, prosimy pamiętać, że automatyczne tłumaczenia mogą zawierać błędy lub nieścisłości. Oryginalny dokument w jego języku źródłowym powinien być uznawany za autorytatywne źródło. W przypadku informacji krytycznych zaleca się skorzystanie z profesjonalnego tłumaczenia przez człowieka. Nie ponosimy odpowiedzialności za jakiekolwiek nieporozumienia lub błędne interpretacje wynikające z użycia tego tłumaczenia.