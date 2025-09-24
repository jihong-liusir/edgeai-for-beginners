<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "562ac0eae12d808c9f45fbb77eb5c84f",
  "translation_date": "2025-09-24T12:21:08+00:00",
  "source_file": "Module08/samples/04/README.md",
  "language_code": "fa"
}
-->
# نمونه ۰۴: برنامه‌های چت تولیدی با Chainlit

یک نمونه جامع که روش‌های مختلفی برای ساخت برنامه‌های چت آماده تولید با استفاده از Microsoft Foundry Local را نشان می‌دهد، شامل رابط‌های وب مدرن، پاسخ‌های استریم‌شده و فناوری‌های پیشرفته مرورگر.

## موارد موجود

- **🚀 برنامه چت Chainlit** (`app.py`): برنامه چت آماده تولید با قابلیت استریم
- **🌐 دمو WebGPU** (`webgpu-demo/`): استنتاج هوش مصنوعی مبتنی بر مرورگر با شتاب سخت‌افزاری
- **🎨 یکپارچه‌سازی Open WebUI** (`open-webui-guide.md`): رابط حرفه‌ای مشابه ChatGPT
- **📚 دفترچه آموزشی** (`chainlit_app.ipynb`): مواد آموزشی تعاملی

## شروع سریع

### ۱. برنامه چت Chainlit

```cmd
# Navigate to Module08 directory
cd Module08

# Start your model
foundry model run phi-4-mini

# Run Chainlit app (using port 8080 to avoid conflicts)
chainlit run samples\04\app.py -w --port 8080
```
  
باز می‌شود در: `http://localhost:8080`

### ۲. دمو مرورگر WebGPU

```cmd
# Navigate to WebGPU demo
cd Module08\samples\04\webgpu-demo

# Serve the demo
python -m http.server 5173
```
  
باز می‌شود در: `http://localhost:5173`

### ۳. تنظیم Open WebUI

```cmd
# Run Open WebUI with Docker
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```
  
باز می‌شود در: `http://localhost:3000`

## الگوهای معماری

### ماتریس تصمیم‌گیری محلی در مقابل ابری

| سناریو | توصیه | دلیل |
|--------|-------|------|
| **داده‌های حساس به حریم خصوصی** | 🏠 محلی (Foundry) | داده‌ها هرگز دستگاه را ترک نمی‌کنند |
| **استدلال پیچیده** | ☁️ ابری (Azure OpenAI) | دسترسی به مدل‌های بزرگ‌تر |
| **چت بلادرنگ** | 🏠 محلی (Foundry) | تأخیر کمتر، پاسخ‌های سریع‌تر |
| **تحلیل اسناد** | 🔄 ترکیبی | محلی برای استخراج، ابری برای تحلیل |
| **تولید کد** | 🏠 محلی (Foundry) | حریم خصوصی + مدل‌های تخصصی |
| **وظایف تحقیقاتی** | ☁️ ابری (Azure OpenAI) | نیاز به پایگاه دانش گسترده |

### مقایسه فناوری‌ها

| فناوری | مورد استفاده | مزایا | معایب |
|--------|--------------|-------|-------|
| **Chainlit** | توسعه‌دهندگان پایتون، نمونه‌سازی سریع | راه‌اندازی آسان، پشتیبانی از استریم | فقط پایتون |
| **WebGPU** | حداکثر حریم خصوصی، سناریوهای آفلاین | بومی مرورگر، بدون نیاز به سرور | اندازه مدل محدود |
| **Open WebUI** | استقرار تولیدی، تیم‌ها | رابط حرفه‌ای، مدیریت کاربران | نیاز به Docker |

## پیش‌نیازها

- **Foundry Local**: نصب و اجرا شده ([دانلود](https://aka.ms/foundry-local-installer))
- **پایتون**: نسخه ۳.۱۰+ با محیط مجازی
- **مدل**: حداقل یک مدل بارگذاری شده (`foundry model run phi-4-mini`)
- **مرورگر**: Chrome/Edge با پشتیبانی WebGPU برای دموها
- **Docker**: برای Open WebUI (اختیاری)

## نصب و راه‌اندازی

### ۱. تنظیم محیط پایتون

```cmd
# Navigate to Module08 directory
cd Module08

# Create and activate virtual environment
py -m venv .venv
.venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```
  
### ۲. تنظیم Foundry Local

```cmd
# Verify Foundry Local installation
foundry --version

# Start the service
foundry service start

# Load a model
foundry model run phi-4-mini

# Verify model is running
foundry service ps
```
  
## برنامه‌های نمونه

### برنامه چت Chainlit

**ویژگی‌ها:**
- 🚀 **استریم بلادرنگ**: توکن‌ها به محض تولید ظاهر می‌شوند
- 🛡️ **مدیریت خطای قوی**: کاهش و بازیابی تدریجی
- 🎨 **رابط کاربری مدرن**: رابط چت حرفه‌ای آماده
- 🔧 **پیکربندی انعطاف‌پذیر**: متغیرهای محیطی و تشخیص خودکار
- 📱 **طراحی واکنش‌گرا**: قابل استفاده در دسکتاپ و دستگاه‌های موبایل

**شروع سریع:**
```cmd
# Run with default settings (recommended)
chainlit run samples\04\app.py -w --port 8080

# Use specific model
set MODEL=qwen2.5-7b-instruct
chainlit run samples\04\app.py -w --port 8080

# Manual endpoint configuration
set BASE_URL=http://localhost:51211
set API_KEY=your-api-key
chainlit run samples\04\app.py -w --port 8080
```
  
### دمو مرورگر WebGPU

**ویژگی‌ها:**
- 🌐 **هوش مصنوعی بومی مرورگر**: بدون نیاز به سرور، کاملاً در مرورگر اجرا می‌شود
- ⚡ **شتاب WebGPU**: شتاب سخت‌افزاری در صورت موجود بودن
- 🔒 **حداکثر حریم خصوصی**: داده‌ها هرگز دستگاه شما را ترک نمی‌کنند
- 🎯 **بدون نیاز به نصب**: در هر مرورگر سازگار کار می‌کند
- 🔄 **بازگشت تدریجی**: در صورت عدم دسترسی به WebGPU به CPU بازمی‌گردد

**اجرا:**
```cmd
cd samples\04\webgpu-demo
python -m http.server 5173
# Open http://localhost:5173
```
  
### یکپارچه‌سازی Open WebUI

**ویژگی‌ها:**
- 🎨 **رابط مشابه ChatGPT**: حرفه‌ای و آشنا
- 👥 **پشتیبانی چندکاربره**: حساب‌های کاربری و تاریخچه مکالمات
- 📁 **پردازش فایل**: بارگذاری و تحلیل اسناد
- 🔄 **تغییر مدل**: تغییر آسان بین مدل‌های مختلف
- 🐳 **استقرار Docker**: تنظیم آماده تولید به صورت کانتینری

**تنظیم سریع:**
```cmd
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```
  
## مرجع پیکربندی

### متغیرهای محیطی

| متغیر | توضیحات | پیش‌فرض | مثال |
|-------|---------|---------|-------|
| `MODEL` | نام مستعار مدل مورد استفاده | `phi-4-mini` | `qwen2.5-7b-instruct` |
| `BASE_URL` | نقطه پایانی Foundry Local | تشخیص خودکار | `http://localhost:51211` |
| `API_KEY` | کلید API (اختیاری برای محلی) | `""` | `your-api-key` |

## رفع مشکلات

### مشکلات رایج

**برنامه Chainlit:**

۱. **سرویس در دسترس نیست:**  
   ```cmd
   # Check Foundry Local status
   foundry service status
   foundry service ps
   
   # Validate API endpoint (note: port 51211)
   curl http://localhost:51211/v1/models
   ```
  
۲. **تعارض پورت‌ها:**  
   ```cmd
   # Check what's using port 8080
   netstat -ano | findstr :8080
   
   # Use different port if needed
   chainlit run samples\04\app.py -w --port 3000
   ```
  
۳. **مشکلات محیط پایتون:**  
   ```cmd
   # Verify correct interpreter in VS Code
   # Ctrl+Shift+P → Python: Select Interpreter
   # Choose: Module08/.venv/Scripts/python.exe
   
   # Reinstall dependencies
   pip install -r requirements.txt
   ```
  
**دمو WebGPU:**

۱. **پشتیبانی نشدن WebGPU:**  
   - به Chrome/Edge نسخه ۱۱۳+ به‌روزرسانی کنید  
   - WebGPU را فعال کنید: `chrome://flags/#enable-unsafe-webgpu`  
   - وضعیت GPU را بررسی کنید: `chrome://gpu`  
   - دمو به صورت خودکار به CPU بازمی‌گردد  

۲. **خطاهای بارگذاری مدل:**  
   - اتصال اینترنت برای دانلود مدل را بررسی کنید  
   - کنسول مرورگر را برای خطاهای CORS بررسی کنید  
   - مطمئن شوید که از طریق HTTP سرویس‌دهی می‌کنید (نه file://)  

**Open WebUI:**

۱. **اتصال رد شد:**  
   ```cmd
   # Check Docker is running
   docker --version
   
   # Check container status
   docker ps | findstr open-webui
   
   # View container logs
   docker logs open-webui
   ```
  
۲. **مدل‌ها ظاهر نمی‌شوند:**  
   ```cmd
   # Verify Foundry Local endpoint
   curl http://localhost:51211/v1/models
   
   # Restart Open WebUI
   docker restart open-webui
   ```
  
### چک‌لیست اعتبارسنجی

```cmd
# ✅ 1. Foundry Local Setup
foundry --version                    # Should show version
foundry service status               # Should show "running"
foundry model list                   # Should show loaded models
curl http://localhost:51211/v1/models  # Should return JSON

# ✅ 2. Python Environment  
python --version                     # Should be 3.10+
pip list | findstr chainlit         # Should show chainlit package
pip list | findstr openai           # Should show openai package

# ✅ 3. Application Testing
chainlit run samples\04\app.py -w --port 8080  # Should open browser
# Test WebGPU demo at localhost:5173
# Test Open WebUI at localhost:3000
```
  
## استفاده پیشرفته

### بهینه‌سازی عملکرد

**Chainlit:**  
- از استریم برای عملکرد بهتر استفاده کنید  
- اتصال‌های مشترک را برای هم‌زمانی بالا پیاده‌سازی کنید  
- پاسخ‌های مدل را برای پرسش‌های تکراری ذخیره کنید  
- استفاده از حافظه را با تاریخچه‌های مکالمه بزرگ نظارت کنید  

**WebGPU:**  
- از WebGPU برای حداکثر حریم خصوصی و سرعت استفاده کنید  
- مدل‌ها را برای اندازه‌های کوچک‌تر کمیت‌سازی کنید  
- از Web Workers برای پردازش پس‌زمینه استفاده کنید  
- مدل‌های کامپایل‌شده را در حافظه مرورگر ذخیره کنید  

**Open WebUI:**  
- از حجم‌های پایدار برای تاریخچه مکالمات استفاده کنید  
- محدودیت‌های منابع را برای کانتینر Docker تنظیم کنید  
- استراتژی‌های پشتیبان‌گیری برای داده‌های کاربران پیاده‌سازی کنید  
- پروکسی معکوس را برای خاتمه SSL تنظیم کنید  

### الگوهای یکپارچه‌سازی

**ترکیبی محلی/ابری:**  
```python
# Route based on complexity and privacy requirements
async def intelligent_routing(prompt: str, metadata: dict):
    if metadata.get("contains_pii"):
        return await foundry_local_completion(prompt)  # Privacy-sensitive
    elif len(prompt.split()) > 200:
        return await azure_openai_completion(prompt)   # Complex reasoning
    else:
        return await foundry_local_completion(prompt)  # Default local
```
  
**خط لوله چندوجهی:**  
```python
# Combine different AI capabilities
async def analyze_document(file_path: str):
    # 1. OCR with WebGPU (browser-based)
    text = await webgpu_ocr(file_path)
    
    # 2. Analysis with Foundry Local (private)
    summary = await foundry_local_analyze(text)
    
    # 3. Enhancement with cloud (if needed)
    if summary.confidence < 0.8:
        summary = await azure_openai_enhance(summary)
    
    return summary
```
  
## استقرار تولیدی

### ملاحظات امنیتی

- **کلیدهای API**: از متغیرهای محیطی استفاده کنید، هرگز کدنویسی نکنید  
- **شبکه**: در تولید از HTTPS استفاده کنید، VPN را برای دسترسی تیم در نظر بگیرید  
- **کنترل دسترسی**: احراز هویت را برای Open WebUI پیاده‌سازی کنید  
- **حریم خصوصی داده‌ها**: بررسی کنید که چه داده‌هایی محلی می‌مانند و چه داده‌هایی به ابر ارسال می‌شوند  
- **به‌روزرسانی‌ها**: Foundry Local و کانتینرها را به‌روز نگه دارید  

### نظارت و نگهداری

- **بررسی سلامت**: نظارت بر نقاط پایانی را پیاده‌سازی کنید  
- **ثبت وقایع**: ثبت وقایع را از همه اجزا متمرکز کنید  
- **معیارها**: زمان پاسخ، نرخ خطا و استفاده از منابع را پیگیری کنید  
- **پشتیبان‌گیری**: پشتیبان‌گیری منظم از داده‌های مکالمه و پیکربندی‌ها  

## منابع و مراجع

### مستندات
- [مستندات Chainlit](https://docs.chainlit.io/) - راهنمای کامل چارچوب  
- [مستندات Foundry Local](https://learn.microsoft.com/azure/ai-foundry/foundry-local/) - مستندات رسمی مایکروسافت  
- [ONNX Runtime Web](https://onnxruntime.ai/docs/get-started/with-javascript/web.html) - یکپارچه‌سازی WebGPU  
- [مستندات Open WebUI](https://docs.openwebui.com/) - پیکربندی پیشرفته  

### فایل‌های نمونه
- [`app.py`](../../../../../Module08/samples/04/app.py) - برنامه Chainlit تولیدی  
- [`chainlit_app.ipynb`](./chainlit_app.ipynb) - دفترچه آموزشی  
- [`webgpu-demo/`](../../../../../Module08/samples/04/webgpu-demo) - استنتاج هوش مصنوعی مبتنی بر مرورگر  
- [`open-webui-guide.md`](./open-webui-guide.md) - تنظیم کامل Open WebUI  

### نمونه‌های مرتبط
- [مستندات جلسه ۴](../../04.CuttingEdgeModels.md) - راهنمای کامل جلسه  
- [نمونه‌های Foundry Local](https://github.com/microsoft/foundry-local/tree/main/samples) - نمونه‌های رسمی  

---

