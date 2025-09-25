<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "13cb0371a2aea01d721186ced4a25e1a",
  "translation_date": "2025-09-24T12:49:53+00:00",
  "source_file": "Module08/samples/08/README.md",
  "language_code": "fa"
}
-->
# نمونه چت ویندوز 11 - Foundry Local

یک برنامه چت مدرن برای ویندوز 11 که Microsoft Foundry Local را با یک رابط کاربری زیبا و بومی ادغام می‌کند. این برنامه با Electron ساخته شده و از الگوهای رسمی Foundry Local مایکروسافت پیروی می‌کند.

## نمای کلی

این نمونه نشان می‌دهد که چگونه می‌توان یک برنامه چت آماده تولید ایجاد کرد که از مدل‌های هوش مصنوعی محلی از طریق Foundry Local استفاده می‌کند و مکالمات هوش مصنوعی متمرکز بر حفظ حریم خصوصی را بدون وابستگی به ابر ارائه می‌دهد.

## ویژگی‌ها

### 🎨 **طراحی بومی ویندوز 11**
- ادغام با سیستم طراحی Fluent
- افکت‌های مواد Mica و شفافیت
- پشتیبانی از تم‌های بومی ویندوز 11
- طراحی واکنش‌گرا برای تمام اندازه‌های صفحه‌نمایش
- تغییر خودکار حالت تاریک/روشن

### 🤖 **ادغام مدل‌های هوش مصنوعی**
- ادغام سرویس Foundry Local
- پشتیبانی از مدل‌های متعدد با قابلیت تعویض سریع
- پاسخ‌های استریم در زمان واقعی
- تغییر بین مدل‌های محلی و ابری
- نظارت بر سلامت مدل و وضعیت آن

### 💬 **تجربه چت**
- نشانگرهای تایپ در زمان واقعی
- حفظ تاریخچه پیام‌ها
- امکان صادرات مکالمات چت
- درخواست‌های سیستمی سفارشی
- مدیریت و شاخه‌بندی مکالمات

### ⚡ **ویژگی‌های عملکردی**
- بارگذاری تنبل و مجازی‌سازی
- رندر بهینه برای مکالمات طولانی
- پیش‌بارگذاری مدل‌ها در پس‌زمینه
- مدیریت کارآمد حافظه
- انیمیشن‌ها و انتقال‌های روان

## معماری

```
┌─────────────────────────────────────────────────────────────┐
│                    Windows 11 Chat App                     │
├─────────────────┬─────────────────┬─────────────────────────┤
│   Electron UI   │   IPC Bridge    │    Foundry Manager      │
│                 │                 │                         │
│ • Fluent Design │ • Secure Comms  │ • Model Loading         │
│ • Chat Interface│ • Event Routing │ • Health Monitoring     │
│ • Settings      │ • State Sync    │ • Performance Tracking │
│ • Themes        │ • Error Handler │ • Resource Management   │
└─────────────────┴─────────────────┴─────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│               Microsoft Foundry Local Service               │
│                                                             │
│ • Local Model Hosting    • OpenAI API Compatibility        │
│ • Real-time Inference    • Model Catalog Management        │
│ • Streaming Responses    • Health & Status Monitoring      │
└─────────────────────────────────────────────────────────────┘
```

## پیش‌نیازها

### الزامات سیستم
- **سیستم‌عامل**: ویندوز 11 (22H2 یا نسخه‌های جدیدتر توصیه می‌شود)
- **رم**: حداقل 8 گیگابایت، 16 گیگابایت یا بیشتر برای مدل‌های بزرگ‌تر توصیه می‌شود
- **فضای ذخیره‌سازی**: حداقل 10 گیگابایت فضای آزاد برای مدل‌ها
- **GPU**: اختیاری اما برای استنتاج سریع‌تر توصیه می‌شود

### وابستگی‌های نرم‌افزاری
- **Node.js**: نسخه 18.0.0 یا جدیدتر
- **Foundry Local**: آخرین نسخه از مایکروسافت
- **Git**: برای کلون کردن و توسعه

## نصب

### 1. نصب Foundry Local
```powershell
# Download from GitHub releases and install
winget install Microsoft.FoundryLocal

# Verify installation
foundry --version
```

### 2. کلون کردن و تنظیم
```bash
# Navigate to sample directory
cd Module08/samples/08

# Install dependencies
npm install

# Install Electron if not global
npm install -g electron
```

### 3. پیکربندی محیط
```powershell
# Optional: Set cloud model credentials for hybrid mode
$env:AZURE_OPENAI_KEY="your-api-key"
$env:AZURE_OPENAI_ENDPOINT="your-endpoint"
$env:AZURE_OPENAI_MODEL="gpt-4"
```

### 4. اجرای برنامه
```bash
# Development mode
npm start

# Production build
npm run build
npm run dist
```

## ساختار پروژه

```
08/
├── README.md                 # This documentation
├── package.json             # Project dependencies and scripts
├── electron.js              # Main Electron process
├── preload.js              # Secure preload script
├── src/
│   ├── index.html          # Main application UI
│   ├── styles/
│   │   ├── fluent.css      # Windows 11 Fluent Design
│   │   ├── chat.css        # Chat interface styles
│   │   └── themes.css      # Light/Dark theme support
│   ├── scripts/
│   │   ├── app.js          # Main application logic
│   │   ├── chat.js         # Chat functionality
│   │   ├── models.js       # Model management
│   │   ├── settings.js     # Settings and preferences
│   │   └── utils.js        # Utility functions
│   └── assets/
│       ├── icons/          # Application icons
│       ├── sounds/         # Notification sounds
│       └── images/         # UI images and illustrations
├── foundry/
│   ├── manager.js          # Foundry Local integration
│   └── health.js           # Health monitoring
└── build/
    ├── icon.ico            # Windows application icon
    └── installer.nsi       # NSIS installer script
```

## بررسی عمیق ویژگی‌های کلیدی

### ادغام ویندوز 11

**سیستم طراحی Fluent**
- مواد پس‌زمینه Mica
- افکت‌های شفافیت Acrylic
- گوشه‌های گرد و فاصله‌گذاری مدرن
- پالت رنگ بومی ویندوز 11
- توکن‌های رنگ معنایی برای دسترسی بهتر

**ویژگی‌های بومی ویندوز**
- ادغام لیست پرش برای چت‌های اخیر
- اعلان‌های ویندوز برای پیام‌های جدید
- پیشرفت نوار وظیفه برای عملیات مدل
- ادغام با سینی سیستم و اقدامات سریع
- پشتیبانی از احراز هویت Windows Hello

### مدیریت مدل‌های هوش مصنوعی

**مدل‌های محلی**
```javascript
// Automatic model discovery and loading
const models = await foundryManager.discoverModels();
await foundryManager.loadModel('phi-4-mini');

// Model health monitoring
const health = await foundryManager.checkHealth();
console.log(`Model Status: ${health.status}`);
console.log(`Memory Usage: ${health.memoryUsage}MB`);
```

**پشتیبانی ترکیبی از ابر/محلی**
```javascript
// Seamless switching between local and cloud models
if (useCloudModel) {
    await chatManager.switchToCloud('gpt-4');
} else {
    await chatManager.switchToLocal('phi-4-mini');
}
```

### ویژگی‌های رابط چت

**استریم در زمان واقعی**
- نمایش پاسخ‌ها به صورت توکن به توکن
- انیمیشن‌های تایپ روان
- درخواست‌های قابل لغو
- نشانگرهای تایپ و وضعیت

**مدیریت مکالمات**
- تاریخچه چت پایدار
- صادرات/واردات مکالمات
- جستجو و فیلتر پیام‌ها
- شاخه‌بندی مکالمات
- درخواست‌های سیستمی سفارشی برای هر مکالمه

**دسترسی**
- ناوبری کامل با صفحه‌کلید
- سازگاری با صفحه‌خوان‌ها
- پشتیبانی از حالت کنتراست بالا
- اندازه فونت‌های قابل تنظیم
- ادغام ورودی صوتی

## مثال‌های استفاده

### ادغام چت پایه
```javascript
// Initialize the chat system
const chat = new ChatManager({
    foundryEndpoint: 'http://localhost:5273',
    defaultModel: 'phi-4-mini',
    streaming: true
});

// Send a message
const response = await chat.sendMessage({
    content: 'Explain quantum computing',
    model: 'phi-4-mini',
    systemPrompt: 'You are a helpful physics teacher.'
});

// Handle streaming responses
chat.on('chunk', (chunk) => {
    appendMessageChunk(chunk.content);
});
```

### مدیریت مدل‌ها
```javascript
// Load a new model
await modelManager.loadModel('qwen2.5-coder-0.5b', {
    showProgress: true,
    autoStart: true
});

// Monitor model performance
modelManager.on('performance', (metrics) => {
    updatePerformanceUI(metrics);
});

// Switch models mid-conversation
await chat.switchModel('phi-4-mini', {
    preserveContext: true
});
```

### تنظیمات و سفارشی‌سازی
```javascript
// Configure chat behavior
const settings = {
    theme: 'system', // auto, light, dark
    model: 'phi-4-mini',
    streaming: true,
    maxTokens: 1000,
    temperature: 0.7,
    systemPrompt: 'You are a helpful assistant.'
};

await settingsManager.updateSettings(settings);
```

## گزینه‌های پیکربندی

### تنظیمات برنامه
- **تم**: حالت خودکار، روشن، تاریک
- **مدل**: انتخاب مدل پیش‌فرض
- **عملکرد**: تنظیمات استنتاج
- **حریم خصوصی**: سیاست‌های حفظ داده
- **اعلان‌ها**: هشدارهای پیام
- **میانبرها**: میانبرهای صفحه‌کلید

### تنظیمات چت
- **استریم**: فعال/غیرفعال کردن پاسخ‌های زمان واقعی
- **طول زمینه**: حافظه مکالمه
- **دما**: خلاقیت پاسخ‌ها
- **حداکثر توکن‌ها**: محدودیت طول پاسخ‌ها
- **درخواست‌های سیستمی**: رفتار پیش‌فرض دستیار

### تنظیمات مدل
- **دانلود خودکار**: به‌روزرسانی خودکار مدل‌ها
- **اندازه کش**: محدودیت‌های ذخیره‌سازی مدل‌های محلی
- **حالت عملکرد**: ترجیحات CPU در مقابل GPU
- **بررسی سلامت**: فواصل نظارت

## توسعه

### ساخت از منبع
```bash
# Install development dependencies
npm install

# Run in development mode
npm run dev

# Build for production
npm run build

# Create installer
npm run dist
```

### اشکال‌زدایی
```bash
# Enable debug mode
set DEBUG=foundry-chat:*
npm start

# View developer tools
# Press F12 in the application
```

### تست
```bash
# Run unit tests
npm test

# Run integration tests
npm run test:integration

# Run end-to-end tests
npm run test:e2e
```

## بهینه‌سازی عملکرد

### مدیریت حافظه
- مجازی‌سازی پیام‌های کارآمد
- جمع‌آوری خودکار زباله‌ها
- نظارت بر حافظه مدل
- پاکسازی منابع هنگام خروج

### بهینه‌سازی رندر
- اسکرول مجازی برای مکالمات طولانی
- بارگذاری تنبل تاریخچه پیام‌ها
- به‌روزرسانی‌های بهینه React/DOM
- انیمیشن‌های شتاب‌گرفته با GPU

### بهینه‌سازی شبکه
- تجمیع اتصال‌ها
- دسته‌بندی درخواست‌ها
- منطق تلاش مجدد خودکار
- پشتیبانی از حالت آفلاین

## ملاحظات امنیتی

### حفظ حریم خصوصی داده‌ها
- معماری محلی‌محور
- بدون انتقال داده به ابر (حالت محلی)
- ذخیره‌سازی مکالمات رمزگذاری‌شده
- مدیریت امن اعتبارنامه‌ها

### امنیت برنامه
- پردازش‌های رندر ایزوله‌شده
- سیاست امنیت محتوا (CSP)
- بدون اجرای کد از راه دور
- ارتباطات IPC امن

## رفع اشکال

### مشکلات رایج

**Foundry Local اجرا نمی‌شود**
```powershell
# Check service status
foundry status

# Restart service
foundry restart

# Check logs
foundry logs
```

**خطاهای بارگذاری مدل**
- فضای دیسک کافی را بررسی کنید
- اتصال اینترنت برای دانلودها را بررسی کنید
- مطمئن شوید که درایورهای GPU به‌روز هستند
- مدل‌های مختلف را امتحان کنید

**مشکلات عملکرد**
- منابع سیستم را نظارت کنید
- تنظیمات مدل را تغییر دهید
- شتاب سخت‌افزاری را فعال کنید
- برنامه‌های دیگر با مصرف منابع بالا را ببندید

### حالت اشکال‌زدایی
فعال کردن ثبت اشکال‌زدایی با تنظیم متغیرهای محیطی:
```powershell
$env:DEBUG="foundry:*"
$env:FOUNDRY_LOG_LEVEL="debug"
```

## مشارکت

### تنظیمات توسعه
1. مخزن را فورک کنید
2. یک شاخه ویژگی ایجاد کنید
3. وابستگی‌ها را نصب کنید: `npm install`
4. تغییرات ایجاد کنید و تست کنید
5. درخواست ادغام ارسال کنید

### سبک کدنویسی
- پیکربندی ESLint ارائه شده است
- Prettier برای قالب‌بندی کد
- TypeScript برای ایمنی نوع‌ها
- نظرات JSDoc برای مستندسازی

## نتایج یادگیری

پس از تکمیل این نمونه، شما درک خواهید کرد:

1. **توسعه بومی ویندوز 11**
   - پیاده‌سازی سیستم طراحی Fluent
   - ادغام بومی ویندوز
   - بهترین شیوه‌های امنیتی Electron

2. **ادغام مدل‌های هوش مصنوعی**
   - معماری سرویس Foundry Local
   - مدیریت چرخه عمر مدل‌ها
   - نظارت و بهینه‌سازی عملکرد

3. **سیستم‌های چت زمان واقعی**
   - مدیریت پاسخ‌های استریم
   - مدیریت حالت مکالمه
   - الگوهای تجربه کاربری

4. **توسعه برنامه‌های تولیدی**
   - مدیریت خطا و بازیابی
   - بهینه‌سازی عملکرد
   - ملاحظات امنیتی
   - استراتژی‌های تست

## مراحل بعدی

- **نمونه 09**: سیستم ارکستراسیون چندعاملی
- **نمونه 10**: ادغام Foundry Local به عنوان ابزارها
- **موضوعات پیشرفته**: تنظیم دقیق مدل‌های سفارشی
- **استقرار**: الگوهای استقرار سازمانی

## مجوز

این نمونه از همان مجوز پروژه Microsoft Foundry Local پیروی می‌کند.

---

