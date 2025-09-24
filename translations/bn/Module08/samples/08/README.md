<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "13cb0371a2aea01d721186ced4a25e1a",
  "translation_date": "2025-09-24T15:34:38+00:00",
  "source_file": "Module08/samples/08/README.md",
  "language_code": "bn"
}
-->
# Windows 11 চ্যাট নমুনা - Foundry Local

Windows 11-এর জন্য একটি আধুনিক চ্যাট অ্যাপ্লিকেশন যা Microsoft Foundry Local-এর সাথে একটি সুন্দর নেটিভ ইন্টারফেসে সংযুক্ত। এটি Electron ব্যবহার করে তৈরি এবং Microsoft-এর অফিসিয়াল Foundry Local প্যাটার্ন অনুসরণ করে।

## সংক্ষিপ্ত বিবরণ

এই নমুনাটি দেখায় কীভাবে একটি প্রোডাকশন-রেডি চ্যাট অ্যাপ্লিকেশন তৈরি করা যায় যা Foundry Local-এর মাধ্যমে স্থানীয় AI মডেল ব্যবহার করে। এটি ব্যবহারকারীদের ক্লাউড নির্ভরতা ছাড়াই গোপনীয়তা-কেন্দ্রিক AI কথোপকথনের সুবিধা প্রদান করে।

## বৈশিষ্ট্যসমূহ

### 🎨 **Windows 11 নেটিভ ডিজাইন**
- Fluent Design System ইন্টিগ্রেশন
- Mica উপাদানের প্রভাব এবং স্বচ্ছতা
- নেটিভ Windows 11 থিমিং সাপোর্ট
- সমস্ত স্ক্রিন সাইজের জন্য রেসপন্সিভ লেআউট
- ডার্ক/লাইট মোড স্বয়ংক্রিয়ভাবে পরিবর্তন

### 🤖 **AI মডেল ইন্টিগ্রেশন**
- Foundry Local সার্ভিস ইন্টিগ্রেশন
- একাধিক মডেল সাপোর্ট এবং হট-সোয়াপিং
- রিয়েল-টাইম স্ট্রিমিং রেসপন্স
- স্থানীয় এবং ক্লাউড মডেল পরিবর্তন
- মডেল স্বাস্থ্য পর্যবেক্ষণ এবং স্ট্যাটাস

### 💬 **চ্যাট অভিজ্ঞতা**
- রিয়েল-টাইম টাইপিং ইন্ডিকেটর
- বার্তা ইতিহাস সংরক্ষণ
- চ্যাট কথোপকথন এক্সপোর্ট
- কাস্টম সিস্টেম প্রম্পট
- কথোপকথন শাখা এবং ব্যবস্থাপনা

### ⚡ **পারফরম্যান্স বৈশিষ্ট্য**
- লেজি লোডিং এবং ভার্চুয়ালাইজেশন
- দীর্ঘ কথোপকথনের জন্য অপ্টিমাইজড রেন্ডারিং
- ব্যাকগ্রাউন্ড মডেল প্রিলোডিং
- দক্ষ মেমরি ব্যবস্থাপনা
- মসৃণ অ্যানিমেশন এবং ট্রানজিশন

## আর্কিটেকচার

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

## প্রয়োজনীয়তা

### সিস্টেমের প্রয়োজনীয়তা
- **OS**: Windows 11 (22H2 বা পরবর্তী সংস্করণ সুপারিশকৃত)
- **RAM**: ন্যূনতম 8GB, বড় মডেলের জন্য 16GB+ সুপারিশকৃত
- **স্টোরেজ**: মডেলের জন্য 10GB+ ফ্রি স্পেস
- **GPU**: ঐচ্ছিক, তবে দ্রুত ইনফারেন্সের জন্য সুপারিশকৃত

### সফটওয়্যার নির্ভরতা
- **Node.js**: v18.0.0 বা পরবর্তী সংস্করণ
- **Foundry Local**: Microsoft থেকে সর্বশেষ সংস্করণ
- **Git**: ক্লোনিং এবং ডেভেলপমেন্টের জন্য

## ইনস্টলেশন

### 1. Foundry Local ইনস্টল করুন
```powershell
# Download from GitHub releases and install
winget install Microsoft.FoundryLocal

# Verify installation
foundry --version
```

### 2. ক্লোন এবং সেটআপ
```bash
# Navigate to sample directory
cd Module08/samples/08

# Install dependencies
npm install

# Install Electron if not global
npm install -g electron
```

### 3. পরিবেশ কনফিগার করুন
```powershell
# Optional: Set cloud model credentials for hybrid mode
$env:AZURE_OPENAI_KEY="your-api-key"
$env:AZURE_OPENAI_ENDPOINT="your-endpoint"
$env:AZURE_OPENAI_MODEL="gpt-4"
```

### 4. অ্যাপ্লিকেশন চালান
```bash
# Development mode
npm start

# Production build
npm run build
npm run dist
```

## প্রকল্পের কাঠামো

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

## মূল বৈশিষ্ট্যের গভীর বিশ্লেষণ

### Windows 11 ইন্টিগ্রেশন

**Fluent Design System**
- Mica ব্যাকগ্রাউন্ড উপাদান
- Acrylic স্বচ্ছতার প্রভাব
- গোলাকার কোণ এবং আধুনিক স্পেসিং
- নেটিভ Windows 11 রঙের প্যালেট
- অ্যাক্সেসিবিলিটির জন্য সেমান্টিক রঙের টোকেন

**নেটিভ Windows বৈশিষ্ট্য**
- সাম্প্রতিক চ্যাটের জন্য জাম্প লিস্ট ইন্টিগ্রেশন
- নতুন বার্তার জন্য Windows নোটিফিকেশন
- মডেল অপারেশনের জন্য টাস্কবার প্রগ্রেস
- সিস্টেম ট্রে ইন্টিগ্রেশন সহ দ্রুত অ্যাকশন
- Windows Hello প্রমাণীকরণ সাপোর্ট

### AI মডেল ব্যবস্থাপনা

**স্থানীয় মডেল**
```javascript
// Automatic model discovery and loading
const models = await foundryManager.discoverModels();
await foundryManager.loadModel('phi-4-mini');

// Model health monitoring
const health = await foundryManager.checkHealth();
console.log(`Model Status: ${health.status}`);
console.log(`Memory Usage: ${health.memoryUsage}MB`);
```

**হাইব্রিড ক্লাউড/স্থানীয় সাপোর্ট**
```javascript
// Seamless switching between local and cloud models
if (useCloudModel) {
    await chatManager.switchToCloud('gpt-4');
} else {
    await chatManager.switchToLocal('phi-4-mini');
}
```

### চ্যাট ইন্টারফেস বৈশিষ্ট্য

**রিয়েল-টাইম স্ট্রিমিং**
- টোকেন-বাই-টোকেন রেসপন্স প্রদর্শন
- মসৃণ টাইপিং অ্যানিমেশন
- বাতিলযোগ্য অনুরোধ
- টাইপিং ইন্ডিকেটর এবং স্ট্যাটাস

**কথোপকথন ব্যবস্থাপনা**
- স্থায়ী চ্যাট ইতিহাস
- কথোপকথন এক্সপোর্ট/ইমপোর্ট
- বার্তা অনুসন্ধান এবং ফিল্টারিং
- কথোপকথন শাখা
- প্রতিটি কথোপকথনের জন্য কাস্টম সিস্টেম প্রম্পট

**অ্যাক্সেসিবিলিটি**
- সম্পূর্ণ কীবোর্ড নেভিগেশন
- স্ক্রিন রিডার সামঞ্জস্যতা
- উচ্চ কনট্রাস্ট মোড সাপোর্ট
- কাস্টমাইজযোগ্য ফন্ট সাইজ
- ভয়েস ইনপুট ইন্টিগ্রেশন

## ব্যবহার উদাহরণ

### বেসিক চ্যাট ইন্টিগ্রেশন
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

### মডেল ব্যবস্থাপনা
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

### সেটিংস এবং কাস্টমাইজেশন
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

## কনফিগারেশন অপশন

### অ্যাপ্লিকেশন সেটিংস
- **থিম**: অটো, লাইট, ডার্ক মোড
- **মডেল**: ডিফল্ট মডেল নির্বাচন
- **পারফরম্যান্স**: ইনফারেন্স সেটিংস
- **গোপনীয়তা**: ডেটা সংরক্ষণ নীতি
- **নোটিফিকেশন**: বার্তা সতর্কতা
- **শর্টকাট**: কীবোর্ড শর্টকাট

### চ্যাট সেটিংস
- **স্ট্রিমিং**: রিয়েল-টাইম রেসপন্স চালু/বন্ধ
- **কনটেক্সট লেংথ**: কথোপকথনের স্মৃতি
- **টেম্পারেচার**: রেসপন্সের সৃজনশীলতা
- **ম্যাক্স টোকেন**: রেসপন্সের দৈর্ঘ্যের সীমা
- **সিস্টেম প্রম্পট**: ডিফল্ট অ্যাসিস্ট্যান্ট আচরণ

### মডেল সেটিংস
- **অটো-ডাউনলোড**: স্বয়ংক্রিয় মডেল আপডেট
- **ক্যাশ সাইজ**: স্থানীয় মডেল স্টোরেজ সীমা
- **পারফরম্যান্স মোড**: CPU বনাম GPU পছন্দ
- **হেলথ চেকস**: পর্যবেক্ষণের সময়সূচি

## উন্নয়ন

### সোর্স থেকে তৈরি করা
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

### ডিবাগিং
```bash
# Enable debug mode
set DEBUG=foundry-chat:*
npm start

# View developer tools
# Press F12 in the application
```

### টেস্টিং
```bash
# Run unit tests
npm test

# Run integration tests
npm run test:integration

# Run end-to-end tests
npm run test:e2e
```

## পারফরম্যান্স অপ্টিমাইজেশন

### মেমরি ব্যবস্থাপনা
- দক্ষ বার্তা ভার্চুয়ালাইজেশন
- স্বয়ংক্রিয় গার্বেজ সংগ্রহ
- মডেল মেমরি পর্যবেক্ষণ
- প্রস্থান করার সময় রিসোর্স ক্লিনআপ

### রেন্ডারিং অপ্টিমাইজেশন
- দীর্ঘ কথোপকথনের জন্য ভার্চুয়াল স্ক্রোলিং
- বার্তা ইতিহাসের লেজি লোডিং
- অপ্টিমাইজড React/DOM আপডেট
- GPU-অ্যাক্সিলারেটেড অ্যানিমেশন

### নেটওয়ার্ক অপ্টিমাইজেশন
- সংযোগ পুলিং
- অনুরোধ ব্যাচিং
- স্বয়ংক্রিয় পুনরায় চেষ্টা করার লজিক
- অফলাইন মোড সাপোর্ট

## নিরাপত্তা বিবেচনা

### ডেটা গোপনীয়তা
- স্থানীয়-প্রথম আর্কিটেকচার
- ক্লাউড ডেটা ট্রান্সমিশন নেই (স্থানীয় মোড)
- এনক্রিপ্টেড কথোপকথন সংরক্ষণ
- নিরাপদ ক্রেডেনশিয়াল ব্যবস্থাপনা

### অ্যাপ্লিকেশন নিরাপত্তা
- স্যান্ডবক্সড রেন্ডারার প্রসেস
- কন্টেন্ট সিকিউরিটি পলিসি (CSP)
- রিমোট কোড এক্সিকিউশন নেই
- নিরাপদ IPC যোগাযোগ

## সমস্যা সমাধান

### সাধারণ সমস্যা

**Foundry Local চালু হচ্ছে না**
```powershell
# Check service status
foundry status

# Restart service
foundry restart

# Check logs
foundry logs
```

**মডেল লোডিং ব্যর্থতা**
- পর্যাপ্ত ডিস্ক স্পেস যাচাই করুন
- ডাউনলোডের জন্য ইন্টারনেট সংযোগ পরীক্ষা করুন
- GPU ড্রাইভার আপডেট নিশ্চিত করুন
- বিভিন্ন মডেল ভেরিয়েন্ট চেষ্টা করুন

**পারফরম্যান্স সমস্যা**
- সিস্টেম রিসোর্স পর্যবেক্ষণ করুন
- মডেল সেটিংস সামঞ্জস্য করুন
- হার্ডওয়্যার অ্যাক্সিলারেশন চালু করুন
- অন্যান্য রিসোর্স-ইনটেনসিভ অ্যাপ্লিকেশন বন্ধ করুন

### ডিবাগ মোড
পরিবেশ ভেরিয়েবল সেট করে ডিবাগ লগিং সক্ষম করুন:
```powershell
$env:DEBUG="foundry:*"
$env:FOUNDRY_LOG_LEVEL="debug"
```

## অবদান

### উন্নয়ন সেটআপ
1. রিপোজিটরি ফর্ক করুন
2. একটি ফিচার ব্রাঞ্চ তৈরি করুন
3. নির্ভরতা ইনস্টল করুন: `npm install`
4. পরিবর্তন করুন এবং পরীক্ষা করুন
5. একটি পুল রিকোয়েস্ট জমা দিন

### কোড স্টাইল
- ESLint কনফিগারেশন প্রদান করা হয়েছে
- কোড ফরম্যাটিংয়ের জন্য Prettier
- টাইপ সুরক্ষার জন্য TypeScript
- ডকুমেন্টেশনের জন্য JSDoc মন্তব্য

## শেখার ফলাফল

এই নমুনাটি সম্পন্ন করার পরে আপনি বুঝতে পারবেন:

1. **Windows 11 নেটিভ ডেভেলপমেন্ট**
   - Fluent Design System বাস্তবায়ন
   - নেটিভ Windows ইন্টিগ্রেশন
   - Electron নিরাপত্তার সেরা অনুশীলন

2. **AI মডেল ইন্টিগ্রেশন**
   - Foundry Local সার্ভিস আর্কিটেকচার
   - মডেল লাইফসাইকেল ব্যবস্থাপনা
   - পারফরম্যান্স পর্যবেক্ষণ এবং অপ্টিমাইজেশন

3. **রিয়েল-টাইম চ্যাট সিস্টেম**
   - স্ট্রিমিং রেসপন্স পরিচালনা
   - কথোপকথনের অবস্থা ব্যবস্থাপনা
   - ব্যবহারকারীর অভিজ্ঞতার প্যাটার্ন

4. **প্রোডাকশন অ্যাপ্লিকেশন ডেভেলপমেন্ট**
   - ত্রুটি পরিচালনা এবং পুনরুদ্ধার
   - পারফরম্যান্স অপ্টিমাইজেশন
   - নিরাপত্তা বিবেচনা
   - টেস্টিং কৌশল

## পরবর্তী পদক্ষেপ

- **নমুনা 09**: মাল্টি-এজেন্ট অর্কেস্ট্রেশন সিস্টেম
- **নমুনা 10**: Foundry Local টুলস ইন্টিগ্রেশন
- **উন্নত বিষয়**: কাস্টম মডেল ফাইন-টিউনিং
- **ডিপ্লয়মেন্ট**: এন্টারপ্রাইজ ডিপ্লয়মেন্ট প্যাটার্ন

## লাইসেন্স

এই নমুনাটি Microsoft Foundry Local প্রকল্পের মতো একই লাইসেন্স অনুসরণ করে।

---

