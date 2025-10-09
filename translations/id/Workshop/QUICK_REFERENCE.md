<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a887b7e85782dadd3fd1216cd63b6c23",
  "translation_date": "2025-10-09T19:29:23+00:00",
  "source_file": "Workshop/QUICK_REFERENCE.md",
  "language_code": "id"
}
-->
# Kartu Referensi Cepat - Contoh Workshop

**Terakhir Diperbarui**: 8 Oktober 2025

---

## 🚀 Mulai Cepat

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

## 📂 Ikhtisar Contoh

| Sesi | Contoh | Tujuan | Waktu |
|------|--------|--------|-------|
| 01 | `chat_bootstrap.py` | Chat dasar + streaming | ~30 detik |
| 02 | `rag_pipeline.py` | RAG dengan embeddings | ~45 detik |
| 02 | `rag_eval_ragas.py` | Evaluasi RAG | ~60 detik |
| 03 | `benchmark_oss_models.py` | Benchmarking model | ~2 menit |
| 04 | `model_compare.py` | SLM vs LLM | ~45 detik |
| 05 | `agents_orchestrator.py` | Sistem multi-agen | ~60 detik |
| 06 | `models_router.py` | Routing intent | ~45 detik |
| 06 | `models_pipeline.py` | Pipeline multi-langkah | ~60 detik |

---

## 🛠️ Variabel Lingkungan

### Penting
```bash
# Choose model
set FOUNDRY_LOCAL_ALIAS=phi-4-mini

# Override endpoint (optional)
set FOUNDRY_LOCAL_ENDPOINT=http://localhost:8000

# Show token usage
set SHOW_USAGE=1
```

### Spesifik Sesi
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

## ✅ Validasi & Pengujian

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

## 🐛 Pemecahan Masalah

### Kesalahan Koneksi
```bash
# Check Foundry Local
foundry service status

# Start if needed
foundry service start
foundry model run phi-4-mini
```

### Kesalahan Impor
```bash
# Install missing dependencies
pip install sentence-transformers ragas datasets

# Or install all
pip install -r Workshop/requirements.txt
```

### Model Tidak Ditemukan
```bash
# List available models
foundry model ls

# Download model
foundry model download phi-4-mini
```

### Performa Lambat
```bash
# Use smaller model
set FOUNDRY_LOCAL_ALIAS=qwen2.5-0.5b

# Reduce benchmark rounds
set BENCH_ROUNDS=1
```

---

## 📖 Pola Umum

### Chat Dasar
```python
from workshop_utils import chat_once

text, usage = chat_once(
    'phi-4-mini',
    messages=[{"role": "user", "content": "Hello"}],
    max_tokens=100,
    temperature=0.7
)
```

### Mendapatkan Client
```python
from workshop_utils import get_client

manager, client, model_id = get_client(
    alias='phi-4-mini',
    endpoint=None  # Auto-detect
)
```

### Penanganan Kesalahan
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

## 📊 Pemilihan Model

| Model | Ukuran | Terbaik Untuk | Kecepatan |
|-------|--------|---------------|-----------|
| `qwen2.5-0.5b` | 0.5B | Klasifikasi cepat | ⚡⚡⚡ |
| `qwen2.5-coder-0.5b` | 0.5B | Generasi kode cepat | ⚡⚡⚡ |
| `gemma-2-2b` | 2B | Penulisan kreatif | ⚡⚡ |
| `phi-3.5-mini` | 3.5B | Kode, refactoring | ⚡⚡ |
| `phi-4-mini` | 4B | Umum, ringkasan | ⚡⚡ |
| `qwen2.5-7b` | 7B | Penalaran kompleks | ⚡ |

---

## 🔗 Sumber Daya

- **Dokumentasi SDK**: https://github.com/microsoft/Foundry-Local/tree/main/sdk/python
- **Referensi Cepat**: `Workshop/FOUNDRY_SDK_QUICKREF.md`
- **Ringkasan Pembaruan**: `Workshop/SAMPLES_UPDATE_SUMMARY.md`
- **Catatan Migrasi**: `Workshop/SDK_MIGRATION_NOTES.md`

---

## 💡 Tips

1. **Cache client**: `workshop_utils` sudah menyediakan cache untuk Anda
2. **Gunakan model kecil**: Mulailah dengan `qwen2.5-0.5b` untuk pengujian
3. **Aktifkan statistik penggunaan**: Atur `SHOW_USAGE=1` untuk melacak token
4. **Pemrosesan batch**: Proses beberapa prompt secara berurutan
5. **Kurangi max_tokens**: Mengurangi latensi untuk respons cepat

---

## 🎯 Alur Kerja Contoh

### Uji Semua
```bash
python scripts/validate_samples.py
python scripts/test_samples.py --quick
```

### Benchmark Model
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

### Sistem Multi-Agen
```bash
cd samples/session05
set AGENT_QUESTION="Why edge AI for healthcare?"
python agents_orchestrator.py
```

---

**Bantuan Cepat**: Jalankan contoh apa pun dengan `--help` atau periksa docstring:
```bash
python chat_bootstrap.py --help
# or
python -c "import chat_bootstrap; help(chat_bootstrap)"
```

---

**Semua contoh diperbarui Oktober 2025 dengan praktik terbaik Foundry Local SDK** ✨

---

**Penafian**:  
Dokumen ini telah diterjemahkan menggunakan layanan terjemahan AI [Co-op Translator](https://github.com/Azure/co-op-translator). Meskipun kami berupaya untuk memberikan hasil yang akurat, harap diperhatikan bahwa terjemahan otomatis mungkin mengandung kesalahan atau ketidakakuratan. Dokumen asli dalam bahasa aslinya harus dianggap sebagai sumber yang berwenang. Untuk informasi yang bersifat kritis, disarankan menggunakan jasa terjemahan manusia profesional. Kami tidak bertanggung jawab atas kesalahpahaman atau interpretasi yang keliru yang timbul dari penggunaan terjemahan ini.