<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "13cb0371a2aea01d721186ced4a25e1a",
  "translation_date": "2025-09-24T21:40:23+00:00",
  "source_file": "Module08/samples/08/README.md",
  "language_code": "pa"
}
-->
# Windows 11 ਚੈਟ ਸੈਂਪਲ - Foundry Local

Windows 11 ਲਈ ਇੱਕ ਆਧੁਨਿਕ ਚੈਟ ਐਪਲੀਕੇਸ਼ਨ ਜੋ Microsoft Foundry Local ਨੂੰ ਸੁੰਦਰ ਨੈਟਿਵ ਇੰਟਰਫੇਸ ਨਾਲ ਜੋੜਦਾ ਹੈ। ਇਹ Electron ਨਾਲ ਬਣਾਇਆ ਗਿਆ ਹੈ ਅਤੇ Microsoft ਦੇ ਅਧਿਕਾਰਕ Foundry Local ਪੈਟਰਨਾਂ ਦੀ ਪਾਲਣਾ ਕਰਦਾ ਹੈ।

## ਝਲਕ

ਇਹ ਸੈਂਪਲ ਦਿਖਾਉਂਦਾ ਹੈ ਕਿ ਕਿਵੇਂ ਇੱਕ ਉਤਪਾਦਨ-ਤਿਆਰ ਚੈਟ ਐਪਲੀਕੇਸ਼ਨ ਬਣਾਈ ਜਾ ਸਕਦੀ ਹੈ ਜੋ Foundry Local ਰਾਹੀਂ ਸਥਾਨਕ AI ਮਾਡਲਾਂ ਦੀ ਵਰਤੋਂ ਕਰਦੀ ਹੈ, ਉਪਭੋਗਤਾਵਾਂ ਨੂੰ ਗੁਪਤਤਾ-ਕੇਂਦਰਤ AI ਗੱਲਬਾਤਾਂ ਪ੍ਰਦਾਨ ਕਰਦੀ ਹੈ ਬਿਨਾਂ ਕਲਾਉਡ ਨਿਰਭਰਤਾ ਦੇ।

## ਵਿਸ਼ੇਸ਼ਤਾਵਾਂ

### 🎨 **Windows 11 ਨੈਟਿਵ ਡਿਜ਼ਾਈਨ**
- Fluent Design System ਦਾ ਇੰਟੀਗ੍ਰੇਸ਼ਨ
- Mica ਮਟੀਰੀਅਲ ਪ੍ਰਭਾਵ ਅਤੇ ਪਾਰਦਰਸ਼ਤਾ
- ਨੈਟਿਵ Windows 11 ਥੀਮਿੰਗ ਸਹਾਇਤਾ
- ਸਾਰੇ ਸਕ੍ਰੀਨ ਆਕਾਰਾਂ ਲਈ ਪ੍ਰਤੀਕ੍ਰਿਆਸ਼ੀਲ ਲੇਆਉਟ
- ਡਾਰਕ/ਲਾਈਟ ਮੋਡ ਆਟੋਮੈਟਿਕ ਸਵਿੱਚਿੰਗ

### 🤖 **AI ਮਾਡਲ ਇੰਟੀਗ੍ਰੇਸ਼ਨ**
- Foundry Local ਸੇਵਾ ਇੰਟੀਗ੍ਰੇਸ਼ਨ
- ਕਈ ਮਾਡਲਾਂ ਦੀ ਸਹਾਇਤਾ ਨਾਲ ਹੌਟ-ਸਵੈਪਿੰਗ
- ਰੀਅਲ-ਟਾਈਮ ਸਟ੍ਰੀਮਿੰਗ ਜਵਾਬ
- ਸਥਾਨਕ ਅਤੇ ਕਲਾਉਡ ਮਾਡਲ ਸਵਿੱਚਿੰਗ
- ਮਾਡਲ ਹੈਲਥ ਮਾਨੀਟਰਿੰਗ ਅਤੇ ਸਥਿਤੀ

### 💬 **ਚੈਟ ਅਨੁਭਵ**
- ਰੀਅਲ-ਟਾਈਮ ਟਾਈਪਿੰਗ ਇੰਡਿਕੇਟਰ
- ਸੁਨੇਹਾ ਇਤਿਹਾਸ ਸਥਿਰਤਾ
- ਚੈਟ ਗੱਲਬਾਤਾਂ ਨੂੰ ਐਕਸਪੋਰਟ ਕਰੋ
- ਕਸਟਮ ਸਿਸਟਮ ਪ੍ਰੋਮਪਟ
- ਗੱਲਬਾਤ ਦੀ ਸ਼ਾਖਾ ਅਤੇ ਪ੍ਰਬੰਧਨ

### ⚡ **ਪ੍ਰਦਰਸ਼ਨ ਵਿਸ਼ੇਸ਼ਤਾਵਾਂ**
- ਲੇਜ਼ੀ ਲੋਡਿੰਗ ਅਤੇ ਵਰਚੁਅਲਾਈਜ਼ੇਸ਼ਨ
- ਲੰਬੀਆਂ ਗੱਲਬਾਤਾਂ ਲਈ ਅਨੁਕੂਲ ਰੇਂਡਰਿੰਗ
- ਬੈਕਗ੍ਰਾਊਂਡ ਮਾਡਲ ਪ੍ਰੀਲੋਡਿੰਗ
- ਕੁਸ਼ਲ ਮੈਮਰੀ ਪ੍ਰਬੰਧਨ
- ਸਮੂਥ ਐਨੀਮੇਸ਼ਨ ਅਤੇ ਟ੍ਰਾਂਜ਼ੀਸ਼ਨ

## ਆਰਚਿਟੈਕਚਰ

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

## ਪੂਰਵ ਸ਼ਰਤਾਂ

### ਸਿਸਟਮ ਦੀਆਂ ਲੋੜਾਂ
- **OS**: Windows 11 (22H2 ਜਾਂ ਇਸ ਤੋਂ ਬਾਅਦ ਦੀ ਸਿਫਾਰਸ਼ ਕੀਤੀ ਗਈ ਹੈ)
- **RAM**: ਘੱਟੋ-ਘੱਟ 8GB, ਵੱਡੇ ਮਾਡਲਾਂ ਲਈ 16GB+ ਦੀ ਸਿਫਾਰਸ਼ ਕੀਤੀ ਗਈ ਹੈ
- **Storage**: ਮਾਡਲਾਂ ਲਈ 10GB+ ਖਾਲੀ ਜਗ੍ਹਾ
- **GPU**: ਵਿਕਲਪਿਕ ਪਰ ਤੇਜ਼ ਇੰਫਰੈਂਸ ਲਈ ਸਿਫਾਰਸ਼ ਕੀਤੀ ਗਈ

### ਸਾਫਟਵੇਅਰ Dependencies
- **Node.js**: v18.0.0 ਜਾਂ ਇਸ ਤੋਂ ਬਾਅਦ
- **Foundry Local**: Microsoft ਤੋਂ ਨਵਾਂ ਵਰਜਨ
- **Git**: ਕਲੋਨਿੰਗ ਅਤੇ ਵਿਕਾਸ ਲਈ

## ਇੰਸਟਾਲੇਸ਼ਨ

### 1. Foundry Local ਇੰਸਟਾਲ ਕਰੋ
```powershell
# Download from GitHub releases and install
winget install Microsoft.FoundryLocal

# Verify installation
foundry --version
```

### 2. ਕਲੋਨ ਅਤੇ ਸੈਟਅੱਪ
```bash
# Navigate to sample directory
cd Module08/samples/08

# Install dependencies
npm install

# Install Electron if not global
npm install -g electron
```

### 3. ਵਾਤਾਵਰਣ ਕਨਫਿਗਰ ਕਰੋ
```powershell
# Optional: Set cloud model credentials for hybrid mode
$env:AZURE_OPENAI_KEY="your-api-key"
$env:AZURE_OPENAI_ENDPOINT="your-endpoint"
$env:AZURE_OPENAI_MODEL="gpt-4"
```

### 4. ਐਪਲੀਕੇਸ਼ਨ ਚਲਾਓ
```bash
# Development mode
npm start

# Production build
npm run build
npm run dist
```

## ਪ੍ਰੋਜੈਕਟ ਸਟ੍ਰਕਚਰ

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

## ਮੁੱਖ ਵਿਸ਼ੇਸ਼ਤਾਵਾਂ ਦੀ ਵਿਸਥਾਰ

### Windows 11 ਇੰਟੀਗ੍ਰੇਸ਼ਨ

**Fluent Design System**
- Mica ਬੈਕਗ੍ਰਾਊਂਡ ਮਟੀਰੀਅਲ
- Acrylic ਪਾਰਦਰਸ਼ਤਾ ਪ੍ਰਭਾਵ
- ਗੋਲ ਕੋਨੇ ਅਤੇ ਆਧੁਨਿਕ ਸਪੇਸਿੰਗ
- ਨੈਟਿਵ Windows 11 ਰੰਗ ਪੈਲੇਟ
- ਪਹੁੰਚਯੋਗਤਾ ਲਈ ਸੈਮੈਂਟਿਕ ਰੰਗ ਟੋਕਨ

**ਨੈਟਿਵ Windows ਵਿਸ਼ੇਸ਼ਤਾਵਾਂ**
- ਹਾਲੀਆ ਚੈਟਾਂ ਲਈ ਜੰਪ ਲਿਸਟ ਇੰਟੀਗ੍ਰੇਸ਼ਨ
- ਨਵੇਂ ਸੁਨੇਹਿਆਂ ਲਈ Windows ਨੋਟੀਫਿਕੇਸ਼ਨ
- ਮਾਡਲ ਓਪਰੇਸ਼ਨਾਂ ਲਈ ਟਾਸਕਬਾਰ ਪ੍ਰਗਤੀ
- ਸਿਸਟਮ ਟ੍ਰੇ ਇੰਟੀਗ੍ਰੇਸ਼ਨ ਨਾਲ ਤੇਜ਼ ਕਾਰਵਾਈ
- Windows Hello ਪ੍ਰਮਾਣਿਕਤਾ ਸਹਾਇਤਾ

### AI ਮਾਡਲ ਪ੍ਰਬੰਧਨ

**ਸਥਾਨਕ ਮਾਡਲ**
```javascript
// Automatic model discovery and loading
const models = await foundryManager.discoverModels();
await foundryManager.loadModel('phi-4-mini');

// Model health monitoring
const health = await foundryManager.checkHealth();
console.log(`Model Status: ${health.status}`);
console.log(`Memory Usage: ${health.memoryUsage}MB`);
```

**ਹਾਈਬ੍ਰਿਡ ਕਲਾਉਡ/ਸਥਾਨਕ ਸਹਾਇਤਾ**
```javascript
// Seamless switching between local and cloud models
if (useCloudModel) {
    await chatManager.switchToCloud('gpt-4');
} else {
    await chatManager.switchToLocal('phi-4-mini');
}
```

### ਚੈਟ ਇੰਟਰਫੇਸ ਵਿਸ਼ੇਸ਼ਤਾਵਾਂ

**ਰੀਅਲ-ਟਾਈਮ ਸਟ੍ਰੀਮਿੰਗ**
- ਟੋਕਨ-ਦਰ-ਟੋਕਨ ਜਵਾਬ ਡਿਸਪਲੇਅ
- ਸਮੂਥ ਟਾਈਪਿੰਗ ਐਨੀਮੇਸ਼ਨ
- ਰੀਕਵੇਸਟ ਰੱਦ ਕਰਨ ਯੋਗ
- ਟਾਈਪਿੰਗ ਇੰਡਿਕੇਟਰ ਅਤੇ ਸਥਿਤੀ

**ਗੱਲਬਾਤ ਪ੍ਰਬੰਧਨ**
- ਸਥਿਰ ਚੈਟ ਇਤਿਹਾਸ
- ਗੱਲਬਾਤ ਐਕਸਪੋਰਟ/ਇੰਪੋਰਟ
- ਸੁਨੇਹਾ ਖੋਜ ਅਤੇ ਫਿਲਟਰਿੰਗ
- ਗੱਲਬਾਤ ਦੀ ਸ਼ਾਖਾ
- ਹਰ ਗੱਲਬਾਤ ਲਈ ਕਸਟਮ ਸਿਸਟਮ ਪ੍ਰੋਮਪਟ

**ਪਹੁੰਚਯੋਗਤਾ**
- ਪੂਰੀ ਕੀਬੋਰਡ ਨੈਵੀਗੇਸ਼ਨ
- ਸਕ੍ਰੀਨ ਰੀਡਰ ਅਨੁਕੂਲਤਾ
- ਹਾਈ ਕਾਂਟ੍ਰਾਸਟ ਮੋਡ ਸਹਾਇਤਾ
- ਕਸਟਮਾਈਜ਼ੇਬਲ ਫੋਂਟ ਆਕਾਰ
- ਵੌਇਸ ਇਨਪੁਟ ਇੰਟੀਗ੍ਰੇਸ਼ਨ

## ਵਰਤੋਂ ਦੇ ਉਦਾਹਰਨ

### ਬੁਨਿਆਦੀ ਚੈਟ ਇੰਟੀਗ੍ਰੇਸ਼ਨ
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

### ਮਾਡਲ ਪ੍ਰਬੰਧਨ
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

### ਸੈਟਿੰਗਸ ਅਤੇ ਕਸਟਮਾਈਜ਼ੇਸ਼ਨ
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

## ਕਨਫਿਗਰੇਸ਼ਨ ਵਿਕਲਪ

### ਐਪਲੀਕੇਸ਼ਨ ਸੈਟਿੰਗਸ
- **ਥੀਮ**: ਆਟੋ, ਲਾਈਟ, ਡਾਰਕ ਮੋਡ
- **ਮਾਡਲ**: ਡਿਫਾਲਟ ਮਾਡਲ ਚੋਣ
- **ਪ੍ਰਦਰਸ਼ਨ**: ਇੰਫਰੈਂਸ ਸੈਟਿੰਗਸ
- **ਗੁਪਤਤਾ**: ਡਾਟਾ ਰਿਟੇਨਸ਼ਨ ਨੀਤੀਆਂ
- **ਨੋਟੀਫਿਕੇਸ਼ਨ**: ਸੁਨੇਹਾ ਚੇਤਾਵਨੀ
- **ਸ਼ਾਰਟਕਟ**: ਕੀਬੋਰਡ ਸ਼ਾਰਟਕਟ

### ਚੈਟ ਸੈਟਿੰਗਸ
- **ਸਟ੍ਰੀਮਿੰਗ**: ਰੀਅਲ-ਟਾਈਮ ਜਵਾਬ ਚਾਲੂ/ਬੰਦ ਕਰੋ
- **ਕੰਟੈਕਸਟ ਲੰਬਾਈ**: ਗੱਲਬਾਤ ਦੀ ਯਾਦ
- **ਟੈਂਪਰੇਚਰ**: ਜਵਾਬ ਦੀ ਰਚਨਾਤਮਕਤਾ
- **ਮੈਕਸ ਟੋਕਨ**: ਜਵਾਬ ਦੀ ਲੰਬਾਈ ਦੀ ਸੀਮਾ
- **ਸਿਸਟਮ ਪ੍ਰੋਮਪਟ**: ਡਿਫਾਲਟ ਸਹਾਇਕ ਵਿਹਾਰ

### ਮਾਡਲ ਸੈਟਿੰਗਸ
- **ਆਟੋ-ਡਾਊਨਲੋਡ**: ਆਟੋਮੈਟਿਕ ਮਾਡਲ ਅਪਡੇਟ
- **ਕੈਸ਼ ਸਾਈਜ਼**: ਸਥਾਨਕ ਮਾਡਲ ਸਟੋਰੇਜ ਸੀਮਾਵਾਂ
- **ਪ੍ਰਦਰਸ਼ਨ ਮੋਡ**: CPU ਵਿਰੁੱਧ GPU ਪਸੰਦ
- **ਹੈਲਥ ਚੈਕਸ**: ਮਾਨੀਟਰਿੰਗ ਅੰਤਰਾਲ

## ਵਿਕਾਸ

### ਸਰੋਤ ਤੋਂ ਬਣਾਉਣਾ
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

### ਡੀਬੱਗਿੰਗ
```bash
# Enable debug mode
set DEBUG=foundry-chat:*
npm start

# View developer tools
# Press F12 in the application
```

### ਟੈਸਟਿੰਗ
```bash
# Run unit tests
npm test

# Run integration tests
npm run test:integration

# Run end-to-end tests
npm run test:e2e
```

## ਪ੍ਰਦਰਸ਼ਨ ਅਨੁਕੂਲਤਾ

### ਮੈਮਰੀ ਪ੍ਰਬੰਧਨ
- ਸੁਨੇਹਾ ਵਰਚੁਅਲਾਈਜ਼ੇਸ਼ਨ ਦੀ ਕੁਸ਼ਲਤਾ
- ਆਟੋਮੈਟਿਕ ਗਾਰਬੇਜ ਕਲੇਕਸ਼ਨ
- ਮਾਡਲ ਮੈਮਰੀ ਮਾਨੀਟਰਿੰਗ
- ਬੰਦ ਕਰਨ 'ਤੇ ਸਰੋਤ ਸਾਫ਼

### ਰੇਂਡਰਿੰਗ ਅਨੁਕੂਲਤਾ
- ਲੰਬੀਆਂ ਗੱਲਬਾਤਾਂ ਲਈ ਵਰਚੁਅਲ ਸਕ੍ਰੋਲਿੰਗ
- ਸੁਨੇਹਾ ਇਤਿਹਾਸ ਦੀ ਲੇਜ਼ੀ ਲੋਡਿੰਗ
- React/DOM ਅਪਡੇਟਾਂ ਦੀ ਅਨੁਕੂਲਤਾ
- GPU-ਐਕਸਲੇਰੇਟਡ ਐਨੀਮੇਸ਼ਨ

### ਨੈਟਵਰਕ ਅਨੁਕੂਲਤਾ
- ਕਨੈਕਸ਼ਨ ਪੂਲਿੰਗ
- ਰੀਕਵੇਸਟ ਬੈਚਿੰਗ
- ਆਟੋਮੈਟਿਕ ਰੀਟ੍ਰਾਈ ਲੌਜਿਕ
- ਆਫਲਾਈਨ ਮੋਡ ਸਹਾਇਤਾ

## ਸੁਰੱਖਿਆ ਵਿਚਾਰ

### ਡਾਟਾ ਗੁਪਤਤਾ
- ਸਥਾਨਕ-ਪਹਿਲਾਂ ਆਰਚਿਟੈਕਚਰ
- ਕੋਈ ਕਲਾਉਡ ਡਾਟਾ ਟ੍ਰਾਂਸਮਿਸ਼ਨ (ਸਥਾਨਕ ਮੋਡ)
- ਗੱਲਬਾਤ ਸਟੋਰੇਜ ਨੂੰ ਇਨਕ੍ਰਿਪਟ ਕੀਤਾ
- ਸੁਰੱਖਿਅਤ ਪ੍ਰਮਾਣ ਪੱਤਰ ਪ੍ਰਬੰਧਨ

### ਐਪਲੀਕੇਸ਼ਨ ਸੁਰੱਖਿਆ
- ਸੈਂਡਬਾਕਸਡ ਰੇਂਡਰਰ ਪ੍ਰੋਸੈਸ
- Content Security Policy (CSP)
- ਕੋਈ ਰਿਮੋਟ ਕੋਡ ਐਗਜ਼ਿਕਿਊਸ਼ਨ ਨਹੀਂ
- ਸੁਰੱਖਿਅਤ IPC ਸੰਚਾਰ

## ਸਮੱਸਿਆ ਹੱਲ

### ਆਮ ਸਮੱਸਿਆਵਾਂ

**Foundry Local ਸ਼ੁਰੂ ਨਹੀਂ ਹੋ ਰਿਹਾ**
```powershell
# Check service status
foundry status

# Restart service
foundry restart

# Check logs
foundry logs
```

**ਮਾਡਲ ਲੋਡ ਕਰਨ ਦੀਆਂ ਗਲਤੀਆਂ**
- ਯਕੀਨੀ ਬਣਾਓ ਕਿ ਕਾਫ਼ੀ ਡਿਸਕ ਸਪੇਸ ਹੈ
- ਡਾਊਨਲੋਡ ਲਈ ਇੰਟਰਨੈਟ ਕਨੈਕਸ਼ਨ ਚੈੱਕ ਕਰੋ
- GPU ਡਰਾਈਵਰ ਅਪਡੇਟ ਕੀਤੇ ਹਨ ਜਾਂ ਨਹੀਂ
- ਵੱਖਰੇ ਮਾਡਲ ਵੈਰੀਐਂਟਸ ਦੀ ਕੋਸ਼ਿਸ਼ ਕਰੋ

**ਪ੍ਰਦਰਸ਼ਨ ਸਮੱਸਿਆਵਾਂ**
- ਸਿਸਟਮ ਸਰੋਤਾਂ ਦੀ ਮਾਨੀਟਰਿੰਗ ਕਰੋ
- ਮਾਡਲ ਸੈਟਿੰਗਸ ਨੂੰ ਅਨੁਕੂਲ ਕਰੋ
- ਹਾਰਡਵੇਅਰ ਐਕਸਲੇਰੇਸ਼ਨ ਚਾਲੂ ਕਰੋ
- ਹੋਰ ਸਰੋਤ-ਗ੍ਰਾਹਕ ਐਪਲੀਕੇਸ਼ਨ ਬੰਦ ਕਰੋ

### ਡੀਬੱਗ ਮੋਡ
ਵਾਤਾਵਰਣ ਵੈਰੀਏਬਲ ਸੈਟ ਕਰਕੇ ਡੀਬੱਗ ਲੌਗਿੰਗ ਚਾਲੂ ਕਰੋ:
```powershell
$env:DEBUG="foundry:*"
$env:FOUNDRY_LOG_LEVEL="debug"
```

## ਯੋਗਦਾਨ

### ਵਿਕਾਸ ਸੈਟਅੱਪ
1. ਰਿਪੋਜ਼ਟਰੀ ਨੂੰ ਫੋਰਕ ਕਰੋ
2. ਇੱਕ ਫੀਚਰ ਬ੍ਰਾਂਚ ਬਣਾਓ
3. Dependencies ਇੰਸਟਾਲ ਕਰੋ: `npm install`
4. ਬਦਲਾਅ ਕਰੋ ਅਤੇ ਟੈਸਟ ਕਰੋ
5. ਇੱਕ ਪੁਲ ਰਿਕਵੇਸਟ ਸਬਮਿਟ ਕਰੋ

### ਕੋਡ ਸ਼ੈਲੀ
- ESLint ਕਨਫਿਗਰੇਸ਼ਨ ਪ੍ਰਦਾਨ ਕੀਤਾ ਗਿਆ
- Prettier ਕੋਡ ਫਾਰਮੈਟਿੰਗ ਲਈ
- TypeScript ਟਾਈਪ ਸੇਫਟੀ ਲਈ
- JSDoc ਟਿੱਪਣੀਆਂ ਦਸਤਾਵੇਜ਼ ਲਈ

## ਸਿੱਖਣ ਦੇ ਨਤੀਜੇ

ਇਹ ਸੈਂਪਲ ਪੂਰਾ ਕਰਨ ਤੋਂ ਬਾਅਦ, ਤੁਸੀਂ ਸਮਝ ਜਾਵੋਗੇ:

1. **Windows 11 ਨੈਟਿਵ ਵਿਕਾਸ**
   - Fluent Design System ਦੀ ਅਮਲਵਾਰੀ
   - ਨੈਟਿਵ Windows ਇੰਟੀਗ੍ਰੇਸ਼ਨ
   - Electron ਸੁਰੱਖਿਆ ਦੇ ਸ੍ਰੇਸ਼ਠ ਅਭਿਆਸ

2. **AI ਮਾਡਲ ਇੰਟੀਗ੍ਰੇਸ਼ਨ**
   - Foundry Local ਸੇਵਾ ਆਰਚਿਟੈਕਚਰ
   - ਮਾਡਲ ਲਾਈਫਸਾਈਕਲ ਪ੍ਰਬੰਧਨ
   - ਪ੍ਰਦਰਸ਼ਨ ਮਾਨੀਟਰਿੰਗ ਅਤੇ ਅਨੁਕੂਲਤਾ

3. **ਰੀਅਲ-ਟਾਈਮ ਚੈਟ ਸਿਸਟਮ**
   - ਸਟ੍ਰੀਮਿੰਗ ਜਵਾਬ ਸੰਭਾਲ
   - ਗੱਲਬਾਤ ਦੀ ਸਥਿਤੀ ਪ੍ਰਬੰਧਨ
   - ਉਪਭੋਗਤਾ ਅਨੁਭਵ ਪੈਟਰਨ

4. **ਉਤਪਾਦਨ ਐਪਲੀਕੇਸ਼ਨ ਵਿਕਾਸ**
   - ਗਲਤੀ ਸੰਭਾਲ ਅਤੇ ਬਹਾਲੀ
   - ਪ੍ਰਦਰਸ਼ਨ ਅਨੁਕੂਲਤਾ
   - ਸੁਰੱਖਿਆ ਵਿਚਾਰ
   - ਟੈਸਟਿੰਗ ਰਣਨੀਤੀਆਂ

## ਅਗਲੇ ਕਦਮ

- **ਸੈਂਪਲ 09**: ਮਲਟੀ-ਏਜੰਟ ਓਰਕੇਸਟ੍ਰੇਸ਼ਨ ਸਿਸਟਮ
- **ਸੈਂਪਲ 10**: Foundry Local ਨੂੰ ਟੂਲਜ਼ ਇੰਟੀਗ੍ਰੇਸ਼ਨ ਵਜੋਂ
- **ਉੱਚਤ ਵਿਸ਼ੇ**: ਕਸਟਮ ਮਾਡਲ ਫਾਈਨ-ਟਿਊਨਿੰਗ
- **ਡਿਪਲੌਇਮੈਂਟ**: ਇੰਟਰਪ੍ਰਾਈਜ਼ ਡਿਪਲੌਇਮੈਂਟ ਪੈਟਰਨ

## ਲਾਇਸੰਸ

ਇਹ ਸੈਂਪਲ Microsoft Foundry Local ਪ੍ਰੋਜੈਕਟ ਦੇ ਸਮਾਨ ਲਾਇਸੰਸ ਦੀ ਪਾਲਣਾ ਕਰਦਾ ਹੈ।

---

