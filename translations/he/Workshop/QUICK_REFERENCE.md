<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a887b7e85782dadd3fd1216cd63b6c23",
  "translation_date": "2025-10-09T16:57:06+00:00",
  "source_file": "Workshop/QUICK_REFERENCE.md",
  "language_code": "he"
}
-->
# דף עזר מהיר - דוגמאות לסדנה

**עדכון אחרון**: 8 באוקטובר, 2025

---

## 🚀 התחלה מהירה

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

## 📂 סקירה כללית של הדוגמאות

| מפגש | דוגמה | מטרה | זמן |
|------|-------|-------|------|
| 01 | `chat_bootstrap.py` | צ'אט בסיסי + סטרימינג | ~30 שניות |
| 02 | `rag_pipeline.py` | RAG עם הטמעות | ~45 שניות |
| 02 | `rag_eval_ragas.py` | הערכת RAG | ~60 שניות |
| 03 | `benchmark_oss_models.py` | השוואת ביצועי מודלים | ~2 דקות |
| 04 | `model_compare.py` | SLM מול LLM | ~45 שניות |
| 05 | `agents_orchestrator.py` | מערכת רב-סוכנים | ~60 שניות |
| 06 | `models_router.py` | ניתוב כוונות | ~45 שניות |
| 06 | `models_pipeline.py` | צינור רב-שלבי | ~60 שניות |

---

## 🛠️ משתני סביבה

### חיוניים
```bash
# Choose model
set FOUNDRY_LOCAL_ALIAS=phi-4-mini

# Override endpoint (optional)
set FOUNDRY_LOCAL_ENDPOINT=http://localhost:8000

# Show token usage
set SHOW_USAGE=1
```

### ספציפיים למפגש
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

## ✅ אימות ובדיקות

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

## 🐛 פתרון בעיות

### שגיאת חיבור
```bash
# Check Foundry Local
foundry service status

# Start if needed
foundry service start
foundry model run phi-4-mini
```

### שגיאת ייבוא
```bash
# Install missing dependencies
pip install sentence-transformers ragas datasets

# Or install all
pip install -r Workshop/requirements.txt
```

### מודל לא נמצא
```bash
# List available models
foundry model ls

# Download model
foundry model download phi-4-mini
```

### ביצועים איטיים
```bash
# Use smaller model
set FOUNDRY_LOCAL_ALIAS=qwen2.5-0.5b

# Reduce benchmark rounds
set BENCH_ROUNDS=1
```

---

## 📖 תבניות נפוצות

### צ'אט בסיסי
```python
from workshop_utils import chat_once

text, usage = chat_once(
    'phi-4-mini',
    messages=[{"role": "user", "content": "Hello"}],
    max_tokens=100,
    temperature=0.7
)
```

### קבלת לקוח
```python
from workshop_utils import get_client

manager, client, model_id = get_client(
    alias='phi-4-mini',
    endpoint=None  # Auto-detect
)
```

### טיפול בשגיאות
```python
try:
    manager, client, model_id = get_client(alias)
except Exception as e:
    print(f"[ERROR] Failed: {e}")
    print("[INFO] Check: foundry service status")
    sys.exit(1)
```

### סטרימינג
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

## 📊 בחירת מודלים

| מודל | גודל | מתאים ל | מהירות |
|------|------|---------|--------|
| `qwen2.5-0.5b` | 0.5B | סיווג מהיר | ⚡⚡⚡ |
| `qwen2.5-coder-0.5b` | 0.5B | יצירת קוד מהירה | ⚡⚡⚡ |
| `gemma-2-2b` | 2B | כתיבה יצירתית | ⚡⚡ |
| `phi-3.5-mini` | 3.5B | קוד, שיפוץ | ⚡⚡ |
| `phi-4-mini` | 4B | כללי, סיכום | ⚡⚡ |
| `qwen2.5-7b` | 7B | הסקת מסקנות מורכבת | ⚡ |

---

## 🔗 משאבים

- **תיעוד SDK**: https://github.com/microsoft/Foundry-Local/tree/main/sdk/python
- **עזר מהיר**: `Workshop/FOUNDRY_SDK_QUICKREF.md`
- **סיכום עדכונים**: `Workshop/SAMPLES_UPDATE_SUMMARY.md`
- **הערות מעבר**: `Workshop/SDK_MIGRATION_NOTES.md`

---

## 💡 טיפים

1. **שמור לקוחות במטמון**: `workshop_utils` עושה זאת עבורך
2. **השתמש במודלים קטנים יותר**: התחל עם `qwen2.5-0.5b` לבדיקות
3. **הפעל סטטיסטיקות שימוש**: הגדר `SHOW_USAGE=1` למעקב אחר טוקנים
4. **עיבוד בקבוצות**: עבד מספר הנחיות ברצף
5. **הקטן max_tokens**: מפחית זמן תגובה לתשובות מהירות

---

## 🎯 תהליכי עבודה לדוגמא

### בדוק הכל
```bash
python scripts/validate_samples.py
python scripts/test_samples.py --quick
```

### השוואת ביצועי מודלים
```bash
cd samples/session03
set BENCH_MODELS=phi-4-mini,qwen2.5-0.5b,gemma-2-2b
set BENCH_ROUNDS=3
python benchmark_oss_models.py
```

### צינור RAG
```bash
cd samples/session02
set RAG_QUESTION="What is RAG?"
python rag_pipeline.py
```

### מערכת רב-סוכנים
```bash
cd samples/session05
set AGENT_QUESTION="Why edge AI for healthcare?"
python agents_orchestrator.py
```

---

**עזרה מהירה**: הרץ כל דוגמה עם `--help` או בדוק את תיעוד הפונקציה:
```bash
python chat_bootstrap.py --help
# or
python -c "import chat_bootstrap; help(chat_bootstrap)"
```

---

**כל הדוגמאות עודכנו באוקטובר 2025 עם שיטות עבודה מומלצות של Foundry Local SDK** ✨

---

**כתב ויתור**:  
מסמך זה תורגם באמצעות שירות תרגום מבוסס בינה מלאכותית [Co-op Translator](https://github.com/Azure/co-op-translator). למרות שאנו שואפים לדיוק, יש לקחת בחשבון שתרגומים אוטומטיים עשויים להכיל שגיאות או אי דיוקים. המסמך המקורי בשפתו המקורית צריך להיחשב כמקור סמכותי. עבור מידע קריטי, מומלץ להשתמש בתרגום מקצועי על ידי אדם. איננו נושאים באחריות לאי הבנות או לפרשנויות שגויות הנובעות משימוש בתרגום זה.