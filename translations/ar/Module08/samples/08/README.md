<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "13cb0371a2aea01d721186ced4a25e1a",
  "translation_date": "2025-09-24T13:47:53+00:00",
  "source_file": "Module08/samples/08/README.md",
  "language_code": "ar"
}
-->
# نموذج دردشة Windows 11 - Foundry Local

تطبيق دردشة حديث لنظام Windows 11 يدمج Microsoft Foundry Local بواجهة أصلية جميلة. تم بناؤه باستخدام Electron ويتبع أنماط Foundry Local الرسمية من Microsoft.

## نظرة عامة

يوضح هذا النموذج كيفية إنشاء تطبيق دردشة جاهز للإنتاج يستفيد من نماذج الذكاء الاصطناعي المحلية عبر Foundry Local، مما يوفر للمستخدمين محادثات ذكاء اصطناعي تركز على الخصوصية دون الاعتماد على السحابة.

## الميزات

### 🎨 **تصميم أصلي لنظام Windows 11**
- تكامل مع نظام التصميم Fluent
- تأثيرات مادة Mica والشفافية
- دعم التخصيص لنظام Windows 11
- تصميم متجاوب لجميع أحجام الشاشات
- التبديل التلقائي بين الوضع الداكن والفاتح

### 🤖 **تكامل نماذج الذكاء الاصطناعي**
- تكامل خدمة Foundry Local
- دعم نماذج متعددة مع التبديل الفوري
- استجابات متدفقة في الوقت الحقيقي
- التبديل بين النماذج المحلية والسحابية
- مراقبة صحة النماذج وحالتها

### 💬 **تجربة الدردشة**
- مؤشرات الكتابة في الوقت الحقيقي
- حفظ تاريخ الرسائل
- تصدير محادثات الدردشة
- مطالبات نظام مخصصة
- إدارة وتفرع المحادثات

### ⚡ **ميزات الأداء**
- التحميل الكسول والتصور الافتراضي
- تحسين العرض للمحادثات الطويلة
- تحميل النماذج في الخلفية
- إدارة فعالة للذاكرة
- انتقالات ورسوم متحركة سلسة

## الهيكلية

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

## المتطلبات الأساسية

### متطلبات النظام
- **نظام التشغيل**: Windows 11 (يفضل الإصدار 22H2 أو أحدث)
- **الذاكرة العشوائية**: 8 جيجابايت كحد أدنى، يفضل 16 جيجابايت أو أكثر للنماذج الكبيرة
- **التخزين**: مساحة خالية 10 جيجابايت أو أكثر للنماذج
- **وحدة معالجة الرسومات (GPU)**: اختيارية ولكن يفضل استخدامها لتسريع الاستنتاج

### متطلبات البرمجيات
- **Node.js**: الإصدار 18.0.0 أو أحدث
- **Foundry Local**: أحدث إصدار من Microsoft
- **Git**: للنسخ والتطوير

## التثبيت

### 1. تثبيت Foundry Local
```powershell
# Download from GitHub releases and install
winget install Microsoft.FoundryLocal

# Verify installation
foundry --version
```

### 2. النسخ والإعداد
```bash
# Navigate to sample directory
cd Module08/samples/08

# Install dependencies
npm install

# Install Electron if not global
npm install -g electron
```

### 3. تكوين البيئة
```powershell
# Optional: Set cloud model credentials for hybrid mode
$env:AZURE_OPENAI_KEY="your-api-key"
$env:AZURE_OPENAI_ENDPOINT="your-endpoint"
$env:AZURE_OPENAI_MODEL="gpt-4"
```

### 4. تشغيل التطبيق
```bash
# Development mode
npm start

# Production build
npm run build
npm run dist
```

## هيكل المشروع

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

## استعراض الميزات الرئيسية

### تكامل Windows 11

**نظام التصميم Fluent**
- مواد خلفية Mica
- تأثيرات شفافية Acrylic
- زوايا مستديرة وتباعد حديث
- لوحة ألوان أصلية لنظام Windows 11
- رموز ألوان دلالية لدعم الوصول

**ميزات Windows الأصلية**
- تكامل قائمة القفز للمحادثات الأخيرة
- إشعارات Windows للرسائل الجديدة
- تقدم شريط المهام لعمليات النماذج
- تكامل مع علبة النظام مع إجراءات سريعة
- دعم المصادقة باستخدام Windows Hello

### إدارة نماذج الذكاء الاصطناعي

**النماذج المحلية**
```javascript
// Automatic model discovery and loading
const models = await foundryManager.discoverModels();
await foundryManager.loadModel('phi-4-mini');

// Model health monitoring
const health = await foundryManager.checkHealth();
console.log(`Model Status: ${health.status}`);
console.log(`Memory Usage: ${health.memoryUsage}MB`);
```

**دعم السحابة/المحلية الهجينة**
```javascript
// Seamless switching between local and cloud models
if (useCloudModel) {
    await chatManager.switchToCloud('gpt-4');
} else {
    await chatManager.switchToLocal('phi-4-mini');
}
```

### ميزات واجهة الدردشة

**التدفق في الوقت الحقيقي**
- عرض الاستجابة كلمة بكلمة
- رسوم متحركة سلسة للكتابة
- طلبات قابلة للإلغاء
- مؤشرات الكتابة والحالة

**إدارة المحادثات**
- حفظ تاريخ الدردشة
- تصدير واستيراد المحادثات
- البحث والتصفية في الرسائل
- تفرع المحادثات
- مطالبات نظام مخصصة لكل محادثة

**إمكانية الوصول**
- التنقل الكامل باستخدام لوحة المفاتيح
- توافق مع قارئات الشاشة
- دعم وضع التباين العالي
- أحجام خطوط قابلة للتخصيص
- تكامل إدخال الصوت

## أمثلة الاستخدام

### تكامل الدردشة الأساسي
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

### إدارة النماذج
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

### الإعدادات والتخصيص
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

## خيارات التكوين

### إعدادات التطبيق
- **التصميم**: تلقائي، الوضع الفاتح، الوضع الداكن
- **النموذج**: اختيار النموذج الافتراضي
- **الأداء**: إعدادات الاستنتاج
- **الخصوصية**: سياسات الاحتفاظ بالبيانات
- **الإشعارات**: تنبيهات الرسائل
- **الاختصارات**: اختصارات لوحة المفاتيح

### إعدادات الدردشة
- **التدفق**: تمكين/تعطيل الاستجابات في الوقت الحقيقي
- **طول السياق**: ذاكرة المحادثة
- **درجة الحرارة**: إبداعية الاستجابة
- **الحد الأقصى للكلمات**: حدود طول الاستجابة
- **مطالبات النظام**: سلوك المساعد الافتراضي

### إعدادات النموذج
- **التنزيل التلقائي**: تحديثات النماذج تلقائيًا
- **حجم التخزين المؤقت**: حدود تخزين النماذج المحلية
- **وضع الأداء**: تفضيلات وحدة المعالجة المركزية مقابل وحدة معالجة الرسومات
- **فحوصات الصحة**: فترات المراقبة

## التطوير

### البناء من المصدر
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

### التصحيح
```bash
# Enable debug mode
set DEBUG=foundry-chat:*
npm start

# View developer tools
# Press F12 in the application
```

### الاختبار
```bash
# Run unit tests
npm test

# Run integration tests
npm run test:integration

# Run end-to-end tests
npm run test:e2e
```

## تحسين الأداء

### إدارة الذاكرة
- تصور الرسائل بكفاءة
- جمع القمامة تلقائيًا
- مراقبة ذاكرة النموذج
- تنظيف الموارد عند الإغلاق

### تحسين العرض
- التمرير الافتراضي للمحادثات الطويلة
- التحميل الكسول لتاريخ الرسائل
- تحسين تحديثات React/DOM
- الرسوم المتحركة المسرعة بواسطة وحدة معالجة الرسومات

### تحسين الشبكة
- تجميع الاتصالات
- تجميع الطلبات
- منطق إعادة المحاولة التلقائي
- دعم وضع عدم الاتصال

## اعتبارات الأمان

### خصوصية البيانات
- هيكلية تعتمد على المحلية أولاً
- عدم نقل البيانات إلى السحابة (وضع المحلي)
- تخزين المحادثات مشفر
- إدارة آمنة للمصادقات

### أمان التطبيق
- عمليات العرض المعزولة
- سياسة أمان المحتوى (CSP)
- عدم تنفيذ التعليمات البرمجية عن بُعد
- اتصال IPC آمن

## استكشاف الأخطاء وإصلاحها

### المشكلات الشائعة

**Foundry Local لا يبدأ**
```powershell
# Check service status
foundry status

# Restart service
foundry restart

# Check logs
foundry logs
```

**فشل تحميل النماذج**
- تحقق من وجود مساحة كافية على القرص
- تحقق من اتصال الإنترنت للتنزيلات
- تأكد من تحديث برامج تشغيل وحدة معالجة الرسومات
- جرب نماذج مختلفة

**مشكلات الأداء**
- مراقبة موارد النظام
- ضبط إعدادات النموذج
- تمكين تسريع الأجهزة
- إغلاق التطبيقات الأخرى التي تستهلك الموارد

### وضع التصحيح
قم بتمكين تسجيل التصحيح عن طريق إعداد متغيرات البيئة:
```powershell
$env:DEBUG="foundry:*"
$env:FOUNDRY_LOG_LEVEL="debug"
```

## المساهمة

### إعداد التطوير
1. قم بعمل نسخة من المستودع
2. أنشئ فرعًا للميزة
3. قم بتثبيت التبعيات: `npm install`
4. قم بإجراء التغييرات واختبرها
5. قدم طلب دمج

### نمط الكود
- تم توفير تكوين ESLint
- Prettier لتنسيق الكود
- TypeScript لضمان النوعية
- تعليقات JSDoc للتوثيق

## نتائج التعلم

بعد إكمال هذا النموذج، ستفهم:

1. **تطوير Windows 11 الأصلي**
   - تنفيذ نظام التصميم Fluent
   - تكامل Windows الأصلي
   - أفضل ممارسات أمان Electron

2. **تكامل نماذج الذكاء الاصطناعي**
   - هيكلية خدمة Foundry Local
   - إدارة دورة حياة النموذج
   - مراقبة الأداء وتحسينه

3. **أنظمة الدردشة في الوقت الحقيقي**
   - معالجة الاستجابات المتدفقة
   - إدارة حالة المحادثة
   - أنماط تجربة المستخدم

4. **تطوير التطبيقات الإنتاجية**
   - معالجة الأخطاء واستردادها
   - تحسين الأداء
   - اعتبارات الأمان
   - استراتيجيات الاختبار

## الخطوات التالية

- **النموذج 09**: نظام تنسيق متعدد الوكلاء
- **النموذج 10**: Foundry Local كتكامل أدوات
- **مواضيع متقدمة**: تحسين النماذج المخصصة
- **النشر**: أنماط النشر للمؤسسات

## الترخيص

يتبع هذا النموذج نفس الترخيص الخاص بمشروع Microsoft Foundry Local.

---

