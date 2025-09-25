<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "13cb0371a2aea01d721186ced4a25e1a",
  "translation_date": "2025-09-24T15:35:04+00:00",
  "source_file": "Module08/samples/08/README.md",
  "language_code": "mr"
}
-->
# Windows 11 चॅट नमुना - Foundry Local

Windows 11 साठी एक आधुनिक चॅट अॅप्लिकेशन जे Microsoft Foundry Local सह एक सुंदर नेटिव्ह इंटरफेसमध्ये समाकलित आहे. Electron वापरून तयार केलेले आणि Microsoft च्या अधिकृत Foundry Local पॅटर्नचे अनुसरण करणारे.

## आढावा

हा नमुना स्थानिक AI मॉडेल्सचा उपयोग करून Foundry Local च्या माध्यमातून उत्पादन-तयार चॅट अॅप्लिकेशन कसे तयार करायचे हे दाखवतो, ज्यामुळे वापरकर्त्यांना क्लाउडवर अवलंबून न राहता गोपनीयता-केंद्रित AI संवाद मिळतो.

## वैशिष्ट्ये

### 🎨 **Windows 11 नेटिव्ह डिझाइन**
- Fluent Design System समाकलन
- Mica मटेरियल प्रभाव आणि पारदर्शकता
- नेटिव्ह Windows 11 थीमिंग समर्थन
- सर्व स्क्रीन आकारांसाठी प्रतिसादक्षम लेआउट
- डार्क/लाइट मोड स्वयंचलित स्विचिंग

### 🤖 **AI मॉडेल समाकलन**
- Foundry Local सेवा समाकलन
- हॉट-स्वॅपिंगसह एकाधिक मॉडेल समर्थन
- रिअल-टाइम स्ट्रीमिंग प्रतिसाद
- स्थानिक आणि क्लाउड मॉडेल स्विचिंग
- मॉडेल आरोग्य निरीक्षण आणि स्थिती

### 💬 **चॅट अनुभव**
- रिअल-टाइम टायपिंग इंडिकेटर्स
- संदेश इतिहास टिकवून ठेवणे
- चॅट संभाषणे निर्यात करा
- सानुकूल प्रणाली प्रॉम्प्ट्स
- संभाषण शाखा आणि व्यवस्थापन

### ⚡ **कामगिरी वैशिष्ट्ये**
- Lazy लोडिंग आणि व्हर्च्युअलायझेशन
- दीर्घ संभाषणांसाठी ऑप्टिमाइझ केलेले रेंडरिंग
- पार्श्वभूमी मॉडेल प्रीलोडिंग
- कार्यक्षम मेमरी व्यवस्थापन
- गुळगुळीत अॅनिमेशन आणि संक्रमण

## आर्किटेक्चर

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

## पूर्वापेक्षा

### प्रणाली आवश्यकता
- **OS**: Windows 11 (22H2 किंवा नंतरची शिफारस केलेली)
- **RAM**: किमान 8GB, मोठ्या मॉडेलसाठी 16GB+ शिफारस केलेली
- **Storage**: मॉडेलसाठी 10GB+ मोकळी जागा
- **GPU**: पर्यायी परंतु जलद निष्कर्षासाठी शिफारस केलेली

### सॉफ्टवेअर अवलंबित्व
- **Node.js**: v18.0.0 किंवा नंतरचे
- **Foundry Local**: Microsoft कडून नवीनतम आवृत्ती
- **Git**: क्लोनिंग आणि विकासासाठी

## स्थापना

### 1. Foundry Local स्थापित करा
```powershell
# Download from GitHub releases and install
winget install Microsoft.FoundryLocal

# Verify installation
foundry --version
```

### 2. क्लोन आणि सेटअप
```bash
# Navigate to sample directory
cd Module08/samples/08

# Install dependencies
npm install

# Install Electron if not global
npm install -g electron
```

### 3. पर्यावरण कॉन्फिगर करा
```powershell
# Optional: Set cloud model credentials for hybrid mode
$env:AZURE_OPENAI_KEY="your-api-key"
$env:AZURE_OPENAI_ENDPOINT="your-endpoint"
$env:AZURE_OPENAI_MODEL="gpt-4"
```

### 4. अॅप्लिकेशन चालवा
```bash
# Development mode
npm start

# Production build
npm run build
npm run dist
```

## प्रकल्प संरचना

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

## प्रमुख वैशिष्ट्यांचा सखोल अभ्यास

### Windows 11 समाकलन

**Fluent Design System**
- Mica पार्श्वभूमी सामग्री
- Acrylic पारदर्शकता प्रभाव
- गोलाकार कोपरे आणि आधुनिक मोकळीक
- नेटिव्ह Windows 11 रंग पॅलेट
- अॅक्सेसिबिलिटीसाठी सेमॅंटिक रंग टोकन

**नेटिव्ह Windows वैशिष्ट्ये**
- अलीकडील चॅटसाठी जंप लिस्ट समाकलन
- नवीन संदेशांसाठी Windows सूचना
- मॉडेल ऑपरेशन्ससाठी टास्कबार प्रगती
- जलद क्रियांसह सिस्टम ट्रे समाकलन
- Windows Hello प्रमाणीकरण समर्थन

### AI मॉडेल व्यवस्थापन

**स्थानिक मॉडेल्स**
```javascript
// Automatic model discovery and loading
const models = await foundryManager.discoverModels();
await foundryManager.loadModel('phi-4-mini');

// Model health monitoring
const health = await foundryManager.checkHealth();
console.log(`Model Status: ${health.status}`);
console.log(`Memory Usage: ${health.memoryUsage}MB`);
```

**हायब्रिड क्लाउड/स्थानिक समर्थन**
```javascript
// Seamless switching between local and cloud models
if (useCloudModel) {
    await chatManager.switchToCloud('gpt-4');
} else {
    await chatManager.switchToLocal('phi-4-mini');
}
```

### चॅट इंटरफेस वैशिष्ट्ये

**रिअल-टाइम स्ट्रीमिंग**
- टोकन-बाय-टोकन प्रतिसाद प्रदर्शन
- गुळगुळीत टायपिंग अॅनिमेशन
- विनंत्या रद्द करण्यायोग्य
- टायपिंग इंडिकेटर्स आणि स्थिती

**संभाषण व्यवस्थापन**
- टिकाऊ चॅट इतिहास
- संभाषण निर्यात/आयात
- संदेश शोध आणि फिल्टरिंग
- संभाषण शाखा
- प्रत्येक संभाषणासाठी सानुकूल प्रणाली प्रॉम्प्ट्स

**अॅक्सेसिबिलिटी**
- पूर्ण कीबोर्ड नेव्हिगेशन
- स्क्रीन रीडर सुसंगतता
- उच्च कॉन्ट्रास्ट मोड समर्थन
- सानुकूलनीय फॉन्ट आकार
- व्हॉइस इनपुट समाकलन

## वापर उदाहरणे

### मूलभूत चॅट समाकलन
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

### मॉडेल व्यवस्थापन
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

### सेटिंग्ज आणि सानुकूलन
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

## कॉन्फिगरेशन पर्याय

### अॅप्लिकेशन सेटिंग्ज
- **थीम**: ऑटो, लाइट, डार्क मोड
- **मॉडेल**: डीफॉल्ट मॉडेल निवड
- **कामगिरी**: निष्कर्ष सेटिंग्ज
- **गोपनीयता**: डेटा टिकवून ठेवण्याच्या धोरणा
- **सूचना**: संदेश अलर्ट
- **शॉर्टकट्स**: कीबोर्ड शॉर्टकट्स

### चॅट सेटिंग्ज
- **स्ट्रीमिंग**: रिअल-टाइम प्रतिसाद सक्षम/अक्षम करा
- **संदर्भ लांबी**: संभाषण मेमरी
- **तापमान**: प्रतिसाद सर्जनशीलता
- **कमाल टोकन**: प्रतिसाद लांबी मर्यादा
- **सिस्टम प्रॉम्प्ट्स**: डीफॉल्ट सहाय्यक वर्तन

### मॉडेल सेटिंग्ज
- **ऑटो-डाउनलोड**: स्वयंचलित मॉडेल अद्यतने
- **कॅश आकार**: स्थानिक मॉडेल स्टोरेज मर्यादा
- **कामगिरी मोड**: CPU विरुद्ध GPU प्राधान्य
- **आरोग्य तपासणी**: निरीक्षण अंतराल

## विकास

### स्रोतातून तयार करणे
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

### डीबगिंग
```bash
# Enable debug mode
set DEBUG=foundry-chat:*
npm start

# View developer tools
# Press F12 in the application
```

### चाचणी
```bash
# Run unit tests
npm test

# Run integration tests
npm run test:integration

# Run end-to-end tests
npm run test:e2e
```

## कामगिरी ऑप्टिमायझेशन

### मेमरी व्यवस्थापन
- कार्यक्षम संदेश व्हर्च्युअलायझेशन
- स्वयंचलित कचरा संकलन
- मॉडेल मेमरी निरीक्षण
- बाहेर पडताना संसाधन साफसफाई

### रेंडरिंग ऑप्टिमायझेशन
- दीर्घ संभाषणांसाठी व्हर्च्युअल स्क्रोलिंग
- संदेश इतिहासाचे Lazy लोडिंग
- React/DOM अद्यतने ऑप्टिमाइझ केली
- GPU-प्रेरित अॅनिमेशन

### नेटवर्क ऑप्टिमायझेशन
- कनेक्शन पूलिंग
- विनंती बॅचिंग
- स्वयंचलित पुनर्प्रयत्न लॉजिक
- ऑफलाइन मोड समर्थन

## सुरक्षा विचार

### डेटा गोपनीयता
- स्थानिक-प्रथम आर्किटेक्चर
- क्लाउड डेटा ट्रान्समिशन नाही (स्थानिक मोड)
- एन्क्रिप्टेड संभाषण संग्रहण
- सुरक्षित क्रेडेन्शियल व्यवस्थापन

### अॅप्लिकेशन सुरक्षा
- सॅंडबॉक्स केलेले रेंडरर प्रक्रिया
- Content Security Policy (CSP)
- रिमोट कोड अंमलबजावणी नाही
- सुरक्षित IPC संवाद

## समस्या निराकरण

### सामान्य समस्या

**Foundry Local सुरू होत नाही**
```powershell
# Check service status
foundry status

# Restart service
foundry restart

# Check logs
foundry logs
```

**मॉडेल लोडिंग अपयश**
- पुरेशी डिस्क जागा सत्यापित करा
- डाउनलोडसाठी इंटरनेट कनेक्शन तपासा
- GPU ड्रायव्हर्स अद्यतनित असल्याची खात्री करा
- वेगवेगळ्या मॉडेल प्रकारांचा प्रयत्न करा

**कामगिरी समस्या**
- प्रणाली संसाधने निरीक्षण करा
- मॉडेल सेटिंग्ज समायोजित करा
- हार्डवेअर प्रवेग सक्षम करा
- इतर संसाधन-गहन अॅप्लिकेशन्स बंद करा

### डीबग मोड
पर्यावरण व्हेरिएबल्स सेट करून डीबग लॉगिंग सक्षम करा:
```powershell
$env:DEBUG="foundry:*"
$env:FOUNDRY_LOG_LEVEL="debug"
```

## योगदान

### विकास सेटअप
1. रेपॉजिटरी फोर्क करा
2. फीचर ब्रँच तयार करा
3. अवलंबित्व स्थापित करा: `npm install`
4. बदल करा आणि चाचणी करा
5. पुल विनंती सबमिट करा

### कोड शैली
- ESLint कॉन्फिगरेशन प्रदान केले
- कोड स्वरूपनासाठी Prettier
- टाइप सुरक्षिततेसाठी TypeScript
- दस्तऐवजीकरणासाठी JSDoc टिप्पण्या

## शिकण्याचे परिणाम

हा नमुना पूर्ण केल्यानंतर, तुम्हाला समजेल:

1. **Windows 11 नेटिव्ह विकास**
   - Fluent Design System अंमलबजावणी
   - नेटिव्ह Windows समाकलन
   - Electron सुरक्षा सर्वोत्तम पद्धती

2. **AI मॉडेल समाकलन**
   - Foundry Local सेवा आर्किटेक्चर
   - मॉडेल जीवनचक्र व्यवस्थापन
   - कामगिरी निरीक्षण आणि ऑप्टिमायझेशन

3. **रिअल-टाइम चॅट प्रणाली**
   - स्ट्रीमिंग प्रतिसाद हाताळणी
   - संभाषण स्थिती व्यवस्थापन
   - वापरकर्ता अनुभव पॅटर्न

4. **उत्पादन अॅप्लिकेशन विकास**
   - त्रुटी हाताळणी आणि पुनर्प्राप्ती
   - कामगिरी ऑप्टिमायझेशन
   - सुरक्षा विचार
   - चाचणी धोरणे

## पुढील पावले

- **नमुना 09**: मल्टी-एजंट ऑर्केस्ट्रेशन सिस्टम
- **नमुना 10**: Foundry Local as Tools समाकलन
- **प्रगत विषय**: सानुकूल मॉडेल फाइन-ट्यूनिंग
- **तैनाती**: एंटरप्राइझ तैनाती पॅटर्न

## परवाना

हा नमुना Microsoft Foundry Local प्रकल्पाच्या समान परवान्याचे अनुसरण करतो.

---

