<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "562ac0eae12d808c9f45fbb77eb5c84f",
  "translation_date": "2025-09-24T13:18:50+00:00",
  "source_file": "Module08/samples/04/README.md",
  "language_code": "ru"
}
-->
# Пример 04: Производственные чат-приложения с Chainlit

Полный пример, демонстрирующий различные подходы к созданию готовых к производству чат-приложений с использованием Microsoft Foundry Local, включая современные веб-интерфейсы, потоковые ответы и передовые технологии браузеров.

## Что включено

- **🚀 Chainlit Chat App** (`app.py`): Готовое к производству чат-приложение с потоковой передачей
- **🌐 WebGPU Demo** (`webgpu-demo/`): AI-вычисления в браузере с аппаратным ускорением
- **🎨 Интеграция Open WebUI** (`open-webui-guide.md`): Профессиональный интерфейс, похожий на ChatGPT
- **📚 Обучающий ноутбук** (`chainlit_app.ipynb`): Интерактивные учебные материалы

## Быстрый старт

### 1. Чат-приложение Chainlit

```cmd
# Navigate to Module08 directory
cd Module08

# Start your model
foundry model run phi-4-mini

# Run Chainlit app (using port 8080 to avoid conflicts)
chainlit run samples\04\app.py -w --port 8080
```

Открывается по адресу: `http://localhost:8080`

### 2. Демонстрация WebGPU в браузере

```cmd
# Navigate to WebGPU demo
cd Module08\samples\04\webgpu-demo

# Serve the demo
python -m http.server 5173
```

Открывается по адресу: `http://localhost:5173`

### 3. Настройка Open WebUI

```cmd
# Run Open WebUI with Docker
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```

Открывается по адресу: `http://localhost:3000`

## Архитектурные шаблоны

### Матрица решений: локально vs облако

| Сценарий | Рекомендация | Причина |
|----------|--------------|---------|
| **Конфиденциальные данные** | 🏠 Локально (Foundry) | Данные не покидают устройство |
| **Сложные рассуждения** | ☁️ Облако (Azure OpenAI) | Доступ к более крупным моделям |
| **Чат в реальном времени** | 🏠 Локально (Foundry) | Меньшая задержка, более быстрые ответы |
| **Анализ документов** | 🔄 Гибрид | Локально для извлечения, облако для анализа |
| **Генерация кода** | 🏠 Локально (Foundry) | Конфиденциальность + специализированные модели |
| **Исследовательские задачи** | ☁️ Облако (Azure OpenAI) | Требуется широкий объем знаний |

### Сравнение технологий

| Технология | Сценарий использования | Преимущества | Недостатки |
|------------|------------------------|--------------|------------|
| **Chainlit** | Python-разработчики, быстрый прототип | Простая настройка, поддержка потоков | Только для Python |
| **WebGPU** | Максимальная конфиденциальность, офлайн-сценарии | Нативный для браузера, сервер не нужен | Ограниченный размер модели |
| **Open WebUI** | Производственное развертывание, команды | Профессиональный интерфейс, управление пользователями | Требуется Docker |

## Предварительные требования

- **Foundry Local**: Установлен и запущен ([Скачать](https://aka.ms/foundry-local-installer))
- **Python**: Версия 3.10+ с виртуальной средой
- **Модель**: Загружена хотя бы одна (`foundry model run phi-4-mini`)
- **Браузер**: Chrome/Edge с поддержкой WebGPU для демонстраций
- **Docker**: Для Open WebUI (опционально)

## Установка и настройка

### 1. Настройка Python-среды

```cmd
# Navigate to Module08 directory
cd Module08

# Create and activate virtual environment
py -m venv .venv
.venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### 2. Настройка Foundry Local

```cmd
# Verify Foundry Local installation
foundry --version

# Start the service
foundry service start

# Load a model
foundry model run phi-4-mini

# Verify model is running
foundry service ps
```

## Пример приложений

### Чат-приложение Chainlit

**Особенности:**
- 🚀 **Потоковая передача в реальном времени**: Токены появляются по мере их генерации
- 🛡️ **Надежная обработка ошибок**: Плавное восстановление после сбоев
- 🎨 **Современный интерфейс**: Профессиональный чат-интерфейс "из коробки"
- 🔧 **Гибкая конфигурация**: Переменные окружения и автоопределение
- 📱 **Адаптивный дизайн**: Работает на настольных и мобильных устройствах

**Быстрый старт:**
```cmd
# Run with default settings (recommended)
chainlit run samples\04\app.py -w --port 8080

# Use specific model
set MODEL=qwen2.5-7b-instruct
chainlit run samples\04\app.py -w --port 8080

# Manual endpoint configuration
set BASE_URL=http://localhost:51211
set API_KEY=your-api-key
chainlit run samples\04\app.py -w --port 8080
```

### Демонстрация WebGPU в браузере

**Особенности:**
- 🌐 **AI, работающий в браузере**: Сервер не требуется, все выполняется в браузере
- ⚡ **Ускорение WebGPU**: Аппаратное ускорение при наличии
- 🔒 **Максимальная конфиденциальность**: Данные никогда не покидают ваше устройство
- 🎯 **Без установки**: Работает в любом совместимом браузере
- 🔄 **Плавный переход**: Переход на CPU, если WebGPU недоступен

**Запуск:**
```cmd
cd samples\04\webgpu-demo
python -m http.server 5173
# Open http://localhost:5173
```

### Интеграция Open WebUI

**Особенности:**
- 🎨 **Интерфейс, похожий на ChatGPT**: Профессиональный, знакомый UI
- 👥 **Поддержка нескольких пользователей**: Учетные записи и история разговоров
- 📁 **Обработка файлов**: Загрузка и анализ документов
- 🔄 **Переключение моделей**: Легкое переключение между различными моделями
- 🐳 **Развертывание в Docker**: Готовая к производству контейнеризированная настройка

**Быстрая настройка:**
```cmd
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```

## Справочник по конфигурации

### Переменные окружения

| Переменная | Описание | Значение по умолчанию | Пример |
|------------|----------|-----------------------|--------|
| `MODEL` | Псевдоним модели для использования | `phi-4-mini` | `qwen2.5-7b-instruct` |
| `BASE_URL` | Endpoint Foundry Local | Автоопределение | `http://localhost:51211` |
| `API_KEY` | API-ключ (опционально для локального использования) | `""` | `your-api-key` |

## Устранение неполадок

### Распространенные проблемы

**Чат-приложение Chainlit:**

1. **Сервис недоступен:**
   ```cmd
   # Check Foundry Local status
   foundry service status
   foundry service ps
   
   # Validate API endpoint (note: port 51211)
   curl http://localhost:51211/v1/models
   ```

2. **Конфликты портов:**
   ```cmd
   # Check what's using port 8080
   netstat -ano | findstr :8080
   
   # Use different port if needed
   chainlit run samples\04\app.py -w --port 3000
   ```

3. **Проблемы с Python-средой:**
   ```cmd
   # Verify correct interpreter in VS Code
   # Ctrl+Shift+P → Python: Select Interpreter
   # Choose: Module08/.venv/Scripts/python.exe
   
   # Reinstall dependencies
   pip install -r requirements.txt
   ```

**Демонстрация WebGPU:**

1. **WebGPU не поддерживается:**
   - Обновите Chrome/Edge до версии 113+
   - Включите WebGPU: `chrome://flags/#enable-unsafe-webgpu`
   - Проверьте статус GPU: `chrome://gpu`
   - Демонстрация автоматически перейдет на CPU

2. **Ошибки загрузки модели:**
   - Убедитесь, что есть подключение к интернету для загрузки модели
   - Проверьте консоль браузера на наличие ошибок CORS
   - Убедитесь, что вы используете HTTP (а не file://)

**Open WebUI:**

1. **Отказ в подключении:**
   ```cmd
   # Check Docker is running
   docker --version
   
   # Check container status
   docker ps | findstr open-webui
   
   # View container logs
   docker logs open-webui
   ```

2. **Модели не отображаются:**
   ```cmd
   # Verify Foundry Local endpoint
   curl http://localhost:51211/v1/models
   
   # Restart Open WebUI
   docker restart open-webui
   ```

### Контрольный список проверки

```cmd
# ✅ 1. Foundry Local Setup
foundry --version                    # Should show version
foundry service status               # Should show "running"
foundry model list                   # Should show loaded models
curl http://localhost:51211/v1/models  # Should return JSON

# ✅ 2. Python Environment  
python --version                     # Should be 3.10+
pip list | findstr chainlit         # Should show chainlit package
pip list | findstr openai           # Should show openai package

# ✅ 3. Application Testing
chainlit run samples\04\app.py -w --port 8080  # Should open browser
# Test WebGPU demo at localhost:5173
# Test Open WebUI at localhost:3000
```

## Расширенное использование

### Оптимизация производительности

**Chainlit:**
- Используйте потоковую передачу для улучшения восприятия производительности
- Реализуйте пул соединений для высокой конкурентности
- Кэшируйте ответы модели для повторяющихся запросов
- Следите за использованием памяти при больших историях разговоров

**WebGPU:**
- Используйте WebGPU для максимальной конфиденциальности и скорости
- Реализуйте квантование модели для уменьшения размера
- Используйте Web Workers для фоновой обработки
- Кэшируйте скомпилированные модели в хранилище браузера

**Open WebUI:**
- Используйте постоянные тома для истории разговоров
- Настройте ограничения ресурсов для контейнера Docker
- Реализуйте стратегии резервного копирования данных пользователей
- Настройте обратный прокси для SSL-терминации

### Шаблоны интеграции

**Гибрид локально/облако:**
```python
# Route based on complexity and privacy requirements
async def intelligent_routing(prompt: str, metadata: dict):
    if metadata.get("contains_pii"):
        return await foundry_local_completion(prompt)  # Privacy-sensitive
    elif len(prompt.split()) > 200:
        return await azure_openai_completion(prompt)   # Complex reasoning
    else:
        return await foundry_local_completion(prompt)  # Default local
```

**Мультимодальный конвейер:**
```python
# Combine different AI capabilities
async def analyze_document(file_path: str):
    # 1. OCR with WebGPU (browser-based)
    text = await webgpu_ocr(file_path)
    
    # 2. Analysis with Foundry Local (private)
    summary = await foundry_local_analyze(text)
    
    # 3. Enhancement with cloud (if needed)
    if summary.confidence < 0.8:
        summary = await azure_openai_enhance(summary)
    
    return summary
```

## Производственное развертывание

### Соображения безопасности

- **API-ключи**: Используйте переменные окружения, никогда не хардкодьте
- **Сеть**: Используйте HTTPS в производстве, рассмотрите VPN для доступа команды
- **Контроль доступа**: Реализуйте аутентификацию для Open WebUI
- **Конфиденциальность данных**: Проверьте, какие данные остаются локальными, а какие отправляются в облако
- **Обновления**: Держите Foundry Local и контейнеры в актуальном состоянии

### Мониторинг и обслуживание

- **Проверка состояния**: Реализуйте мониторинг конечных точек
- **Логирование**: Централизуйте логи всех компонентов
- **Метрики**: Отслеживайте время ответа, частоту ошибок, использование ресурсов
- **Резервное копирование**: Регулярное резервное копирование данных разговоров и конфигураций

## Ссылки и ресурсы

### Документация
- [Документация Chainlit](https://docs.chainlit.io/) - Полное руководство по фреймворку
- [Документация Foundry Local](https://learn.microsoft.com/azure/ai-foundry/foundry-local/) - Официальная документация Microsoft
- [ONNX Runtime Web](https://onnxruntime.ai/docs/get-started/with-javascript/web.html) - Интеграция WebGPU
- [Документация Open WebUI](https://docs.openwebui.com/) - Расширенная конфигурация

### Пример файлов
- [`app.py`](../../../../../Module08/samples/04/app.py) - Производственное приложение Chainlit
- [`chainlit_app.ipynb`](./chainlit_app.ipynb) - Обучающий ноутбук
- [`webgpu-demo/`](../../../../../Module08/samples/04/webgpu-demo) - AI-вычисления в браузере
- [`open-webui-guide.md`](./open-webui-guide.md) - Полная настройка Open WebUI

### Связанные примеры
- [Документация сессии 4](../../04.CuttingEdgeModels.md) - Полное руководство по сессии
- [Примеры Foundry Local](https://github.com/microsoft/foundry-local/tree/main/samples) - Официальные примеры

---

