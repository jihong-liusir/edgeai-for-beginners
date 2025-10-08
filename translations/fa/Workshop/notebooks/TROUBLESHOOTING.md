<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "e88a16101de37838f7cf256a9cd0f199",
  "translation_date": "2025-10-08T22:05:10+00:00",
  "source_file": "Workshop/notebooks/TROUBLESHOOTING.md",
  "language_code": "fa"
}
-->
# دفترچه‌های کارگاه - راهنمای رفع مشکلات

## فهرست مطالب

- [مشکلات رایج و راه‌حل‌ها](../../../../Workshop/notebooks)
- [مشکلات خاص جلسه ۰۴](../../../../Workshop/notebooks)
- [مشکلات خاص جلسه ۰۵](../../../../Workshop/notebooks)
- [مشکلات خاص جلسه ۰۶](../../../../Workshop/notebooks)
- [مشکلات مربوط به سخت‌افزار](../../../../Workshop/notebooks)
- [دستورات تشخیصی](../../../../Workshop/notebooks)
- [دریافت کمک](../../../../Workshop/notebooks)

---

## مشکلات رایج و راه‌حل‌ها

### 🔴 خطای CUDA Out of Memory

**پیام خطا:**
```
CUDA failure 2: out of memory
```

**علت اصلی:** کارت گرافیک (GPU) حافظه کافی برای بارگذاری مدل ندارد.

**راه‌حل‌ها:**

#### گزینه ۱: استفاده از نسخه‌های CPU (توصیه‌شده)
```python
# In your notebook, update the CATALOG to use CPU variants
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```

#### گزینه ۲: استفاده از مدل‌های کوچک‌تر روی GPU
```python
# Use only the smallest model
CATALOG = {
    'qwen2.5-0.5b': {'capabilities':['general','code','summarize','classification'],'priority':1},
}
```

#### گزینه ۳: پاک کردن حافظه GPU
```bash
# Close other GPU-intensive applications
# Check GPU memory usage
nvidia-smi

# Restart Foundry Local service
foundry service stop
foundry service start
```

#### گزینه ۴: افزایش حافظه GPU (در صورت امکان)
- بستن تب‌های مرورگر، ویرایشگرهای ویدئو یا سایر برنامه‌های GPU
- کاهش جلوه‌های بصری ویندوز
- استفاده از GPU اختصاصی در صورت داشتن GPU یکپارچه و اختصاصی

---

### 🔴 خطای APIConnectionError: Connection Error

**پیام خطا:**
```
APIConnectionError: Connection error
[Retry 1/2] Setup failed for 'phi-4-mini': APIConnectionError: Connection error.
```

**علت اصلی:** سرویس Foundry Local اجرا نمی‌شود یا قابل دسترسی نیست.

**راه‌حل‌ها:**

#### مرحله ۱: بررسی وضعیت سرویس
```bash
foundry service status
```

#### مرحله ۲: راه‌اندازی سرویس در صورت توقف
```bash
foundry service start
```

#### مرحله ۳: بررسی نقطه پایانی
```bash
# Check what port the service is using
foundry service status

# Test with curl (adjust port if different)
curl http://localhost:59959/health
curl http://localhost:55769/health
```

#### مرحله ۴: بارگذاری مدل‌های مورد نیاز
```bash
foundry model run phi-4-mini
foundry model run qwen2.5-3b
foundry model run phi-3.5-mini
```

#### مرحله ۵: راه‌اندازی مجدد کرنل دفترچه
پس از راه‌اندازی سرویس و بارگذاری مدل‌ها، کرنل دفترچه را مجدداً راه‌اندازی کرده و تمام سلول‌ها را دوباره اجرا کنید.

---

### 🔴 مدل در کاتالوگ یافت نشد

**پیام خطا:**
```
ValueError: Model phi-3.5-mini-cpu not found in the catalog.
[ERROR] Model 'phi-4-mini' not found in the catalog
```

**علت اصلی:** مدل دانلود نشده یا در Foundry Local بارگذاری نشده است.

**راه‌حل‌ها:**

#### گزینه ۱: دانلود و بارگذاری مدل‌ها
```bash
# List available models
foundry model ls

# Download the model if not present
foundry model download phi-4-mini
foundry model download qwen2.5-3b
foundry model download phi-3.5-mini

# Load the model into memory
foundry model run phi-4-mini
foundry model run qwen2.5-3b
foundry model run phi-3.5-mini
```

#### گزینه ۲: استفاده از حالت انتخاب خودکار
کاتالوگ خود را به نام‌های مدل پایه (بدون پسوند `-cpu`) به‌روزرسانی کنید:

```python
CATALOG = {
    'phi-4-mini': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini': {'capabilities':['code','refactor'],'priority':3},
}
```

SDK Foundry Local به‌طور خودکار بهترین نسخه (CPU، GPU یا NPU) را برای سخت‌افزار شما انتخاب می‌کند.

---

### 🔴 خطای HttpResponseError: 500 - Failed Loading Model

**پیام خطا:**
```
HttpResponseError: 500 - Failed loading model
```

**علت اصلی:** فایل مدل خراب شده یا با سخت‌افزار سازگار نیست.

**راه‌حل‌ها:**

#### دانلود مجدد مدل
```bash
# Remove corrupted model
foundry model remove phi-3.5-mini

# Download fresh copy
foundry model download phi-3.5-mini
```

#### استفاده از نسخه متفاوت
```bash
# Try CPU variant instead
foundry model download phi-3.5-mini-cpu
```

---

### 🔴 خطای ImportError: No Module Found

**پیام خطا:**
```
ModuleNotFoundError: No module named 'foundry_local'
```

**علت اصلی:** بسته foundry-local-sdk نصب نشده است.

**راه‌حل‌ها:**

```bash
# Install SDK
pip install foundry-local-sdk

# Verify installation
pip show foundry-local-sdk
python -c "from foundry_local import FoundryLocalManager; print('SDK OK')"
```

---

### � درخواست اول کند

**نشانه:** تکمیل اول بیش از ۳۰ ثانیه طول می‌کشد، درخواست‌های بعدی سریع هستند.

**علت اصلی:** این رفتار طبیعی است - سرویس در حال بارگذاری مدل در حافظه در درخواست اول است.

**راه‌حل‌ها:**

#### پیش‌بارگذاری مدل‌ها
```bash
# Download and load all models you'll use before running notebooks
foundry model download phi-4-mini
foundry model download qwen2.5-3b
foundry model download phi-3.5-mini

foundry model run phi-4-mini
foundry model run qwen2.5-3b
```

#### نگه داشتن سرویس در حال اجرا
```bash
# Start service manually and leave it running
foundry service start
```

---

## مشکلات خاص جلسه ۰۴

### پیکربندی اشتباه پورت

**مشکل:** دفترچه به پورت اشتباه متصل می‌شود (۵۵۷۶۹ در مقابل ۵۹۹۵۹ در مقابل ۵۷۱۲۷)

**راه‌حل:**

1. بررسی کنید که Foundry Local از کدام پورت استفاده می‌کند:
```bash
foundry service status
# Note the port number displayed
```

2. سلول ۱۰ را در دفترچه به‌روزرسانی کنید:
```python
ENDPOINT = os.getenv('FOUNDRY_LOCAL_ENDPOINT', 'http://localhost:59959/v1')
# Replace 59959 with your actual port
```

3. کرنل را مجدداً راه‌اندازی کرده و سلول‌های ۶، ۸، ۱۰، ۱۲، ۱۶، ۲۰، ۲۲ را دوباره اجرا کنید.

---

### انتخاب اشتباه مدل

**مشکل:** دفترچه مدل gpt-oss-20b یا qwen2.5-7b را به جای qwen2.5-3b نشان می‌دهد.

**راه‌حل:**

1. کرنل دفترچه را مجدداً راه‌اندازی کنید (متغیرهای قدیمی پاک می‌شوند)
2. سلول ۱۰ را دوباره اجرا کنید (تنظیم نام‌های مستعار مدل)
3. سلول ۱۲ را دوباره اجرا کنید (نمایش پیکربندی)
4. **تأیید:** سلول ۱۲ باید نشان دهد `LLM Model: qwen2.5-3b`

---

### سلول تشخیصی شکست می‌خورد

**مشکل:** سلول ۱۶ پیام "❌ Foundry Local service not found!" را نشان می‌دهد.

**راه‌حل:**

1. بررسی کنید که سرویس در حال اجرا است:
```bash
foundry service status
```

2. نقطه پایانی را به‌صورت دستی تست کنید:
```bash
curl http://localhost:59959/v1/models
```

3. اگر curl کار می‌کند اما دفترچه کار نمی‌کند:
   - کرنل دفترچه را مجدداً راه‌اندازی کنید
   - سلول‌ها را به ترتیب اجرا کنید: ۶، ۸، ۱۰، ۱۲، ۱۴، ۱۶

4. اگر curl شکست می‌خورد:
   - سرویس را راه‌اندازی کنید: `foundry service start`
   - مدل‌ها را بارگذاری کنید: `foundry model run phi-4-mini` و `foundry model run qwen2.5-3b`

---

### بررسی پیش‌پرواز شکست می‌خورد

**مشکل:** سلول ۲۰ خطاهای اتصال را نشان می‌دهد حتی اگر تشخیص موفق باشد.

**راه‌حل:**

1. بررسی کنید که مدل‌ها بارگذاری شده‌اند:
```bash
foundry model ls
# Should show phi-4-mini and qwen2.5-3b
```

2. اگر مدل‌ها وجود ندارند:
```bash
foundry model run phi-4-mini
foundry model run qwen2.5-3b
```

3. سلول ۲۰ را پس از بارگذاری مدل‌ها دوباره اجرا کنید.

---

### مقایسه با مقادیر None شکست می‌خورد

**مشکل:** سلول ۲۲ کامل می‌شود اما تأخیر را به صورت None نشان می‌دهد.

**راه‌حل:**

1. ابتدا بررسی کنید که پیش‌پرواز موفق بوده است (سلول ۲۰)
2. سلول ۲۲ را دوباره اجرا کنید - ممکن است مدل‌ها در درخواست اول نیاز به گرم شدن داشته باشند.
3. تأیید کنید که هر دو مدل بارگذاری شده‌اند: `foundry model ls`

---

## مشکلات خاص جلسه ۰۵

### عامل از مدل اشتباه استفاده می‌کند

**مشکل:** عامل از مدل مورد انتظار استفاده نمی‌کند.

**راه‌حل:**

پیکربندی را بررسی کنید:
```python
# Check which models are assigned
print(f"Researcher: {researcher.model_id}")
print(f"Editor: {editor.model_id}")
```

کرنل را مجدداً راه‌اندازی کنید اگر مدل‌ها اشتباه هستند.

---

### سرریز حافظه زمینه

**مشکل:** پاسخ‌های عامل با گذشت زمان کاهش کیفیت پیدا می‌کنند.

**راه‌حل:** به‌طور خودکار مدیریت شده است - عوامل فقط آخرین ۶ پیام را در حافظه نگه می‌دارند.

---

## مشکلات خاص جلسه ۰۶

### سردرگمی بین مدل‌های CPU و GPU

**مشکل:** دریافت خطاهای CUDA هنگام استفاده از پیکربندی پیش‌فرض

**راه‌حل:** پیکربندی پیش‌فرض اکنون از مدل‌های CPU استفاده می‌کند. اگر خطاهای CUDA مشاهده کردید:

1. بررسی کنید که از کاتالوگ پیش‌فرض CPU استفاده می‌کنید:
```python
# Cell should show CPU variants
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```

2. کرنل را مجدداً راه‌اندازی کرده و تمام سلول‌ها را دوباره اجرا کنید.

---

### تشخیص قصد کار نمی‌کند

**مشکل:** درخواست‌ها به مدل‌های اشتباه هدایت می‌شوند.

**راه‌حل:**

تشخیص قصد را تست کنید:
```python
# Run the intent detection test cell
for prompt in test_prompts:
    intent = detect_intent(prompt)
    print(f"{prompt[:50]}... → {intent}")
```

RULES را به‌روزرسانی کنید اگر الگوها نیاز به تنظیم دارند.

---

## مشکلات مربوط به سخت‌افزار

### کارت گرافیک NVIDIA

**بررسی وضعیت GPU:**
```bash
nvidia-smi
```

**مشکلات رایج:**
- **درایور قدیمی:** درایورهای NVIDIA را به‌روزرسانی کنید.
- **عدم تطابق نسخه CUDA:** Foundry Local را دوباره نصب کنید.
- **حافظه GPU پراکنده:** سیستم را مجدداً راه‌اندازی کنید.

### پردازنده NPU Qualcomm

**بررسی وضعیت NPU:**
```bash
foundry device info
```

**مشکلات رایج:**
- **درایورهای NPU نصب نشده:** درایورهای NPU Qualcomm را نصب کنید.
- **نسخه NPU موجود نیست:** از نسخه CPU استفاده کنید.
- **نسخه ویندوز خیلی قدیمی:** به آخرین نسخه ویندوز ۱۱ به‌روزرسانی کنید.

### سیستم‌های فقط CPU

**مدل‌های توصیه‌شده:**
```python
CATALOG = {
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','general'],'priority':2},
}
```

**نکات عملکردی:**
- از کوچک‌ترین مدل‌ها استفاده کنید.
- مقدار max_tokens را کاهش دهید.
- برای درخواست اول صبور باشید.

---

## دستورات تشخیصی

### بررسی همه چیز
```bash
# Service status
foundry service status

# List models
foundry model ls

# Device info
foundry device info

# Version info
foundry --version

# Health check
curl http://localhost:55769/health
```

### در پایتون
```python
# Check SDK import
try:
    from foundry_local import FoundryLocalManager
    print('✓ SDK imported')
except ImportError as e:
    print(f'✗ SDK import failed: {e}')

# Check service connectivity
from openai import OpenAI

try:
    client = OpenAI(base_url='http://localhost:59959/v1', api_key='test')
    models = client.models.list()
    print(f'✓ Service reachable, {len(list(models.data))} models available')
except Exception as e:
    print(f'✗ Service not reachable: {e}')
```

---

## دریافت کمک

### ۱. بررسی لاگ‌ها
```bash
# Windows
foundry service logs

# Or check Windows Event Viewer
# Application Logs -> Microsoft-FoundryLocal
```

### ۲. مشکلات GitHub
- جستجوی مشکلات موجود: https://github.com/microsoft/Foundry-Local/issues
- ایجاد مشکل جدید با:
  - پیام خطا (متن کامل)
  - خروجی `foundry service status`
  - خروجی `foundry --version`
  - اطلاعات GPU/NPU (nvidia-smi و غیره)
  - مراحل بازتولید

### ۳. مستندات
- **مخزن اصلی:** https://github.com/microsoft/Foundry-Local
- **SDK پایتون:** https://github.com/microsoft/Foundry-Local/tree/main/sdk/python
- **مرجع CLI:** https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-cli.md
- **رفع مشکلات:** https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-troubleshooting.md

---

## چک‌لیست رفع سریع مشکلات

وقتی مشکلی پیش می‌آید، این مراحل را به ترتیب امتحان کنید:

- [ ] بررسی کنید که سرویس در حال اجرا است: `foundry service status`
- [ ] سرویس را مجدداً راه‌اندازی کنید: `foundry service stop && foundry service start`
- [ ] تأیید کنید که مدل وجود دارد: `foundry model ls | grep phi-4-mini`
- [ ] مدل‌های مورد نیاز را بارگذاری کنید: `foundry model run phi-4-mini`
- [ ] حافظه GPU را بررسی کنید: `nvidia-smi` (اگر NVIDIA دارید)
- [ ] نسخه CPU را امتحان کنید: از `phi-4-mini-cpu` به جای `phi-4-mini` استفاده کنید.
- [ ] کرنل دفترچه را مجدداً راه‌اندازی کنید.
- [ ] خروجی‌های دفترچه را پاک کرده و تمام سلول‌ها را دوباره اجرا کنید.
- [ ] SDK را دوباره نصب کنید: `pip install --upgrade --force-reinstall foundry-local-sdk`
- [ ] سیستم را مجدداً راه‌اندازی کنید (آخرین راه‌حل).

---

## نکات پیشگیری

### بهترین روش‌ها

1. **همیشه ابتدا سرویس را بررسی کنید:**
   ```bash
   foundry service status
   ```

2. **به‌طور پیش‌فرض از نسخه‌های CPU استفاده کنید:**
   ```python
   CATALOG = {
       'phi-4-mini-cpu': {...},
       'qwen2.5-0.5b-cpu': {...},
   }
   ```

3. **مدل‌ها را قبل از اجرای دفترچه‌ها پیش‌بارگذاری کنید:**
   ```bash
   foundry model run phi-4-mini
   foundry model run qwen2.5-3b
   ```

4. **سرویس را در حال اجرا نگه دارید:**
   - سرویس را بی‌دلیل متوقف/راه‌اندازی نکنید.
   - اجازه دهید بین جلسات در پس‌زمینه اجرا شود.

5. **منابع را نظارت کنید:**
   - حافظه GPU را قبل از اجرا بررسی کنید.
   - برنامه‌های غیرضروری GPU را ببندید.
   - از Task Manager / nvidia-smi استفاده کنید.

6. **به‌طور منظم به‌روزرسانی کنید:**
   ```bash
   winget upgrade Microsoft.FoundryLocal
   pip install --upgrade foundry-local-sdk
   ```

---

**آخرین به‌روزرسانی:** ۸ اکتبر ۲۰۲۵

---

**سلب مسئولیت**:  
این سند با استفاده از سرویس ترجمه هوش مصنوعی [Co-op Translator](https://github.com/Azure/co-op-translator) ترجمه شده است. در حالی که ما تلاش می‌کنیم ترجمه‌ها دقیق باشند، لطفاً توجه داشته باشید که ترجمه‌های خودکار ممکن است شامل خطاها یا نادرستی‌هایی باشند. سند اصلی به زبان اصلی آن باید به عنوان منبع معتبر در نظر گرفته شود. برای اطلاعات حساس، توصیه می‌شود از ترجمه انسانی حرفه‌ای استفاده کنید. ما مسئولیتی در قبال سوء تفاهم‌ها یا تفسیرهای نادرست ناشی از استفاده از این ترجمه نداریم.