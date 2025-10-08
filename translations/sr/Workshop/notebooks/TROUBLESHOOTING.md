<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "e88a16101de37838f7cf256a9cd0f199",
  "translation_date": "2025-10-08T14:33:05+00:00",
  "source_file": "Workshop/notebooks/TROUBLESHOOTING.md",
  "language_code": "sr"
}
-->
# Водич за решавање проблема - Радне свеске

## Садржај

- [Уобичајени проблеми и решења](../../../../Workshop/notebooks)
- [Проблеми специфични за сесију 04](../../../../Workshop/notebooks)
- [Проблеми специфични за сесију 05](../../../../Workshop/notebooks)
- [Проблеми специфични за сесију 06](../../../../Workshop/notebooks)
- [Проблеми специфични за хардвер](../../../../Workshop/notebooks)
- [Дијагностичке команде](../../../../Workshop/notebooks)
- [Како добити помоћ](../../../../Workshop/notebooks)

---

## Уобичајени проблеми и решења

### 🔴 CUDA недостатак меморије

**Порука о грешци:**
```
CUDA failure 2: out of memory
```
  
**Основни узрок:** GPU нема довољно VRAM-а за учитавање модела.

**Решења:**

#### Опција 1: Користите CPU варијанте (препоручено)
```python
# In your notebook, update the CATALOG to use CPU variants
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```
  
#### Опција 2: Користите мање моделе на GPU-у
```python
# Use only the smallest model
CATALOG = {
    'qwen2.5-0.5b': {'capabilities':['general','code','summarize','classification'],'priority':1},
}
```
  
#### Опција 3: Очистите GPU меморију
```bash
# Close other GPU-intensive applications
# Check GPU memory usage
nvidia-smi

# Restart Foundry Local service
foundry service stop
foundry service start
```
  
#### Опција 4: Повећајте GPU меморију (ако је могуће)
- Затворите картице у претраживачу, видео едиторе или друге GPU апликације
- Смањите визуелне ефекте у Windows-у
- Користите наменски GPU ако имате интегрисани + наменски

---

### 🔴 APIConnectionError: Грешка у вези

**Порука о грешци:**
```
APIConnectionError: Connection error
[Retry 1/2] Setup failed for 'phi-4-mini': APIConnectionError: Connection error.
```
  
**Основни узрок:** Foundry Local сервис не ради или није доступан.

**Решења:**

#### Корак 1: Проверите статус сервиса
```bash
foundry service status
```
  
#### Корак 2: Покрените сервис ако је заустављен
```bash
foundry service start
```
  
#### Корак 3: Потврдите крајњу тачку
```bash
# Check what port the service is using
foundry service status

# Test with curl (adjust port if different)
curl http://localhost:59959/health
curl http://localhost:55769/health
```
  
#### Корак 4: Учитајте потребне моделе
```bash
foundry model run phi-4-mini
foundry model run qwen2.5-3b
foundry model run phi-3.5-mini
```
  
#### Корак 5: Поново покрените језгро радне свеске
Након покретања сервиса и учитавања модела, поново покрените језгро радне свеске и поново покрените све ћелије.

---

### 🔴 Модел није пронађен у каталогу

**Порука о грешци:**
```
ValueError: Model phi-3.5-mini-cpu not found in the catalog.
[ERROR] Model 'phi-4-mini' not found in the catalog
```
  
**Основни узрок:** Модел није преузет или учитан у Foundry Local.

**Решења:**

#### Опција 1: Преузмите и учитајте моделе
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
  
#### Опција 2: Користите режим аутоматског избора
Ажурирајте свој CATALOG да користи основна имена модела (без суфикса `-cpu`):

```python
CATALOG = {
    'phi-4-mini': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini': {'capabilities':['code','refactor'],'priority':3},
}
```
  
Foundry Local SDK ће аутоматски изабрати најбољу варијанту (CPU, GPU или NPU) за ваш хардвер.

---

### 🔴 HttpResponseError: 500 - Неуспешно учитавање модела

**Порука о грешци:**
```
HttpResponseError: 500 - Failed loading model
```
  
**Основни узрок:** Фајл модела је оштећен или није компатибилан са хардвером.

**Решења:**

#### Поново преузмите модел
```bash
# Remove corrupted model
foundry model remove phi-3.5-mini

# Download fresh copy
foundry model download phi-3.5-mini
```
  
#### Користите другу варијанту
```bash
# Try CPU variant instead
foundry model download phi-3.5-mini-cpu
```
  
---

### 🔴 ImportError: Модул није пронађен

**Порука о грешци:**
```
ModuleNotFoundError: No module named 'foundry_local'
```
  
**Основни узрок:** пакет foundry-local-sdk није инсталиран.

**Решења:**

```bash
# Install SDK
pip install foundry-local-sdk

# Verify installation
pip show foundry-local-sdk
python -c "from foundry_local import FoundryLocalManager; print('SDK OK')"
```
  
---

### � Спора прва захтев

**Симптом:** Прво довршавање траје 30+ секунди, наредни захтеви су брзи.

**Основни узрок:** Ово је нормално понашање - сервис учитава модел у меморију при првом захтеву.

**Решења:**

#### Пре-учитајте моделе
```bash
# Download and load all models you'll use before running notebooks
foundry model download phi-4-mini
foundry model download qwen2.5-3b
foundry model download phi-3.5-mini

foundry model run phi-4-mini
foundry model run qwen2.5-3b
```
  
#### Држите сервис активним
```bash
# Start service manually and leave it running
foundry service start
```
  
---

## Проблеми специфични за сесију 04

### Погрешна конфигурација порта

**Проблем:** Радна свеска се повезује на погрешан порт (55769 уместо 59959 или 57127)

**Решење:**

1. Проверите који порт користи Foundry Local:
```bash
foundry service status
# Note the port number displayed
```
  
2. Ажурирајте ћелију 10 у радној свесци:
```python
ENDPOINT = os.getenv('FOUNDRY_LOCAL_ENDPOINT', 'http://localhost:59959/v1')
# Replace 59959 with your actual port
```
  
3. Поново покрените језгро и поново покрените ћелије 6, 8, 10, 12, 16, 20, 22

---

### Погрешан избор модела

**Проблем:** Радна свеска приказује gpt-oss-20b или qwen2.5-7b уместо qwen2.5-3b

**Решење:**

1. Поново покрените језгро радне свеске (чисти старо стање променљивих)
2. Поново покрените ћелију 10 (Поставите алијасе модела)
3. Поново покрените ћелију 12 (Прикажи конфигурацију)
4. **Потврдите:** Ћелија 12 треба да приказује `LLM Model: qwen2.5-3b`

---

### Дијагностичка ћелија не успева

**Проблем:** Ћелија 16 приказује "❌ Foundry Local сервис није пронађен!"

**Решење:**

1. Потврдите да сервис ради:
```bash
foundry service status
```
  
2. Ручно тестирајте крајњу тачку:
```bash
curl http://localhost:59959/v1/models
```
  
3. Ако curl ради, али радна свеска не:
   - Поново покрените језгро радне свеске
   - Поново покрените ћелије редом: 6, 8, 10, 12, 14, 16

4. Ако curl не ради:
   - Покрените сервис: `foundry service start`
   - Учитајте моделе: `foundry model run phi-4-mini` и `foundry model run qwen2.5-3b`

---

### Провера пре покретања не успева

**Проблем:** Ћелија 20 приказује грешке у вези иако је дијагностика прошла

**Решење:**

1. Проверите да ли су модели учитани:
```bash
foundry model ls
# Should show phi-4-mini and qwen2.5-3b
```
  
2. Ако недостају модели:
```bash
foundry model run phi-4-mini
foundry model run qwen2.5-3b
```
  
3. Поново покрените ћелију 20 након што су модели учитани

---

### Поређење не успева са None вредностима

**Проблем:** Ћелија 22 се завршава, али приказује латенцију као None

**Решење:**

1. Проверите да ли је провера пре покретања прошла (Ћелија 20)
2. Поново покрените ћелију 22 - моделима може бити потребно загревање при првом захтеву
3. Потврдите да су оба модела учитана: `foundry model ls`

---

## Проблеми специфични за сесију 05

### Агент користи погрешан модел

**Проблем:** Агент не користи очекивани модел

**Решење:**

Проверите конфигурацију:
```python
# Check which models are assigned
print(f"Researcher: {researcher.model_id}")
print(f"Editor: {editor.model_id}")
```
  
Поново покрените језгро ако су модели нетачни.

---

### Преливање контекста меморије

**Проблем:** Одговори агента се погоршавају током времена

**Решење:** Већ је аутоматски решено - агенти чувају само последњих 6 порука у меморији.

---

## Проблеми специфични за сесију 06

### Забуна између CPU и GPU модела

**Проблем:** CUDA грешке при коришћењу подразумеване конфигурације

**Решење:** Подразумевана конфигурација сада користи CPU моделе. Ако видите CUDA грешке:

1. Потврдите да користите подразумевани CPU каталог:
```python
# Cell should show CPU variants
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```
  
2. Поново покрените језгро и поново покрените све ћелије

---

### Детекција намере не ради

**Проблем:** Упити се усмеравају на погрешне моделе

**Решење:**

Тестирајте детекцију намере:
```python
# Run the intent detection test cell
for prompt in test_prompts:
    intent = detect_intent(prompt)
    print(f"{prompt[:50]}... → {intent}")
```
  
Ажурирајте RULES ако је потребно прилагодити шаблоне.

---

## Проблеми специфични за хардвер

### NVIDIA GPU

**Проверите статус GPU-а:**
```bash
nvidia-smi
```
  
**Уобичајени проблеми:**
- **Застарели драјвери:** Ажурирајте NVIDIA драјвере
- **Неслагање CUDA верзије:** Поново инсталирајте Foundry Local
- **Фрагментирана меморија GPU-а:** Поново покрените систем

### Qualcomm NPU

**Проверите статус NPU-а:**
```bash
foundry device info
```
  
**Уобичајени проблеми:**
- **NPU драјвери нису инсталирани:** Инсталирајте Qualcomm NPU драјвере
- **NPU варијанта није доступна:** Користите CPU варијанту
- **Превише стара верзија Windows-а:** Ажурирајте на најновији Windows 11

### Системи само са CPU-ом

**Препоручени модели:**
```python
CATALOG = {
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','general'],'priority':2},
}
```
  
**Савети за перформансе:**
- Користите најмање моделе
- Смањите max_tokens
- Повећајте стрпљење за први захтев

---

## Дијагностичке команде

### Проверите све
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
  
### У Python-у
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

## Како добити помоћ

### 1. Проверите логове
```bash
# Windows
foundry service logs

# Or check Windows Event Viewer
# Application Logs -> Microsoft-FoundryLocal
```
  
### 2. GitHub Issues
- Претражите постојеће проблеме: https://github.com/microsoft/Foundry-Local/issues
- Креирајте нови проблем са:
  - Поруком о грешци (цели текст)
  - Излазом команде `foundry service status`
  - Излазом команде `foundry --version`
  - Информацијама о GPU/NPU (nvidia-smi, итд.)
  - Корацима за репродукцију

### 3. Документација
- **Главни репозиторијум:** https://github.com/microsoft/Foundry-Local
- **Python SDK:** https://github.com/microsoft/Foundry-Local/tree/main/sdk/python
- **CLI референца:** https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-cli.md
- **Решавање проблема:** https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-troubleshooting.md

---

## Контролна листа за брза решења

Када нешто крене наопако, пробајте следеће редом:

- [ ] Проверите да ли сервис ради: `foundry service status`
- [ ] Поново покрените сервис: `foundry service stop && foundry service start`
- [ ] Потврдите да модел постоји: `foundry model ls | grep phi-4-mini`
- [ ] Учитајте потребне моделе: `foundry model run phi-4-mini`
- [ ] Проверите меморију GPU-а: `nvidia-smi` (ако користите NVIDIA)
- [ ] Пробајте CPU варијанту: Користите `phi-4-mini-cpu` уместо `phi-4-mini`
- [ ] Поново покрените језгро радне свеске
- [ ] Очистите излазе радне свеске и поново покрените све ћелије
- [ ] Поново инсталирајте SDK: `pip install --upgrade --force-reinstall foundry-local-sdk`
- [ ] Поново покрените систем (као последње решење)

---

## Савети за превенцију

### Најбоље праксе

1. **Увек прво проверите сервис:**
   ```bash
   foundry service status
   ```
  
2. **Користите CPU варијанте по подразумеваном подешавању:**
   ```python
   CATALOG = {
       'phi-4-mini-cpu': {...},
       'qwen2.5-0.5b-cpu': {...},
   }
   ```
  
3. **Пре-учитајте моделе пре покретања радних свески:**
   ```bash
   foundry model run phi-4-mini
   foundry model run qwen2.5-3b
   ```
  
4. **Држите сервис активним:**
   - Не заустављајте/покрећите сервис непотребно
   - Нека ради у позадини између сесија

5. **Пратите ресурсе:**
   - Проверите меморију GPU-а пре покретања
   - Затворите непотребне GPU апликације
   - Користите Task Manager / nvidia-smi

6. **Ажурирајте редовно:**
   ```bash
   winget upgrade Microsoft.FoundryLocal
   pip install --upgrade foundry-local-sdk
   ```
  
---

**Последње ажурирање:** 8. октобар 2025.

---

**Одрицање од одговорности**:  
Овај документ је преведен помоћу услуге за превођење уз помоћ вештачке интелигенције [Co-op Translator](https://github.com/Azure/co-op-translator). Иако настојимо да обезбедимо тачност, молимо вас да имате у виду да аутоматски преводи могу садржати грешке или нетачности. Оригинални документ на његовом изворном језику треба сматрати меродавним извором. За критичне информације препоручује се професионални превод од стране људи. Не преузимамо одговорност за било каква погрешна тумачења или неспоразуме који могу настати услед коришћења овог превода.