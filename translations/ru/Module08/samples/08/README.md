<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "13cb0371a2aea01d721186ced4a25e1a",
  "translation_date": "2025-09-24T13:47:26+00:00",
  "source_file": "Module08/samples/08/README.md",
  "language_code": "ru"
}
-->
# Windows 11 Chat Sample - Foundry Local

Современное приложение для чата на Windows 11, которое интегрирует Microsoft Foundry Local с красивым нативным интерфейсом. Создано с использованием Electron и в соответствии с официальными шаблонами Foundry Local от Microsoft.

## Обзор

Этот пример демонстрирует, как создать готовое к производству приложение для чата, использующее локальные модели ИИ через Foundry Local, обеспечивая пользователям конфиденциальные разговоры с ИИ без зависимости от облака.

## Возможности

### 🎨 **Нативный дизайн Windows 11**
- Интеграция с Fluent Design System
- Эффекты материала Mica и прозрачности
- Поддержка тем оформления Windows 11
- Адаптивный макет для всех размеров экрана
- Автоматическое переключение между темной и светлой темами

### 🤖 **Интеграция моделей ИИ**
- Интеграция с сервисом Foundry Local
- Поддержка нескольких моделей с возможностью горячей замены
- Потоковые ответы в реальном времени
- Переключение между локальными и облачными моделями
- Мониторинг состояния и работоспособности моделей

### 💬 **Опыт общения**
- Индикаторы ввода в реальном времени
- Сохранение истории сообщений
- Экспорт разговоров
- Настраиваемые системные подсказки
- Ветвление и управление беседами

### ⚡ **Особенности производительности**
- Ленивое загрузка и виртуализация
- Оптимизированный рендеринг для длинных разговоров
- Предзагрузка моделей в фоновом режиме
- Эффективное управление памятью
- Плавные анимации и переходы

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

## Предварительные требования

### Системные требования
- **ОС**: Windows 11 (рекомендуется версия 22H2 или новее)
- **ОЗУ**: минимум 8 ГБ, рекомендуется 16 ГБ+ для больших моделей
- **Хранилище**: минимум 10 ГБ свободного места для моделей
- **GPU**: необязательно, но рекомендуется для ускорения работы

### Программные зависимости
- **Node.js**: версия 18.0.0 или новее
- **Foundry Local**: последняя версия от Microsoft
- **Git**: для клонирования и разработки

## Установка

### 1. Установите Foundry Local
```powershell
# Download from GitHub releases and install
winget install Microsoft.FoundryLocal

# Verify installation
foundry --version
```

### 2. Клонирование и настройка
```bash
# Navigate to sample directory
cd Module08/samples/08

# Install dependencies
npm install

# Install Electron if not global
npm install -g electron
```

### 3. Настройка окружения
```powershell
# Optional: Set cloud model credentials for hybrid mode
$env:AZURE_OPENAI_KEY="your-api-key"
$env:AZURE_OPENAI_ENDPOINT="your-endpoint"
$env:AZURE_OPENAI_MODEL="gpt-4"
```

### 4. Запуск приложения
```bash
# Development mode
npm start

# Production build
npm run build
npm run dist
```

## Структура проекта

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

## Подробный обзор ключевых возможностей

### Интеграция с Windows 11

**Fluent Design System**
- Материалы фона Mica
- Эффекты прозрачности Acrylic
- Закругленные углы и современное расстояние между элементами
- Нативная цветовая палитра Windows 11
- Семантические цветовые токены для доступности

**Нативные функции Windows**
- Интеграция списка переходов для недавних чатов
- Уведомления Windows о новых сообщениях
- Прогресс на панели задач для операций с моделями
- Интеграция системного трея с быстрыми действиями
- Поддержка аутентификации Windows Hello

### Управление моделями ИИ

**Локальные модели**
```javascript
// Automatic model discovery and loading
const models = await foundryManager.discoverModels();
await foundryManager.loadModel('phi-4-mini');

// Model health monitoring
const health = await foundryManager.checkHealth();
console.log(`Model Status: ${health.status}`);
console.log(`Memory Usage: ${health.memoryUsage}MB`);
```

**Гибридная поддержка облака/локальных моделей**
```javascript
// Seamless switching between local and cloud models
if (useCloudModel) {
    await chatManager.switchToCloud('gpt-4');
} else {
    await chatManager.switchToLocal('phi-4-mini');
}
```

### Функции интерфейса чата

**Потоковая передача в реальном времени**
- Отображение ответа токен за токен
- Плавные анимации ввода текста
- Возможность отмены запросов
- Индикаторы ввода и статуса

**Управление беседами**
- Сохранение истории чатов
- Экспорт/импорт бесед
- Поиск и фильтрация сообщений
- Ветвление бесед
- Настраиваемые системные подсказки для каждой беседы

**Доступность**
- Полная навигация с клавиатуры
- Совместимость с экранными читалками
- Поддержка режима высокого контраста
- Настраиваемые размеры шрифта
- Интеграция голосового ввода

## Примеры использования

### Базовая интеграция чата
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

### Управление моделями
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

### Настройки и кастомизация
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

## Опции конфигурации

### Настройки приложения
- **Тема**: Авто, светлая, темная
- **Модель**: Выбор модели по умолчанию
- **Производительность**: Настройки вывода
- **Конфиденциальность**: Политики хранения данных
- **Уведомления**: Оповещения о сообщениях
- **Ярлыки**: Горячие клавиши

### Настройки чата
- **Потоковая передача**: Включение/отключение ответов в реальном времени
- **Длина контекста**: Память беседы
- **Температура**: Креативность ответов
- **Максимум токенов**: Ограничения длины ответа
- **Системные подсказки**: Поведение помощника по умолчанию

### Настройки модели
- **Автозагрузка**: Автоматическое обновление моделей
- **Размер кэша**: Ограничения локального хранилища моделей
- **Режим производительности**: Предпочтения CPU или GPU
- **Проверка состояния**: Интервалы мониторинга

## Разработка

### Сборка из исходного кода
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

### Отладка
```bash
# Enable debug mode
set DEBUG=foundry-chat:*
npm start

# View developer tools
# Press F12 in the application
```

### Тестирование
```bash
# Run unit tests
npm test

# Run integration tests
npm run test:integration

# Run end-to-end tests
npm run test:e2e
```

## Оптимизация производительности

### Управление памятью
- Эффективная виртуализация сообщений
- Автоматический сбор мусора
- Мониторинг памяти моделей
- Очистка ресурсов при выходе

### Оптимизация рендеринга
- Виртуальная прокрутка для длинных бесед
- Ленивое загрузка истории сообщений
- Оптимизированные обновления React/DOM
- Анимации с ускорением GPU

### Оптимизация сети
- Пул соединений
- Пакетная обработка запросов
- Логика автоматического повторного запроса
- Поддержка автономного режима

## Соображения безопасности

### Конфиденциальность данных
- Архитектура с приоритетом локального хранения
- Отсутствие передачи данных в облако (локальный режим)
- Шифрованное хранилище бесед
- Безопасное управление учетными данными

### Безопасность приложения
- Изолированные процессы рендеринга
- Политика безопасности контента (CSP)
- Отсутствие удаленного выполнения кода
- Безопасная межпроцессорная связь (IPC)

## Устранение неполадок

### Распространенные проблемы

**Foundry Local не запускается**
```powershell
# Check service status
foundry status

# Restart service
foundry restart

# Check logs
foundry logs
```

**Ошибки загрузки моделей**
- Убедитесь, что достаточно места на диске
- Проверьте подключение к интернету для загрузки
- Убедитесь, что драйверы GPU обновлены
- Попробуйте разные варианты моделей

**Проблемы с производительностью**
- Мониторинг системных ресурсов
- Настройка параметров модели
- Включение аппаратного ускорения
- Закрытие других ресурсоемких приложений

### Режим отладки
Включите ведение журнала отладки, установив переменные окружения:
```powershell
$env:DEBUG="foundry:*"
$env:FOUNDRY_LOG_LEVEL="debug"
```

## Вклад

### Настройка разработки
1. Форкните репозиторий
2. Создайте ветку для новой функции
3. Установите зависимости: `npm install`
4. Внесите изменения и протестируйте
5. Отправьте pull request

### Стиль кода
- Предоставлена конфигурация ESLint
- Prettier для форматирования кода
- TypeScript для обеспечения типобезопасности
- JSDoc комментарии для документации

## Результаты обучения

После завершения работы с этим примером вы узнаете:

1. **Нативная разработка для Windows 11**
   - Реализация Fluent Design System
   - Интеграция с Windows
   - Лучшие практики безопасности Electron

2. **Интеграция моделей ИИ**
   - Архитектура сервиса Foundry Local
   - Управление жизненным циклом моделей
   - Мониторинг и оптимизация производительности

3. **Системы чата в реальном времени**
   - Обработка потоковых ответов
   - Управление состоянием беседы
   - Шаблоны пользовательского опыта

4. **Разработка производственных приложений**
   - Обработка ошибок и восстановление
   - Оптимизация производительности
   - Соображения безопасности
   - Стратегии тестирования

## Следующие шаги

- **Пример 09**: Система оркестрации нескольких агентов
- **Пример 10**: Интеграция Foundry Local как инструментов
- **Продвинутые темы**: Тонкая настройка пользовательских моделей
- **Развертывание**: Шаблоны развертывания для предприятий

## Лицензия

Этот пример следует той же лицензии, что и проект Microsoft Foundry Local.

---

