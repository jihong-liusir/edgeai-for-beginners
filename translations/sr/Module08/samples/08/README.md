<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "13cb0371a2aea01d721186ced4a25e1a",
  "translation_date": "2025-09-25T02:50:18+00:00",
  "source_file": "Module08/samples/08/README.md",
  "language_code": "sr"
}
-->
# Windows 11 Chat Sample - Foundry Local

Модерна апликација за ћаскање за Windows 11 која интегрише Microsoft Foundry Local са прелепим, природним интерфејсом. Направљена уз помоћ Electron-а и у складу са званичним Microsoft Foundry Local шаблонима.

## Преглед

Овај пример показује како направити апликацију за ћаскање спремну за производњу, која користи локалне AI моделе преко Foundry Local-а, омогућавајући корисницима приватне AI разговоре без зависности од облака.

## Карактеристике

### 🎨 **Природни дизајн за Windows 11**
- Интеграција Fluent Design System-а
- Ефекти материјала Mica и транспарентност
- Подршка за природно теме Windows 11
- Прилагодљив распоред за све величине екрана
- Аутоматско пребацивање између тамног и светлог режима

### 🤖 **Интеграција AI модела**
- Интеграција Foundry Local сервиса
- Подршка за више модела са брзим пребацивањем
- Одговори у реалном времену
- Пребацивање између локалних и облачних модела
- Праћење здравља модела и статус

### 💬 **Искуство ћаскања**
- Индикатори куцања у реалном времену
- Чување историје порука
- Извоз разговора
- Прилагођени системски упити
- Управљање и разгранавање разговора

### ⚡ **Карактеристике перформанси**
- Лено учитавање и виртуализација
- Оптимизовано рендеровање за дуге разговоре
- Предучитавање модела у позадини
- Ефикасно управљање меморијом
- Глатке анимације и прелази

## Архитектура

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

## Предуслови

### Системски захтеви
- **ОС**: Windows 11 (препоручено 22H2 или новије)
- **РАМ**: Минимум 8GB, препоручено 16GB+ за веће моделе
- **Складиште**: 10GB+ слободног простора за моделе
- **GPU**: Опционо, али препоручено за бржу обраду

### Софтверске зависности
- **Node.js**: v18.0.0 или новије
- **Foundry Local**: Најновија верзија од Microsoft-а
- **Git**: За клонирање и развој

## Инсталација

### 1. Инсталирајте Foundry Local
```powershell
# Download from GitHub releases and install
winget install Microsoft.FoundryLocal

# Verify installation
foundry --version
```

### 2. Клонирајте и подесите
```bash
# Navigate to sample directory
cd Module08/samples/08

# Install dependencies
npm install

# Install Electron if not global
npm install -g electron
```

### 3. Конфигуришите окружење
```powershell
# Optional: Set cloud model credentials for hybrid mode
$env:AZURE_OPENAI_KEY="your-api-key"
$env:AZURE_OPENAI_ENDPOINT="your-endpoint"
$env:AZURE_OPENAI_MODEL="gpt-4"
```

### 4. Покрените апликацију
```bash
# Development mode
npm start

# Production build
npm run build
npm run dist
```

## Структура пројекта

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

## Детаљан преглед кључних карактеристика

### Интеграција са Windows 11

**Fluent Design System**
- Мика материјали у позадини
- Ефекти акрилне транспарентности
- Заобљени углови и модеран размак
- Природна палета боја Windows 11
- Семантички колор токени за приступачност

**Природне функције Windows-а**
- Интеграција Jump листе за недавне разговоре
- Windows обавештења за нове поруке
- Напредак на траци задатака за операције модела
- Интеграција системске траке са брзим акцијама
- Подршка за Windows Hello аутентификацију

### Управљање AI моделима

**Локални модели**
```javascript
// Automatic model discovery and loading
const models = await foundryManager.discoverModels();
await foundryManager.loadModel('phi-4-mini');

// Model health monitoring
const health = await foundryManager.checkHealth();
console.log(`Model Status: ${health.status}`);
console.log(`Memory Usage: ${health.memoryUsage}MB`);
```

**Хибридна подршка за облак/локал**
```javascript
// Seamless switching between local and cloud models
if (useCloudModel) {
    await chatManager.switchToCloud('gpt-4');
} else {
    await chatManager.switchToLocal('phi-4-mini');
}
```

### Карактеристике интерфејса за ћаскање

**Стриминг у реалном времену**
- Приказ одговора токен по токен
- Глатке анимације куцања
- Захтеви који се могу отказати
- Индикатори куцања и статус

**Управљање разговорима**
- Чување историје ћаскања
- Извоз/увоз разговора
- Претрага и филтрирање порука
- Разгранавање разговора
- Прилагођени системски упити за сваки разговор

**Приступачност**
- Потпуна навигација преко тастатуре
- Компатибилност са читачем екрана
- Подршка за режим високог контраста
- Прилагодљиве величине фонта
- Интеграција гласовног уноса

## Примери употребе

### Основна интеграција ћаскања
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

### Управљање моделима
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

### Подешавања и прилагођавање
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

## Опције конфигурације

### Подешавања апликације
- **Тема**: Аутоматски, светли, тамни режим
- **Модел**: Подразумевани избор модела
- **Перформансе**: Подешавања обраде
- **Приватност**: Политике задржавања података
- **Обавештења**: Алерти за поруке
- **Пречице**: Пречице на тастатури

### Подешавања ћаскања
- **Стриминг**: Омогућавање/онемогућавање одговора у реалном времену
- **Дужина контекста**: Меморија разговора
- **Температура**: Креативност одговора
- **Максимални токени**: Ограничења дужине одговора
- **Системски упити**: Подразумевано понашање асистента

### Подешавања модела
- **Аутоматско преузимање**: Аутоматска ажурирања модела
- **Величина кеша**: Ограничења локалног складишта модела
- **Режим перформанси**: Преференције за CPU или GPU
- **Провере здравља**: Интервали праћења

## Развој

### Изградња из извора
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

### Дебаговање
```bash
# Enable debug mode
set DEBUG=foundry-chat:*
npm start

# View developer tools
# Press F12 in the application
```

### Тестирање
```bash
# Run unit tests
npm test

# Run integration tests
npm run test:integration

# Run end-to-end tests
npm run test:e2e
```

## Оптимизација перформанси

### Управљање меморијом
- Ефикасна виртуализација порука
- Аутоматско сакупљање смећа
- Праћење меморије модела
- Чишћење ресурса при изласку

### Оптимизација рендеровања
- Виртуално скроловање за дуге разговоре
- Лено учитавање историје порука
- Оптимизована ажурирања React/DOM-а
- Анимације убрзане преко GPU-а

### Оптимизација мреже
- Удруживање веза
- Груписање захтева
- Аутоматска логика поновног покушаја
- Подршка за офлајн режим

## Безбедносни аспекти

### Приватност података
- Архитектура која прво користи локалне ресурсе
- Нема преноса података у облак (локални режим)
- Шифровано складиштење разговора
- Сигурно управљање акредитивима

### Безбедност апликације
- Процеси рендеровања у песковнику
- Политика безбедности садржаја (CSP)
- Нема извршавања удаљеног кода
- Сигурна IPC комуникација

## Решавање проблема

### Уобичајени проблеми

**Foundry Local се не покреће**
```powershell
# Check service status
foundry status

# Restart service
foundry restart

# Check logs
foundry logs
```

**Неуспеси у учитавању модела**
- Проверите да ли има довољно простора на диску
- Проверите интернет конекцију за преузимања
- Уверите се да су GPU драјвери ажурирани
- Пробајте различите варијанте модела

**Проблеми са перформансама**
- Пратите системске ресурсе
- Прилагодите подешавања модела
- Омогућите хардверско убрзање
- Затворите друге апликације које троше ресурсе

### Режим дебаговања
Омогућите дебаговање постављањем променљивих окружења:
```powershell
$env:DEBUG="foundry:*"
$env:FOUNDRY_LOG_LEVEL="debug"
```

## Допринос

### Подешавање за развој
1. Форкујте репозиторијум
2. Направите грану за функцију
3. Инсталирајте зависности: `npm install`
4. Направите измене и тестирајте
5. Пошаљите pull request

### Стил кода
- Пружена ESLint конфигурација
- Prettier за форматирање кода
- TypeScript за сигурност типова
- JSDoc коментари за документацију

## Исходи учења

Након завршетка овог примера, разумећете:

1. **Природни развој за Windows 11**
   - Имплементацију Fluent Design System-а
   - Интеграцију са Windows-ом
   - Најбоље праксе за безбедност у Electron-у

2. **Интеграцију AI модела**
   - Архитектуру Foundry Local сервиса
   - Управљање животним циклусом модела
   - Праћење и оптимизацију перформанси

3. **Системе за ћаскање у реалном времену**
   - Обраду одговора у стримингу
   - Управљање стањем разговора
   - Шаблоне корисничког искуства

4. **Развој апликација за производњу**
   - Руковање грешкама и опоравак
   - Оптимизацију перформанси
   - Безбедносне аспекте
   - Стратегије тестирања

## Следећи кораци

- **Пример 09**: Систем за оркестрацију више агената
- **Пример 10**: Foundry Local као интеграција алата
- **Напредне теме**: Прилагођено фино подешавање модела
- **Дистрибуција**: Шаблони за дистрибуцију у предузећима

## Лиценца

Овај пример следи исту лиценцу као и пројекат Microsoft Foundry Local.

---

