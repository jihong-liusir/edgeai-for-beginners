<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "13cb0371a2aea01d721186ced4a25e1a",
  "translation_date": "2025-09-25T02:49:53+00:00",
  "source_file": "Module08/samples/08/README.md",
  "language_code": "bg"
}
-->
# Windows 11 Chat Sample - Foundry Local

Модерно приложение за чат за Windows 11, което интегрира Microsoft Foundry Local с красив и естествен интерфейс. Изградено с Electron и следвайки официалните модели на Microsoft Foundry Local.

## Преглед

Този пример демонстрира как да създадете готово за производство приложение за чат, което използва локални AI модели чрез Foundry Local, предоставяйки на потребителите AI разговори с фокус върху поверителността без зависимост от облака.

## Характеристики

### 🎨 **Нативен дизайн за Windows 11**
- Интеграция с Fluent Design System
- Ефекти на материала Mica и прозрачност
- Поддръжка на нативна тематика за Windows 11
- Отзивчив дизайн за всички размери на екрана
- Автоматично превключване между тъмен/светъл режим

### 🤖 **Интеграция на AI модели**
- Интеграция с услугата Foundry Local
- Поддръжка на множество модели с бързо превключване
- Отговори в реално време
- Превключване между локални и облачни модели
- Мониторинг на здравето и състоянието на модела

### 💬 **Чат изживяване**
- Индикатори за писане в реално време
- Запазване на историята на съобщенията
- Експорт на чат разговори
- Персонализирани системни подсказки
- Управление и разклоняване на разговори

### ⚡ **Функции за производителност**
- Мързеливо зареждане и виртуализация
- Оптимизирано рендиране за дълги разговори
- Предварително зареждане на модели във фонов режим
- Ефективно управление на паметта
- Гладки анимации и преходи

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

## Предпоставки

### Системни изисквания
- **ОС**: Windows 11 (22H2 или по-нова версия препоръчителна)
- **RAM**: Минимум 8GB, препоръчително 16GB+ за по-големи модели
- **Съхранение**: 10GB+ свободно пространство за модели
- **GPU**: Опционално, но препоръчително за по-бърза обработка

### Софтуерни зависимости
- **Node.js**: v18.0.0 или по-нова версия
- **Foundry Local**: Най-новата версия от Microsoft
- **Git**: За клониране и разработка

## Инсталация

### 1. Инсталирайте Foundry Local
```powershell
# Download from GitHub releases and install
winget install Microsoft.FoundryLocal

# Verify installation
foundry --version
```

### 2. Клониране и настройка
```bash
# Navigate to sample directory
cd Module08/samples/08

# Install dependencies
npm install

# Install Electron if not global
npm install -g electron
```

### 3. Конфигурирайте средата
```powershell
# Optional: Set cloud model credentials for hybrid mode
$env:AZURE_OPENAI_KEY="your-api-key"
$env:AZURE_OPENAI_ENDPOINT="your-endpoint"
$env:AZURE_OPENAI_MODEL="gpt-4"
```

### 4. Стартирайте приложението
```bash
# Development mode
npm start

# Production build
npm run build
npm run dist
```

## Структура на проекта

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

## Подробен преглед на ключовите функции

### Интеграция с Windows 11

**Fluent Design System**
- Материали с фон Mica
- Ефекти на прозрачност с Acrylic
- Заоблени ъгли и модерен дизайн
- Нативна цветова палитра за Windows 11
- Семантични цветови токени за достъпност

**Нативни функции на Windows**
- Интеграция на списък за скорошни чатове
- Уведомления за нови съобщения
- Прогрес на задачите за операции с модели
- Интеграция с системната лента с бързи действия
- Поддръжка на Windows Hello за удостоверяване

### Управление на AI модели

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

**Хибридна поддръжка облак/локално**
```javascript
// Seamless switching between local and cloud models
if (useCloudModel) {
    await chatManager.switchToCloud('gpt-4');
} else {
    await chatManager.switchToLocal('phi-4-mini');
}
```

### Функции на интерфейса за чат

**Поточно предаване в реално време**
- Показване на отговори токен по токен
- Гладки анимации за писане
- Отменяеми заявки
- Индикатори за писане и статус

**Управление на разговори**
- Запазване на историята на чата
- Експорт/импорт на разговори
- Търсене и филтриране на съобщения
- Разклоняване на разговори
- Персонализирани системни подсказки за всеки разговор

**Достъпност**
- Пълна навигация с клавиатура
- Съвместимост с екранни четци
- Поддръжка на режим с висок контраст
- Персонализируеми размери на шрифта
- Интеграция на гласов вход

## Примери за употреба

### Основна интеграция на чат
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

### Управление на модели
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

### Настройки и персонализация
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

## Опции за конфигурация

### Настройки на приложението
- **Тема**: Автоматичен, светъл, тъмен режим
- **Модел**: Избор на модел по подразбиране
- **Производителност**: Настройки за обработка
- **Поверителност**: Политики за запазване на данни
- **Уведомления**: Известия за съобщения
- **Пряк път**: Клавишни комбинации

### Настройки на чата
- **Поточно предаване**: Включване/изключване на отговори в реално време
- **Дължина на контекста**: Памет на разговора
- **Температура**: Креативност на отговорите
- **Максимални токени**: Ограничения за дължина на отговорите
- **Системни подсказки**: Поведение на асистента по подразбиране

### Настройки на модела
- **Автоматично изтегляне**: Автоматични актуализации на модела
- **Размер на кеша**: Ограничения за локално съхранение на модели
- **Режим на производителност**: Предпочитания за CPU срещу GPU
- **Проверки на здравето**: Интервали за мониторинг

## Разработка

### Създаване от източника
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

### Отстраняване на грешки
```bash
# Enable debug mode
set DEBUG=foundry-chat:*
npm start

# View developer tools
# Press F12 in the application
```

### Тестване
```bash
# Run unit tests
npm test

# Run integration tests
npm run test:integration

# Run end-to-end tests
npm run test:e2e
```

## Оптимизация на производителността

### Управление на паметта
- Ефективна виртуализация на съобщенията
- Автоматично събиране на боклука
- Мониторинг на паметта на модела
- Почистване на ресурси при изход

### Оптимизация на рендирането
- Виртуално превъртане за дълги разговори
- Мързеливо зареждане на историята на съобщенията
- Оптимизирани актуализации на React/DOM
- Анимации, ускорени от GPU

### Оптимизация на мрежата
- Обединяване на връзки
- Групиране на заявки
- Логика за автоматично повторение
- Поддръжка на офлайн режим

## Съображения за сигурност

### Поверителност на данните
- Архитектура с локален приоритет
- Без предаване на данни към облака (локален режим)
- Шифровано съхранение на разговори
- Сигурно управление на идентификационни данни

### Сигурност на приложението
- Процеси на рендериране в пясъчник
- Политика за сигурност на съдържанието (CSP)
- Без изпълнение на отдалечен код
- Сигурна IPC комуникация

## Отстраняване на проблеми

### Често срещани проблеми

**Foundry Local не стартира**
```powershell
# Check service status
foundry status

# Restart service
foundry restart

# Check logs
foundry logs
```

**Неуспехи при зареждане на модели**
- Проверете достатъчното дисково пространство
- Проверете интернет връзката за изтегляния
- Уверете се, че драйверите на GPU са актуализирани
- Опитайте различни варианти на модела

**Проблеми с производителността**
- Мониторинг на системните ресурси
- Настройка на параметрите на модела
- Включване на хардуерно ускорение
- Затваряне на други приложения, които използват много ресурси

### Режим за отстраняване на грешки
Активирайте регистриране на грешки, като зададете променливи на средата:
```powershell
$env:DEBUG="foundry:*"
$env:FOUNDRY_LOG_LEVEL="debug"
```

## Принос

### Настройка за разработка
1. Направете форк на хранилището
2. Създайте клон за функции
3. Инсталирайте зависимости: `npm install`
4. Направете промени и тествайте
5. Изпратете pull request

### Стил на кода
- Предоставена конфигурация за ESLint
- Prettier за форматиране на кода
- TypeScript за безопасност на типовете
- JSDoc коментари за документация

## Резултати от обучението

След завършване на този пример ще разберете:

1. **Нативна разработка за Windows 11**
   - Имплементация на Fluent Design System
   - Нативна интеграция с Windows
   - Най-добри практики за сигурност с Electron

2. **Интеграция на AI модели**
   - Архитектура на услугата Foundry Local
   - Управление на жизнения цикъл на модела
   - Мониторинг и оптимизация на производителността

3. **Системи за чат в реално време**
   - Обработка на поточни отговори
   - Управление на състоянието на разговорите
   - Модели за потребителско изживяване

4. **Разработка на приложения за производство**
   - Обработка на грешки и възстановяване
   - Оптимизация на производителността
   - Съображения за сигурност
   - Стратегии за тестване

## Следващи стъпки

- **Пример 09**: Система за оркестрация на множество агенти
- **Пример 10**: Foundry Local като интеграция на инструменти
- **Разширени теми**: Персонализирано обучение на модели
- **Деплоймент**: Модели за внедряване в предприятия

## Лиценз

Този пример следва същия лиценз като проекта Microsoft Foundry Local.

---

