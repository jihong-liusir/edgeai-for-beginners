<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "13cb0371a2aea01d721186ced4a25e1a",
  "translation_date": "2025-10-11T12:54:07+00:00",
  "source_file": "Module08/samples/08/README.md",
  "language_code": "ta"
}
-->
# Windows 11 அரட்டை மாதிரி - Foundry Local

Windows 11 க்கான ஒரு நவீன அரட்டை பயன்பாடு, Microsoft Foundry Local ஐ அழகான இயல்பான இடைமுகத்துடன் ஒருங்கிணைக்கிறது. இது Electron மூலம் உருவாக்கப்பட்டு, Microsoft இன் Foundry Local முறைமைகளைக் கடைபிடிக்கிறது.

## மேலோட்டம்

இந்த மாதிரி, Foundry Local மூலம் உள்ளூர் AI மாதிரிகளைப் பயன்படுத்தி, மேக சார்ந்த சார்பில்லாமல் தனியுரிமை மையமாக்கப்பட்ட AI உரையாடல்களை வழங்கும் உற்பத்தி-தயார் அரட்டை பயன்பாட்டை உருவாக்குவது எப்படி என்பதை விளக்குகிறது.

## அம்சங்கள்

### 🎨 **Windows 11 இயல்பான வடிவமைப்பு**
- Fluent Design System ஒருங்கிணைப்பு
- மைகா பொருள் விளைவுகள் மற்றும் வெளிப்படைத்தன்மை
- இயல்பான Windows 11 தீம் ஆதரவு
- அனைத்து திரை அளவுகளுக்கும் பதிலளிக்கும் அமைப்பு
- இருள்/ஒளி முறை தானியங்கி மாறுதல்

### 🤖 **AI மாதிரி ஒருங்கிணைப்பு**
- Foundry Local சேவை ஒருங்கிணைப்பு
- பல மாதிரி ஆதரவு மற்றும் உடனடி மாறுதல்
- நேரடி ஸ்ட்ரீமிங் பதில்கள்
- உள்ளூர் மற்றும் மேக மாதிரி மாறுதல்
- மாதிரி ஆரோக்கிய கண்காணிப்பு மற்றும் நிலை

### 💬 **அரட்டை அனுபவம்**
- நேரடி தட்டச்சு குறியீடுகள்
- செய்தி வரலாறு நிலைத்தன்மை
- அரட்டை உரையாடல்களை ஏற்றுமதி செய்யும் வசதி
- தனிப்பயன் அமைப்பு உத்தேசங்கள்
- உரையாடல் கிளை மற்றும் மேலாண்மை

### ⚡ **செயல்திறன் அம்சங்கள்**
- சோம்பல் ஏற்றுதல் மற்றும் மெய்நிகர்
- நீண்ட உரையாடல்களுக்கு மேம்பட்ட காட்சிப்படுத்தல்
- பின்னணி மாதிரி முன் ஏற்றுதல்
- திறமையான நினைவக மேலாண்மை
- மென்மையான அனிமேஷன்கள் மற்றும் மாற்றங்கள்

## கட்டமைப்பு

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

## முன் தேவைகள்

### அமைப்பு தேவைகள்
- **OS**: Windows 11 (22H2 அல்லது அதற்கு மேல் பரிந்துரைக்கப்படுகிறது)
- **RAM**: குறைந்தபட்சம் 8GB, பெரிய மாதிரிகளுக்கு 16GB+ பரிந்துரைக்கப்படுகிறது
- **சேமிப்பு**: மாதிரிகளுக்கு 10GB+ இலவச இடம்
- **GPU**: விருப்பமானது ஆனால் வேகமான முடிவுகளுக்கு பரிந்துரைக்கப்படுகிறது

### மென்பொருள் சார்ந்த தேவைகள்
- **Node.js**: v18.0.0 அல்லது அதற்கு மேல்
- **Foundry Local**: Microsoft இன் சமீபத்திய பதிப்பு
- **Git**: கிளோனிங் மற்றும் மேம்பாட்டிற்காக

## நிறுவல்

### 1. Foundry Local ஐ நிறுவவும்
```powershell
# Download from GitHub releases and install
winget install Microsoft.FoundryLocal

# Verify installation
foundry --version
```

### 2. கிளோன் மற்றும் அமைப்பு
```bash
# Navigate to sample directory
cd Module08/samples/08

# Install dependencies
npm install

# Install Electron if not global
npm install -g electron
```

### 3. சூழல் அமைப்பை உள்ளமைக்கவும்
```powershell
# Optional: Set cloud model credentials for hybrid mode
$env:AZURE_OPENAI_KEY="your-api-key"
$env:AZURE_OPENAI_ENDPOINT="your-endpoint"
$env:AZURE_OPENAI_MODEL="gpt-4"
```

### 4. பயன்பாட்டை இயக்கவும்
```bash
# Development mode
npm start

# Production build
npm run build
npm run dist
```

## திட்ட அமைப்பு

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

## முக்கிய அம்சங்கள் விரிவான பார்வை

### Windows 11 ஒருங்கிணைப்பு

**Fluent Design System**
- மைகா பின்னணி பொருட்கள்
- அக்ரிலிக் வெளிப்படைத்தன்மை விளைவுகள்
- வட்டமான மூலைகள் மற்றும் நவீன இடைவெளி
- இயல்பான Windows 11 நிறத் தொகுப்பு
- அணுகல் வசதிக்கான அர்த்தமுள்ள நிற டோக்கன்கள்

**இயல்பான Windows அம்சங்கள்**
- சமீபத்திய அரட்டைகளுக்கான ஜம்ப் பட்டியல் ஒருங்கிணைப்பு
- புதிய செய்திகளுக்கான Windows அறிவிப்புகள்
- மாதிரி செயல்பாடுகளுக்கான டாஸ்க்பார் முன்னேற்றம்
- விரைவான செயல்பாடுகளுடன் சிஸ்டம் டிரே ஒருங்கிணைப்பு
- Windows Hello அங்கீகார ஆதரவு

### AI மாதிரி மேலாண்மை

**உள்ளூர் மாதிரிகள்**
```javascript
// Automatic model discovery and loading
const models = await foundryManager.discoverModels();
await foundryManager.loadModel('phi-4-mini');

// Model health monitoring
const health = await foundryManager.checkHealth();
console.log(`Model Status: ${health.status}`);
console.log(`Memory Usage: ${health.memoryUsage}MB`);
```

**இணைந்த மேகம்/உள்ளூர் ஆதரவு**
```javascript
// Seamless switching between local and cloud models
if (useCloudModel) {
    await chatManager.switchToCloud('gpt-4');
} else {
    await chatManager.switchToLocal('phi-4-mini');
}
```

### அரட்டை இடைமுக அம்சங்கள்

**நேரடி ஸ்ட்ரீமிங்**
- ஒவ்வொரு டோக்கனாக பதில்களை காட்சிப்படுத்தல்
- மென்மையான தட்டச்சு அனிமேஷன்கள்
- ரத்து செய்யக்கூடிய கோரிக்கைகள்
- தட்டச்சு குறியீடுகள் மற்றும் நிலை

**உரையாடல் மேலாண்மை**
- நிலைத்த செய்தி வரலாறு
- உரையாடல் ஏற்றுமதி/இறக்குமதி
- செய்தி தேடல் மற்றும் வடிகட்டி
- உரையாடல் கிளை
- ஒவ்வொரு உரையாடலுக்கும் தனிப்பயன் அமைப்பு உத்தேசங்கள்

**அணுகல் வசதி**
- முழு விசைப்பலகை வழிசெலுத்தல்
- திரை வாசிப்பான் இணக்கத்தன்மை
- உயர் மாறுபாட்டுத்திறன் முறை ஆதரவு
- தனிப்பயன் எழுத்துரு அளவுகள்
- குரல் உள்ளீடு ஒருங்கிணைப்பு

## பயன்பாட்டு உதாரணங்கள்

### அடிப்படை அரட்டை ஒருங்கிணைப்பு
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

### மாதிரி மேலாண்மை
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

### அமைப்புகள் மற்றும் தனிப்பயனாக்கம்
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

## உள்ளமைவு விருப்பங்கள்

### பயன்பாட்டு அமைப்புகள்
- **தீம்**: தானாக, ஒளி, இருள் முறை
- **மாதிரி**: இயல்புநிலை மாதிரி தேர்வு
- **செயல்திறன்**: முடிவு அமைப்புகள்
- **தனியுரிமை**: தரவுகள் காப்பக கொள்கைகள்
- **அறிவிப்புகள்**: செய்தி எச்சரிக்கைகள்
- **குறுக்குவழிகள்**: விசைப்பலகை குறுக்குவழிகள்

### அரட்டை அமைப்புகள்
- **ஸ்ட்ரீமிங்**: நேரடி பதில்களை இயக்கு/முடக்கு
- **சூழல் நீளம்**: உரையாடல் நினைவகம்
- **வெப்பநிலை**: பதிலின் படைப்பாற்றல்
- **அதிகபட்ச டோக்கன்கள்**: பதிலின் நீள வரம்புகள்
- **அமைப்பு உத்தேசங்கள்**: இயல்புநிலை உதவியாளர் நடத்தை

### மாதிரி அமைப்புகள்
- **தானியங்கி பதிவிறக்கம்**: தானாக மாதிரி புதுப்பிப்புகள்
- **கேஷ் அளவு**: உள்ளூர் மாதிரி சேமிப்பு வரம்புகள்
- **செயல்திறன் முறை**: CPU மற்றும் GPU விருப்பங்கள்
- **ஆரோக்கிய சோதனைகள்**: கண்காணிப்பு இடைவெளிகள்

## மேம்பாடு

### மூலத்திலிருந்து கட்டமைத்தல்
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

### பிழைத்திருத்தம்
```bash
# Enable debug mode
set DEBUG=foundry-chat:*
npm start

# View developer tools
# Press F12 in the application
```

### சோதனை
```bash
# Run unit tests
npm test

# Run integration tests
npm run test:integration

# Run end-to-end tests
npm run test:e2e
```

## செயல்திறன் மேம்பாடு

### நினைவக மேலாண்மை
- திறமையான செய்தி மெய்நிகர்
- தானியங்கி கழிவறை சேகரிப்பு
- மாதிரி நினைவக கண்காணிப்பு
- வெளியேறும்போது வளங்களை சுத்தம் செய்தல்

### காட்சிப்படுத்தல் மேம்பாடு
- நீண்ட உரையாடல்களுக்கு மெய்நிகர் ஸ்க்ரோலிங்
- செய்தி வரலாற்றின் சோம்பல் ஏற்றுதல்
- React/DOM புதுப்பிப்புகளை மேம்படுத்தல்
- GPU-ஐ மையமாகக் கொண்ட அனிமேஷன்கள்

### நெட்வொர்க் மேம்பாடு
- இணைப்பு குளங்கள்
- கோரிக்கை தொகுப்புகள்
- தானியங்கி மீண்டும் முயற்சி செய்யும் தந்திரம்
- ஆஃப்லைன் முறை ஆதரவு

## பாதுகாப்பு கருத்துக்கள்

### தரவுக் தனியுரிமை
- உள்ளூர்-முதலில் கட்டமைப்பு
- மேக தரவுப் பரிமாற்றம் இல்லை (உள்ளூர் முறை)
- குறியாக்கப்பட்ட உரையாடல் சேமிப்பு
- பாதுகாப்பான சான்றிதழ் மேலாண்மை

### பயன்பாட்டு பாதுகாப்பு
- மண்சரிவு செய்யப்பட்ட ரெண்டரர் செயல்முறைகள்
- உள்ளடக்க பாதுகாப்பு கொள்கை (CSP)
- தொலைதூர குறியீடு செயல்படுத்தல் இல்லை
- பாதுகாப்பான IPC தொடர்பு

## பிழைத்திருத்தம்

### பொதுவான சிக்கல்கள்

**Foundry Local தொடங்கவில்லை**
```powershell
# Check service status
foundry status

# Restart service
foundry restart

# Check logs
foundry logs
```

**மாதிரி ஏற்றுதல் தோல்வி**
- போதுமான டிஸ்க் இடத்தை சரிபார்க்கவும்
- பதிவிறக்கங்களுக்கு இணைய இணைப்பைச் சரிபார்க்கவும்
- GPU டிரைவர்களை புதுப்பிக்கவும்
- வேறு மாதிரி மாறுபாடுகளை முயற்சிக்கவும்

**செயல்திறன் சிக்கல்கள்**
- அமைப்பு வளங்களை கண்காணிக்கவும்
- மாதிரி அமைப்புகளை சரிசெய்க
- மென்பொருள் துரிதமாக்கலை இயக்கு
- பிற வளங்களை அதிகமாக பயன்படுத்தும் பயன்பாடுகளை மூடவும்

### பிழைத்திருத்த முறை
சூழல் மாறிகளை அமைத்து பிழைத்திருத்த பதிவு செய்யவும்:
```powershell
$env:DEBUG="foundry:*"
$env:FOUNDRY_LOG_LEVEL="debug"
```

## பங்களிப்பு

### மேம்பாட்டு அமைப்பு
1. களஞ்சியத்தை கிளோன் செய்யவும்
2. ஒரு அம்ச கிளையை உருவாக்கவும்
3. சார்ந்தவற்றை நிறுவவும்: `npm install`
4. மாற்றங்களைச் செய்து சோதிக்கவும்
5. ஒரு புல் கோரிக்கையை சமர்ப்பிக்கவும்

### குறியீட்டு பாணி
- ESLint அமைப்பு வழங்கப்பட்டுள்ளது
- கோடுகளை வடிவமைக்க Prettier
- வகை பாதுகாப்புக்கு TypeScript
- ஆவணங்களுக்கு JSDoc கருத்துகள்

## கற்றல் முடிவுகள்

இந்த மாதிரியை முடித்த பிறகு, நீங்கள் புரிந்துகொள்வீர்கள்:

1. **Windows 11 இயல்பான மேம்பாடு**
   - Fluent Design System செயல்படுத்தல்
   - இயல்பான Windows ஒருங்கிணைப்பு
   - Electron பாதுகாப்பு சிறந்த நடைமுறைகள்

2. **AI மாதிரி ஒருங்கிணைப்பு**
   - Foundry Local சேவை கட்டமைப்பு
   - மாதிரி வாழ்க்கைச் சுழற்சி மேலாண்மை
   - செயல்திறன் கண்காணிப்பு மற்றும் மேம்பாடு

3. **நேரடி அரட்டை அமைப்புகள்**
   - ஸ்ட்ரீமிங் பதில்களை கையாளுதல்
   - உரையாடல் நிலை மேலாண்மை
   - பயனர் அனுபவ முறைமைகள்

4. **உற்பத்தி பயன்பாட்டு மேம்பாடு**
   - பிழை கையாளல் மற்றும் மீட்பு
   - செயல்திறன் மேம்பாடு
   - பாதுகாப்பு கருத்துக்கள்
   - சோதனை தந்திரங்கள்

## அடுத்த படிகள்

- **மாதிரி 09**: பல முகவர் ஒருங்கிணைப்பு முறைமை
- **மாதிரி 10**: Foundry Local கருவிகள் ஒருங்கிணைப்பு
- **மேம்பட்ட தலைப்புகள்**: தனிப்பயன் மாதிரி நுட்பமாக்கல்
- **வெளியீடு**: நிறுவன வெளியீட்டு முறைமைகள்

## உரிமம்

இந்த மாதிரி Microsoft Foundry Local திட்டத்தின் அதே உரிமத்தைப் பின்பற்றுகிறது.

---

**குறிப்பு**:  
இந்த ஆவணம் [Co-op Translator](https://github.com/Azure/co-op-translator) என்ற AI மொழிபெயர்ப்பு சேவையைப் பயன்படுத்தி மொழிபெயர்க்கப்பட்டுள்ளது. நாங்கள் துல்லியத்திற்காக முயற்சிக்கிறோம், ஆனால் தானியங்கி மொழிபெயர்ப்புகளில் பிழைகள் அல்லது தவறான தகவல்கள் இருக்கக்கூடும் என்பதை தயவுசெய்து கவனத்தில் கொள்ளவும். அதன் தாய்மொழியில் உள்ள மூல ஆவணம் அதிகாரப்பூர்வ ஆதாரமாக கருதப்பட வேண்டும். முக்கியமான தகவல்களுக்கு, தொழில்முறை மனித மொழிபெயர்ப்பு பரிந்துரைக்கப்படுகிறது. இந்த மொழிபெயர்ப்பைப் பயன்படுத்துவதால் ஏற்படும் எந்த தவறான புரிதல்கள் அல்லது தவறான விளக்கங்களுக்கு நாங்கள் பொறுப்பல்ல.