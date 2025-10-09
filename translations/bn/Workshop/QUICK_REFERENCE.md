<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a887b7e85782dadd3fd1216cd63b6c23",
  "translation_date": "2025-10-09T09:39:40+00:00",
  "source_file": "Workshop/QUICK_REFERENCE.md",
  "language_code": "bn"
}
-->
# ওয়ার্কশপ নমুনা - দ্রুত রেফারেন্স কার্ড

**সর্বশেষ আপডেট**: ৮ অক্টোবর, ২০২৫

---

## 🚀 দ্রুত শুরু

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

## 📂 নমুনার সংক্ষিপ্ত বিবরণ

| সেশন | নমুনা | উদ্দেশ্য | সময় |
|------|-------|----------|------|
| ০১ | `chat_bootstrap.py` | বেসিক চ্যাট + স্ট্রিমিং | ~৩০ সেকেন্ড |
| ০২ | `rag_pipeline.py` | এম্বেডিং সহ RAG | ~৪৫ সেকেন্ড |
| ০২ | `rag_eval_ragas.py` | RAG মূল্যায়ন | ~৬০ সেকেন্ড |
| ০৩ | `benchmark_oss_models.py` | মডেল বেঞ্চমার্কিং | ~২ মিনিট |
| ০৪ | `model_compare.py` | SLM বনাম LLM | ~৪৫ সেকেন্ড |
| ০৫ | `agents_orchestrator.py` | মাল্টি-এজেন্ট সিস্টেম | ~৬০ সেকেন্ড |
| ০৬ | `models_router.py` | ইন্টেন্ট রাউটিং | ~৪৫ সেকেন্ড |
| ০৬ | `models_pipeline.py` | মাল্টি-স্টেপ পাইপলাইন | ~৬০ সেকেন্ড |

---

## 🛠️ পরিবেশ ভেরিয়েবল

### প্রয়োজনীয়
```bash
# Choose model
set FOUNDRY_LOCAL_ALIAS=phi-4-mini

# Override endpoint (optional)
set FOUNDRY_LOCAL_ENDPOINT=http://localhost:8000

# Show token usage
set SHOW_USAGE=1
```

### সেশন-নির্দিষ্ট
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

## ✅ যাচাই ও পরীক্ষা

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

## 🐛 সমস্যা সমাধান

### সংযোগ ত্রুটি
```bash
# Check Foundry Local
foundry service status

# Start if needed
foundry service start
foundry model run phi-4-mini
```

### ইমপোর্ট ত্রুটি
```bash
# Install missing dependencies
pip install sentence-transformers ragas datasets

# Or install all
pip install -r Workshop/requirements.txt
```

### মডেল পাওয়া যায়নি
```bash
# List available models
foundry model ls

# Download model
foundry model download phi-4-mini
```

### ধীর কর্মক্ষমতা
```bash
# Use smaller model
set FOUNDRY_LOCAL_ALIAS=qwen2.5-0.5b

# Reduce benchmark rounds
set BENCH_ROUNDS=1
```

---

## 📖 সাধারণ প্যাটার্ন

### বেসিক চ্যাট
```python
from workshop_utils import chat_once

text, usage = chat_once(
    'phi-4-mini',
    messages=[{"role": "user", "content": "Hello"}],
    max_tokens=100,
    temperature=0.7
)
```

### ক্লায়েন্ট পাওয়া
```python
from workshop_utils import get_client

manager, client, model_id = get_client(
    alias='phi-4-mini',
    endpoint=None  # Auto-detect
)
```

### ত্রুটি পরিচালনা
```python
try:
    manager, client, model_id = get_client(alias)
except Exception as e:
    print(f"[ERROR] Failed: {e}")
    print("[INFO] Check: foundry service status")
    sys.exit(1)
```

### স্ট্রিমিং
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

## 📊 মডেল নির্বাচন

| মডেল | আকার | সেরা ব্যবহারের ক্ষেত্র | গতি |
|------|------|------------------------|------|
| `qwen2.5-0.5b` | ০.৫B | দ্রুত শ্রেণীবিভাগ | ⚡⚡⚡ |
| `qwen2.5-coder-0.5b` | ০.৫B | দ্রুত কোড জেনারেশন | ⚡⚡⚡ |
| `gemma-2-2b` | ২B | সৃজনশীল লেখা | ⚡⚡ |
| `phi-3.5-mini` | ৩.৫B | কোড, রিফ্যাক্টরিং | ⚡⚡ |
| `phi-4-mini` | ৪B | সাধারণ, সারাংশ | ⚡⚡ |
| `qwen2.5-7b` | ৭B | জটিল যুক্তি | ⚡ |

---

## 🔗 সম্পদ

- **SDK ডকস**: https://github.com/microsoft/Foundry-Local/tree/main/sdk/python
- **দ্রুত রেফারেন্স**: `Workshop/FOUNDRY_SDK_QUICKREF.md`
- **আপডেট সারাংশ**: `Workshop/SAMPLES_UPDATE_SUMMARY.md`
- **মাইগ্রেশন নোটস**: `Workshop/SDK_MIGRATION_NOTES.md`

---

## 💡 টিপস

1. **ক্লায়েন্ট ক্যাশ করুন**: `workshop_utils` এটি আপনার জন্য করে
2. **ছোট মডেল ব্যবহার করুন**: পরীক্ষার জন্য `qwen2.5-0.5b` দিয়ে শুরু করুন
3. **ব্যবহার পরিসংখ্যান সক্ষম করুন**: টোকেন ট্র্যাক করতে `SHOW_USAGE=1` সেট করুন
4. **ব্যাচ প্রসেসিং**: একাধিক প্রম্পট ক্রমান্বয়ে প্রক্রিয়া করুন
5. **কমিয়ে দিন max_tokens**: দ্রুত প্রতিক্রিয়ার জন্য বিলম্ব হ্রাস করে

---

## 🎯 নমুনা কার্যপ্রবাহ

### সবকিছু পরীক্ষা করুন
```bash
python scripts/validate_samples.py
python scripts/test_samples.py --quick
```

### মডেল বেঞ্চমার্ক করুন
```bash
cd samples/session03
set BENCH_MODELS=phi-4-mini,qwen2.5-0.5b,gemma-2-2b
set BENCH_ROUNDS=3
python benchmark_oss_models.py
```

### RAG পাইপলাইন
```bash
cd samples/session02
set RAG_QUESTION="What is RAG?"
python rag_pipeline.py
```

### মাল্টি-এজেন্ট সিস্টেম
```bash
cd samples/session05
set AGENT_QUESTION="Why edge AI for healthcare?"
python agents_orchestrator.py
```

---

**দ্রুত সহায়তা**: যেকোনো নমুনা `--help` দিয়ে চালান বা ডকস্ট্রিং দেখুন:
```bash
python chat_bootstrap.py --help
# or
python -c "import chat_bootstrap; help(chat_bootstrap)"
```

---

**সব নমুনা অক্টোবর ২০২৫-এ Foundry Local SDK-এর সেরা অনুশীলন অনুযায়ী আপডেট করা হয়েছে** ✨

---

**অস্বীকৃতি**:  
এই নথিটি AI অনুবাদ পরিষেবা [Co-op Translator](https://github.com/Azure/co-op-translator) ব্যবহার করে অনুবাদ করা হয়েছে। আমরা যথাসাধ্য সঠিকতার জন্য চেষ্টা করি, তবে অনুগ্রহ করে মনে রাখবেন যে স্বয়ংক্রিয় অনুবাদে ত্রুটি বা অসঙ্গতি থাকতে পারে। মূল ভাষায় থাকা নথিটিকে প্রামাণিক উৎস হিসেবে বিবেচনা করা উচিত। গুরুত্বপূর্ণ তথ্যের জন্য, পেশাদার মানব অনুবাদ সুপারিশ করা হয়। এই অনুবাদ ব্যবহারের ফলে কোনো ভুল বোঝাবুঝি বা ভুল ব্যাখ্যা হলে আমরা দায়বদ্ধ থাকব না।