<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "562ac0eae12d808c9f45fbb77eb5c84f",
  "translation_date": "2025-09-25T01:48:34+00:00",
  "source_file": "Module08/samples/04/README.md",
  "language_code": "bg"
}
-->
# Пример 04: Производствени чат приложения с Chainlit

Изчерпателен пример, демонстриращ множество подходи за създаване на готови за производство чат приложения с Microsoft Foundry Local, включващ модерни уеб интерфейси, стрийминг отговори и най-новите технологии за браузъри.

## Какво е включено

- **🚀 Chainlit Chat App** (`app.py`): Готово за производство чат приложение със стрийминг
- **🌐 WebGPU Demo** (`webgpu-demo/`): AI изчисления в браузъра с хардуерно ускорение
- **🎨 Интеграция с Open WebUI** (`open-webui-guide.md`): Професионален интерфейс, подобен на ChatGPT
- **📚 Образователен Notebook** (`chainlit_app.ipynb`): Интерактивни учебни материали

## Бърз старт

### 1. Chainlit Chat Application

```cmd
# Navigate to Module08 directory
cd Module08

# Start your model
foundry model run phi-4-mini

# Run Chainlit app (using port 8080 to avoid conflicts)
chainlit run samples\04\app.py -w --port 8080
```

Отваря се на: `http://localhost:8080`

### 2. WebGPU Browser Demo

```cmd
# Navigate to WebGPU demo
cd Module08\samples\04\webgpu-demo

# Serve the demo
python -m http.server 5173
```

Отваря се на: `http://localhost:5173`

### 3. Open WebUI Setup

```cmd
# Run Open WebUI with Docker
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```

Отваря се на: `http://localhost:3000`

## Архитектурни модели

### Матрица за решение: Локално срещу облачно

| Сценарий | Препоръка | Причина |
|----------|-----------|---------|
| **Чувствителни данни** | 🏠 Локално (Foundry) | Данните никога не напускат устройството |
| **Сложни разсъждения** | ☁️ Облачно (Azure OpenAI) | Достъп до по-големи модели |
| **Чат в реално време** | 🏠 Локално (Foundry) | По-ниска латентност, по-бързи отговори |
| **Анализ на документи** | 🔄 Хибрид | Локално за извличане, облачно за анализ |
| **Генериране на код** | 🏠 Локално (Foundry) | Поверителност + специализирани модели |
| **Изследователски задачи** | ☁️ Облачно (Azure OpenAI) | Необходима е широка база от знания |

### Сравнение на технологии

| Технология | Приложение | Предимства | Недостатъци |
|------------|------------|------------|-------------|
| **Chainlit** | Python разработчици, бързо прототипиране | Лесна настройка, поддръжка на стрийминг | Само за Python |
| **WebGPU** | Максимална поверителност, офлайн сценарии | Нативно за браузъра, без нужда от сървър | Ограничен размер на модела |
| **Open WebUI** | Производствено внедряване, екипи | Професионален интерфейс, управление на потребители | Изисква Docker |

## Предпоставки

- **Foundry Local**: Инсталиран и работещ ([Изтегли](https://aka.ms/foundry-local-installer))
- **Python**: 3.10+ с виртуална среда
- **Модел**: Зареден поне един (`foundry model run phi-4-mini`)
- **Браузър**: Chrome/Edge с поддръжка на WebGPU за демонстрации
- **Docker**: За Open WebUI (по избор)

## Инсталация и настройка

### 1. Настройка на Python среда

```cmd
# Navigate to Module08 directory
cd Module08

# Create and activate virtual environment
py -m venv .venv
.venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### 2. Настройка на Foundry Local

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

## Примерни приложения

### Chainlit Chat Application

**Характеристики:**
- 🚀 **Стрийминг в реално време**: Токените се появяват, докато се генерират
- 🛡️ **Стабилно управление на грешки**: Гъвкаво възстановяване при проблеми
- 🎨 **Модерен интерфейс**: Професионален чат интерфейс готов за употреба
- 🔧 **Гъвкава конфигурация**: Променливи на средата и автоматично откриване
- 📱 **Респонсив дизайн**: Работи на настолни и мобилни устройства

**Бърз старт:**
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

### WebGPU Browser Demo

**Характеристики:**
- 🌐 **AI нативен за браузъра**: Без нужда от сървър, работи изцяло в браузъра
- ⚡ **WebGPU ускорение**: Хардуерно ускорение, когато е налично
- 🔒 **Максимална поверителност**: Данните никога не напускат устройството
- 🎯 **Без инсталация**: Работи във всеки съвместим браузър
- 🔄 **Гъвкаво резервно решение**: Преминава към CPU, ако WebGPU не е наличен

**Стартиране:**
```cmd
cd samples\04\webgpu-demo
python -m http.server 5173
# Open http://localhost:5173
```

### Open WebUI Integration

**Характеристики:**
- 🎨 **Интерфейс, подобен на ChatGPT**: Професионален и познат UI
- 👥 **Поддръжка на множество потребители**: Потребителски акаунти и история на разговорите
- 📁 **Обработка на файлове**: Качване и анализ на документи
- 🔄 **Превключване на модели**: Лесно превключване между различни модели
- 🐳 **Docker внедряване**: Готово за производство контейнеризирано решение

**Бърза настройка:**
```cmd
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```

## Референция за конфигурация

### Променливи на средата

| Променлива | Описание | По подразбиране | Пример |
|------------|----------|-----------------|--------|
| `MODEL` | Алиас на модела за използване | `phi-4-mini` | `qwen2.5-7b-instruct` |
| `BASE_URL` | Endpoint на Foundry Local | Автоматично открит | `http://localhost:51211` |
| `API_KEY` | API ключ (по избор за локално) | `""` | `your-api-key` |

## Отстраняване на проблеми

### Чести проблеми

**Chainlit Application:**

1. **Услугата не е налична:**
   ```cmd
   # Check Foundry Local status
   foundry service status
   foundry service ps
   
   # Validate API endpoint (note: port 51211)
   curl http://localhost:51211/v1/models
   ```

2. **Конфликти на портове:**
   ```cmd
   # Check what's using port 8080
   netstat -ano | findstr :8080
   
   # Use different port if needed
   chainlit run samples\04\app.py -w --port 3000
   ```

3. **Проблеми с Python средата:**
   ```cmd
   # Verify correct interpreter in VS Code
   # Ctrl+Shift+P → Python: Select Interpreter
   # Choose: Module08/.venv/Scripts/python.exe
   
   # Reinstall dependencies
   pip install -r requirements.txt
   ```

**WebGPU Demo:**

1. **WebGPU не се поддържа:**
   - Обновете до Chrome/Edge 113+
   - Активирайте WebGPU: `chrome://flags/#enable-unsafe-webgpu`
   - Проверете статуса на GPU: `chrome://gpu`
   - Демото автоматично ще премине към CPU

2. **Грешки при зареждане на модела:**
   - Уверете се, че имате интернет връзка за изтегляне на модела
   - Проверете конзолата на браузъра за CORS грешки
   - Уверете се, че използвате HTTP (не file://)

**Open WebUI:**

1. **Отказ на връзката:**
   ```cmd
   # Check Docker is running
   docker --version
   
   # Check container status
   docker ps | findstr open-webui
   
   # View container logs
   docker logs open-webui
   ```

2. **Моделите не се появяват:**
   ```cmd
   # Verify Foundry Local endpoint
   curl http://localhost:51211/v1/models
   
   # Restart Open WebUI
   docker restart open-webui
   ```

### Контролен списък за валидиране

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

## Разширено използване

### Оптимизация на производителността

**Chainlit:**
- Използвайте стрийминг за по-добро възприемане на производителността
- Имплементирайте пулове за връзки за висока конкуренция
- Кеширайте отговорите на модела за повтарящи се заявки
- Наблюдавайте използването на паметта при големи истории на разговори

**WebGPU:**
- Използвайте WebGPU за максимална поверителност и скорост
- Имплементирайте квантоване на модела за по-малки модели
- Използвайте Web Workers за обработка във фонов режим
- Кеширайте компилираните модели в паметта на браузъра

**Open WebUI:**
- Използвайте постоянни обеми за историята на разговорите
- Конфигурирайте ограничения на ресурсите за Docker контейнера
- Имплементирайте стратегии за архивиране на потребителски данни
- Настройте обратен прокси за SSL терминализация

### Модели за интеграция

**Хибридно локално/облачно:**
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

**Мултимодален процес:**
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

## Производствено внедряване

### Съображения за сигурност

- **API ключове**: Използвайте променливи на средата, никога не ги кодирайте директно
- **Мрежа**: Използвайте HTTPS в производствена среда, обмислете VPN за достъп на екипа
- **Контрол на достъпа**: Имплементирайте автентикация за Open WebUI
- **Поверителност на данните**: Одитирайте кои данни остават локални и кои отиват в облака
- **Обновления**: Поддържайте Foundry Local и контейнерите актуализирани

### Мониторинг и поддръжка

- **Проверки на здравето**: Имплементирайте мониторинг на endpoint-ове
- **Логове**: Централизирайте логовете от всички компоненти
- **Метрики**: Следете времето за отговор, честотата на грешки, използването на ресурси
- **Архивиране**: Редовно архивирайте данните от разговорите и конфигурациите

## Референции и ресурси

### Документация
- [Chainlit Documentation](https://docs.chainlit.io/) - Пълно ръководство за фреймуърка
- [Foundry Local Documentation](https://learn.microsoft.com/azure/ai-foundry/foundry-local/) - Официална документация на Microsoft
- [ONNX Runtime Web](https://onnxruntime.ai/docs/get-started/with-javascript/web.html) - Интеграция с WebGPU
- [Open WebUI Documentation](https://docs.openwebui.com/) - Разширена конфигурация

### Примерни файлове
- [`app.py`](../../../../../Module08/samples/04/app.py) - Производствено приложение Chainlit
- [`chainlit_app.ipynb`](./chainlit_app.ipynb) - Образователен notebook
- [`webgpu-demo/`](../../../../../Module08/samples/04/webgpu-demo) - AI изчисления в браузъра
- [`open-webui-guide.md`](./open-webui-guide.md) - Пълна настройка на Open WebUI

### Свързани примери
- [Session 4 Documentation](../../04.CuttingEdgeModels.md) - Пълно ръководство за сесията
- [Foundry Local Samples](https://github.com/microsoft/foundry-local/tree/main/samples) - Официални примери

---

