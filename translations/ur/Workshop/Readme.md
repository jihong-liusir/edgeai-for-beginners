<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "48d0fb38be925084a6ebd957d4b045e5",
  "translation_date": "2025-10-09T06:52:19+00:00",
  "source_file": "Workshop/Readme.md",
  "language_code": "ur"
}
-->
# EdgeAI برائے ابتدائی - ورکشاپ

> **پروڈکشن کے لیے تیار ایج AI ایپلیکیشنز بنانے کا عملی راستہ**
>
> Microsoft Foundry Local کے ساتھ مقامی AI ڈیپلائمنٹ میں مہارت حاصل کریں، پہلے چیٹ کمپلیشن سے لے کر ملٹی ایجنٹ آرکیسٹریشن تک 6 ترقی پسند سیشنز میں۔

---

## 🎯 تعارف

**EdgeAI برائے ابتدائی ورکشاپ** میں خوش آمدید - یہ آپ کی عملی رہنمائی ہے جو آپ کو ایسے ذہین ایپلیکیشنز بنانے میں مدد دے گی جو مکمل طور پر مقامی ہارڈویئر پر چلتی ہیں۔ یہ ورکشاپ نظریاتی Edge AI تصورات کو حقیقی دنیا کی مہارتوں میں تبدیل کرتی ہے، Microsoft Foundry Local اور Small Language Models (SLMs) کے ذریعے بتدریج چیلنجنگ مشقوں کے ذریعے۔

### یہ ورکشاپ کیوں؟

**Edge AI انقلاب یہاں ہے**

دنیا بھر کی تنظیمیں تین اہم وجوہات کی بنا پر کلاؤڈ پر منحصر AI سے ایج کمپیوٹنگ کی طرف منتقل ہو رہی ہیں:

1. **پرائیویسی اور کمپلائنس** - حساس ڈیٹا کو مقامی طور پر پروسیس کریں بغیر کلاؤڈ پر منتقل کیے (HIPAA، GDPR، مالیاتی ضوابط)
2. **کارکردگی** - نیٹ ورک لیٹنسی کو ختم کریں (50-500ms مقامی بمقابلہ 500-2000ms کلاؤڈ راؤنڈ ٹرپ)
3. **لاگت کا کنٹرول** - فی ٹوکن API اخراجات کو ختم کریں اور کلاؤڈ اخراجات کے بغیر اسکیل کریں

**لیکن Edge AI مختلف ہے**

مقامی طور پر AI چلانے کے لیے نئی مہارتوں کی ضرورت ہوتی ہے:
- ماڈل کا انتخاب اور وسائل کی پابندیوں کے لیے اصلاح
- مقامی سروس مینجمنٹ اور ہارڈویئر ایکسیلیریشن
- چھوٹے ماڈلز کے لیے پرامپٹ انجینئرنگ
- ایج ڈیوائسز کے لیے پروڈکشن ڈیپلائمنٹ پیٹرنز

**یہ ورکشاپ وہ مہارتیں فراہم کرتی ہے**

6 مرکوز سیشنز (~3 گھنٹے کل)، آپ "ہیلو ورلڈ" سے پروڈکشن کے لیے تیار ملٹی ایجنٹ سسٹمز کی تعیناتی تک ترقی کریں گے - سب کچھ مقامی طور پر آپ کی مشین پر چل رہا ہوگا۔

---

## 📚 سیکھنے کے مقاصد

اس ورکشاپ کو مکمل کرنے کے بعد، آپ قابل ہوں گے:

### بنیادی مہارتیں
1. **مقامی AI سروسز کو تعینات اور منظم کریں**
   - Microsoft Foundry Local انسٹال اور کنفیگر کریں
   - ایج ڈیپلائمنٹ کے لیے مناسب ماڈلز کا انتخاب کریں
   - ماڈل لائف سائیکل کا انتظام کریں (ڈاؤن لوڈ، لوڈ، کیش)
   - وسائل کے استعمال کی نگرانی کریں اور کارکردگی کو بہتر بنائیں

2. **AI سے چلنے والی ایپلیکیشنز بنائیں**
   - مقامی طور پر OpenAI کے مطابق چیٹ کمپلیشنز نافذ کریں
   - Small Language Models کے لیے مؤثر پرامپٹس ڈیزائن کریں
   - بہتر UX کے لیے اسٹریمنگ جوابات کو ہینڈل کریں
   - مقامی ماڈلز کو موجودہ ایپلیکیشنز میں ضم کریں

3. **RAG (Retrieval Augmented Generation) سسٹمز بنائیں**
   - ایمبیڈنگز کے ساتھ سیمینٹک سرچ بنائیں
   - LLM جوابات کو ڈومین مخصوص علم میں گراؤنڈ کریں
   - RAG معیار کو انڈسٹری اسٹینڈرڈ میٹرکس کے ساتھ جانچیں
   - پروٹوٹائپ سے پروڈکشن تک اسکیل کریں

4. **ماڈل کی کارکردگی کو بہتر بنائیں**
   - اپنے استعمال کے کیس کے لیے متعدد ماڈلز کا بینچ مارک کریں
   - لیٹنسی، تھروپٹ، اور فرسٹ ٹوکن ٹائم کی پیمائش کریں
   - رفتار/معیار کے توازن کی بنیاد پر بہترین ماڈلز کا انتخاب کریں
   - حقیقی منظرناموں میں SLM بمقابلہ LLM کے تجارتی معاہدے کا موازنہ کریں

5. **ملٹی ایجنٹ سسٹمز کو آرکیسٹریٹ کریں**
   - مختلف کاموں کے لیے خصوصی ایجنٹس ڈیزائن کریں
   - ایجنٹ میموری اور سیاق و سباق کا انتظام کریں
   - پیچیدہ ورک فلو میں ایجنٹس کو مربوط کریں
   - متعدد ماڈلز کے درمیان درخواستوں کو ذہانت سے روٹ کریں

6. **پروڈکشن کے لیے تیار حل تعینات کریں**
   - ایرر ہینڈلنگ اور ری ٹرائی لاجک نافذ کریں
   - ٹوکن کے استعمال اور سسٹم وسائل کی نگرانی کریں
   - ماڈل-ایز-ٹولز پیٹرنز کے ساتھ اسکیل ایبل آرکیٹیکچرز بنائیں
   - ایج سے ہائبرڈ (ایج + کلاؤڈ) تک منتقلی کے راستے کی منصوبہ بندی کریں

---

## 🎓 سیکھنے کے نتائج

### آپ کیا بنائیں گے

اس ورکشاپ کے اختتام تک، آپ نے درج ذیل تخلیق کیا ہوگا:

| سیشن | ڈیلیورایبل | مظاہرہ شدہ مہارتیں |
|---------|-------------|---------------------|
| **1** | اسٹریمنگ کے ساتھ چیٹ ایپلیکیشن | سروس سیٹ اپ، بنیادی کمپلیشنز، اسٹریمنگ UX |
| **2** | RAG سسٹم کے ساتھ تشخیص | ایمبیڈنگز، سیمینٹک سرچ، معیار میٹرکس |
| **3** | ملٹی ماڈل بینچ مارک سوٹ | کارکردگی کی پیمائش، ماڈل کا موازنہ |
| **4** | SLM بمقابلہ LLM کمپیریٹر | تجارتی معاہدے کا تجزیہ، اصلاحی حکمت عملی |
| **5** | ملٹی ایجنٹ آرکیسٹریٹر | ایجنٹ ڈیزائن، میموری مینجمنٹ، ہم آہنگی |
| **6** | ذہین روٹنگ سسٹم | ارادے کا پتہ لگانا، ماڈل کا انتخاب، اسکیل ایبلٹی |

### مہارت کی میٹرکس

| مہارت کی سطح | سیشن 1-2 | سیشن 3-4 | سیشن 5-6 |
|-------------|-------------|-------------|-------------|
| **ابتدائی** | ✅ سیٹ اپ اور بنیادی باتیں | ⚠️ چیلنجنگ | ❌ بہت زیادہ |
| **درمیانی** | ✅ فوری جائزہ | ✅ بنیادی سیکھنا | ⚠️ اسٹریچ گولز |
| **ماہر** | ✅ آسانی سے مکمل کریں | ✅ اصلاح | ✅ پروڈکشن پیٹرنز |

### کیریئر کے لیے تیار مہارتیں

**اس ورکشاپ کے بعد، آپ تیار ہوں گے:**

✅ **پرائیویسی فرسٹ ایپلیکیشنز بنائیں**
- صحت کی دیکھ بھال کی ایپس جو مقامی طور پر PHI/PII کو ہینڈل کرتی ہیں
- مالیاتی خدمات جو کمپلائنس کی ضروریات کو پورا کرتی ہیں
- حکومتی نظام جو ڈیٹا کی خودمختاری کی ضرورت رکھتے ہیں

✅ **ایج ماحول کے لیے اصلاح کریں**
- محدود وسائل والے IoT ڈیوائسز
- آف لائن-فرسٹ موبائل ایپلیکیشنز
- کم لیٹنسی والے ریئل ٹائم سسٹمز

✅ **ذہین آرکیٹیکچرز ڈیزائن کریں**
- پیچیدہ ورک فلو کے لیے ملٹی ایجنٹ سسٹمز
- ہائبرڈ ایج-کلاؤڈ ڈیپلائمنٹس
- لاگت کے لحاظ سے بہتر AI انفراسٹرکچر

✅ **ایج AI اقدامات کی قیادت کریں**
- پروجیکٹس کے لیے ایج AI کی فزیبلٹی کا جائزہ لیں
- مناسب ماڈلز اور فریم ورک کا انتخاب کریں
- اسکیل ایبل مقامی AI حل آرکیٹیکٹ کریں

---

## 🗺️ ورکشاپ کا ڈھانچہ

### سیشن کا جائزہ (6 سیشنز × 30 منٹ = 3 گھنٹے)

| سیشن | موضوع | فوکس | دورانیہ |
|---------|-------|-------|----------|
| **1** | Foundry Local کے ساتھ شروعات | انسٹال، تصدیق، پہلے کمپلیشنز | 30 منٹ |
| **2** | RAG کے ساتھ AI حل بنانا | پرامپٹ انجینئرنگ، ایمبیڈنگز، تشخیص | 30 منٹ |
| **3** | اوپن سورس ماڈلز | ماڈل دریافت، بینچ مارکنگ، انتخاب | 30 منٹ |
| **4** | جدید ماڈلز | SLM بمقابلہ LLM، اصلاح، فریم ورک | 30 منٹ |
| **5** | AI سے چلنے والے ایجنٹس | ایجنٹ ڈیزائن، آرکیسٹریشن، میموری | 30 منٹ |
| **6** | ماڈلز بطور ٹولز | روٹنگ، چیننگ، اسکیلنگ حکمت عملی | 30 منٹ |

---

## 🚀 فوری آغاز

### ضروریات

**سسٹم کی ضروریات:**
- **OS**: Windows 10/11، macOS 11+، یا Linux (Ubuntu 20.04+)
- **RAM**: کم از کم 8GB، 16GB+ تجویز کردہ
- **اسٹوریج**: ماڈلز کے لیے 10GB+ خالی جگہ
- **CPU**: جدید پروسیسر AVX2 سپورٹ کے ساتھ
- **GPU** (اختیاری): CUDA-مطابقت پذیر یا Qualcomm NPU ایکسیلیریشن کے لیے

**سافٹ ویئر کی ضروریات:**
- **Python 3.8+** ([ڈاؤن لوڈ کریں](https://www.python.org/downloads/))
- **Microsoft Foundry Local** ([انسٹالیشن گائیڈ](../../../Workshop))
- **Git** ([ڈاؤن لوڈ کریں](https://git-scm.com/downloads))
- **Visual Studio Code** (تجویز کردہ) ([ڈاؤن لوڈ کریں](https://code.visualstudio.com/))

### 3 مراحل میں سیٹ اپ

#### 1. Foundry Local انسٹال کریں

**Windows:**
```powershell
winget install Microsoft.FoundryLocal
```

**macOS:**
```bash
brew tap microsoft/foundrylocal
brew install foundrylocal
```

**انسٹالیشن کی تصدیق کریں:**
```bash
foundry --version
foundry service status
```

#### 2. ریپوزٹری کلون کریں اور ڈیپینڈنسیز انسٹال کریں

```bash
# Clone repository
git clone https://github.com/microsoft/edgeai-for-beginners.git
cd edgeai-for-beginners/Workshop

# Create virtual environment
python -m venv .venv

# Activate virtual environment
# Windows:
.\.venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

#### 3. اپنا پہلا نمونہ چلائیں

```bash
# Start Foundry Local and load a model
foundry model run phi-4-mini

# Run the chat bootstrap sample
cd samples/session01
python chat_bootstrap.py "What is edge AI?"
```

**✅ کامیابی!** آپ کو ایج AI کے بارے میں اسٹریمنگ جواب نظر آنا چاہیے۔

---

## 📦 ورکشاپ کے وسائل

### Python نمونے

ہر تصور کو ظاہر کرنے والے ترقی پسند عملی مثالیں:

| سیشن | نمونہ | تفصیل | چلانے کا وقت |
|---------|--------|-------------|----------|
| 1 | [`chat_bootstrap.py`](../../../Workshop/samples/session01/chat_bootstrap.py) | بنیادی اور اسٹریمنگ چیٹ | ~30 سیکنڈ |
| 2 | [`rag_pipeline.py`](../../../Workshop/samples/session02/rag_pipeline.py) | ایمبیڈنگز کے ساتھ RAG | ~45 سیکنڈ |
| 2 | [`rag_eval_ragas.py`](../../../Workshop/samples/session02/rag_eval_ragas.py) | RAG معیار کی تشخیص | ~60 سیکنڈ |
| 3 | [`benchmark_oss_models.py`](../../../Workshop/samples/session03/benchmark_oss_models.py) | ملٹی ماڈل بینچ مارکنگ | ~2-3 منٹ |
| 4 | [`model_compare.py`](../../../Workshop/samples/session04/model_compare.py) | SLM بمقابلہ LLM موازنہ | ~45 سیکنڈ |
| 5 | [`agents_orchestrator.py`](../../../Workshop/samples/session05/agents_orchestrator.py) | ملٹی ایجنٹ سسٹم | ~60 سیکنڈ |
| 6 | [`models_router.py`](../../../Workshop/samples/session06/models_router.py) | ارادے پر مبنی روٹنگ | ~45 سیکنڈ |
| 6 | [`models_pipeline.py`](../../../Workshop/samples/session06/models_pipeline.py) | ملٹی اسٹیپ پائپ لائن | ~60 سیکنڈ |

### Jupyter نوٹ بکس

وضاحتوں اور بصریات کے ساتھ انٹرایکٹو ایکسپلوریشن:

| سیشن | نوٹ بک | تفصیل | مشکل |
|---------|----------|-------------|------------|
| 1 | [`session01_chat_bootstrap.ipynb`](./notebooks/session01_chat_bootstrap.ipynb) | چیٹ کی بنیادی باتیں اور اسٹریمنگ | ⭐ ابتدائی |
| 2 | [`session02_rag_pipeline.ipynb`](./notebooks/session02_rag_pipeline.ipynb) | RAG سسٹم بنائیں | ⭐⭐ درمیانی |
| 2 | [`session02_rag_eval_ragas.ipynb`](./notebooks/session02_rag_eval_ragas.ipynb) | RAG معیار کی تشخیص کریں | ⭐⭐ درمیانی |
| 3 | [`session03_benchmark_oss_models.ipynb`](./notebooks/session03_benchmark_oss_models.ipynb) | ماڈل بینچ مارکنگ | ⭐⭐ درمیانی |
| 4 | [`session04_model_compare.ipynb`](./notebooks/session04_model_compare.ipynb) | ماڈل کا موازنہ | ⭐⭐ درمیانی |
| 5 | [`session05_agents_orchestrator.ipynb`](./notebooks/session05_agents_orchestrator.ipynb) | ایجنٹ آرکیسٹریشن | ⭐⭐⭐ ماہر |
| 6 | [`session06_models_router.ipynb`](./notebooks/session06_models_router.ipynb) | ارادے کی روٹنگ | ⭐⭐⭐ ماہر |
| 6 | [`session06_models_pipeline.ipynb`](./notebooks/session06_models_pipeline.ipynb) | پائپ لائن آرکیسٹریشن | ⭐⭐⭐ ماہر |

### دستاویزات

جامع گائیڈز اور حوالہ جات:

| دستاویز | تفصیل | کب استعمال کریں |
|----------|-------------|----------|
| [QUICK_START.md](./QUICK_START.md) | تیز رفتار سیٹ اپ گائیڈ | شروع سے شروع کرتے وقت |
| [QUICK_REFERENCE.md](./QUICK_REFERENCE.md) | کمانڈ اور API چیٹ شیٹ | فوری جوابات کی ضرورت ہو |
| [FOUNDRY_SDK_QUICKREF.md](./FOUNDRY_SDK_QUICKREF.md) | SDK پیٹرنز اور مثالیں | کوڈ لکھتے وقت |
| [ENV_CONFIGURATION.md](./ENV_CONFIGURATION.md) | ماحولیات متغیر گائیڈ | نمونوں کو کنفیگر کرتے وقت |
| [SAMPLES_UPDATE_SUMMARY.md](./SAMPLES_UPDATE_SUMMARY.md) | تازہ ترین نمونہ بہتری | تبدیلیوں کو سمجھنا |
| [SDK_MIGRATION_NOTES.md](./SDK_MIGRATION_NOTES.md) | مائیگریشن گائیڈ | کوڈ اپ گریڈ کرتے وقت |
| [notebooks/TROUBLESHOOTING.md](./notebooks/TROUBLESHOOTING.md) | عام مسائل اور حل | مسائل کو ڈیبگ کرتے وقت |

---

## 🎓 سیکھنے کے راستے کی سفارشات

### ابتدائی افراد کے لیے (3-4 گھنٹے)
1. ✅ سیشن 1: شروعات (سیٹ اپ اور بنیادی چیٹ پر توجہ دیں)
2. ✅ سیشن 2: RAG کی بنیادی باتیں (تشخیص کو ابتدا میں چھوڑ دیں)
3. ✅ سیشن 3: سادہ بینچ مارکنگ (صرف 2 ماڈلز)
4. ⏭️ سیشنز 4-6 کو فی الحال چھوڑ دیں
5. 🔄 پہلے ایپلیکیشن بنانے کے بعد سیشنز 4-6 پر واپس آئیں

### درمیانی ڈویلپرز کے لیے (3 گھنٹے)
1. ⚡ سیشن 1: فوری سیٹ اپ کی تصدیق
2. ✅ سیشن 2: مکمل RAG پائپ لائن کے ساتھ تشخیص
3. ✅ سیشن 3: مکمل بینچ مارکنگ سوٹ
4. ✅ سیشن 4: ماڈل کی اصلاح
5. ✅ سیشنز 5-6: آرکیٹیکچر پیٹرنز پر توجہ دیں

### ماہرین کے لیے (2-3 گھنٹے)
1. ⚡ سیشنز 1-3: فوری جائزہ اور تصدیق
2. ✅ سیشن 4: اصلاح پر گہری نظر
3. ✅ سیشن 5: ملٹی ایجنٹ آرکیٹیکچر
4. ✅ سیشن 6: پروڈکشن پیٹرنز اور اسکیلنگ
5. 🚀 توسیع: کسٹم روٹنگ لاجک اور ہائبرڈ ڈیپلائمنٹس بنائیں

---

## ورکشاپ سیشن پیک (مرکوز 30 منٹ کی لیبز)

اگر آپ 6 سیشنز کے مختصر ورکشاپ فارمیٹ کی پیروی کر رہے ہیں، تو ان مخصوص گائیڈز کا استعمال کریں (ہر ایک وسیع ماڈیول دستاویزات کے ساتھ مطابقت رکھتا ہے):

| ورکشاپ سیشن | گائیڈ | بنیادی فوکس |
|------------------|-------|------------|
| 1 | [Session01-GettingStartedFoundryLocal](./Session01-GettingStartedFoundryLocal.md) | انسٹال، تصدیق، phi & GPT-OSS-20B چلائیں، ایکسیلیریشن |
| 2 | [Session02-BuildAISolutionsRAG](./Session02-BuildAISolutionsRAG.md) | پرامپٹ انجینئرنگ، RAG پیٹرنز، CSV اور دستاویز گراؤنڈنگ، مائیگریشن |
| 3 | [Session03-OpenSourceModels](./Session03-OpenSourceModels.md) | Hugging Face انٹیگریشن، بینچ مارکنگ، ماڈل کا انتخاب |
| 4 | [Session04-CuttingEdgeModels](./Session04-CuttingEdgeModels.md) | S
ہر سیشن فائل میں شامل ہوتا ہے: خلاصہ، سیکھنے کے مقاصد، 30 منٹ کا ڈیمو فلو، اسٹارٹر پروجیکٹ، توثیق کی چیک لسٹ، خرابیوں کا پتہ لگانا، اور آفیشل Foundry Local Python SDK کے حوالہ جات۔

### نمونہ اسکرپٹس

ورکشاپ کی ضروریات انسٹال کریں (ونڈوز):

```powershell
cd Workshop
py -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt
```

macOS / Linux:

```bash
cd Workshop
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

اگر Foundry Local سروس کو macOS سے مختلف (ونڈوز) مشین یا VM پر چلایا جا رہا ہو، تو اینڈ پوائنٹ ایکسپورٹ کریں:

```bash
export FOUNDRY_LOCAL_ENDPOINT=http://<windows-host>:5273/v1
```

| سیشن | اسکرپٹ(س) | وضاحت |
|------|-----------|-------|
| 1 | `samples/session01/chat_bootstrap.py` | سروس شروع کریں اور چیٹ اسٹریم کریں |
| 2 | `samples/session02/rag_pipeline.py` | کم سے کم RAG (ان-میموری ایمبیڈنگز) |
|   | `samples/session02/rag_eval_ragas.py` | RAG کی تشخیص ragas میٹرکس کے ساتھ |
| 3 | `samples/session03/benchmark_oss_models.py` | ملٹی ماڈل لیٹنسی اور تھروپٹ بینچ مارکنگ |
| 4 | `samples/session04/model_compare.py` | SLM بمقابلہ LLM موازنہ (لیٹنسی اور نمونہ آؤٹ پٹ) |
| 5 | `samples/session05/agents_orchestrator.py` | دو ایجنٹ تحقیق → ایڈیٹوریل پائپ لائن |
| 6 | `samples/session06/models_router.py` | ارادے پر مبنی روٹنگ ڈیمو |
|   | `samples/session06/models_pipeline.py` | ملٹی اسٹیپ پلان/ایگزیکیوٹ/ریفائن چین |

### ماحول کے متغیرات (نمونوں میں عام)

| متغیر | مقصد | مثال |
|-------|-------|-------|
| `FOUNDRY_LOCAL_ALIAS` | بنیادی نمونوں کے لیے ڈیفالٹ سنگل ماڈل عرف | `phi-4-mini` |
| `SLM_ALIAS` / `LLM_ALIAS` | واضح SLM بمقابلہ بڑے ماڈل کا موازنہ | `phi-4-mini` / `gpt-oss-20b` |
| `BENCH_MODELS` | بینچ مارک کے لیے عرف کی کاما فہرست | `qwen2.5-0.5b,gemma-2-2b,mistral-7b` |
| `BENCH_ROUNDS` | ہر ماڈل کے لیے بینچ مارک دہرانا | `3` |
| `BENCH_PROMPT` | بینچ مارکنگ میں استعمال ہونے والا پرامپٹ | `Explain retrieval augmented generation briefly.` |
| `EMBED_MODEL` | جملہ-ٹرانسفارمرز ایمبیڈنگ ماڈل | `sentence-transformers/all-MiniLM-L6-v2` |
| `RAG_QUESTION` | RAG پائپ لائن کے لیے ٹیسٹ سوال کو اووررائیڈ کریں | `Why use RAG with local inference?` |
| `AGENT_QUESTION` | ایجنٹس پائپ لائن سوال کو اووررائیڈ کریں | `Explain why edge AI matters for compliance.` |
| `AGENT_MODEL_PRIMARY` | تحقیق ایجنٹ کے لیے ماڈل عرف | `phi-4-mini` |
| `AGENT_MODEL_EDITOR` | ایڈیٹر ایجنٹ کے لیے ماڈل عرف (مختلف ہو سکتا ہے) | `gpt-oss-20b` |
| `SHOW_USAGE` | جب `1` ہو، ہر تکمیل پر ٹوکن استعمال پرنٹ کرتا ہے | `1` |
| `RETRY_ON_FAIL` | جب `1` ہو، عارضی چیٹ غلطیوں پر ایک بار دوبارہ کوشش کریں | `1` |
| `RETRY_BACKOFF` | دوبارہ کوشش سے پہلے انتظار کرنے کے سیکنڈز | `1.0` |

اگر کوئی متغیر سیٹ نہیں کیا گیا ہو، تو اسکرپٹس معقول ڈیفالٹس پر واپس آ جاتے ہیں۔ سنگل ماڈل ڈیموز کے لیے آپ کو عام طور پر صرف `FOUNDRY_LOCAL_ALIAS` کی ضرورت ہوتی ہے۔

### یوٹیلیٹی ماڈیول

تمام نمونے اب ایک مددگار `samples/workshop_utils.py` شیئر کرتے ہیں جو فراہم کرتا ہے:

* Cached `FoundryLocalManager` + OpenAI کلائنٹ تخلیق
* `chat_once()` مددگار اختیاری دوبارہ کوشش + استعمال پرنٹنگ کے ساتھ
* سادہ ٹوکن استعمال رپورٹنگ (فعال کریں `SHOW_USAGE=1` کے ذریعے)

یہ نقل کو کم کرتا ہے اور مقامی ماڈل آرکیسٹریشن کے لیے بہترین طریقوں کو اجاگر کرتا ہے۔

## اختیاری بہتریاں (کراس-سیشن)

| تھیم | بہتری | سیشنز | Env / ٹوگل |
|------|-------|-------|------------|
| تعین | مقررہ درجہ حرارت + مستحکم پرامپٹ سیٹ | 1–6 | `temperature=0`, `top_p=1` سیٹ کریں |
| ٹوکن استعمال کی مرئیت | مستقل لاگت/کارکردگی کی تعلیم | 1–6 | `SHOW_USAGE=1` |
| پہلا ٹوکن اسٹریم کرنا | محسوس شدہ لیٹنسی میٹرک | 1,3,4,6 | `BENCH_STREAM=1` (بینچ مارک) |
| دوبارہ کوشش کی لچک | عارضی کولڈ اسٹارٹ کو ہینڈل کرتا ہے | تمام | `RETRY_ON_FAIL=1` + `RETRY_BACKOFF` |
| ملٹی-ماڈل ایجنٹس | مختلف کردار کی مہارت | 5 | `AGENT_MODEL_PRIMARY`, `AGENT_MODEL_EDITOR` |
| موافقت پذیر روٹنگ | ارادے + لاگت کی ہیورسٹکس | 6 | روٹر کو اسکیلیشن منطق کے ساتھ بڑھائیں |
| ویکٹر میموری | طویل مدتی معنوی یادداشت | 2,5,6 | FAISS/Chroma ایمبیڈنگ انڈیکس کو ضم کریں |
| ٹریس ایکسپورٹ | آڈٹنگ اور تشخیص | 2,5,6 | ہر مرحلے پر JSON لائنز شامل کریں |
| کوالٹی روبریکس | معیاری ٹریکنگ | 3–6 | ثانوی اسکورنگ پرامپٹس |
| اسموک ٹیسٹس | ورکشاپ سے پہلے کی فوری توثیق | تمام | `python Workshop/tests/smoke.py` |

### تعیناتی فوری آغاز

```powershell
set FOUNDRY_LOCAL_ALIAS=phi-4-mini
set SHOW_USAGE=1
python Workshop\tests\smoke.py
```

متوقع مستحکم ٹوکن گنتی ایک جیسے ان پٹس کے بار بار استعمال پر۔

### RAG تشخیص (سیشن 2)

جواب کی مطابقت، وفاداری، اور سیاق و سباق کی درستگی کو چھوٹے مصنوعی ڈیٹا سیٹ پر حساب کرنے کے لیے `rag_eval_ragas.py` استعمال کریں:

```powershell
python samples/session02/rag_eval_ragas.py
```

بڑے JSONL سوالات، سیاق و سباق، اور گراؤنڈ ٹروتھ فراہم کر کے توسیع کریں، پھر اسے Hugging Face `Dataset` میں تبدیل کریں۔

## CLI کمانڈ درستگی ضمیمہ

ورکشاپ جان بوجھ کر صرف موجودہ دستاویزی / مستحکم Foundry Local CLI کمانڈز استعمال کرتی ہے۔

### مستحکم کمانڈز کا حوالہ

| زمرہ | کمانڈ | مقصد |
|------|-------|-------|
| کور | `foundry --version` | انسٹال شدہ ورژن دکھائیں |
| کور | `foundry init` | کنفیگریشن شروع کریں |
| سروس | `foundry service start` | مقامی سروس شروع کریں (اگر خودکار نہیں) |
| سروس | `foundry status` | سروس کی حیثیت دکھائیں |
| ماڈلز | `foundry model list` | کیٹلاگ / دستیاب ماڈلز کی فہرست |
| ماڈلز | `foundry model download <alias>` | ماڈل ویٹس کو کیش میں ڈاؤن لوڈ کریں |
| ماڈلز | `foundry model run <alias>` | ماڈل کو مقامی طور پر لانچ کریں؛ ایک شاٹ کے لیے `--prompt` کے ساتھ ملائیں |
| ماڈلز | `foundry model unload <alias>` / `foundry model stop <alias>` | ماڈل کو میموری سے ان لوڈ کریں (اگر سپورٹ ہو) |
| کیش | `foundry cache list` | کیش شدہ (ڈاؤن لوڈ شدہ) ماڈلز کی فہرست |
| سسٹم | `foundry system info` | ہارڈویئر اور ایکسیلیریشن صلاحیتوں کا اسنیپ شاٹ |
| سسٹم | `foundry system gpu-info` | GPU تشخیصی معلومات |
| کنفیگ | `foundry config list` | موجودہ کنفیگ ویلیوز دکھائیں |
| کنفیگ | `foundry config set <key> <value>` | کنفیگریشن کو اپ ڈیٹ کریں |

### ایک شاٹ پرامپٹ پیٹرن

منسوخ شدہ `model chat` سب کمانڈ کے بجائے، استعمال کریں:

```powershell
foundry model run <alias> --prompt "Your question here"
```

یہ ایک واحد پرامپٹ/جواب سائیکل کو انجام دیتا ہے اور پھر باہر نکلتا ہے۔

### ہٹائے گئے / گریز کیے گئے پیٹرنز

| منسوخ شدہ / غیر دستاویزی | متبادل / رہنمائی |
|--------------------------|------------------|
| `foundry model chat <model> "..."` | `foundry model run <model> --prompt "..."` |
| `foundry model list --running` | سادہ `foundry model list` + حالیہ سرگرمی / لاگز استعمال کریں |
| `foundry model list --cached` | `foundry cache list` |
| `foundry model stats <model>` | بینچ مارک پائتھون اسکرپٹ + OS ٹولز (ٹاسک مینیجر / `nvidia-smi`) استعمال کریں |
| `foundry model benchmark ...` | `samples/session03/benchmark_oss_models.py` |

### بینچ مارکنگ اور ٹیلیمیٹری

- لیٹنسی، p95، ٹوکنز/سیکنڈ: `samples/session03/benchmark_oss_models.py`
- پہلا ٹوکن لیٹنسی (اسٹریمنگ): `BENCH_STREAM=1` سیٹ کریں
- وسائل کا استعمال: OS مانیٹرز (ٹاسک مینیجر، ایکٹیویٹی مانیٹر، `nvidia-smi`) + `foundry system info`.

جیسے ہی نئے CLI ٹیلیمیٹری کمانڈز اپ اسٹریم مستحکم ہوں گے، انہیں سیشن مارک ڈاؤنز میں کم سے کم ترمیم کے ساتھ شامل کیا جا سکتا ہے۔

### خودکار لنٹ گارڈ

ایک خودکار لنٹر منسوخ شدہ CLI پیٹرنز کو مارک ڈاؤن فائلز کے کوڈ بلاکس کے اندر دوبارہ متعارف کرانے سے روکتا ہے:

اسکرپٹ: `Workshop/scripts/lint_markdown_cli.py`

منسوخ شدہ پیٹرنز کو کوڈ فینسز کے اندر بلاک کیا جاتا ہے۔

تجویز کردہ متبادل:
| منسوخ شدہ | متبادل |
|----------|--------|
| `foundry model chat <a> "..."` | `foundry model run <a> --prompt "..."` |
| `model list --running` | `model list` |
| `model list --cached` | `cache list` |
| `model stats` | بینچ مارک اسکرپٹ + سسٹم ٹولز |
| `model benchmark` | `samples/session03/benchmark_oss_models.py` |
| `model list --available` | `model list` |

مقامی طور پر چلائیں:
```powershell
python Workshop\scripts\lint_markdown_cli.py --verbose
```

GitHub ایکشن: `.github/workflows/markdown-cli-lint.yml` ہر پش اور PR پر چلتا ہے۔

اختیاری پری-کمیٹ ہک:
```bash
echo "python Workshop/scripts/lint_markdown_cli.py" > .git/hooks/pre-commit
chmod +x .git/hooks/pre-commit
```

## فوری CLI → SDK مائیگریشن ٹیبل

| کام | CLI ون لائنر | SDK (پائتھون) مساوی | نوٹس |
|-----|-------------|---------------------|------|
| ماڈل کو ایک بار چلائیں (پرامپٹ) | `foundry model run phi-4-mini --prompt "Hello"` | `manager=FoundryLocalManager("phi-4-mini"); client=OpenAI(base_url=manager.endpoint, api_key=manager.api_key or "not-needed"); client.chat.completions.create(model=manager.get_model_info("phi-4-mini").id, messages=[{"role":"user","content":"Hello"}])` | SDK سروس اور کیشنگ کو خود بخود شروع کرتا ہے |
| ماڈل ڈاؤن لوڈ کریں (کیش) | `foundry model download qwen2.5-0.5b` | `FoundryLocalManager("qwen2.5-0.5b")  # triggers download/load` | مینیجر بہترین ویریئنٹ کا انتخاب کرتا ہے اگر عرف متعدد بلڈز پر میپ کرتا ہو |
| کیٹلاگ کی فہرست | `foundry model list` | `# use manager for each alias or maintain known list` | CLI مجموعی ہے؛ SDK فی عرف انسٹیٹیوشن فی الحال |
| کیش شدہ ماڈلز کی فہرست | `foundry cache list` | `manager.list_cached_models()` | مینیجر انیشیٹ کے بعد (کسی بھی عرف کے ساتھ) |
| GPU ایکسیلیریشن فعال کریں | `foundry config set compute.onnx.enable_gpu true` | `# CLI action; SDK assumes config already applied` | کنفیگریشن بیرونی سائیڈ ایفیکٹ ہے |
| اینڈ پوائنٹ URL حاصل کریں | (غیر واضح) | `manager.endpoint` | OpenAI-مطابقت پذیر کلائنٹ بنانے کے لیے استعمال ہوتا ہے |
| ماڈل کو گرم کریں | `foundry model run <alias>` پھر پہلا پرامپٹ | `chat_once(alias, messages=[...])` (یوٹیلیٹی) | یوٹیلیٹیز ابتدائی کولڈ لیٹنسی وارم اپ کو ہینڈل کرتی ہیں |
| لیٹنسی کی پیمائش کریں | `python benchmark_oss_models.py` | `import benchmark_oss_models` (یا نیا ایکسپورٹر اسکرپٹ) | مستقل میٹرکس کے لیے اسکرپٹ کو ترجیح دیں |
| ماڈل کو روکیں / ان لوڈ کریں | `foundry model unload <alias>` | (ظاہر نہیں کیا گیا – سروس / پروسیس کو دوبارہ شروع کریں) | ورکشاپ فلو کے لیے عام طور پر ضروری نہیں |
| ٹوکن استعمال حاصل کریں | (آؤٹ پٹ دیکھیں) | `resp.usage.total_tokens` | فراہم کیا گیا اگر بیک اینڈ استعمال آبجیکٹ واپس کرے |

## بینچ مارک مارک ڈاؤن ایکسپورٹ

اسکرپٹ `Workshop/scripts/export_benchmark_markdown.py` استعمال کریں تاکہ تازہ بینچ مارک چلایا جا سکے (اسی منطق جیسے `samples/session03/benchmark_oss_models.py`) اور ایک GitHub-دوستانہ مارک ڈاؤن ٹیبل اور خام JSON جاری کریں۔

### مثال

```powershell
python Workshop\scripts\export_benchmark_markdown.py --models "qwen2.5-0.5b,gemma-2-2b,mistral-7b" --prompt "Explain retrieval augmented generation briefly." --rounds 3 --output benchmark_report.md
```

پیدا شدہ فائلیں:
| فائل | مواد |
|------|------|
| `benchmark_report.md` | مارک ڈاؤن ٹیبل + تشریحی اشارے |
| `benchmark_report.json` | خام میٹرکس آرے (فرق / رجحان ٹریکنگ کے لیے) |

ماحول میں `BENCH_STREAM=1` سیٹ کریں تاکہ پہلے ٹوکن لیٹنسی کو شامل کیا جا سکے اگر سپورٹ ہو۔

---

**ڈسکلیمر**:  
یہ دستاویز AI ترجمہ سروس [Co-op Translator](https://github.com/Azure/co-op-translator) کا استعمال کرتے ہوئے ترجمہ کی گئی ہے۔ ہم درستگی کے لیے کوشش کرتے ہیں، لیکن براہ کرم آگاہ رہیں کہ خودکار ترجمے میں غلطیاں یا غیر درستیاں ہو سکتی ہیں۔ اصل دستاویز کو اس کی اصل زبان میں مستند ذریعہ سمجھا جانا چاہیے۔ اہم معلومات کے لیے، پیشہ ور انسانی ترجمہ کی سفارش کی جاتی ہے۔ ہم اس ترجمے کے استعمال سے پیدا ہونے والی کسی بھی غلط فہمی یا غلط تشریح کے ذمہ دار نہیں ہیں۔