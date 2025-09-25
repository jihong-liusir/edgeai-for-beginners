<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "562ac0eae12d808c9f45fbb77eb5c84f",
  "translation_date": "2025-09-25T02:34:02+00:00",
  "source_file": "Module08/samples/04/README.md",
  "language_code": "uk"
}
-->
# Зразок 04: Чат-додатки для виробництва з Chainlit

Комплексний зразок, що демонструє різні підходи до створення готових до виробництва чат-додатків за допомогою Microsoft Foundry Local, з сучасними веб-інтерфейсами, потоковими відповідями та передовими браузерними технологіями.

## Що включено

- **🚀 Chainlit Chat App** (`app.py`): Готовий до виробництва чат-додаток із потоковою передачею
- **🌐 Демонстрація WebGPU** (`webgpu-demo/`): AI-обчислення в браузері з апаратним прискоренням
- **🎨 Інтеграція Open WebUI** (`open-webui-guide.md`): Професійний інтерфейс, схожий на ChatGPT
- **📚 Навчальний ноутбук** (`chainlit_app.ipynb`): Інтерактивні навчальні матеріали

## Швидкий старт

### 1. Чат-додаток Chainlit

```cmd
# Navigate to Module08 directory
cd Module08

# Start your model
foundry model run phi-4-mini

# Run Chainlit app (using port 8080 to avoid conflicts)
chainlit run samples\04\app.py -w --port 8080
```

Відкривається за адресою: `http://localhost:8080`

### 2. Демонстрація WebGPU у браузері

```cmd
# Navigate to WebGPU demo
cd Module08\samples\04\webgpu-demo

# Serve the demo
python -m http.server 5173
```

Відкривається за адресою: `http://localhost:5173`

### 3. Налаштування Open WebUI

```cmd
# Run Open WebUI with Docker
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```

Відкривається за адресою: `http://localhost:3000`

## Архітектурні шаблони

### Матриця рішень: локально чи в хмарі

| Сценарій | Рекомендація | Причина |
|----------|--------------|---------|
| **Конфіденційні дані** | 🏠 Локально (Foundry) | Дані не залишають пристрій |
| **Складні міркування** | ☁️ Хмара (Azure OpenAI) | Доступ до більших моделей |
| **Чат у реальному часі** | 🏠 Локально (Foundry) | Менша затримка, швидші відповіді |
| **Аналіз документів** | 🔄 Гібрид | Локально для вилучення, у хмарі для аналізу |
| **Генерація коду** | 🏠 Локально (Foundry) | Конфіденційність + спеціалізовані моделі |
| **Дослідницькі завдання** | ☁️ Хмара (Azure OpenAI) | Потрібна широка база знань |

### Порівняння технологій

| Технологія | Використання | Переваги | Недоліки |
|------------|--------------|----------|----------|
| **Chainlit** | Розробники Python, швидке прототипування | Легке налаштування, підтримка потоків | Тільки Python |
| **WebGPU** | Максимальна конфіденційність, офлайн-сценарії | Браузерна технологія, без сервера | Обмежений розмір моделі |
| **Open WebUI** | Розгортання для команд | Професійний інтерфейс, управління користувачами | Потребує Docker |

## Попередні вимоги

- **Foundry Local**: Встановлено та запущено ([Завантажити](https://aka.ms/foundry-local-installer))
- **Python**: Версія 3.10+ із віртуальним середовищем
- **Модель**: Завантажена хоча б одна (`foundry model run phi-4-mini`)
- **Браузер**: Chrome/Edge із підтримкою WebGPU для демонстрацій
- **Docker**: Для Open WebUI (опціонально)

## Встановлення та налаштування

### 1. Налаштування середовища Python

```cmd
# Navigate to Module08 directory
cd Module08

# Create and activate virtual environment
py -m venv .venv
.venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### 2. Налаштування Foundry Local

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

## Зразки додатків

### Чат-додаток Chainlit

**Особливості:**
- 🚀 **Потокова передача в реальному часі**: Токени з'являються під час їх генерації
- 🛡️ **Надійна обробка помилок**: Плавне зниження функціональності та відновлення
- 🎨 **Сучасний інтерфейс**: Професійний чат-інтерфейс "з коробки"
- 🔧 **Гнучке налаштування**: Змінні середовища та автоматичне виявлення
- 📱 **Адаптивний дизайн**: Працює на настільних і мобільних пристроях

**Швидкий старт:**
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

### Демонстрація WebGPU у браузері

**Особливості:**
- 🌐 **AI у браузері**: Не потрібен сервер, працює повністю в браузері
- ⚡ **Прискорення WebGPU**: Апаратне прискорення, якщо доступне
- 🔒 **Максимальна конфіденційність**: Дані ніколи не залишають ваш пристрій
- 🎯 **Без встановлення**: Працює в будь-якому сумісному браузері
- 🔄 **Плавне резервування**: Перемикається на CPU, якщо WebGPU недоступний

**Запуск:**
```cmd
cd samples\04\webgpu-demo
python -m http.server 5173
# Open http://localhost:5173
```

### Інтеграція Open WebUI

**Особливості:**
- 🎨 **Інтерфейс, схожий на ChatGPT**: Професійний, знайомий UI
- 👥 **Підтримка кількох користувачів**: Облікові записи користувачів та історія розмов
- 📁 **Обробка файлів**: Завантаження та аналіз документів
- 🔄 **Перемикання моделей**: Легке перемикання між різними моделями
- 🐳 **Розгортання через Docker**: Готове до виробництва контейнеризоване налаштування

**Швидке налаштування:**
```cmd
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```

## Довідник конфігурації

### Змінні середовища

| Змінна | Опис | За замовчуванням | Приклад |
|--------|------|------------------|---------|
| `MODEL` | Псевдонім моделі для використання | `phi-4-mini` | `qwen2.5-7b-instruct` |
| `BASE_URL` | Локальна точка доступу Foundry | Автоматично визначається | `http://localhost:51211` |
| `API_KEY` | API-ключ (опціонально для локального використання) | `""` | `your-api-key` |

## Вирішення проблем

### Поширені проблеми

**Чат-додаток Chainlit:**

1. **Сервіс недоступний:**
   ```cmd
   # Check Foundry Local status
   foundry service status
   foundry service ps
   
   # Validate API endpoint (note: port 51211)
   curl http://localhost:51211/v1/models
   ```

2. **Конфлікти портів:**
   ```cmd
   # Check what's using port 8080
   netstat -ano | findstr :8080
   
   # Use different port if needed
   chainlit run samples\04\app.py -w --port 3000
   ```

3. **Проблеми з середовищем Python:**
   ```cmd
   # Verify correct interpreter in VS Code
   # Ctrl+Shift+P → Python: Select Interpreter
   # Choose: Module08/.venv/Scripts/python.exe
   
   # Reinstall dependencies
   pip install -r requirements.txt
   ```

**Демонстрація WebGPU:**

1. **WebGPU не підтримується:**
   - Оновіть до Chrome/Edge 113+
   - Увімкніть WebGPU: `chrome://flags/#enable-unsafe-webgpu`
   - Перевірте статус GPU: `chrome://gpu`
   - Демонстрація автоматично переключиться на CPU

2. **Помилки завантаження моделі:**
   - Переконайтеся, що є підключення до інтернету для завантаження моделі
   - Перевірте консоль браузера на помилки CORS
   - Переконайтеся, що ви використовуєте HTTP (а не file://)

**Open WebUI:**

1. **Відмова у з'єднанні:**
   ```cmd
   # Check Docker is running
   docker --version
   
   # Check container status
   docker ps | findstr open-webui
   
   # View container logs
   docker logs open-webui
   ```

2. **Моделі не з'являються:**
   ```cmd
   # Verify Foundry Local endpoint
   curl http://localhost:51211/v1/models
   
   # Restart Open WebUI
   docker restart open-webui
   ```

### Контрольний список перевірки

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

## Розширене використання

### Оптимізація продуктивності

**Chainlit:**
- Використовуйте потокову передачу для покращення сприйняття продуктивності
- Реалізуйте пул з'єднань для високої одночасності
- Кешуйте відповіді моделі для повторних запитів
- Моніторьте використання пам'яті з великими історіями розмов

**WebGPU:**
- Використовуйте WebGPU для максимальної конфіденційності та швидкості
- Реалізуйте квантування моделі для зменшення розміру
- Використовуйте Web Workers для фонової обробки
- Кешуйте скомпільовані моделі в пам'яті браузера

**Open WebUI:**
- Використовуйте постійні томи для історії розмов
- Налаштуйте обмеження ресурсів для контейнера Docker
- Реалізуйте стратегії резервного копіювання для даних користувачів
- Налаштуйте зворотний проксі для завершення SSL

### Шаблони інтеграції

**Гібрид локально/хмара:**
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

**Мультимодальний конвеєр:**
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

## Розгортання у виробництві

### Міркування щодо безпеки

- **API-ключі**: Використовуйте змінні середовища, ніколи не вбудовуйте
- **Мережа**: Використовуйте HTTPS у виробництві, розгляньте VPN для доступу команди
- **Контроль доступу**: Реалізуйте аутентифікацію для Open WebUI
- **Конфіденційність даних**: Перевірте, які дані залишаються локально, а які передаються в хмару
- **Оновлення**: Регулярно оновлюйте Foundry Local та контейнери

### Моніторинг та обслуговування

- **Перевірка стану**: Реалізуйте моніторинг точок доступу
- **Логування**: Централізуйте журнали з усіх компонентів
- **Метрики**: Відстежуйте час відповіді, рівень помилок, використання ресурсів
- **Резервне копіювання**: Регулярно створюйте резервні копії даних розмов та конфігурацій

## Довідники та ресурси

### Документація
- [Документація Chainlit](https://docs.chainlit.io/) - Повний посібник по фреймворку
- [Документація Foundry Local](https://learn.microsoft.com/azure/ai-foundry/foundry-local/) - Офіційна документація Microsoft
- [ONNX Runtime Web](https://onnxruntime.ai/docs/get-started/with-javascript/web.html) - Інтеграція WebGPU
- [Документація Open WebUI](https://docs.openwebui.com/) - Розширена конфігурація

### Зразки файлів
- [`app.py`](../../../../../Module08/samples/04/app.py) - Чат-додаток Chainlit для виробництва
- [`chainlit_app.ipynb`](./chainlit_app.ipynb) - Навчальний ноутбук
- [`webgpu-demo/`](../../../../../Module08/samples/04/webgpu-demo) - AI-обчислення в браузері
- [`open-webui-guide.md`](./open-webui-guide.md) - Повне налаштування Open WebUI

### Схожі зразки
- [Документація сесії 4](../../04.CuttingEdgeModels.md) - Повний посібник сесії
- [Зразки Foundry Local](https://github.com/microsoft/foundry-local/tree/main/samples) - Офіційні зразки

---

