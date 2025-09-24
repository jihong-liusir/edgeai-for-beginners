<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "13cb0371a2aea01d721186ced4a25e1a",
  "translation_date": "2025-09-24T15:35:37+00:00",
  "source_file": "Module08/samples/08/README.md",
  "language_code": "ne"
}
-->
# Windows 11 च्याट नमूना - Foundry Local

Windows 11 को लागि आधुनिक च्याट एप्लिकेसन, जसले Microsoft Foundry Local लाई सुन्दर र प्राकृतिक इन्टरफेससँग एकीकृत गर्दछ। Electron प्रयोग गरेर निर्माण गरिएको र Microsoft को आधिकारिक Foundry Local ढाँचाहरू अनुसरण गरिएको।

## अवलोकन

यो नमूनाले उत्पादन-तयार च्याट एप्लिकेसन कसरी बनाउने भन्ने देखाउँछ, जसले Foundry Local मार्फत स्थानीय AI मोडेलहरू प्रयोग गर्दछ। यसले प्रयोगकर्ताहरूलाई क्लाउड निर्भरता बिना गोपनीयता-केंद्रित AI संवाद प्रदान गर्दछ।

## विशेषताहरू

### 🎨 **Windows 11 प्राकृतिक डिजाइन**
- Fluent Design System को एकीकरण
- Mica सामग्री प्रभावहरू र पारदर्शिता
- Windows 11 को प्राकृतिक थिम समर्थन
- सबै स्क्रिन आकारहरूको लागि उत्तरदायी लेआउट
- अटोमेटिक डार्क/लाइट मोड स्विचिंग

### 🤖 **AI मोडेल एकीकरण**
- Foundry Local सेवा एकीकरण
- बहु मोडेल समर्थन र तातो-स्विचिंग
- वास्तविक-समय स्ट्रिमिङ प्रतिक्रिया
- स्थानीय र क्लाउड मोडेल स्विचिंग
- मोडेल स्वास्थ्य निगरानी र स्थिति

### 💬 **च्याट अनुभव**
- वास्तविक-समय टाइपिङ संकेतकहरू
- सन्देश इतिहासको स्थायित्व
- च्याट संवादहरू निर्यात गर्नुहोस्
- अनुकूलन प्रणाली प्रॉम्प्टहरू
- संवाद शाखा र व्यवस्थापन

### ⚡ **प्रदर्शन विशेषताहरू**
- Lazy लोडिङ र भर्चुअलाइजेशन
- लामो संवादहरूको लागि अनुकूलित रेंडरिङ
- पृष्ठभूमि मोडेल प्रीलोडिङ
- कुशल मेमोरी व्यवस्थापन
- स्मूथ एनिमेसन र ट्रान्जिसनहरू

## वास्तुकला

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

## आवश्यकताहरू

### प्रणाली आवश्यकताहरू
- **OS**: Windows 11 (22H2 वा पछिल्लो सिफारिस गरिएको)
- **RAM**: न्यूनतम 8GB, ठूला मोडेलहरूको लागि 16GB+ सिफारिस गरिएको
- **स्टोरेज**: मोडेलहरूको लागि 10GB+ खाली ठाउँ
- **GPU**: वैकल्पिक तर छिटो इन्फरेन्सको लागि सिफारिस गरिएको

### सफ्टवेयर निर्भरता
- **Node.js**: v18.0.0 वा पछिल्लो
- **Foundry Local**: Microsoft बाट पछिल्लो संस्करण
- **Git**: क्लोनिङ र विकासको लागि

## स्थापना

### 1. Foundry Local स्थापना गर्नुहोस्
```powershell
# Download from GitHub releases and install
winget install Microsoft.FoundryLocal

# Verify installation
foundry --version
```

### 2. क्लोन र सेटअप गर्नुहोस्
```bash
# Navigate to sample directory
cd Module08/samples/08

# Install dependencies
npm install

# Install Electron if not global
npm install -g electron
```

### 3. वातावरण कन्फिगर गर्नुहोस्
```powershell
# Optional: Set cloud model credentials for hybrid mode
$env:AZURE_OPENAI_KEY="your-api-key"
$env:AZURE_OPENAI_ENDPOINT="your-endpoint"
$env:AZURE_OPENAI_MODEL="gpt-4"
```

### 4. एप्लिकेसन चलाउनुहोस्
```bash
# Development mode
npm start

# Production build
npm run build
npm run dist
```

## परियोजना संरचना

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

## प्रमुख विशेषताहरूको गहिरो अध्ययन

### Windows 11 एकीकरण

**Fluent Design System**
- Mica पृष्ठभूमि सामग्रीहरू
- Acrylic पारदर्शिता प्रभावहरू
- गोलाकार कुनाहरू र आधुनिक स्पेसिङ
- Windows 11 को प्राकृतिक रंग प्यालेट
- पहुँचयोग्यताका लागि सेम्यान्टिक रंग टोकनहरू

**प्राकृतिक Windows विशेषताहरू**
- हालका च्याटहरूको लागि जम्प सूची एकीकरण
- नयाँ सन्देशहरूको लागि Windows सूचनाहरू
- मोडेल अपरेशनहरूको लागि टास्कबार प्रगति
- छिटो कार्यहरूको लागि प्रणाली ट्रे एकीकरण
- Windows Hello प्रमाणीकरण समर्थन

### AI मोडेल व्यवस्थापन

**स्थानीय मोडेलहरू**
```javascript
// Automatic model discovery and loading
const models = await foundryManager.discoverModels();
await foundryManager.loadModel('phi-4-mini');

// Model health monitoring
const health = await foundryManager.checkHealth();
console.log(`Model Status: ${health.status}`);
console.log(`Memory Usage: ${health.memoryUsage}MB`);
```

**हाइब्रिड क्लाउड/स्थानीय समर्थन**
```javascript
// Seamless switching between local and cloud models
if (useCloudModel) {
    await chatManager.switchToCloud('gpt-4');
} else {
    await chatManager.switchToLocal('phi-4-mini');
}
```

### च्याट इन्टरफेस विशेषताहरू

**वास्तविक-समय स्ट्रिमिङ**
- टोकन-दर-टोकन प्रतिक्रिया प्रदर्शन
- स्मूथ टाइपिङ एनिमेसनहरू
- अनुरोध रद्द गर्न सकिने
- टाइपिङ संकेतकहरू र स्थिति

**संवाद व्यवस्थापन**
- स्थायी च्याट इतिहास
- संवाद निर्यात/आयात
- सन्देश खोजी र फिल्टरिङ
- संवाद शाखा
- प्रत्येक संवादको लागि अनुकूलन प्रणाली प्रॉम्प्टहरू

**पहुंचयोग्यता**
- पूर्ण किबोर्ड नेभिगेसन
- स्क्रिन रिडर अनुकूलता
- उच्च कन्फ्रास्ट मोड समर्थन
- अनुकूलन योग्य फन्ट आकारहरू
- भ्वाइस इनपुट एकीकरण

## प्रयोग उदाहरणहरू

### आधारभूत च्याट एकीकरण
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

### मोडेल व्यवस्थापन
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

### सेटिङ्स र अनुकूलन
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

## कन्फिगरेसन विकल्पहरू

### एप्लिकेसन सेटिङ्स
- **थिम**: अटो, लाइट, डार्क मोड
- **मोडेल**: डिफल्ट मोडेल चयन
- **प्रदर्शन**: इन्फरेन्स सेटिङ्स
- **गोपनीयता**: डाटा प्रतिधारण नीतिहरू
- **सूचनाहरू**: सन्देश अलर्टहरू
- **सर्टकटहरू**: किबोर्ड सर्टकटहरू

### च्याट सेटिङ्स
- **स्ट्रिमिङ**: वास्तविक-समय प्रतिक्रियाहरू सक्षम/अक्षम गर्नुहोस्
- **सन्दर्भ लम्बाइ**: संवाद स्मृति
- **तापक्रम**: प्रतिक्रिया सिर्जनशीलता
- **अधिकतम टोकनहरू**: प्रतिक्रिया लम्बाइ सीमा
- **सिस्टम प्रॉम्प्टहरू**: डिफल्ट सहायक व्यवहार

### मोडेल सेटिङ्स
- **अटो-डाउनलोड**: स्वचालित मोडेल अपडेटहरू
- **क्यास आकार**: स्थानीय मोडेल भण्डारण सीमा
- **प्रदर्शन मोड**: CPU बनाम GPU प्राथमिकताहरू
- **स्वास्थ्य जाँचहरू**: निगरानी अन्तरालहरू

## विकास

### स्रोतबाट निर्माण
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

### डिबगिङ
```bash
# Enable debug mode
set DEBUG=foundry-chat:*
npm start

# View developer tools
# Press F12 in the application
```

### परीक्षण
```bash
# Run unit tests
npm test

# Run integration tests
npm run test:integration

# Run end-to-end tests
npm run test:e2e
```

## प्रदर्शन अनुकूलन

### मेमोरी व्यवस्थापन
- कुशल सन्देश भर्चुअलाइजेशन
- स्वचालित गार्बेज कलेक्शन
- मोडेल मेमोरी निगरानी
- बाहिर निस्कँदा स्रोत सफा गर्नुहोस्

### रेंडरिङ अनुकूलन
- लामो संवादहरूको लागि भर्चुअल स्क्रोलिङ
- सन्देश इतिहासको Lazy लोडिङ
- React/DOM अपडेटहरूको अनुकूलन
- GPU-प्रदत्त एनिमेसनहरू

### नेटवर्क अनुकूलन
- कनेक्शन पूलिङ
- अनुरोध ब्याचिङ
- स्वचालित पुन: प्रयास तर्क
- अफलाइन मोड समर्थन

## सुरक्षा विचारहरू

### डाटा गोपनीयता
- स्थानीय-प्रथम वास्तुकला
- क्लाउड डाटा प्रसारण छैन (स्थानीय मोड)
- एन्क्रिप्टेड संवाद भण्डारण
- सुरक्षित प्रमाणपत्र व्यवस्थापन

### एप्लिकेसन सुरक्षा
- स्यान्डबक्स गरिएको रेंडरर प्रक्रियाहरू
- सामग्री सुरक्षा नीति (CSP)
- रिमोट कोड कार्यान्वयन छैन
- सुरक्षित IPC संचार

## समस्या समाधान

### सामान्य समस्याहरू

**Foundry Local सुरु हुँदैन**
```powershell
# Check service status
foundry status

# Restart service
foundry restart

# Check logs
foundry logs
```

**मोडेल लोडिङ असफलता**
- पर्याप्त डिस्क स्थान सुनिश्चित गर्नुहोस्
- डाउनलोडहरूको लागि इन्टरनेट कनेक्शन जाँच गर्नुहोस्
- GPU ड्राइभरहरू अपडेट गर्नुहोस्
- विभिन्न मोडेल भेरियन्टहरू प्रयास गर्नुहोस्

**प्रदर्शन समस्याहरू**
- प्रणाली स्रोतहरू निगरानी गर्नुहोस्
- मोडेल सेटिङ्स समायोजन गर्नुहोस्
- हार्डवेयर एक्सेलेरेशन सक्षम गर्नुहोस्
- अन्य स्रोत-गहन एप्लिकेसनहरू बन्द गर्नुहोस्

### डिबग मोड
डिबग लगिङ सक्षम गर्न वातावरण चर सेट गर्नुहोस्:
```powershell
$env:DEBUG="foundry:*"
$env:FOUNDRY_LOG_LEVEL="debug"
```

## योगदान

### विकास सेटअप
1. रिपोजिटरी फोर्क गर्नुहोस्
2. फिचर ब्रान्च बनाउनुहोस्
3. निर्भरता स्थापना गर्नुहोस्: `npm install`
4. परिवर्तनहरू गर्नुहोस् र परीक्षण गर्नुहोस्
5. पुल अनुरोध सबमिट गर्नुहोस्

### कोड शैली
- ESLint कन्फिगरेसन प्रदान गरिएको
- कोड फर्म्याटिङको लागि Prettier
- टाइप सुरक्षा लागि TypeScript
- दस्तावेजीकरणको लागि JSDoc टिप्पणीहरू

## सिकाइ परिणामहरू

यो नमूना पूरा गरेपछि, तपाईंले बुझ्नुहुनेछ:

1. **Windows 11 प्राकृतिक विकास**
   - Fluent Design System कार्यान्वयन
   - प्राकृतिक Windows एकीकरण
   - Electron सुरक्षा उत्तम अभ्यासहरू

2. **AI मोडेल एकीकरण**
   - Foundry Local सेवा वास्तुकला
   - मोडेल जीवनचक्र व्यवस्थापन
   - प्रदर्शन निगरानी र अनुकूलन

3. **वास्तविक-समय च्याट प्रणालीहरू**
   - स्ट्रिमिङ प्रतिक्रिया ह्यान्डलिङ
   - संवाद अवस्था व्यवस्थापन
   - प्रयोगकर्ता अनुभव ढाँचाहरू

4. **उत्पादन एप्लिकेसन विकास**
   - त्रुटि ह्यान्डलिङ र पुन: प्राप्ति
   - प्रदर्शन अनुकूलन
   - सुरक्षा विचारहरू
   - परीक्षण रणनीतिहरू

## अर्को चरणहरू

- **नमूना 09**: बहु-एजेन्ट समन्वय प्रणाली
- **नमूना 10**: Foundry Local उपकरण एकीकरण
- **उन्नत विषयहरू**: अनुकूलन मोडेल फाइन-ट्युनिङ
- **परिनियोजन**: उद्यम परिनियोजन ढाँचाहरू

## लाइसेन्स

यो नमूनाले Microsoft Foundry Local परियोजनाको समान लाइसेन्स अनुसरण गर्दछ।

---

