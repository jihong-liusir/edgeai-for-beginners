<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "13cb0371a2aea01d721186ced4a25e1a",
  "translation_date": "2025-09-25T02:51:59+00:00",
  "source_file": "Module08/samples/08/README.md",
  "language_code": "uk"
}
-->
# Windows 11 Chat Sample - Foundry Local

Сучасний чат-додаток для Windows 11, який інтегрує Microsoft Foundry Local з красивим нативним інтерфейсом. Побудований на Electron і відповідає офіційним шаблонам Foundry Local від Microsoft.

## Огляд

Цей приклад демонструє, як створити готовий до використання чат-додаток, який використовує локальні AI-моделі через Foundry Local, забезпечуючи користувачам конфіденційні AI-розмови без залежності від хмарних сервісів.

## Особливості

### 🎨 **Нативний дизайн Windows 11**
- Інтеграція Fluent Design System
- Ефекти матеріалу Mica та прозорість
- Підтримка нативного темування Windows 11
- Адаптивний макет для всіх розмірів екранів
- Автоматичне перемикання між темним і світлим режимами

### 🤖 **Інтеграція AI-моделей**
- Інтеграція сервісу Foundry Local
- Підтримка кількох моделей із можливістю швидкого перемикання
- Потокові відповіді в реальному часі
- Перемикання між локальними та хмарними моделями
- Моніторинг стану моделей

### 💬 **Чат-досвід**
- Індикатори набору тексту в реальному часі
- Збереження історії повідомлень
- Експорт чат-розмов
- Кастомні системні підказки
- Розгалуження та управління розмовами

### ⚡ **Особливості продуктивності**
- Ледаче завантаження та віртуалізація
- Оптимізоване рендеринг для довгих розмов
- Попереднє завантаження моделей у фоновому режимі
- Ефективне управління пам'яттю
- Плавні анімації та переходи

## Архітектура

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

## Попередні вимоги

### Системні вимоги
- **ОС**: Windows 11 (рекомендується версія 22H2 або новіша)
- **ОЗП**: мінімум 8 ГБ, рекомендується 16 ГБ+ для більших моделей
- **Сховище**: 10 ГБ+ вільного місця для моделей
- **GPU**: необов'язково, але рекомендується для швидшого виконання

### Програмні залежності
- **Node.js**: версія 18.0.0 або новіша
- **Foundry Local**: остання версія від Microsoft
- **Git**: для клонування та розробки

## Встановлення

### 1. Встановіть Foundry Local
```powershell
# Download from GitHub releases and install
winget install Microsoft.FoundryLocal

# Verify installation
foundry --version
```

### 2. Клонування та налаштування
```bash
# Navigate to sample directory
cd Module08/samples/08

# Install dependencies
npm install

# Install Electron if not global
npm install -g electron
```

### 3. Налаштування середовища
```powershell
# Optional: Set cloud model credentials for hybrid mode
$env:AZURE_OPENAI_KEY="your-api-key"
$env:AZURE_OPENAI_ENDPOINT="your-endpoint"
$env:AZURE_OPENAI_MODEL="gpt-4"
```

### 4. Запуск додатку
```bash
# Development mode
npm start

# Production build
npm run build
npm run dist
```

## Структура проекту

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

## Детальний огляд ключових функцій

### Інтеграція Windows 11

**Fluent Design System**
- Матеріали Mica для фону
- Ефекти прозорості Acrylic
- Закруглені кути та сучасні відступи
- Нативна палітра кольорів Windows 11
- Семантичні кольорові токени для доступності

**Нативні функції Windows**
- Інтеграція списку переходів для останніх чатів
- Сповіщення Windows про нові повідомлення
- Прогрес у панелі завдань для операцій з моделями
- Інтеграція системного трея з швидкими діями
- Підтримка аутентифікації Windows Hello

### Управління AI-моделями

**Локальні моделі**
```javascript
// Automatic model discovery and loading
const models = await foundryManager.discoverModels();
await foundryManager.loadModel('phi-4-mini');

// Model health monitoring
const health = await foundryManager.checkHealth();
console.log(`Model Status: ${health.status}`);
console.log(`Memory Usage: ${health.memoryUsage}MB`);
```

**Гібридна підтримка хмари/локальних моделей**
```javascript
// Seamless switching between local and cloud models
if (useCloudModel) {
    await chatManager.switchToCloud('gpt-4');
} else {
    await chatManager.switchToLocal('phi-4-mini');
}
```

### Особливості інтерфейсу чату

**Потокова передача в реальному часі**
- Відображення відповіді токен за токеном
- Плавні анімації набору тексту
- Можливість скасування запитів
- Індикатори набору тексту та статусу

**Управління розмовами**
- Збереження історії чатів
- Експорт/імпорт розмов
- Пошук і фільтрація повідомлень
- Розгалуження розмов
- Кастомні системні підказки для кожної розмови

**Доступність**
- Повна навігація за допомогою клавіатури
- Сумісність із екранними читачами
- Підтримка режиму високої контрастності
- Налаштування розміру шрифтів
- Інтеграція голосового введення

## Приклади використання

### Базова інтеграція чату
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

### Управління моделями
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

### Налаштування та кастомізація
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

## Опції конфігурації

### Налаштування додатку
- **Тема**: Авто, Світлий, Темний режим
- **Модель**: Вибір моделі за замовчуванням
- **Продуктивність**: Налаштування виконання
- **Конфіденційність**: Політики збереження даних
- **Сповіщення**: Оповіщення про повідомлення
- **Швидкі клавіші**: Гарячі клавіші

### Налаштування чату
- **Потокова передача**: Увімкнення/вимкнення відповідей у реальному часі
- **Довжина контексту**: Пам'ять розмови
- **Температура**: Креативність відповідей
- **Максимальна кількість токенів**: Обмеження довжини відповіді
- **Системні підказки**: Поведінка асистента за замовчуванням

### Налаштування моделі
- **Автоматичне завантаження**: Автоматичне оновлення моделей
- **Розмір кешу**: Ліміти локального сховища моделей
- **Режим продуктивності**: Налаштування CPU або GPU
- **Перевірка стану**: Інтервали моніторингу

## Розробка

### Збірка з вихідного коду
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

### Налагодження
```bash
# Enable debug mode
set DEBUG=foundry-chat:*
npm start

# View developer tools
# Press F12 in the application
```

### Тестування
```bash
# Run unit tests
npm test

# Run integration tests
npm run test:integration

# Run end-to-end tests
npm run test:e2e
```

## Оптимізація продуктивності

### Управління пам'яттю
- Ефективна віртуалізація повідомлень
- Автоматичне збирання сміття
- Моніторинг пам'яті моделей
- Очищення ресурсів при виході

### Оптимізація рендерингу
- Віртуальне прокручування для довгих розмов
- Ледаче завантаження історії повідомлень
- Оптимізовані оновлення React/DOM
- Анімації з прискоренням GPU

### Оптимізація мережі
- Пулінг з'єднань
- Пакетна обробка запитів
- Автоматична логіка повторних спроб
- Підтримка офлайн-режиму

## Міркування щодо безпеки

### Конфіденційність даних
- Архітектура з локальним пріоритетом
- Відсутність передачі даних у хмару (локальний режим)
- Зашифроване збереження розмов
- Безпечне управління обліковими даними

### Безпека додатку
- Пісочниця для процесів рендерингу
- Політика безпеки контенту (CSP)
- Відсутність виконання віддаленого коду
- Безпечна IPC-комунікація

## Вирішення проблем

### Поширені проблеми

**Foundry Local не запускається**
```powershell
# Check service status
foundry status

# Restart service
foundry restart

# Check logs
foundry logs
```

**Помилки завантаження моделей**
- Перевірте достатній обсяг дискового простору
- Переконайтеся, що є інтернет-з'єднання для завантажень
- Перевірте оновлення драйверів GPU
- Спробуйте інші варіанти моделей

**Проблеми продуктивності**
- Моніторинг системних ресурсів
- Налаштування параметрів моделі
- Увімкнення апаратного прискорення
- Закриття інших ресурсомістких додатків

### Режим налагодження
Увімкніть журнал налагодження, встановивши змінні середовища:
```powershell
$env:DEBUG="foundry:*"
$env:FOUNDRY_LOG_LEVEL="debug"
```

## Внесок у проект

### Налаштування для розробки
1. Форкніть репозиторій
2. Створіть гілку для функції
3. Встановіть залежності: `npm install`
4. Внесіть зміни та протестуйте
5. Надішліть pull request

### Стиль коду
- Надається конфігурація ESLint
- Prettier для форматування коду
- TypeScript для забезпечення типізації
- JSDoc-коментарі для документації

## Результати навчання

Після завершення цього прикладу ви зрозумієте:

1. **Нативна розробка для Windows 11**
   - Реалізація Fluent Design System
   - Інтеграція з Windows
   - Найкращі практики безпеки Electron

2. **Інтеграція AI-моделей**
   - Архітектура сервісу Foundry Local
   - Управління життєвим циклом моделей
   - Моніторинг продуктивності та оптимізація

3. **Системи чату в реальному часі**
   - Обробка потокових відповідей
   - Управління станом розмов
   - Шаблони користувацького досвіду

4. **Розробка додатків для продакшну**
   - Обробка помилок і відновлення
   - Оптимізація продуктивності
   - Міркування щодо безпеки
   - Стратегії тестування

## Наступні кроки

- **Приклад 09**: Система оркестрації багатьох агентів
- **Приклад 10**: Інтеграція Foundry Local як інструментів
- **Розширені теми**: Кастомізація моделей
- **Розгортання**: Шаблони розгортання для підприємств

## Ліцензія

Цей приклад відповідає ліцензії проекту Microsoft Foundry Local.

---

