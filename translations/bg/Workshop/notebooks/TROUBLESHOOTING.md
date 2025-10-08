<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "e88a16101de37838f7cf256a9cd0f199",
  "translation_date": "2025-10-08T14:32:25+00:00",
  "source_file": "Workshop/notebooks/TROUBLESHOOTING.md",
  "language_code": "bg"
}
-->
# Работни тетрадки - Ръководство за отстраняване на проблеми

## Съдържание

- [Често срещани проблеми и решения](../../../../Workshop/notebooks)
- [Проблеми, специфични за сесия 04](../../../../Workshop/notebooks)
- [Проблеми, специфични за сесия 05](../../../../Workshop/notebooks)
- [Проблеми, специфични за сесия 06](../../../../Workshop/notebooks)
- [Проблеми, свързани с хардуера](../../../../Workshop/notebooks)
- [Диагностични команди](../../../../Workshop/notebooks)
- [Получаване на помощ](../../../../Workshop/notebooks)

---

## Често срещани проблеми и решения

### 🔴 CUDA Out of Memory

**Съобщение за грешка:**
```
CUDA failure 2: out of memory
```
  
**Причина:** GPU няма достатъчно VRAM за зареждане на модела.

**Решения:**

#### Опция 1: Използвайте CPU варианти (Препоръчително)
```python
# In your notebook, update the CATALOG to use CPU variants
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```
  
#### Опция 2: Използвайте по-малки модели на GPU
```python
# Use only the smallest model
CATALOG = {
    'qwen2.5-0.5b': {'capabilities':['general','code','summarize','classification'],'priority':1},
}
```
  
#### Опция 3: Изчистете паметта на GPU
```bash
# Close other GPU-intensive applications
# Check GPU memory usage
nvidia-smi

# Restart Foundry Local service
foundry service stop
foundry service start
```
  
#### Опция 4: Увеличете паметта на GPU (ако е възможно)
- Затворете раздели на браузъра, видео редактори или други приложения, използващи GPU
- Намалете визуалните ефекти на Windows
- Използвайте специален GPU, ако имате интегриран + специален

---

### 🔴 APIConnectionError: Connection Error

**Съобщение за грешка:**
```
APIConnectionError: Connection error
[Retry 1/2] Setup failed for 'phi-4-mini': APIConnectionError: Connection error.
```
  
**Причина:** Услугата Foundry Local не работи или не е достъпна.

**Решения:**

#### Стъпка 1: Проверете състоянието на услугата
```bash
foundry service status
```
  
#### Стъпка 2: Стартирайте услугата, ако е спряна
```bash
foundry service start
```
  
#### Стъпка 3: Проверете крайна точка
```bash
# Check what port the service is using
foundry service status

# Test with curl (adjust port if different)
curl http://localhost:59959/health
curl http://localhost:55769/health
```
  
#### Стъпка 4: Заредете необходимите модели
```bash
foundry model run phi-4-mini
foundry model run qwen2.5-3b
foundry model run phi-3.5-mini
```
  
#### Стъпка 5: Рестартирайте ядрото на тетрадката
След стартиране на услугата и зареждане на модели, рестартирайте ядрото на тетрадката и изпълнете всички клетки отново.

---

### 🔴 Model Not Found in Catalog

**Съобщение за грешка:**
```
ValueError: Model phi-3.5-mini-cpu not found in the catalog.
[ERROR] Model 'phi-4-mini' not found in the catalog
```
  
**Причина:** Моделът не е изтеглен или зареден във Foundry Local.

**Решения:**

#### Опция 1: Изтеглете и заредете модели
```bash
# List available models
foundry model ls

# Download the model if not present
foundry model download phi-4-mini
foundry model download qwen2.5-3b
foundry model download phi-3.5-mini

# Load the model into memory
foundry model run phi-4-mini
foundry model run qwen2.5-3b
foundry model run phi-3.5-mini
```
  
#### Опция 2: Използвайте режим на автоматичен избор
Актуализирайте вашия CATALOG, за да използвате основни имена на модели (без суфикса `-cpu`):

```python
CATALOG = {
    'phi-4-mini': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini': {'capabilities':['code','refactor'],'priority':3},
}
```
  
Foundry Local SDK автоматично ще избере най-добрия вариант (CPU, GPU или NPU) за вашия хардуер.

---

### 🔴 HttpResponseError: 500 - Failed Loading Model

**Съобщение за грешка:**
```
HttpResponseError: 500 - Failed loading model
```
  
**Причина:** Файлът на модела е повреден или несъвместим с хардуера.

**Решения:**

#### Презаредете модела
```bash
# Remove corrupted model
foundry model remove phi-3.5-mini

# Download fresh copy
foundry model download phi-3.5-mini
```
  
#### Използвайте различен вариант
```bash
# Try CPU variant instead
foundry model download phi-3.5-mini-cpu
```
  
---

### 🔴 ImportError: No Module Found

**Съобщение за грешка:**
```
ModuleNotFoundError: No module named 'foundry_local'
```
  
**Причина:** Пакетът foundry-local-sdk не е инсталиран.

**Решения:**

```bash
# Install SDK
pip install foundry-local-sdk

# Verify installation
pip show foundry-local-sdk
python -c "from foundry_local import FoundryLocalManager; print('SDK OK')"
```
  
---

### � Бавно първо запитване

**Симптом:** Първото завършване отнема над 30 секунди, следващите запитвания са бързи.

**Причина:** Това е нормално поведение - услугата зарежда модела в паметта при първото запитване.

**Решения:**

#### Предварително заредете модели
```bash
# Download and load all models you'll use before running notebooks
foundry model download phi-4-mini
foundry model download qwen2.5-3b
foundry model download phi-3.5-mini

foundry model run phi-4-mini
foundry model run qwen2.5-3b
```
  
#### Поддържайте услугата активна
```bash
# Start service manually and leave it running
foundry service start
```
  
---

## Проблеми, специфични за сесия 04

### Неправилна конфигурация на порт

**Проблем:** Тетрадката се свързва с грешен порт (55769 вместо 59959 или 57127)

**Решение:**

1. Проверете кой порт използва Foundry Local:
```bash
foundry service status
# Note the port number displayed
```
  
2. Актуализирайте клетка 10 в тетрадката:
```python
ENDPOINT = os.getenv('FOUNDRY_LOCAL_ENDPOINT', 'http://localhost:59959/v1')
# Replace 59959 with your actual port
```
  
3. Рестартирайте ядрото и изпълнете клетки 6, 8, 10, 12, 16, 20, 22

---

### Неправилен избор на модел

**Проблем:** Тетрадката показва gpt-oss-20b или qwen2.5-7b вместо qwen2.5-3b

**Решение:**

1. Рестартирайте ядрото на тетрадката (изчиства старото състояние на променливите)
2. Изпълнете клетка 10 (Задаване на псевдоними на модели)
3. Изпълнете клетка 12 (Показване на конфигурация)
4. **Проверете:** Клетка 12 трябва да показва `LLM Model: qwen2.5-3b`

---

### Диагностичната клетка не работи

**Проблем:** Клетка 16 показва "❌ Foundry Local service not found!"

**Решение:**

1. Проверете дали услугата работи:
```bash
foundry service status
```
  
2. Тествайте крайна точка ръчно:
```bash
curl http://localhost:59959/v1/models
```
  
3. Ако curl работи, но тетрадката не:
   - Рестартирайте ядрото на тетрадката
   - Изпълнете клетките в ред: 6, 8, 10, 12, 14, 16

4. Ако curl не работи:
   - Стартирайте услугата: `foundry service start`
   - Заредете модели: `foundry model run phi-4-mini` и `foundry model run qwen2.5-3b`

---

### Предварителната проверка не успява

**Проблем:** Клетка 20 показва грешки в свързването, въпреки че диагностиката е успешна

**Решение:**

1. Проверете дали моделите са заредени:
```bash
foundry model ls
# Should show phi-4-mini and qwen2.5-3b
```
  
2. Ако моделите липсват:
```bash
foundry model run phi-4-mini
foundry model run qwen2.5-3b
```
  
3. Изпълнете клетка 20 след зареждане на модели

---

### Сравнението не работи с None стойности

**Проблем:** Клетка 22 завършва, но показва латентност като None

**Решение:**

1. Проверете дали предварителната проверка е успешна (Клетка 20)
2. Изпълнете клетка 22 - моделите може да се нуждаят от загряване при първото запитване
3. Проверете дали и двата модела са заредени: `foundry model ls`

---

## Проблеми, специфични за сесия 05

### Агентът използва грешен модел

**Проблем:** Агентът не използва очаквания модел

**Решение:**

Проверете конфигурацията:
```python
# Check which models are assigned
print(f"Researcher: {researcher.model_id}")
print(f"Editor: {editor.model_id}")
```
  
Рестартирайте ядрото, ако моделите са неправилни.

---

### Препълване на контекста на паметта

**Проблем:** Отговорите на агента се влошават с времето

**Решение:** Вече е автоматично обработено - агентите запазват само последните 6 съобщения в паметта.

---

## Проблеми, специфични за сесия 06

### Объркване между CPU и GPU модели

**Проблем:** Получавате CUDA грешки при използване на стандартната конфигурация

**Решение:** Стандартната конфигурация вече използва CPU модели. Ако виждате CUDA грешки:

1. Проверете дали използвате стандартния CPU каталог:
```python
# Cell should show CPU variants
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```
  
2. Рестартирайте ядрото и изпълнете всички клетки отново

---

### Неработещо откриване на намерения

**Проблем:** Подканите се насочват към грешни модели

**Решение:**

Тествайте откриването на намерения:
```python
# Run the intent detection test cell
for prompt in test_prompts:
    intent = detect_intent(prompt)
    print(f"{prompt[:50]}... → {intent}")
```
  
Актуализирайте RULES, ако моделите се нуждаят от корекция.

---

## Проблеми, свързани с хардуера

### NVIDIA GPU

**Проверете състоянието на GPU:**
```bash
nvidia-smi
```
  
**Често срещани проблеми:**
- **Остарял драйвер:** Актуализирайте NVIDIA драйверите
- **Несъответствие на CUDA версията:** Преинсталирайте Foundry Local
- **Фрагментирана памет на GPU:** Рестартирайте системата

### Qualcomm NPU

**Проверете състоянието на NPU:**
```bash
foundry device info
```
  
**Често срещани проблеми:**
- **Драйверите на NPU не са инсталирани:** Инсталирайте Qualcomm NPU драйвери
- **NPU вариантът не е наличен:** Използвайте CPU вариант
- **Твърде стара версия на Windows:** Актуализирайте до последната версия на Windows 11

### Системи само с CPU

**Препоръчителни модели:**
```python
CATALOG = {
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','general'],'priority':2},
}
```
  
**Съвети за производителност:**
- Използвайте най-малките модели
- Намалете max_tokens
- Бъдете търпеливи при първото запитване

---

## Диагностични команди

### Проверете всичко
```bash
# Service status
foundry service status

# List models
foundry model ls

# Device info
foundry device info

# Version info
foundry --version

# Health check
curl http://localhost:55769/health
```
  
### В Python
```python
# Check SDK import
try:
    from foundry_local import FoundryLocalManager
    print('✓ SDK imported')
except ImportError as e:
    print(f'✗ SDK import failed: {e}')

# Check service connectivity
from openai import OpenAI

try:
    client = OpenAI(base_url='http://localhost:59959/v1', api_key='test')
    models = client.models.list()
    print(f'✓ Service reachable, {len(list(models.data))} models available')
except Exception as e:
    print(f'✗ Service not reachable: {e}')
```
  
---

## Получаване на помощ

### 1. Проверете логовете
```bash
# Windows
foundry service logs

# Or check Windows Event Viewer
# Application Logs -> Microsoft-FoundryLocal
```
  
### 2. GitHub Issues
- Търсете съществуващи проблеми: https://github.com/microsoft/Foundry-Local/issues
- Създайте нов проблем с:
  - Съобщение за грешка (пълния текст)
  - Резултат от `foundry service status`
  - Резултат от `foundry --version`
  - Информация за GPU/NPU (nvidia-smi и др.)
  - Стъпки за възпроизвеждане

### 3. Документация
- **Основно хранилище:** https://github.com/microsoft/Foundry-Local
- **Python SDK:** https://github.com/microsoft/Foundry-Local/tree/main/sdk/python
- **CLI референция:** https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-cli.md
- **Отстраняване на проблеми:** https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-troubleshooting.md

---

## Контролен списък за бързи поправки

Когато нещо се обърка, опитайте следните стъпки в ред:

- [ ] Проверете дали услугата работи: `foundry service status`
- [ ] Рестартирайте услугата: `foundry service stop && foundry service start`
- [ ] Проверете дали моделът съществува: `foundry model ls | grep phi-4-mini`
- [ ] Заредете необходимите модели: `foundry model run phi-4-mini`
- [ ] Проверете паметта на GPU: `nvidia-smi` (ако използвате NVIDIA)
- [ ] Опитайте CPU вариант: Използвайте `phi-4-mini-cpu` вместо `phi-4-mini`
- [ ] Рестартирайте ядрото на тетрадката
- [ ] Изчистете изходите на тетрадката и изпълнете всички клетки отново
- [ ] Преинсталирайте SDK: `pip install --upgrade --force-reinstall foundry-local-sdk`
- [ ] Рестартирайте системата (като последна мярка)

---

## Съвети за превенция

### Най-добри практики

1. **Винаги проверявайте услугата първо:**
   ```bash
   foundry service status
   ```
  
2. **Използвайте CPU варианти по подразбиране:**
   ```python
   CATALOG = {
       'phi-4-mini-cpu': {...},
       'qwen2.5-0.5b-cpu': {...},
   }
   ```
  
3. **Предварително заредете модели преди изпълнение на тетрадки:**
   ```bash
   foundry model run phi-4-mini
   foundry model run qwen2.5-3b
   ```
  
4. **Поддържайте услугата активна:**
   - Не спирайте/стартирайте услугата ненужно
   - Оставете я да работи във фонов режим между сесиите

5. **Следете ресурсите:**
   - Проверявайте паметта на GPU преди изпълнение
   - Затваряйте ненужни GPU приложения
   - Използвайте Task Manager / nvidia-smi

6. **Актуализирайте редовно:**
   ```bash
   winget upgrade Microsoft.FoundryLocal
   pip install --upgrade foundry-local-sdk
   ```
  
---

**Последна актуализация:** 8 октомври 2025

---

**Отказ от отговорност**:  
Този документ е преведен с помощта на AI услуга за превод [Co-op Translator](https://github.com/Azure/co-op-translator). Въпреки че се стремим към точност, моля, имайте предвид, че автоматизираните преводи може да съдържат грешки или неточности. Оригиналният документ на неговия роден език трябва да се счита за авторитетен източник. За критична информация се препоръчва професионален човешки превод. Ние не носим отговорност за недоразумения или погрешни интерпретации, произтичащи от използването на този превод.