<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "13cb0371a2aea01d721186ced4a25e1a",
  "translation_date": "2025-09-24T12:50:59+00:00",
  "source_file": "Module08/samples/08/README.md",
  "language_code": "hi"
}
-->
# Windows 11 चैट सैंपल - Foundry Local

Windows 11 के लिए एक आधुनिक चैट एप्लिकेशन, जो Microsoft Foundry Local को एक सुंदर और नेचुरल इंटरफेस के साथ इंटीग्रेट करता है। इसे Electron के साथ बनाया गया है और Microsoft के आधिकारिक Foundry Local पैटर्न का पालन करता है।

## अवलोकन

यह सैंपल दिखाता है कि कैसे एक प्रोडक्शन-रेडी चैट एप्लिकेशन बनाया जा सकता है, जो Foundry Local के माध्यम से लोकल AI मॉडल्स का उपयोग करता है। यह उपयोगकर्ताओं को क्लाउड पर निर्भरता के बिना प्राइवेसी-केंद्रित AI बातचीत प्रदान करता है।

## विशेषताएँ

### 🎨 **Windows 11 का नेचुरल डिज़ाइन**
- Fluent Design System का इंटीग्रेशन
- Mica मटेरियल इफेक्ट्स और ट्रांसपेरेंसी
- Windows 11 थीमिंग का सपोर्ट
- सभी स्क्रीन साइज के लिए रिस्पॉन्सिव लेआउट
- डार्क/लाइट मोड का ऑटोमैटिक स्विचिंग

### 🤖 **AI मॉडल इंटीग्रेशन**
- Foundry Local सेवा का इंटीग्रेशन
- मल्टीपल मॉडल सपोर्ट और हॉट-स्वैपिंग
- रियल-टाइम स्ट्रीमिंग रिस्पॉन्स
- लोकल और क्लाउड मॉडल स्विचिंग
- मॉडल हेल्थ मॉनिटरिंग और स्टेटस

### 💬 **चैट अनुभव**
- रियल-टाइम टाइपिंग इंडिकेटर्स
- संदेश इतिहास का स्थायित्व
- चैट वार्तालापों का निर्यात
- कस्टम सिस्टम प्रॉम्प्ट्स
- वार्तालाप शाखा और प्रबंधन

### ⚡ **प्रदर्शन विशेषताएँ**
- लेज़ी लोडिंग और वर्चुअलाइजेशन
- लंबे वार्तालापों के लिए ऑप्टिमाइज़्ड रेंडरिंग
- बैकग्राउंड मॉडल प्रीलोडिंग
- प्रभावी मेमोरी प्रबंधन
- स्मूथ एनीमेशन और ट्रांज़िशन

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

## आवश्यकताएँ

### सिस्टम आवश्यकताएँ
- **OS**: Windows 11 (22H2 या बाद का संस्करण अनुशंसित)
- **RAM**: न्यूनतम 8GB, बड़े मॉडल्स के लिए 16GB+ अनुशंसित
- **स्टोरेज**: मॉडल्स के लिए 10GB+ खाली स्थान
- **GPU**: वैकल्पिक, लेकिन तेज़ इन्फरेंस के लिए अनुशंसित

### सॉफ़्टवेयर डिपेंडेंसीज़
- **Node.js**: v18.0.0 या बाद का संस्करण
- **Foundry Local**: Microsoft से नवीनतम संस्करण
- **Git**: क्लोनिंग और विकास के लिए

## इंस्टॉलेशन

### 1. Foundry Local इंस्टॉल करें
```powershell
# Download from GitHub releases and install
winget install Microsoft.FoundryLocal

# Verify installation
foundry --version
```

### 2. क्लोन और सेटअप करें
```bash
# Navigate to sample directory
cd Module08/samples/08

# Install dependencies
npm install

# Install Electron if not global
npm install -g electron
```

### 3. पर्यावरण को कॉन्फ़िगर करें
```powershell
# Optional: Set cloud model credentials for hybrid mode
$env:AZURE_OPENAI_KEY="your-api-key"
$env:AZURE_OPENAI_ENDPOINT="your-endpoint"
$env:AZURE_OPENAI_MODEL="gpt-4"
```

### 4. एप्लिकेशन चलाएँ
```bash
# Development mode
npm start

# Production build
npm run build
npm run dist
```

## प्रोजेक्ट संरचना

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

## प्रमुख विशेषताओं की गहराई से जानकारी

### Windows 11 इंटीग्रेशन

**Fluent Design System**
- Mica बैकग्राउंड मटेरियल्स
- Acrylic ट्रांसपेरेंसी इफेक्ट्स
- राउंडेड कॉर्नर्स और आधुनिक स्पेसिंग
- नेचुरल Windows 11 कलर पैलेट
- एक्सेसिबिलिटी के लिए सेमांटिक कलर टोकन्स

**नेचुरल Windows फीचर्स**
- हाल की चैट्स के लिए जंप लिस्ट इंटीग्रेशन
- नए संदेशों के लिए Windows नोटिफिकेशन
- मॉडल ऑपरेशन्स के लिए टास्कबार प्रोग्रेस
- क्विक एक्शन्स के साथ सिस्टम ट्रे इंटीग्रेशन
- Windows Hello ऑथेंटिकेशन सपोर्ट

### AI मॉडल प्रबंधन

**लोकल मॉडल्स**
```javascript
// Automatic model discovery and loading
const models = await foundryManager.discoverModels();
await foundryManager.loadModel('phi-4-mini');

// Model health monitoring
const health = await foundryManager.checkHealth();
console.log(`Model Status: ${health.status}`);
console.log(`Memory Usage: ${health.memoryUsage}MB`);
```

**हाइब्रिड क्लाउड/लोकल सपोर्ट**
```javascript
// Seamless switching between local and cloud models
if (useCloudModel) {
    await chatManager.switchToCloud('gpt-4');
} else {
    await chatManager.switchToLocal('phi-4-mini');
}
```

### चैट इंटरफेस फीचर्स

**रियल-टाइम स्ट्रीमिंग**
- टोकन-बाय-टोकन रिस्पॉन्स डिस्प्ले
- स्मूथ टाइपिंग एनीमेशन
- अनुरोध रद्द करने की सुविधा
- टाइपिंग इंडिकेटर्स और स्टेटस

**वार्तालाप प्रबंधन**
- स्थायी चैट इतिहास
- वार्तालाप निर्यात/आयात
- संदेश खोज और फ़िल्टरिंग
- वार्तालाप शाखा
- प्रत्येक वार्तालाप के लिए कस्टम सिस्टम प्रॉम्प्ट्स

**एक्सेसिबिलिटी**
- पूर्ण कीबोर्ड नेविगेशन
- स्क्रीन रीडर संगतता
- हाई कॉन्ट्रास्ट मोड सपोर्ट
- कस्टमाइज़ेबल फ़ॉन्ट साइज
- वॉयस इनपुट इंटीग्रेशन

## उपयोग के उदाहरण

### बेसिक चैट इंटीग्रेशन
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

### मॉडल प्रबंधन
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

### सेटिंग्स और कस्टमाइज़ेशन
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

## कॉन्फ़िगरेशन विकल्प

### एप्लिकेशन सेटिंग्स
- **थीम**: ऑटो, लाइट, डार्क मोड
- **मॉडल**: डिफ़ॉल्ट मॉडल चयन
- **प्रदर्शन**: इन्फरेंस सेटिंग्स
- **प्राइवेसी**: डेटा रिटेंशन नीतियाँ
- **नोटिफिकेशन**: संदेश अलर्ट
- **शॉर्टकट्स**: कीबोर्ड शॉर्टकट्स

### चैट सेटिंग्स
- **स्ट्रीमिंग**: रियल-टाइम रिस्पॉन्स सक्षम/अक्षम करें
- **कॉन्टेक्स्ट लंबाई**: वार्तालाप मेमोरी
- **टेम्परेचर**: रिस्पॉन्स की क्रिएटिविटी
- **मैक्स टोकन्स**: रिस्पॉन्स की लंबाई की सीमा
- **सिस्टम प्रॉम्प्ट्स**: डिफ़ॉल्ट असिस्टेंट व्यवहार

### मॉडल सेटिंग्स
- **ऑटो-डाउनलोड**: स्वचालित मॉडल अपडेट्स
- **कैश साइज**: लोकल मॉडल स्टोरेज की सीमा
- **प्रदर्शन मोड**: CPU बनाम GPU प्राथमिकताएँ
- **हेल्थ चेक्स**: मॉनिटरिंग अंतराल

## विकास

### स्रोत से निर्माण
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

### डिबगिंग
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

### मेमोरी प्रबंधन
- प्रभावी संदेश वर्चुअलाइजेशन
- स्वचालित गार्बेज कलेक्शन
- मॉडल मेमोरी मॉनिटरिंग
- एग्जिट पर संसाधन सफाई

### रेंडरिंग अनुकूलन
- लंबे वार्तालापों के लिए वर्चुअल स्क्रॉलिंग
- संदेश इतिहास का लेज़ी लोडिंग
- ऑप्टिमाइज़्ड React/DOM अपडेट्स
- GPU-त्वरित एनीमेशन

### नेटवर्क अनुकूलन
- कनेक्शन पूलिंग
- अनुरोध बैचिंग
- स्वचालित पुनः प्रयास लॉजिक
- ऑफलाइन मोड सपोर्ट

## सुरक्षा विचार

### डेटा प्राइवेसी
- लोकल-फर्स्ट आर्किटेक्चर
- कोई क्लाउड डेटा ट्रांसमिशन नहीं (लोकल मोड)
- एन्क्रिप्टेड वार्तालाप संग्रहण
- सुरक्षित क्रेडेंशियल प्रबंधन

### एप्लिकेशन सुरक्षा
- सैंडबॉक्स्ड रेंडरर प्रोसेस
- कंटेंट सिक्योरिटी पॉलिसी (CSP)
- कोई रिमोट कोड निष्पादन नहीं
- सुरक्षित IPC संचार

## समस्या निवारण

### सामान्य समस्याएँ

**Foundry Local शुरू नहीं हो रहा है**
```powershell
# Check service status
foundry status

# Restart service
foundry restart

# Check logs
foundry logs
```

**मॉडल लोडिंग विफलताएँ**
- पर्याप्त डिस्क स्थान सत्यापित करें
- डाउनलोड के लिए इंटरनेट कनेक्शन जांचें
- GPU ड्राइवर्स अपडेट करें
- विभिन्न मॉडल वेरिएंट्स आज़माएँ

**प्रदर्शन समस्याएँ**
- सिस्टम संसाधनों की निगरानी करें
- मॉडल सेटिंग्स समायोजित करें
- हार्डवेयर एक्सेलेरेशन सक्षम करें
- अन्य संसाधन-गहन एप्लिकेशन बंद करें

### डिबग मोड
पर्यावरण वेरिएबल्स सेट करके डिबग लॉगिंग सक्षम करें:
```powershell
$env:DEBUG="foundry:*"
$env:FOUNDRY_LOG_LEVEL="debug"
```

## योगदान

### विकास सेटअप
1. रिपॉजिटरी को फोर्क करें
2. एक फीचर ब्रांच बनाएं
3. डिपेंडेंसीज़ इंस्टॉल करें: `npm install`
4. बदलाव करें और परीक्षण करें
5. एक पुल अनुरोध सबमिट करें

### कोड स्टाइल
- ESLint कॉन्फ़िगरेशन प्रदान किया गया है
- कोड फॉर्मेटिंग के लिए Prettier
- टाइप सेफ्टी के लिए TypeScript
- डाक्यूमेंटेशन के लिए JSDoc टिप्पणियाँ

## सीखने के परिणाम

इस सैंपल को पूरा करने के बाद, आप समझेंगे:

1. **Windows 11 नेचुरल विकास**
   - Fluent Design System का कार्यान्वयन
   - नेचुरल Windows इंटीग्रेशन
   - Electron सुरक्षा सर्वोत्तम प्रथाएँ

2. **AI मॉडल इंटीग्रेशन**
   - Foundry Local सेवा आर्किटेक्चर
   - मॉडल जीवनचक्र प्रबंधन
   - प्रदर्शन मॉनिटरिंग और अनुकूलन

3. **रियल-टाइम चैट सिस्टम्स**
   - स्ट्रीमिंग रिस्पॉन्स हैंडलिंग
   - वार्तालाप स्थिति प्रबंधन
   - उपयोगकर्ता अनुभव पैटर्न

4. **प्रोडक्शन एप्लिकेशन विकास**
   - त्रुटि हैंडलिंग और रिकवरी
   - प्रदर्शन अनुकूलन
   - सुरक्षा विचार
   - परीक्षण रणनीतियाँ

## अगले कदम

- **सैंपल 09**: मल्टी-एजेंट ऑर्केस्ट्रेशन सिस्टम
- **सैंपल 10**: Foundry Local को टूल्स के रूप में इंटीग्रेट करना
- **एडवांस्ड टॉपिक्स**: कस्टम मॉडल फाइन-ट्यूनिंग
- **डिप्लॉयमेंट**: एंटरप्राइज़ डिप्लॉयमेंट पैटर्न

## लाइसेंस

यह सैंपल Microsoft Foundry Local प्रोजेक्ट के समान लाइसेंस का पालन करता है।

---

