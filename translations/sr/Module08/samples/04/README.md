<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "2f1754a482b6a84e07287a5b775e65b6",
  "translation_date": "2025-10-01T01:38:06+00:00",
  "source_file": "Module08/samples/04/README.md",
  "language_code": "sr"
}
-->
# Пример 04: Производне апликације за ћаскање са Chainlit

Свеобухватан пример који демонстрира различите приступе за изградњу апликација за ћаскање спремних за производњу користећи Microsoft Foundry Local, са модерним веб интерфејсима, стриминг одговорима и најсавременијим технологијама за претраживаче.

## Шта је укључено

- **🚀 Chainlit апликација за ћаскање** (`app.py`): Апликација за ћаскање спремна за производњу са стримингом
- **🌐 WebGPU демонстрација** (`webgpu-demo/`): AI инференција у претраживачу са хардверским убрзањем
- **🎨 Интеграција Open WebUI** (`open-webui-guide.md`): Професионални интерфејс сличан ChatGPT-у
- **📚 Едукативни нотебук** (`chainlit_app.ipynb`): Интерактивни материјали за учење

## Брзи почетак

### 1. Chainlit апликација за ћаскање

```cmd
# Navigate to Module08 directory
cd Module08

# Start your model
foundry model run phi-4-mini

# Run Chainlit app (using port 8080 to avoid conflicts)
chainlit run samples\04\app.py -w --port 8080
```

Отвара се на: `http://localhost:8080`

### 2. WebGPU демонстрација у претраживачу

```cmd
# Navigate to WebGPU demo
cd Module08\samples\04\webgpu-demo

# Serve the demo
python -m http.server 5173
```

Отвара се на: `http://localhost:5173`

### 3. Подешавање Open WebUI

```cmd
# Run Open WebUI with Docker
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```

Отвара се на: `http://localhost:3000`

## Шаблони архитектуре

### Матрица одлуке: Локално vs Облак

| Сценарио | Препорука | Разлог |
|----------|-----------|--------|
| **Подаци осетљиви на приватност** | 🏠 Локално (Foundry) | Подаци никада не напуштају уређај |
| **Комплексно резоновање** | ☁️ Облак (Azure OpenAI) | Приступ већим моделима |
| **Ћаскање у реалном времену** | 🏠 Локално (Foundry) | Мања латенција, бржи одговори |
| **Анализа докумената** | 🔄 Хибридно | Локално за екстракцију, облак за анализу |
| **Генерисање кода** | 🏠 Локално (Foundry) | Приватност + специјализовани модели |
| **Истраживачки задаци** | ☁️ Облак (Azure OpenAI) | Потребна широка база знања |

### Поређење технологија

| Технологија | Намена | Предности | Недостаци |
|-------------|--------|-----------|-----------|
| **Chainlit** | Python програмери, брзо прототипирање | Лако подешавање, подршка за стриминг | Само за Python |
| **WebGPU** | Максимална приватност, офлајн сценарији | Нативно за претраживач, није потребан сервер | Ограничена величина модела |
| **Open WebUI** | Производно распоређивање, тимови | Професионални UI, управљање корисницима | Захтева Docker |

## Предуслови

- **Foundry Local**: Инсталиран и покренут ([Преузми](https://aka.ms/foundry-local-installer))
- **Python**: Верзија 3.10+ са виртуелним окружењем
- **Модел**: Најмање један учитан (`foundry model run phi-4-mini`)
- **Претраживач**: Chrome/Edge са WebGPU подршком за демонстрације
- **Docker**: За Open WebUI (опционо)

## Инсталација и подешавање

### 1. Подешавање Python окружења

```cmd
# Navigate to Module08 directory
cd Module08

# Create and activate virtual environment
py -m venv .venv
.venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### 2. Подешавање Foundry Local

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

## Пример апликација

### Chainlit апликација за ћаскање

**Карактеристике:**
- 🚀 **Стриминг у реалном времену**: Токени се појављују како се генеришу
- 🛡️ **Робусно руковање грешкама**: Грациозно опадање и опоравак
- 🎨 **Модеран UI**: Професионални интерфејс за ћаскање одмах доступан
- 🔧 **Флексибилна конфигурација**: Променљиве окружења и аутоматска детекција
- 📱 **Респонзивни дизајн**: Ради на десктоп и мобилним уређајима

**Брзи почетак:**
```cmd
# Run with default settings (recommended)
chainlit run samples\04\app.py -w --port 8080

# Use specific model
set MODEL=qwen2.5-7b
chainlit run samples\04\app.py -w --port 8080

# Manual endpoint configuration
set BASE_URL=http://localhost:51211
set API_KEY=your-api-key
chainlit run samples\04\app.py -w --port 8080
```

### WebGPU демонстрација у претраживачу

**Карактеристике:**
- 🌐 **Нативни AI за претраживач**: Није потребан сервер, ради искључиво у претраживачу
- ⚡ **WebGPU убрзање**: Хардверско убрзање када је доступно
- 🔒 **Максимална приватност**: Подаци никада не напуштају ваш уређај
- 🎯 **Без инсталације**: Ради у било ком компатибилном претраживачу
- 🔄 **Грациозно опадање**: Прелази на CPU ако WebGPU није доступан

**Покретање:**
```cmd
cd samples\04\webgpu-demo
python -m http.server 5173
# Open http://localhost:5173
```

### Интеграција Open WebUI

**Карактеристике:**
- 🎨 **Интерфејс сличан ChatGPT-у**: Професионалан, познат UI
- 👥 **Подршка за више корисника**: Кориснички налози и историја разговора
- 📁 **Обрада датотека**: Отпремање и анализа докумената
- 🔄 **Пребацивање модела**: Лако пребацивање између различитих модела
- 🐳 **Docker распоређивање**: Производно спремно контејнеризовано подешавање

**Брзо подешавање:**
```cmd
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```

## Референца конфигурације

### Променљиве окружења

| Променљива | Опис | Подразумевано | Пример |
|------------|------|---------------|--------|
| `MODEL` | Алијас модела који се користи | `phi-4-mini` | `qwen2.5-7b` |
| `BASE_URL` | Foundry Local крајња тачка | Аутоматски детектовано | `http://localhost:51211` |
| `API_KEY` | API кључ (опционо за локално) | `""` | `your-api-key` |

## Решавање проблема

### Уобичајени проблеми

**Chainlit апликација:**

1. **Услуга није доступна:**
   ```cmd
   # Check Foundry Local status
   foundry service status
   foundry service ps
   
   # Validate API endpoint (note: port 51211)
   curl http://localhost:51211/v1/models
   ```

2. **Конфликти портова:**
   ```cmd
   # Check what's using port 8080
   netstat -ano | findstr :8080
   
   # Use different port if needed
   chainlit run samples\04\app.py -w --port 3000
   ```

3. **Проблеми са Python окружењем:**
   ```cmd
   # Verify correct interpreter in VS Code
   # Ctrl+Shift+P → Python: Select Interpreter
   # Choose: Module08/.venv/Scripts/python.exe
   
   # Reinstall dependencies
   pip install -r requirements.txt
   ```

**WebGPU демонстрација:**

1. **WebGPU није подржан:**
   - Ажурирајте на Chrome/Edge 113+
   - Омогућите WebGPU: `chrome://flags/#enable-unsafe-webgpu`
   - Проверите статус GPU-а: `chrome://gpu`
   - Демонстрација ће аутоматски прећи на CPU

2. **Грешке при учитавању модела:**
   - Осигурајте интернет конекцију за преузимање модела
   - Проверите конзолу претраживача за CORS грешке
   - Проверите да ли служите преко HTTP-а (не file://)

**Open WebUI:**

1. **Веза одбијена:**
   ```cmd
   # Check Docker is running
   docker --version
   
   # Check container status
   docker ps | findstr open-webui
   
   # View container logs
   docker logs open-webui
   ```

2. **Модели се не приказују:**
   ```cmd
   # Verify Foundry Local endpoint
   curl http://localhost:51211/v1/models
   
   # Restart Open WebUI
   docker restart open-webui
   ```

### Контролна листа за валидацију

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

## Напредна употреба

### Оптимизација перформанси

**Chainlit:**
- Користите стриминг за бољи перципирани учинак
- Имплементирајте pooling веза за високу конкурентност
- Кеширајте одговоре модела за поновљене упите
- Пратите употребу меморије са великим историјама разговора

**WebGPU:**
- Користите WebGPU за максималну приватност и брзину
- Имплементирајте квантовање модела за мање моделе
- Користите Web Workers за обраду у позадини
- Кеширајте компајлиране моделе у складишту претраживача

**Open WebUI:**
- Користите перзистентне волумене за историју разговора
- Конфигуришите ограничења ресурса за Docker контејнер
- Имплементирајте стратегије резервних копија за корисничке податке
- Поставите реверсни прокси за SSL терминацију

### Шаблони интеграције

**Хибридно Локално/Облак:**
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

**Мултимодални процес:**
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

## Производно распоређивање

### Безбедносни аспекти

- **API кључеви**: Користите променљиве окружења, никада не хардкодирајте
- **Мрежа**: Користите HTTPS у производњи, размотрите VPN за тимски приступ
- **Контрола приступа**: Имплементирајте аутентификацију за Open WebUI
- **Приватност података**: Аудитирајте који подаци остају локални, а који иду у облак
- **Ажурирања**: Одржавајте Foundry Local и контејнере ажурираним

### Надзор и одржавање

- **Провере здравља**: Имплементирајте надзор крајњих тачака
- **Логовање**: Централизујте логове из свих компоненти
- **Метрике**: Пратите време одговора, стопе грешака, употребу ресурса
- **Резервне копије**: Редовно правите резервне копије података о разговорима и конфигурацијама

## Референце и ресурси

### Документација
- [Chainlit документација](https://docs.chainlit.io/) - Комплетан водич за оквир
- [Foundry Local документација](https://learn.microsoft.com/azure/ai-foundry/foundry-local/) - Званична Microsoft документација
- [ONNX Runtime Web](https://onnxruntime.ai/docs/get-started/with-javascript/web.html) - WebGPU интеграција
- [Open WebUI документација](https://docs.openwebui.com/) - Напредна конфигурација

### Пример датотека
- [`app.py`](../../../../../Module08/samples/04/app.py) - Производна Chainlit апликација
- [`chainlit_app.ipynb`](./chainlit_app.ipynb) - Едукативни нотебук
- [`webgpu-demo/`](../../../../../Module08/samples/04/webgpu-demo) - AI инференција у претраживачу
- [`open-webui-guide.md`](./open-webui-guide.md) - Комплетно подешавање Open WebUI

### Повезани примери
- [Документација за сесију 4](../../04.CuttingEdgeModels.md) - Комплетан водич за сесију
- [Foundry Local примери](https://github.com/microsoft/foundry-local/tree/main/samples) - Званични примери

---

**Одрицање од одговорности**:  
Овај документ је преведен помоћу услуге за превођење уз помоћ вештачке интелигенције [Co-op Translator](https://github.com/Azure/co-op-translator). Иако се трудимо да обезбедимо тачност, молимо вас да имате у виду да аутоматски преводи могу садржати грешке или нетачности. Оригинални документ на његовом изворном језику треба сматрати меродавним извором. За критичне информације препоручује се професионални превод од стране људи. Не сносимо одговорност за било каква погрешна тумачења или неспоразуме који могу произаћи из употребе овог превода.