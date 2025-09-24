<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "50d80c321803b5170d9a9cd9bbfb37a3",
  "translation_date": "2025-09-24T12:16:23+00:00",
  "source_file": "Module08/README.md",
  "language_code": "fa"
}
-->
# ماژول ۰۸: کار عملی با Microsoft Foundry Local - ابزار کامل توسعه‌دهنده

## مرور کلی

Microsoft Foundry Local نسل جدید توسعه هوش مصنوعی در لبه را نمایان می‌کند و ابزارهای قدرتمندی را برای توسعه‌دهندگان فراهم می‌کند تا برنامه‌های هوش مصنوعی را به صورت محلی بسازند، اجرا کنند و مقیاس‌بندی کنند، در حالی که یکپارچگی بی‌نقصی با Azure AI Foundry حفظ می‌شود. این ماژول پوشش کاملی از Foundry Local، از نصب تا توسعه پیشرفته عامل‌ها، ارائه می‌دهد.

**فناوری‌های کلیدی:**
- CLI و SDK Microsoft Foundry Local
- یکپارچگی با Azure AI Foundry
- استنتاج مدل روی دستگاه
- کش و بهینه‌سازی مدل محلی
- معماری‌های مبتنی بر عامل

## اهداف یادگیری

با تکمیل این ماژول، شما:

- **تسلط بر Foundry Local**: نصب، پیکربندی و بهینه‌سازی برای توسعه در ویندوز ۱۱
- **اجرای مدل‌های متنوع**: اجرای مدل‌های phi، qwen، deepseek و GPT به صورت محلی با دستورات CLI
- **ساخت راه‌حل‌های تولیدی**: ایجاد برنامه‌های هوش مصنوعی با مهندسی پیشرفته پرامپت و یکپارچگی داده‌ها
- **استفاده از اکوسیستم متن‌باز**: یکپارچگی مدل‌های Hugging Face و مشارکت‌های جامعه
- **توسعه عامل‌های هوش مصنوعی**: ساخت عامل‌های هوشمند با قابلیت‌های grounding و orchestration
- **اجرای الگوهای سازمانی**: ایجاد راه‌حل‌های هوش مصنوعی ماژولار و مقیاس‌پذیر برای استقرار تولیدی

## ساختار جلسات

### [۱: شروع به کار با Foundry Local](./01.FoundryLocalSetup.md)
**تمرکز**: نصب، تنظیم CLI، استقرار مدل و بهینه‌سازی سخت‌افزار

**موضوعات کلیدی**: نصب کامل • دستورات CLI • کش مدل • شتاب‌دهی سخت‌افزاری • استقرار چندمدلی

**نمونه‌ها**: [شروع سریع REST Chat](./samples/01/README.md) • [یکپارچگی OpenAI SDK](./samples/02/README.md) • [کشف و ارزیابی مدل](./samples/03/README.md)

**مدت زمان**: ۲-۳ ساعت | **سطح**: مبتدی

---

### [۲: ساخت راه‌حل‌های هوش مصنوعی با Azure AI Foundry](./02.AzureAIFoundryIntegration.md)
**تمرکز**: مهندسی پیشرفته پرامپت، یکپارچگی داده‌ها و اتصال به ابر

**موضوعات کلیدی**: مهندسی پرامپت • یکپارچگی داده‌ها • جریان‌های کاری Azure • بهینه‌سازی عملکرد • نظارت

**نمونه‌ها**: [برنامه Chainlit RAG](./samples/04/README.md)

**مدت زمان**: ۲-۳ ساعت | **سطح**: متوسط

---

### [۳: مدل‌های متن‌باز در Foundry Local](./03.OpenSourceModels.md)
**تمرکز**: یکپارچگی Hugging Face، استراتژی‌های BYOM و مدل‌های جامعه

**موضوعات کلیدی**: یکپارچگی HuggingFace • مدل‌های خودتان را بیاورید • بینش‌های Model Mondays • مشارکت‌های جامعه • انتخاب مدل

**نمونه‌ها**: [Orchestration چندعاملی](./samples/05/README.md)

**مدت زمان**: ۲-۳ ساعت | **سطح**: متوسط

---

### [۴: کشف مدل‌های پیشرفته](./04.CuttingEdgeModels.md)
**تمرکز**: مقایسه LLMs و SLMs، پیاده‌سازی EdgeAI و دموهای پیشرفته

**موضوعات کلیدی**: مقایسه مدل‌ها • استنتاج در لبه در مقابل ابر • Phi + ONNX Runtime • برنامه Chainlit RAG • بهینه‌سازی WebGPU

**نمونه‌ها**: [Router مدل‌ها به عنوان ابزار](./samples/06/README.md)

**مدت زمان**: ۳-۴ ساعت | **سطح**: پیشرفته

---

### [۵: ساخت سریع عامل‌های هوش مصنوعی](./05.AIPoweredAgents.md)
**تمرکز**: معماری‌های عامل، پرامپت‌های سیستمی، grounding و orchestration

**موضوعات کلیدی**: الگوهای طراحی عامل • مهندسی پرامپت سیستمی • تکنیک‌های grounding • سیستم‌های چندعاملی • استقرار تولیدی

**نمونه‌ها**: [Orchestration چندعاملی](./samples/05/README.md) • [سیستم چندعاملی پیشرفته](./samples/09/README.md)

**مدت زمان**: ۳-۴ ساعت | **سطح**: پیشرفته

---

### [۶: Foundry Local - مدل‌ها به عنوان ابزار](./06.ModelsAsTools.md)
**تمرکز**: راه‌حل‌های هوش مصنوعی ماژولار، مقیاس‌پذیری سازمانی و الگوهای تولیدی

**موضوعات کلیدی**: مدل‌ها به عنوان ابزار • استقرار روی دستگاه • یکپارچگی SDK/API • معماری‌های سازمانی • استراتژی‌های مقیاس‌بندی

**نمونه‌ها**: [Router مدل‌ها به عنوان ابزار](./samples/06/README.md) • [چارچوب ابزارهای Foundry](./samples/10/README.md)

**مدت زمان**: ۳-۴ ساعت | **سطح**: متخصص

---

### [۷: الگوهای یکپارچگی مستقیم API](./samples/07/README.md)
**تمرکز**: یکپارچگی خالص REST API بدون وابستگی به SDK برای کنترل حداکثری

**موضوعات کلیدی**: پیاده‌سازی کلاینت HTTP • احراز هویت سفارشی • نظارت بر سلامت مدل • پاسخ‌های استریمینگ • مدیریت خطاهای تولیدی

**نمونه‌ها**: [کلاینت مستقیم API](./samples/07/README.md)

**مدت زمان**: ۲-۳ ساعت | **سطح**: متوسط

---

### [۸: برنامه چت بومی ویندوز ۱۱](./samples/08/README.md)
**تمرکز**: ساخت برنامه‌های چت بومی مدرن با یکپارچگی Foundry Local

**موضوعات کلیدی**: توسعه Electron • سیستم طراحی Fluent • یکپارچگی بومی ویندوز • استریمینگ بلادرنگ • طراحی رابط چت

**نمونه‌ها**: [برنامه چت ویندوز ۱۱](./samples/08/README.md)

**مدت زمان**: ۳-۴ ساعت | **سطح**: پیشرفته

---

### [۹: Orchestration چندعاملی پیشرفته](./samples/09/README.md)
**تمرکز**: هماهنگی عامل‌های پیچیده، تفویض وظایف تخصصی و جریان‌های کاری همکاری هوش مصنوعی

**موضوعات کلیدی**: هماهنگی عامل‌های هوشمند • الگوهای فراخوانی توابع • ارتباط بین عامل‌ها • Orchestration جریان‌های کاری • مکانیزم‌های تضمین کیفیت

**نمونه‌ها**: [سیستم چندعاملی پیشرفته](./samples/09/README.md)

**مدت زمان**: ۴-۵ ساعت | **سطح**: متخصص

---

### [۱۰: Foundry Local به عنوان چارچوب ابزارها](./samples/10/README.md)
**تمرکز**: معماری مبتنی بر ابزار برای یکپارچگی Foundry Local در برنامه‌ها و چارچوب‌های موجود

**موضوعات کلیدی**: یکپارچگی LangChain • توابع Semantic Kernel • چارچوب‌های REST API • ابزارهای CLI • یکپارچگی Jupyter • الگوهای استقرار تولیدی

**نمونه‌ها**: [چارچوب ابزارهای Foundry](./samples/10/README.md)

**مدت زمان**: ۴-۵ ساعت | **سطح**: متخصص

## پیش‌نیازها

### الزامات سیستم
- **سیستم عامل**: ویندوز ۱۱ (۲۲H۲ یا بالاتر)
- **حافظه**: ۱۶ گیگابایت رم (۳۲ گیگابایت توصیه می‌شود برای مدل‌های بزرگ‌تر)
- **فضای ذخیره‌سازی**: ۵۰ گیگابایت فضای آزاد برای کش مدل
- **سخت‌افزار**: دستگاه مجهز به NPU توصیه می‌شود (Copilot+ PC)، GPU اختیاری
- **شبکه**: اینترنت پرسرعت برای دانلود اولیه مدل‌ها

### محیط توسعه
- Visual Studio Code با افزونه AI Toolkit
- Python 3.10+ و pip
- Git برای کنترل نسخه
- PowerShell یا Command Prompt
- Azure CLI (اختیاری برای یکپارچگی ابری)

### دانش پیش‌نیاز
- درک پایه‌ای از مفاهیم هوش مصنوعی/یادگیری ماشین
- آشنایی با خط فرمان
- اصول برنامه‌نویسی Python
- مفاهیم REST API
- دانش پایه‌ای از پرامپتینگ و استنتاج مدل

## جدول زمانی ماژول

**زمان تخمینی کل**: ۳۰-۳۸ ساعت

| جلسه | حوزه تمرکز | نمونه‌ها | زمان | پیچیدگی |
|------|------------|----------|------|---------|
|  ۱ | تنظیمات و اصول | ۰۱، ۰۲، ۰۳ | ۲-۳ ساعت | مبتدی |
|  ۲ | راه‌حل‌های هوش مصنوعی | ۰۴ | ۲-۳ ساعت | متوسط |
|  ۳ | متن‌باز | ۰۵ | ۲-۳ ساعت | متوسط |
|  ۴ | مدل‌های پیشرفته | ۰۶ | ۳-۴ ساعت | پیشرفته |
|  ۵ | عامل‌های هوش مصنوعی | ۰۵، ۰۹ | ۳-۴ ساعت | پیشرفته |
|  ۶ | ابزارهای سازمانی | ۰۶، ۱۰ | ۳-۴ ساعت | متخصص |
|  ۷ | یکپارچگی مستقیم API | ۰۷ | ۲-۳ ساعت | متوسط |
|  ۸ | برنامه چت ویندوز ۱۱ | ۰۸ | ۳-۴ ساعت | پیشرفته |
|  ۹ | چندعاملی پیشرفته | ۰۹ | ۴-۵ ساعت | متخصص |
| ۱۰ | چارچوب ابزارها | ۱۰ | ۴-۵ ساعت | متخصص |

## منابع کلیدی

**مستندات رسمی:**
- [GitHub Microsoft Foundry Local](https://github.com/microsoft/Foundry-Local) - کد منبع و نمونه‌های رسمی
- [مستندات Azure AI Foundry](https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/) - راهنمای کامل تنظیم و استفاده
- [سری Model Mondays](https://aka.ms/model-mondays) - نکات برجسته و آموزش‌های هفتگی مدل

**جامعه و پشتیبانی:**
- [بحث‌های Foundry Local](https://github.com/microsoft/Foundry-Local/discussions) - پرسش و پاسخ جامعه و درخواست‌های ویژگی
- [جامعه توسعه‌دهندگان هوش مصنوعی Microsoft](https://techcommunity.microsoft.com/category/artificialintelligence) - اخبار و بهترین شیوه‌ها

## نتایج یادگیری

با تکمیل این ماژول، شما مجهز خواهید شد به:

### تسلط فنی
- **استقرار و مدیریت**: نصب‌های Foundry Local در محیط‌های توسعه و تولید
- **یکپارچگی مدل‌ها**: کار بی‌نقص با خانواده‌های مدل متنوع از Microsoft، Hugging Face و منابع جامعه
- **ساخت برنامه‌ها**: ایجاد برنامه‌های هوش مصنوعی آماده تولید با ویژگی‌ها و بهینه‌سازی‌های پیشرفته
- **توسعه عامل‌ها**: پیاده‌سازی عامل‌های هوش مصنوعی پیچیده با grounding، استدلال و یکپارچگی ابزار

### درک استراتژیک
- **تصمیمات معماری**: انتخاب‌های آگاهانه بین استقرار محلی و ابری
- **بهینه‌سازی عملکرد**: بهینه‌سازی عملکرد استنتاج در پیکربندی‌های سخت‌افزاری مختلف
- **مقیاس‌پذیری سازمانی**: طراحی برنامه‌هایی که از نمونه‌های اولیه محلی تا استقرارهای سازمانی مقیاس‌پذیر هستند
- **حریم خصوصی و امنیت**: پیاده‌سازی راه‌حل‌های هوش مصنوعی حفظ‌کننده حریم خصوصی با استنتاج محلی

### قابلیت‌های نوآوری
- **نمونه‌سازی سریع**: ساخت و آزمایش سریع مفاهیم برنامه‌های هوش مصنوعی در تمام ۱۰ الگوی نمونه
- **یکپارچگی جامعه**: استفاده از مدل‌های متن‌باز و مشارکت در اکوسیستم
- **الگوهای پیشرفته**: پیاده‌سازی الگوهای هوش مصنوعی پیشرفته شامل RAG، عامل‌ها و یکپارچگی ابزار
- **تسلط بر چارچوب‌ها**: یکپارچگی در سطح متخصص با LangChain، Semantic Kernel، Chainlit و Electron
- **استقرار تولیدی**: استقرار راه‌حل‌های هوش مصنوعی مقیاس‌پذیر از نمونه‌های اولیه محلی تا سیستم‌های سازمانی
- **توسعه آماده آینده**: ساخت برنامه‌هایی آماده برای فناوری‌ها و الگوهای نوظهور هوش مصنوعی

## شروع به کار

۱. **تنظیم محیط**: اطمینان حاصل کنید که ویندوز ۱۱ با سخت‌افزار توصیه‌شده (به پیش‌نیازها مراجعه کنید)
۲. **نصب Foundry Local**: جلسه ۱ را برای نصب و پیکربندی کامل دنبال کنید
۳. **اجرای نمونه ۰۱**: با یکپارچگی اولیه REST API شروع کنید تا تنظیمات را تأیید کنید
۴. **پیشرفت در نمونه‌ها**: نمونه‌های ۰۱-۱۰ را برای تسلط جامع تکمیل کنید

## معیارهای موفقیت

پیشرفت خود را در تمام ۱۰ نمونه جامع دنبال کنید:

### سطح پایه (نمونه‌های ۰۱-۰۳)
- [ ] نصب و پیکربندی موفق Foundry Local
- [ ] تکمیل یکپارچگی REST API (نمونه ۰۱)
- [ ] پیاده‌سازی سازگاری OpenAI SDK (نمونه ۰۲)
- [ ] انجام کشف و ارزیابی مدل (نمونه ۰۳)

### سطح کاربردی (نمونه‌های ۰۴-۰۶)
- [ ] استقرار و اجرای حداقل ۴ خانواده مدل مختلف
- [ ] ساخت یک برنامه چت RAG کاربردی (نمونه ۰۴)
- [ ] ایجاد سیستم Orchestration چندعاملی (نمونه ۰۵)
- [ ] پیاده‌سازی مسیریابی مدل هوشمند (نمونه ۰۶)

### سطح یکپارچگی پیشرفته (نمونه‌های ۰۷-۱۰)
- [ ] ساخت کلاینت API آماده تولید (نمونه ۰۷)
- [ ] توسعه برنامه چت بومی ویندوز ۱۱ (نمونه ۰۸)
- [ ] پیاده‌سازی سیستم چندعاملی پیشرفته (نمونه ۰۹)
- [ ] ایجاد چارچوب ابزار جامع (نمونه ۱۰)

### شاخص‌های تسلط
- [ ] اجرای موفقیت‌آمیز تمام ۱۰ نمونه بدون خطا
- [ ] سفارشی‌سازی حداقل ۳ نمونه برای موارد استفاده خاص
- [ ] استقرار ۲+ نمونه در محیط‌های شبیه تولید
- [ ] مشارکت در بهبود یا گسترش کد نمونه
- [ ] یکپارچگی الگوهای Foundry Local در پروژه‌های شخصی/حرفه‌ای

## راهنمای شروع سریع - تمام ۱۰ نمونه

### تنظیم محیط (مورد نیاز برای تمام نمونه‌ها)

```powershell
# 1. Clone and navigate to Module08
cd Module08

# 2. Create Python virtual environment
py -m venv .venv
.\.venv\Scripts\activate

# 3. Install base dependencies
pip install -r requirements.txt

# 4. Install Foundry Local (if not already installed)
winget install Microsoft.FoundryLocal

# 5. Verify Foundry Local installation
foundry --version
foundry model list
```

### نمونه‌های پایه اصلی (۰۱-۰۶)

**نمونه ۰۱: شروع سریع REST Chat**
```powershell
# Start Foundry Local service
foundry model run phi-4-mini

# Run REST chat demo
python samples/01/chat_quickstart.py
```

**نمونه ۰۲: یکپارچگی OpenAI SDK**
```powershell
# Ensure model is running
foundry status

# Run SDK demo
python samples/02/sdk_quickstart.py
```

**نمونه ۰۳: کشف و ارزیابی مدل**
```powershell
# Run comprehensive model testing
samples/03/list_and_bench.cmd

# Or run individual components
foundry model list --available
foundry model download qwen2.5-0.5b
foundry model benchmark phi-4-mini
```

**نمونه ۰۴: برنامه Chainlit RAG**
```powershell
# Install Chainlit dependencies
pip install chainlit langchain chromadb

# Start RAG chat application
chainlit run samples/04/app.py -w
# Opens browser at http://localhost:8000
```

**نمونه ۰۵: Orchestration چندعاملی**
```powershell
# Run agent coordinator demo
python -m samples.05.agents.coordinator

# Run specific agent examples
python samples/05/examples/specialists_demo.py
```

**نمونه ۰۶: Router مدل‌ها به عنوان ابزار**
```powershell
# Configure environment
set BASE_URL=http://localhost:8000
set GENERAL_MODEL=phi-4-mini
set CODE_MODEL=qwen2.5-7b-instruct

# Run intelligent router
python samples/06/router.py "Analyze this Python code for performance issues"
```

### نمونه‌های یکپارچگی پیشرفته (۰۷-۱۰)

**نمونه ۰۷: کلاینت مستقیم API**
```powershell
# Navigate to sample directory
cd samples/07

# Install additional dependencies
pip install -r requirements.txt

# Run basic API examples
python examples/basic_usage.py

# Try streaming responses
python examples/streaming.py

# Test production patterns
python examples/production.py
```

**نمونه ۰۸: برنامه چت ویندوز ۱۱**
```powershell
# Navigate to sample directory
cd samples/08

# Install Node.js dependencies
npm install

# Start Electron application
npm start

# Or build for production
npm run build
```

**نمونه ۰۹: سیستم چندعاملی پیشرفته**
```powershell
# Navigate to sample directory
cd samples/09

# Install agent system dependencies
pip install -r requirements.txt

# Run basic coordination example
python examples/basic_coordination.py

# Try complex workflow
python examples/complex_workflow.py

# Interactive agent demo
python examples/interactive_demo.py
```

**نمونه ۱۰: چارچوب ابزارهای Foundry**
```powershell
# Navigate to sample directory
cd samples/10

# Install framework dependencies
pip install -r requirements.txt

# Run basic tools demo
python examples/basic_tools.py

# Start REST API server
python examples/rest_api_server.py
# API available at http://localhost:8080

# Try CLI application
python examples/cli_application.py --help

# Launch Jupyter notebook
jupyter notebook examples/jupyter_notebook.ipynb

# Test LangChain integration
python examples/langchain_demo.py
```

### رفع مشکلات رایج

**خطاهای اتصال Foundry Local**
```powershell
# Check service status
foundry status

# Restart if needed
foundry restart

# Verify endpoint accessibility
curl http://localhost:5273/v1/models
```

**مشکلات بارگذاری مدل**
```powershell
# Check available models
foundry model list --cached

# Download missing models
foundry model download phi-4-mini
foundry model download qwen2.5-0.5b

# Force reload if needed
foundry model unload --all
foundry model run phi-4-mini
```

**مشکلات وابستگی**
```powershell
# Upgrade pip and reinstall
python -m pip install --upgrade pip
pip install -r requirements.txt --force-reinstall

# For Node.js samples
npm cache clean --force
npm install
```

## خلاصه
این ماژول نمایانگر پیشرفته‌ترین سطح توسعه هوش مصنوعی در لبه است که ابزارهای سطح سازمانی مایکروسافت را با انعطاف‌پذیری و نوآوری اکوسیستم متن‌باز ترکیب می‌کند. با تسلط بر Foundry Local از طریق تمام ۱۰ نمونه جامع، شما در خط مقدم توسعه کاربردهای هوش مصنوعی قرار خواهید گرفت.

**مسیر کامل یادگیری:**
- **پایه** (نمونه‌های ۰۱-۰۳): یکپارچه‌سازی API و مدیریت مدل
- **کاربردها** (نمونه‌های ۰۴-۰۶): RAG، عوامل و مسیریابی هوشمند
- **پیشرفته** (نمونه‌های ۰۷-۱۰): چارچوب‌های تولید و یکپارچه‌سازی سازمانی

برای یکپارچه‌سازی Azure OpenAI (جلسه ۲)، به فایل‌های README نمونه‌های جداگانه مراجعه کنید تا متغیرهای محیطی مورد نیاز و تنظیمات نسخه API را مشاهده کنید.

---

