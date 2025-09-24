<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "13cb0371a2aea01d721186ced4a25e1a",
  "translation_date": "2025-09-24T13:48:17+00:00",
  "source_file": "Module08/samples/08/README.md",
  "language_code": "ur"
}
-->
# ونڈوز 11 چیٹ سیمپل - فاؤنڈری لوکل

ونڈوز 11 کے لیے ایک جدید چیٹ ایپلیکیشن جو مائیکروسافٹ فاؤنڈری لوکل کو ایک خوبصورت نیٹو انٹرفیس کے ساتھ ضم کرتی ہے۔ یہ ایپلیکیشن الیکٹران کے ساتھ بنائی گئی ہے اور مائیکروسافٹ کے آفیشل فاؤنڈری لوکل پیٹرنز کی پیروی کرتی ہے۔

## جائزہ

یہ سیمپل دکھاتا ہے کہ کس طرح ایک پروڈکشن کے لیے تیار چیٹ ایپلیکیشن بنائی جا سکتی ہے جو فاؤنڈری لوکل کے ذریعے لوکل AI ماڈلز کا استعمال کرتی ہے، صارفین کو پرائیویسی پر مبنی AI گفتگو فراہم کرتی ہے بغیر کلاؤڈ پر انحصار کیے۔

## خصوصیات

### 🎨 **ونڈوز 11 نیٹو ڈیزائن**
- فلوئینٹ ڈیزائن سسٹم کا انضمام
- مائیکا میٹیریل ایفیکٹس اور شفافیت
- نیٹو ونڈوز 11 تھیم سپورٹ
- تمام اسکرین سائزز کے لیے ریسپانسیو لے آؤٹ
- ڈارک/لائٹ موڈ کا خودکار سوئچنگ

### 🤖 **AI ماڈل انضمام**
- فاؤنڈری لوکل سروس انٹیگریشن
- متعدد ماڈلز کی سپورٹ کے ساتھ ہاٹ-سوئپنگ
- ریئل ٹائم اسٹریمنگ جوابات
- لوکل اور کلاؤڈ ماڈل سوئچنگ
- ماڈل کی صحت کی نگرانی اور اسٹیٹس

### 💬 **چیٹ کا تجربہ**
- ریئل ٹائم ٹائپنگ انڈیکیٹرز
- پیغام کی تاریخ کا تسلسل
- چیٹ گفتگو کو ایکسپورٹ کریں
- کسٹم سسٹم پرامپٹس
- گفتگو کی شاخ بندی اور انتظام

### ⚡ **کارکردگی کی خصوصیات**
- لیزی لوڈنگ اور ورچوئلائزیشن
- طویل گفتگو کے لیے بہتر رینڈرنگ
- بیک گراؤنڈ ماڈل پری لوڈنگ
- مؤثر میموری مینجمنٹ
- ہموار اینیمیشنز اور ٹرانزیشنز

## آرکیٹیکچر

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

## ضروریات

### سسٹم کی ضروریات
- **OS**: ونڈوز 11 (22H2 یا اس کے بعد کی تجویز کردہ)
- **RAM**: کم از کم 8GB، بڑے ماڈلز کے لیے 16GB+ تجویز کردہ
- **Storage**: ماڈلز کے لیے 10GB+ خالی جگہ
- **GPU**: اختیاری لیکن تیز انفرنس کے لیے تجویز کردہ

### سافٹ ویئر کی ضروریات
- **Node.js**: v18.0.0 یا اس کے بعد
- **Foundry Local**: مائیکروسافٹ سے تازہ ترین ورژن
- **Git**: کلوننگ اور ڈیولپمنٹ کے لیے

## انسٹالیشن

### 1. فاؤنڈری لوکل انسٹال کریں
```powershell
# Download from GitHub releases and install
winget install Microsoft.FoundryLocal

# Verify installation
foundry --version
```

### 2. کلون اور سیٹ اپ کریں
```bash
# Navigate to sample directory
cd Module08/samples/08

# Install dependencies
npm install

# Install Electron if not global
npm install -g electron
```

### 3. ماحول کو ترتیب دیں
```powershell
# Optional: Set cloud model credentials for hybrid mode
$env:AZURE_OPENAI_KEY="your-api-key"
$env:AZURE_OPENAI_ENDPOINT="your-endpoint"
$env:AZURE_OPENAI_MODEL="gpt-4"
```

### 4. ایپلیکیشن چلائیں
```bash
# Development mode
npm start

# Production build
npm run build
npm run dist
```

## پروجیکٹ کی ساخت

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

## کلیدی خصوصیات کی تفصیل

### ونڈوز 11 انضمام

**فلوئینٹ ڈیزائن سسٹم**
- مائیکا بیک گراؤنڈ میٹیریلز
- ایکریلک شفافیت کے اثرات
- گول کنارے اور جدید اسپیسنگ
- نیٹو ونڈوز 11 کلر پیلیٹ
- رسائی کے لیے سیمینٹک کلر ٹوکنز

**نیٹو ونڈوز خصوصیات**
- حالیہ چیٹس کے لیے جمپ لسٹ انضمام
- نئے پیغامات کے لیے ونڈوز نوٹیفیکیشنز
- ماڈل آپریشنز کے لیے ٹاسک بار پروگریس
- سسٹم ٹرے انضمام کے ساتھ فوری ایکشنز
- ونڈوز ہیلو تصدیق کی حمایت

### AI ماڈل مینجمنٹ

**لوکل ماڈلز**
```javascript
// Automatic model discovery and loading
const models = await foundryManager.discoverModels();
await foundryManager.loadModel('phi-4-mini');

// Model health monitoring
const health = await foundryManager.checkHealth();
console.log(`Model Status: ${health.status}`);
console.log(`Memory Usage: ${health.memoryUsage}MB`);
```

**ہائبرڈ کلاؤڈ/لوکل سپورٹ**
```javascript
// Seamless switching between local and cloud models
if (useCloudModel) {
    await chatManager.switchToCloud('gpt-4');
} else {
    await chatManager.switchToLocal('phi-4-mini');
}
```

### چیٹ انٹرفیس کی خصوصیات

**ریئل ٹائم اسٹریمنگ**
- ٹوکن بہ ٹوکن جواب کی نمائش
- ہموار ٹائپنگ اینیمیشنز
- قابل منسوخ درخواستیں
- ٹائپنگ انڈیکیٹرز اور اسٹیٹس

**گفتگو کا انتظام**
- مستقل چیٹ ہسٹری
- گفتگو کو ایکسپورٹ/امپورٹ کریں
- پیغام کی تلاش اور فلٹرنگ
- گفتگو کی شاخ بندی
- ہر گفتگو کے لیے کسٹم سسٹم پرامپٹس

**رسائی**
- مکمل کی بورڈ نیویگیشن
- اسکرین ریڈر مطابقت
- ہائی کنٹراسٹ موڈ سپورٹ
- قابل تخصیص فونٹ سائز
- وائس ان پٹ انضمام

## استعمال کی مثالیں

### بنیادی چیٹ انضمام
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

### ماڈل مینجمنٹ
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

### سیٹنگز اور تخصیص
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

## کنفیگریشن آپشنز

### ایپلیکیشن سیٹنگز
- **تھیم**: آٹو، لائٹ، ڈارک موڈ
- **ماڈل**: ڈیفالٹ ماڈل کا انتخاب
- **کارکردگی**: انفرنس سیٹنگز
- **پرائیویسی**: ڈیٹا برقرار رکھنے کی پالیسیاں
- **نوٹیفیکیشنز**: پیغام کے الرٹس
- **شارٹ کٹس**: کی بورڈ شارٹ کٹس

### چیٹ سیٹنگز
- **اسٹریمنگ**: ریئل ٹائم جوابات کو فعال/غیر فعال کریں
- **کانٹیکسٹ لینتھ**: گفتگو کی یادداشت
- **ٹمپریچر**: جواب کی تخلیقی صلاحیت
- **میکس ٹوکنز**: جواب کی لمبائی کی حدود
- **سسٹم پرامپٹس**: ڈیفالٹ اسسٹنٹ کا رویہ

### ماڈل سیٹنگز
- **آٹو-ڈاؤنلوڈ**: ماڈل کی خودکار اپڈیٹس
- **کیچ سائز**: لوکل ماڈل اسٹوریج کی حدود
- **پرفارمنس موڈ**: CPU بمقابلہ GPU ترجیحات
- **ہیلتھ چیکس**: نگرانی کے وقفے

## ڈیولپمنٹ

### سورس سے بنانا
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

### ڈیبگنگ
```bash
# Enable debug mode
set DEBUG=foundry-chat:*
npm start

# View developer tools
# Press F12 in the application
```

### ٹیسٹنگ
```bash
# Run unit tests
npm test

# Run integration tests
npm run test:integration

# Run end-to-end tests
npm run test:e2e
```

## کارکردگی کی اصلاح

### میموری مینجمنٹ
- مؤثر پیغام ورچوئلائزیشن
- خودکار گاربیج کلیکشن
- ماڈل میموری کی نگرانی
- ایپلیکیشن بند ہونے پر وسائل کی صفائی

### رینڈرنگ کی اصلاح
- طویل گفتگو کے لیے ورچوئل اسکرولنگ
- پیغام کی تاریخ کا لیزی لوڈنگ
- بہتر React/DOM اپڈیٹس
- GPU-ایکسلیریٹڈ اینیمیشنز

### نیٹ ورک کی اصلاح
- کنکشن پولنگ
- درخواستوں کا بیچنگ
- خودکار ریٹری لاجک
- آف لائن موڈ سپورٹ

## سیکیورٹی کے تحفظات

### ڈیٹا پرائیویسی
- لوکل-فرسٹ آرکیٹیکچر
- کلاؤڈ ڈیٹا ٹرانسمیشن نہیں (لوکل موڈ)
- گفتگو کی انکرپٹڈ اسٹوریج
- محفوظ کریڈینشل مینجمنٹ

### ایپلیکیشن سیکیورٹی
- سینڈباکسڈ رینڈرر پروسیسز
- مواد کی سیکیورٹی پالیسی (CSP)
- ریموٹ کوڈ ایکزیکیوشن نہیں
- محفوظ IPC کمیونیکیشن

## خرابیوں کا پتہ لگانا

### عام مسائل

**فاؤنڈری لوکل شروع نہیں ہو رہا**
```powershell
# Check service status
foundry status

# Restart service
foundry restart

# Check logs
foundry logs
```

**ماڈل لوڈنگ کی ناکامیاں**
- کافی ڈسک اسپیس کی تصدیق کریں
- ڈاؤنلوڈز کے لیے انٹرنیٹ کنکشن چیک کریں
- GPU ڈرائیورز کو اپڈیٹ کریں
- مختلف ماڈل ویریئنٹس آزمائیں

**کارکردگی کے مسائل**
- سسٹم وسائل کی نگرانی کریں
- ماڈل سیٹنگز کو ایڈجسٹ کریں
- ہارڈویئر ایکسیلیریشن کو فعال کریں
- دیگر وسائل کے استعمال کرنے والی ایپلیکیشنز بند کریں

### ڈیبگ موڈ
ماحول کے متغیرات سیٹ کرکے ڈیبگ لاگنگ کو فعال کریں:
```powershell
$env:DEBUG="foundry:*"
$env:FOUNDRY_LOG_LEVEL="debug"
```

## تعاون

### ڈیولپمنٹ سیٹ اپ
1. ریپوزیٹری کو فورک کریں
2. فیچر برانچ بنائیں
3. ڈیپینڈنسیز انسٹال کریں: `npm install`
4. تبدیلیاں کریں اور ٹیسٹ کریں
5. پل ریکویسٹ جمع کروائیں

### کوڈ اسٹائل
- ESLint کنفیگریشن فراہم کی گئی ہے
- کوڈ فارمیٹنگ کے لیے Prettier
- ٹائپ سیفٹی کے لیے TypeScript
- دستاویزات کے لیے JSDoc کمنٹس

## سیکھنے کے نتائج

اس سیمپل کو مکمل کرنے کے بعد آپ سمجھ جائیں گے:

1. **ونڈوز 11 نیٹو ڈیولپمنٹ**
   - فلوئینٹ ڈیزائن سسٹم کا نفاذ
   - نیٹو ونڈوز انضمام
   - الیکٹران سیکیورٹی کے بہترین طریقے

2. **AI ماڈل انضمام**
   - فاؤنڈری لوکل سروس آرکیٹیکچر
   - ماڈل لائف سائیکل مینجمنٹ
   - کارکردگی کی نگرانی اور اصلاح

3. **ریئل ٹائم چیٹ سسٹمز**
   - اسٹریمنگ جواب کی ہینڈلنگ
   - گفتگو کی حالت کا انتظام
   - صارف کے تجربے کے پیٹرنز

4. **پروڈکشن ایپلیکیشن ڈیولپمنٹ**
   - خرابیوں کا پتہ لگانا اور بحالی
   - کارکردگی کی اصلاح
   - سیکیورٹی کے تحفظات
   - ٹیسٹنگ کی حکمت عملی

## اگلے مراحل

- **سیمپل 09**: ملٹی-ایجنٹ آرکیسٹریشن سسٹم
- **سیمپل 10**: فاؤنڈری لوکل بطور ٹولز انضمام
- **ایڈوانسڈ ٹاپکس**: کسٹم ماڈل فائن-ٹیوننگ
- **ڈیپلائمنٹ**: انٹرپرائز ڈیپلائمنٹ پیٹرنز

## لائسنس

یہ سیمپل مائیکروسافٹ فاؤنڈری لوکل پروجیکٹ کے جیسے ہی لائسنس کی پیروی کرتا ہے۔

---

