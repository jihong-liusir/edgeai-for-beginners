<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "48d0fb38be925084a6ebd957d4b045e5",
  "translation_date": "2025-10-08T21:47:26+00:00",
  "source_file": "Workshop/Readme.md",
  "language_code": "fa"
}
-->
# EdgeAI برای مبتدیان - کارگاه

> **مسیر یادگیری عملی برای ساخت برنامه‌های Edge AI آماده تولید**
>
> تسلط بر استقرار هوش مصنوعی محلی با Microsoft Foundry Local، از اولین تکمیل چت تا هماهنگی چند عامل در ۶ جلسه پیشرفته.

---

## 🎯 مقدمه

به **کارگاه EdgeAI برای مبتدیان** خوش آمدید - راهنمای عملی شما برای ساخت برنامه‌های هوشمند که به طور کامل بر روی سخت‌افزار محلی اجرا می‌شوند. این کارگاه مفاهیم نظری Edge AI را به مهارت‌های دنیای واقعی تبدیل می‌کند، از طریق تمرین‌های چالش‌برانگیز تدریجی با استفاده از Microsoft Foundry Local و مدل‌های زبان کوچک (SLMs).

### چرا این کارگاه؟

**انقلاب Edge AI آغاز شده است**

سازمان‌ها در سراسر جهان به دلایل مهم زیر از هوش مصنوعی وابسته به ابر به محاسبات لبه‌ای روی آورده‌اند:

1. **حریم خصوصی و انطباق** - پردازش داده‌های حساس به صورت محلی بدون انتقال به ابر (HIPAA، GDPR، مقررات مالی)
2. **عملکرد** - حذف تأخیر شبکه (۵۰-۵۰۰ میلی‌ثانیه محلی در مقابل ۵۰۰-۲۰۰۰ میلی‌ثانیه رفت و برگشت ابر)
3. **کنترل هزینه** - حذف هزینه‌های API بر اساس توکن و مقیاس‌پذیری بدون هزینه‌های ابر

**اما Edge AI متفاوت است**

اجرای هوش مصنوعی در محل نیاز به مهارت‌های جدید دارد:
- انتخاب و بهینه‌سازی مدل برای محدودیت‌های منابع
- مدیریت خدمات محلی و شتاب‌دهی سخت‌افزاری
- مهندسی درخواست برای مدل‌های کوچک‌تر
- الگوهای استقرار تولید برای دستگاه‌های لبه‌ای

**این کارگاه این مهارت‌ها را ارائه می‌دهد**

در ۶ جلسه متمرکز (~۳ ساعت در مجموع)، شما از "سلام دنیا" تا استقرار سیستم‌های چند عاملی آماده تولید پیشرفت خواهید کرد - همه به صورت محلی بر روی دستگاه شما اجرا می‌شوند.

---

## 📚 اهداف یادگیری

با تکمیل این کارگاه، شما قادر خواهید بود:

### مهارت‌های اصلی
1. **استقرار و مدیریت خدمات هوش مصنوعی محلی**
   - نصب و پیکربندی Microsoft Foundry Local
   - انتخاب مدل‌های مناسب برای استقرار لبه‌ای
   - مدیریت چرخه عمر مدل (دانلود، بارگذاری، کش)
   - نظارت بر استفاده از منابع و بهینه‌سازی عملکرد

2. **ساخت برنامه‌های هوش مصنوعی**
   - اجرای تکمیل‌های چت سازگار با OpenAI به صورت محلی
   - طراحی درخواست‌های مؤثر برای مدل‌های زبان کوچک
   - مدیریت پاسخ‌های جریان‌دار برای تجربه کاربری بهتر
   - ادغام مدل‌های محلی در برنامه‌های موجود

3. **ایجاد سیستم‌های RAG (تولید تقویت‌شده با بازیابی)**
   - ساخت جستجوی معنایی با تعبیه‌ها
   - پایه‌گذاری پاسخ‌های LLM در دانش خاص دامنه
   - ارزیابی کیفیت RAG با معیارهای استاندارد صنعتی
   - مقیاس‌پذیری از نمونه اولیه تا تولید

4. **بهینه‌سازی عملکرد مدل**
   - ارزیابی چندین مدل برای مورد استفاده شما
   - اندازه‌گیری تأخیر، توان عملیاتی، و زمان اولین توکن
   - انتخاب مدل‌های بهینه بر اساس تعادل سرعت/کیفیت
   - مقایسه SLM و LLM در سناریوهای واقعی

5. **هماهنگی سیستم‌های چند عاملی**
   - طراحی عوامل تخصصی برای وظایف مختلف
   - پیاده‌سازی حافظه عامل و مدیریت زمینه
   - هماهنگی عوامل در جریان‌های کاری پیچیده
   - مسیریابی درخواست‌ها به صورت هوشمندانه بین مدل‌های متعدد

6. **استقرار راه‌حل‌های آماده تولید**
   - پیاده‌سازی مدیریت خطا و منطق تلاش مجدد
   - نظارت بر استفاده از توکن و منابع سیستم
   - ساخت معماری‌های مقیاس‌پذیر با الگوهای مدل به عنوان ابزار
   - برنامه‌ریزی مسیرهای مهاجرت از لبه به ترکیبی (لبه + ابر)

---

## 🎓 نتایج یادگیری

### آنچه خواهید ساخت

تا پایان این کارگاه، شما موارد زیر را ایجاد خواهید کرد:

| جلسه | خروجی | مهارت‌های نشان داده شده |
|------|-------|--------------------------|
| **۱** | برنامه چت با جریان | تنظیم خدمات، تکمیل‌های پایه، تجربه کاربری جریان |
| **۲** | سیستم RAG با ارزیابی | تعبیه‌ها، جستجوی معنایی، معیارهای کیفیت |
| **۳** | مجموعه ارزیابی چند مدل | اندازه‌گیری عملکرد، مقایسه مدل‌ها |
| **۴** | مقایسه‌کننده SLM و LLM | تحلیل تعادل، استراتژی‌های بهینه‌سازی |
| **۵** | هماهنگ‌کننده چند عامل | طراحی عامل، مدیریت حافظه، هماهنگی |
| **۶** | سیستم مسیریابی هوشمند | تشخیص قصد، انتخاب مدل، مقیاس‌پذیری |

### ماتریس شایستگی

| سطح مهارت | جلسه ۱-۲ | جلسه ۳-۴ | جلسه ۵-۶ |
|-----------|----------|----------|----------|
| **مبتدی** | ✅ تنظیم و اصول | ⚠️ چالش‌برانگیز | ❌ خیلی پیشرفته |
| **متوسط** | ✅ مرور سریع | ✅ یادگیری اصلی | ⚠️ اهداف کششی |
| **پیشرفته** | ✅ به راحتی | ✅ پالایش | ✅ الگوهای تولید |

### مهارت‌های آماده شغلی

**پس از این کارگاه، شما آماده خواهید بود:**

✅ **ساخت برنامه‌های اولویت‌دار حریم خصوصی**
- برنامه‌های مراقبت‌های بهداشتی که PHI/PII را به صورت محلی مدیریت می‌کنند
- خدمات مالی با الزامات انطباق
- سیستم‌های دولتی با نیازهای حاکمیت داده

✅ **بهینه‌سازی برای محیط‌های لبه‌ای**
- دستگاه‌های IoT با منابع محدود
- برنامه‌های موبایل آفلاین اول
- سیستم‌های بلادرنگ با تأخیر کم

✅ **طراحی معماری‌های هوشمند**
- سیستم‌های چند عاملی برای جریان‌های کاری پیچیده
- استقرار ترکیبی لبه-ابر
- زیرساخت هوش مصنوعی بهینه‌سازی شده از نظر هزینه

✅ **رهبری ابتکارات Edge AI**
- ارزیابی امکان‌پذیری Edge AI برای پروژه‌ها
- انتخاب مدل‌ها و چارچوب‌های مناسب
- معماری راه‌حل‌های هوش مصنوعی محلی مقیاس‌پذیر

---

## 🗺️ ساختار کارگاه

### مرور جلسات (۶ جلسه × ۳۰ دقیقه = ۳ ساعت)

| جلسه | موضوع | تمرکز | مدت زمان |
|------|-------|-------|----------|
| **۱** | شروع کار با Foundry Local | نصب، اعتبارسنجی، تکمیل‌های اولیه | ۳۰ دقیقه |
| **۲** | ساخت راه‌حل‌های هوش مصنوعی با RAG | مهندسی درخواست، تعبیه‌ها، ارزیابی | ۳۰ دقیقه |
| **۳** | مدل‌های متن‌باز | کشف مدل، ارزیابی، انتخاب | ۳۰ دقیقه |
| **۴** | مدل‌های پیشرفته | SLM در مقابل LLM، بهینه‌سازی، چارچوب‌ها | ۳۰ دقیقه |
| **۵** | عوامل هوش مصنوعی | طراحی عامل، هماهنگی، حافظه | ۳۰ دقیقه |
| **۶** | مدل‌ها به عنوان ابزار | مسیریابی، زنجیره‌سازی، استراتژی‌های مقیاس‌پذیری | ۳۰ دقیقه |

---

## 🚀 شروع سریع

### پیش‌نیازها

**نیازمندی‌های سیستم:**
- **سیستم‌عامل**: Windows 10/11، macOS 11+، یا Linux (Ubuntu 20.04+)
- **رم**: حداقل ۸ گیگابایت، توصیه شده ۱۶ گیگابایت+
- **فضای ذخیره‌سازی**: حداقل ۱۰ گیگابایت فضای آزاد برای مدل‌ها
- **پردازنده**: پردازنده مدرن با پشتیبانی از AVX2
- **GPU** (اختیاری): سازگار با CUDA یا NPU Qualcomm برای شتاب‌دهی

**نیازمندی‌های نرم‌افزار:**
- **Python 3.8+** ([دانلود](https://www.python.org/downloads/))
- **Microsoft Foundry Local** ([راهنمای نصب](../../../Workshop))
- **Git** ([دانلود](https://git-scm.com/downloads))
- **Visual Studio Code** (توصیه شده) ([دانلود](https://code.visualstudio.com/))

### تنظیم در ۳ مرحله

#### ۱. نصب Foundry Local

**Windows:**
```powershell
winget install Microsoft.FoundryLocal
```

**macOS:**
```bash
brew tap microsoft/foundrylocal
brew install foundrylocal
```

**تأیید نصب:**
```bash
foundry --version
foundry service status
```

#### ۲. کلون کردن مخزن و نصب وابستگی‌ها

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

#### ۳. اجرای نمونه اول

```bash
# Start Foundry Local and load a model
foundry model run phi-4-mini

# Run the chat bootstrap sample
cd samples/session01
python chat_bootstrap.py "What is edge AI?"
```

**✅ موفقیت!** باید یک پاسخ جریان‌دار درباره Edge AI مشاهده کنید.

---

## 📦 منابع کارگاه

### نمونه‌های Python

مثال‌های عملی تدریجی که هر مفهوم را نشان می‌دهند:

| جلسه | نمونه | توضیحات | زمان اجرا |
|------|-------|---------|-----------|
| ۱ | [`chat_bootstrap.py`](../../../Workshop/samples/session01/chat_bootstrap.py) | چت پایه و جریان‌دار | ~۳۰ ثانیه |
| ۲ | [`rag_pipeline.py`](../../../Workshop/samples/session02/rag_pipeline.py) | RAG با تعبیه‌ها | ~۴۵ ثانیه |
| ۲ | [`rag_eval_ragas.py`](../../../Workshop/samples/session02/rag_eval_ragas.py) | ارزیابی کیفیت RAG | ~۶۰ ثانیه |
| ۳ | [`benchmark_oss_models.py`](../../../Workshop/samples/session03/benchmark_oss_models.py) | ارزیابی چند مدل | ~۲-۳ دقیقه |
| ۴ | [`model_compare.py`](../../../Workshop/samples/session04/model_compare.py) | مقایسه SLM و LLM | ~۴۵ ثانیه |
| ۵ | [`agents_orchestrator.py`](../../../Workshop/samples/session05/agents_orchestrator.py) | سیستم چند عاملی | ~۶۰ ثانیه |
| ۶ | [`models_router.py`](../../../Workshop/samples/session06/models_router.py) | مسیریابی مبتنی بر قصد | ~۴۵ ثانیه |
| ۶ | [`models_pipeline.py`](../../../Workshop/samples/session06/models_pipeline.py) | خط لوله چند مرحله‌ای | ~۶۰ ثانیه |

### نوت‌بوک‌های Jupyter

کاوش تعاملی با توضیحات و تجسم‌ها:

| جلسه | نوت‌بوک | توضیحات | سختی |
|------|---------|---------|------|
| ۱ | [`session01_chat_bootstrap.ipynb`](./notebooks/session01_chat_bootstrap.ipynb) | اصول چت و جریان‌دار | ⭐ مبتدی |
| ۲ | [`session02_rag_pipeline.ipynb`](./notebooks/session02_rag_pipeline.ipynb) | ساخت سیستم RAG | ⭐⭐ متوسط |
| ۲ | [`session02_rag_eval_ragas.ipynb`](./notebooks/session02_rag_eval_ragas.ipynb) | ارزیابی کیفیت RAG | ⭐⭐ متوسط |
| ۳ | [`session03_benchmark_oss_models.ipynb`](./notebooks/session03_benchmark_oss_models.ipynb) | ارزیابی مدل | ⭐⭐ متوسط |
| ۴ | [`session04_model_compare.ipynb`](./notebooks/session04_model_compare.ipynb) | مقایسه مدل | ⭐⭐ متوسط |
| ۵ | [`session05_agents_orchestrator.ipynb`](./notebooks/session05_agents_orchestrator.ipynb) | هماهنگی عامل | ⭐⭐⭐ پیشرفته |
| ۶ | [`session06_models_router.ipynb`](./notebooks/session06_models_router.ipynb) | مسیریابی قصد | ⭐⭐⭐ پیشرفته |
| ۶ | [`session06_models_pipeline.ipynb`](./notebooks/session06_models_pipeline.ipynb) | هماهنگی خط لوله | ⭐⭐⭐ پیشرفته |

### مستندات

راهنماها و منابع جامع:

| سند | توضیحات | زمان استفاده |
|-----|---------|--------------|
| [QUICK_START.md](./QUICK_START.md) | راهنمای تنظیم سریع | شروع از ابتدا |
| [QUICK_REFERENCE.md](./QUICK_REFERENCE.md) | برگه تقلب دستورات و API | نیاز به پاسخ سریع |
| [FOUNDRY_SDK_QUICKREF.md](./FOUNDRY_SDK_QUICKREF.md) | الگوها و مثال‌های SDK | نوشتن کد |
| [ENV_CONFIGURATION.md](./ENV_CONFIGURATION.md) | راهنمای متغیرهای محیطی | پیکربندی نمونه‌ها |
| [SAMPLES_UPDATE_SUMMARY.md](./SAMPLES_UPDATE_SUMMARY.md) | بهبودهای اخیر نمونه‌ها | درک تغییرات |
| [SDK_MIGRATION_NOTES.md](./SDK_MIGRATION_NOTES.md) | راهنمای مهاجرت | ارتقاء کد |
| [notebooks/TROUBLESHOOTING.md](./notebooks/TROUBLESHOOTING.md) | مشکلات رایج و رفع آن‌ها | اشکال‌زدایی مشکلات |

---

## 🎓 توصیه‌های مسیر یادگیری

### برای مبتدیان (۳-۴ ساعت)
1. ✅ جلسه ۱: شروع کار (تمرکز بر تنظیم و چت پایه)
2. ✅ جلسه ۲: اصول RAG (ابتدا ارزیابی را رد کنید)
3. ✅ جلسه ۳: ارزیابی ساده (فقط ۲ مدل)
4. ⏭️ جلسات ۴-۶ را فعلاً رد کنید
5. 🔄 به جلسات ۴-۶ پس از ساخت اولین برنامه بازگردید

### برای توسعه‌دهندگان متوسط (۳ ساعت)
1. ⚡ جلسه ۱: اعتبارسنجی تنظیم سریع
2. ✅ جلسه ۲: تکمیل خط لوله RAG با ارزیابی
3. ✅ جلسه ۳: مجموعه کامل ارزیابی
4. ✅ جلسه ۴: بهینه‌سازی مدل
5. ✅ جلسات ۵-۶: تمرکز بر الگوهای معماری

### برای متخصصان پیشرفته (۲-۳ ساعت)
1. ⚡ جلسات ۱-۳: مرور سریع و اعتبارسنجی
2. ✅ جلسه ۴: بررسی عمیق بهینه‌سازی
3. ✅ جلسه ۵: معماری چند عاملی
4. ✅ جلسه ۶: الگوهای تولید و مقیاس‌پذیری
5. 🚀 گسترش: ساخت منطق مسیریابی سفارشی و استقرار ترکیبی

---

## بسته جلسات کارگاه (آزمایشگاه‌های متمرکز ۳۰ دقیقه‌ای)

اگر از قالب کارگاه ۶ جلسه‌ای فشرده پیروی می‌کنید، از این راهنماهای اختصاصی استفاده کنید (هر کدام با ماژول‌های گسترده‌تر بالا مطابقت دارد و آن‌ها را تکمیل می‌کند):

| جلسه کارگاه | راهنما | تمرکز اصلی |
|-------------|--------|------------|
| ۱ | [Session01-GettingStartedFoundryLocal](./Session01-GettingStartedFoundryLocal.md) | نصب، اعتبارسنجی، اجرای phi و GPT-OSS-20B، شتاب‌دهی |
| ۲ | [Session02-BuildAISolutionsRAG](./Session02-BuildAISolutionsRAG.md) | مهندسی درخواست، الگوهای RAG، پایه‌گذاری CSV و سند، مهاجرت |
| ۳ | [Session03-OpenSourceModels](./Session03-OpenSourceModels.md) | ادغام Hugging Face، ارزیابی، انتخاب مدل |
| ۴ | [Session04-CuttingEdgeModels](./Session04-CuttingEdgeModels.md) | SLM در مقابل LLM، WebGPU، Chainlit RAG، شتاب‌دهی ONNX |
| ۵ | [Session05-AIPoweredAgents](./Session05-AIPoweredAgents.md) | نقش‌های عامل، حافظه، ابزارها، هماهنگی |
| ۶ | [Session06-ModelsAsTools](./Session06-ModelsAsTools.md) | مسیریابی، زنجیره‌سازی، مسیر مقیاس‌پذیری به Azure |
هر فایل جلسه شامل موارد زیر است: خلاصه، اهداف یادگیری، جریان نمایشی ۳۰ دقیقه‌ای، پروژه شروع‌کننده، چک‌لیست اعتبارسنجی، رفع اشکال و ارجاعات به SDK رسمی Foundry Local Python.

### اسکریپت‌های نمونه

نصب وابستگی‌های کارگاه (ویندوز):

```powershell
cd Workshop
py -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt
```

macOS / لینوکس:

```bash
cd Workshop
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

اگر سرویس Foundry Local را روی یک ماشین یا VM متفاوت (ویندوز) از macOS اجرا می‌کنید، نقطه پایانی را صادر کنید:

```bash
export FOUNDRY_LOCAL_ENDPOINT=http://<windows-host>:5273/v1
```

| جلسه | اسکریپت(ها) | توضیحات |
|------|------------|----------|
| ۱ | `samples/session01/chat_bootstrap.py` | راه‌اندازی سرویس و چت استریمینگ |
| ۲ | `samples/session02/rag_pipeline.py` | RAG حداقلی (تعبیه‌های در حافظه) |
|   | `samples/session02/rag_eval_ragas.py` | ارزیابی RAG با معیارهای ragas |
| ۳ | `samples/session03/benchmark_oss_models.py` | ارزیابی تأخیر و توان چند مدل |
| ۴ | `samples/session04/model_compare.py` | مقایسه SLM و LLM (تأخیر و خروجی نمونه) |
| ۵ | `samples/session05/agents_orchestrator.py` | تحقیق دو عامل → خط تولید ویرایش |
| ۶ | `samples/session06/models_router.py` | نمایشی مسیریابی مبتنی بر قصد |
|   | `samples/session06/models_pipeline.py` | زنجیره چند مرحله‌ای برنامه‌ریزی/اجرا/اصلاح |

### متغیرهای محیطی (مشترک بین نمونه‌ها)

| متغیر | هدف | مثال |
|-------|-----|-------|
| `FOUNDRY_LOCAL_ALIAS` | نام مستعار مدل پیش‌فرض برای نمونه‌های ساده | `phi-4-mini` |
| `SLM_ALIAS` / `LLM_ALIAS` | مدل SLM صریح در مقابل مدل بزرگ‌تر برای مقایسه | `phi-4-mini` / `gpt-oss-20b` |
| `BENCH_MODELS` | لیست نام مستعار مدل‌ها برای ارزیابی | `qwen2.5-0.5b,gemma-2-2b,mistral-7b` |
| `BENCH_ROUNDS` | تعداد تکرارهای ارزیابی برای هر مدل | `3` |
| `BENCH_PROMPT` | درخواست استفاده شده در ارزیابی | `Explain retrieval augmented generation briefly.` |
| `EMBED_MODEL` | مدل تعبیه‌کننده sentence-transformers | `sentence-transformers/all-MiniLM-L6-v2` |
| `RAG_QUESTION` | پرسش آزمایشی برای خط لوله RAG | `Why use RAG with local inference?` |
| `AGENT_QUESTION` | پرسش خط لوله عوامل | `Explain why edge AI matters for compliance.` |
| `AGENT_MODEL_PRIMARY` | نام مستعار مدل برای عامل تحقیق | `phi-4-mini` |
| `AGENT_MODEL_EDITOR` | نام مستعار مدل برای عامل ویرایشگر (می‌تواند متفاوت باشد) | `gpt-oss-20b` |
| `SHOW_USAGE` | وقتی `1` باشد، استفاده از توکن‌ها را در هر تکمیل چاپ می‌کند | `1` |
| `RETRY_ON_FAIL` | وقتی `1` باشد، در صورت خطای چت گذرا یک بار تلاش مجدد می‌کند | `1` |
| `RETRY_BACKOFF` | ثانیه‌هایی که باید قبل از تلاش مجدد منتظر بمانید | `1.0` |

اگر متغیری تنظیم نشده باشد، اسکریپت‌ها به مقادیر پیش‌فرض منطقی بازمی‌گردند. برای نمایش‌های تک‌مدلی معمولاً فقط به `FOUNDRY_LOCAL_ALIAS` نیاز دارید.

### ماژول کمکی

تمام نمونه‌ها اکنون یک فایل کمکی `samples/workshop_utils.py` را به اشتراک می‌گذارند که شامل موارد زیر است:

* ایجاد کش شده `FoundryLocalManager` + کلاینت OpenAI
* تابع کمکی `chat_once()` با تلاش مجدد اختیاری + چاپ استفاده
* گزارش ساده استفاده از توکن (فعال‌سازی با `SHOW_USAGE=1`)

این کار تکرار را کاهش می‌دهد و بهترین روش‌ها را برای هماهنگی کارآمد مدل‌های محلی برجسته می‌کند.

## بهبودهای اختیاری (بین جلسات)

| موضوع | بهبود | جلسات | محیط / تنظیم |
|-------|-------|-------|--------------|
| تعیین‌پذیری | دمای ثابت + مجموعه درخواست‌های پایدار | ۱–۶ | تنظیم `temperature=0`, `top_p=1` |
| نمایش استفاده از توکن | آموزش هزینه/کارایی سازگار | ۱–۶ | `SHOW_USAGE=1` |
| اولین توکن استریمینگ | معیار تأخیر ادراکی | ۱، ۳، ۴، ۶ | `BENCH_STREAM=1` (ارزیابی) |
| مقاومت در برابر تلاش مجدد | مدیریت شروع سرد گذرا | همه | `RETRY_ON_FAIL=1` + `RETRY_BACKOFF` |
| عوامل چندمدلی | تخصص نقش‌های ناهمگن | ۵ | `AGENT_MODEL_PRIMARY`, `AGENT_MODEL_EDITOR` |
| مسیریابی تطبیقی | منطق قصد + هزینه | ۶ | گسترش مسیریاب با منطق تشدید |
| حافظه برداری | یادآوری معنایی بلندمدت | ۲، ۵، ۶ | ادغام شاخص تعبیه FAISS/Chroma |
| صادرات ردگیری | حسابرسی و ارزیابی | ۲، ۵، ۶ | افزودن خطوط JSON در هر مرحله |
| معیارهای کیفیت | ردیابی کیفی | ۳–۶ | درخواست‌های امتیازدهی ثانویه |
| آزمایش‌های دود | اعتبارسنجی سریع پیش از کارگاه | همه | `python Workshop/tests/smoke.py` |

### شروع سریع تعیین‌پذیر

```powershell
set FOUNDRY_LOCAL_ALIAS=phi-4-mini
set SHOW_USAGE=1
python Workshop\tests\smoke.py
```

انتظار داشته باشید که تعداد توکن‌ها در ورودی‌های یکسان تکراری ثابت باشد.

### ارزیابی RAG (جلسه ۲)

از `rag_eval_ragas.py` برای محاسبه مرتبط بودن پاسخ، وفاداری و دقت زمینه در یک مجموعه داده مصنوعی کوچک استفاده کنید:

```powershell
python samples/session02/rag_eval_ragas.py
```

با ارائه یک JSONL بزرگ‌تر از پرسش‌ها، زمینه‌ها و حقایق پایه، سپس تبدیل به یک `Dataset` از Hugging Face گسترش دهید.

## ضمیمه دقت فرمان CLI

کارگاه عمداً فقط از دستورات CLI مستند / پایدار Foundry Local استفاده می‌کند.

### دستورات پایدار مورد اشاره

| دسته‌بندی | فرمان | هدف |
|-----------|-------|------|
| اصلی | `foundry --version` | نمایش نسخه نصب شده |
| اصلی | `foundry init` | مقداردهی اولیه پیکربندی |
| سرویس | `foundry service start` | شروع سرویس محلی (در صورت عدم خودکار بودن) |
| سرویس | `foundry status` | نمایش وضعیت سرویس |
| مدل‌ها | `foundry model list` | لیست کاتالوگ / مدل‌های موجود |
| مدل‌ها | `foundry model download <alias>` | دانلود وزن‌های مدل به کش |
| مدل‌ها | `foundry model run <alias>` | اجرای (بارگذاری) یک مدل محلی؛ ترکیب با `--prompt` برای یک‌بار اجرا |
| مدل‌ها | `foundry model unload <alias>` / `foundry model stop <alias>` | بارگذاری مدل از حافظه (در صورت پشتیبانی) |
| کش | `foundry cache list` | لیست مدل‌های کش شده (دانلود شده) |
| سیستم | `foundry system info` | عکس‌برداری از قابلیت‌های سخت‌افزار و شتاب‌دهی |
| سیستم | `foundry system gpu-info` | اطلاعات تشخیصی GPU |
| پیکربندی | `foundry config list` | نمایش مقادیر پیکربندی فعلی |
| پیکربندی | `foundry config set <key> <value>` | به‌روزرسانی پیکربندی |

### الگوی درخواست یک‌بار اجرا

به جای زیر فرمان منسوخ `model chat`، از این استفاده کنید:

```powershell
foundry model run <alias> --prompt "Your question here"
```

این یک چرخه درخواست/پاسخ واحد را اجرا می‌کند و سپس خارج می‌شود.

### الگوهای حذف شده / اجتناب شده

| منسوخ / مستند نشده | جایگزین / راهنما |
|--------------------|------------------|
| `foundry model chat <model> "..."` | `foundry model run <model> --prompt "..."` |
| `foundry model list --running` | استفاده از `foundry model list` ساده + فعالیت اخیر / لاگ‌ها |
| `foundry model list --cached` | `foundry cache list` |
| `foundry model stats <model>` | استفاده از اسکریپت ارزیابی Python + ابزارهای سیستم عامل (Task Manager / `nvidia-smi`) |
| `foundry model benchmark ...` | `samples/session03/benchmark_oss_models.py` |

### ارزیابی و تله‌متری

- تأخیر، p95، توکن‌ها/ثانیه: `samples/session03/benchmark_oss_models.py`
- تأخیر اولین توکن (استریمینگ): تنظیم `BENCH_STREAM=1`
- استفاده از منابع: مانیتورهای سیستم عامل (Task Manager، Activity Monitor، `nvidia-smi`) + `foundry system info`.

با تثبیت دستورات تله‌متری CLI جدید در بالادست، می‌توان آن‌ها را با حداقل ویرایش به مارک‌داون جلسات اضافه کرد.

### نگهبان خودکار Lint

یک ابزار lint خودکار از بازگشت الگوهای CLI منسوخ در داخل بلوک‌های کد محصور شده فایل‌های مارک‌داون جلوگیری می‌کند:

اسکریپت: `Workshop/scripts/lint_markdown_cli.py`

الگوهای منسوخ در داخل بلوک‌های کد مسدود می‌شوند.

جایگزین‌های توصیه‌شده:
| منسوخ | جایگزین |
|-------|---------|
| `foundry model chat <a> "..."` | `foundry model run <a> --prompt "..."` |
| `model list --running` | `model list` |
| `model list --cached` | `cache list` |
| `model stats` | اسکریپت ارزیابی + ابزارهای سیستم |
| `model benchmark` | `samples/session03/benchmark_oss_models.py` |
| `model list --available` | `model list` |

اجرای محلی:
```powershell
python Workshop\scripts\lint_markdown_cli.py --verbose
```

GitHub Action: `.github/workflows/markdown-cli-lint.yml` در هر push و PR اجرا می‌شود.

هوک اختیاری پیش از commit:
```bash
echo "python Workshop/scripts/lint_markdown_cli.py" > .git/hooks/pre-commit
chmod +x .git/hooks/pre-commit
```

## جدول مهاجرت سریع CLI → SDK

| وظیفه | دستور CLI یک‌خطی | معادل SDK (Python) | توضیحات |
|-------|------------------|--------------------|---------|
| اجرای یک مدل یک‌بار (درخواست) | `foundry model run phi-4-mini --prompt "Hello"` | `manager=FoundryLocalManager("phi-4-mini"); client=OpenAI(base_url=manager.endpoint, api_key=manager.api_key or "not-needed"); client.chat.completions.create(model=manager.get_model_info("phi-4-mini").id, messages=[{"role":"user","content":"Hello"}])` | SDK سرویس و کش را به‌طور خودکار مقداردهی اولیه می‌کند |
| دانلود (کش) مدل | `foundry model download qwen2.5-0.5b` | `FoundryLocalManager("qwen2.5-0.5b")  # triggers download/load` | مدیر بهترین نسخه را انتخاب می‌کند اگر نام مستعار به چندین ساخت نگاشت شود |
| لیست کاتالوگ | `foundry model list` | `# use manager for each alias or maintain known list` | CLI جمع‌آوری می‌کند؛ SDK در حال حاضر برای هر نام مستعار مقداردهی اولیه می‌شود |
| لیست مدل‌های کش شده | `foundry cache list` | `manager.list_cached_models()` | پس از مقداردهی اولیه مدیر (هر نام مستعار) |
| فعال‌سازی شتاب GPU | `foundry config set compute.onnx.enable_gpu true` | `# CLI action; SDK assumes config already applied` | پیکربندی اثر جانبی خارجی است |
| دریافت URL نقطه پایانی | (ضمنی) | `manager.endpoint` | برای ایجاد کلاینت سازگار با OpenAI استفاده می‌شود |
| گرم کردن یک مدل | `foundry model run <alias>` سپس اولین درخواست | `chat_once(alias, messages=[...])` (کمکی) | ابزارها تأخیر اولیه سرد را مدیریت می‌کنند |
| اندازه‌گیری تأخیر | `python benchmark_oss_models.py` | `import benchmark_oss_models` (یا اسکریپت صادرکننده جدید) | ترجیحاً از اسکریپت برای معیارهای سازگار استفاده کنید |
| توقف / بارگذاری مدل | `foundry model unload <alias>` | (افشا نشده – راه‌اندازی مجدد سرویس / فرآیند) | معمولاً برای جریان کارگاه مورد نیاز نیست |
| بازیابی استفاده از توکن | (مشاهده خروجی) | `resp.usage.total_tokens` | ارائه شده اگر backend شیء استفاده را بازگرداند |

## صادرات مارک‌داون ارزیابی

از اسکریپت `Workshop/scripts/export_benchmark_markdown.py` برای اجرای یک ارزیابی جدید (منطق مشابه `samples/session03/benchmark_oss_models.py`) و تولید یک جدول مارک‌داون سازگار با GitHub به همراه JSON خام استفاده کنید.

### مثال

```powershell
python Workshop\scripts\export_benchmark_markdown.py --models "qwen2.5-0.5b,gemma-2-2b,mistral-7b" --prompt "Explain retrieval augmented generation briefly." --rounds 3 --output benchmark_report.md
```

فایل‌های تولید شده:
| فایل | محتویات |
|------|----------|
| `benchmark_report.md` | جدول مارک‌داون + نکات تفسیری |
| `benchmark_report.json` | آرایه معیارهای خام (برای مقایسه / ردیابی روند) |

تنظیم `BENCH_STREAM=1` در محیط برای شامل کردن تأخیر اولین توکن در صورت پشتیبانی.

---

**سلب مسئولیت**:  
این سند با استفاده از سرویس ترجمه هوش مصنوعی [Co-op Translator](https://github.com/Azure/co-op-translator) ترجمه شده است. در حالی که ما تلاش می‌کنیم دقت را حفظ کنیم، لطفاً توجه داشته باشید که ترجمه‌های خودکار ممکن است حاوی خطاها یا نادرستی‌هایی باشند. سند اصلی به زبان بومی آن باید به عنوان منبع معتبر در نظر گرفته شود. برای اطلاعات حساس، ترجمه حرفه‌ای انسانی توصیه می‌شود. ما هیچ مسئولیتی در قبال سوءتفاهم‌ها یا تفسیرهای نادرست ناشی از استفاده از این ترجمه نداریم.