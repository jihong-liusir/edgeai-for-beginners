<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "e88a16101de37838f7cf256a9cd0f199",
  "translation_date": "2025-10-08T12:29:56+00:00",
  "source_file": "Workshop/notebooks/TROUBLESHOOTING.md",
  "language_code": "uk"
}
-->
# Зошити для воркшопу - Посібник з усунення несправностей

## Зміст

- [Поширені проблеми та їх вирішення](../../../../Workshop/notebooks)
- [Проблеми, специфічні для сесії 04](../../../../Workshop/notebooks)
- [Проблеми, специфічні для сесії 05](../../../../Workshop/notebooks)
- [Проблеми, специфічні для сесії 06](../../../../Workshop/notebooks)
- [Проблеми, пов'язані з обладнанням](../../../../Workshop/notebooks)
- [Діагностичні команди](../../../../Workshop/notebooks)
- [Отримання допомоги](../../../../Workshop/notebooks)

---

## Поширені проблеми та їх вирішення

### 🔴 CUDA Out of Memory

**Повідомлення про помилку:**
```
CUDA failure 2: out of memory
```

**Причина:** GPU не має достатньо VRAM для завантаження моделі.

**Рішення:**

#### Варіант 1: Використовувати варіанти для CPU (рекомендовано)
```python
# In your notebook, update the CATALOG to use CPU variants
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```

#### Варіант 2: Використовувати менші моделі на GPU
```python
# Use only the smallest model
CATALOG = {
    'qwen2.5-0.5b': {'capabilities':['general','code','summarize','classification'],'priority':1},
}
```

#### Варіант 3: Очистити пам'ять GPU
```bash
# Close other GPU-intensive applications
# Check GPU memory usage
nvidia-smi

# Restart Foundry Local service
foundry service stop
foundry service start
```

#### Варіант 4: Збільшити пам'ять GPU (якщо можливо)
- Закрийте вкладки браузера, відеоредактори або інші програми, що використовують GPU
- Зменшіть візуальні ефекти Windows
- Використовуйте виділений GPU, якщо у вас є інтегрований + виділений

---

### 🔴 APIConnectionError: Connection Error

**Повідомлення про помилку:**
```
APIConnectionError: Connection error
[Retry 1/2] Setup failed for 'phi-4-mini': APIConnectionError: Connection error.
```

**Причина:** Сервіс Foundry Local не працює або недоступний.

**Рішення:**

#### Крок 1: Перевірте статус сервісу
```bash
foundry service status
```

#### Крок 2: Запустіть сервіс, якщо він зупинений
```bash
foundry service start
```

#### Крок 3: Перевірте кінцеву точку
```bash
# Check what port the service is using
foundry service status

# Test with curl (adjust port if different)
curl http://localhost:59959/health
curl http://localhost:55769/health
```

#### Крок 4: Завантажте необхідні моделі
```bash
foundry model run phi-4-mini
foundry model run qwen2.5-3b
foundry model run phi-3.5-mini
```

#### Крок 5: Перезапустіть ядро зошита
Після запуску сервісу та завантаження моделей перезапустіть ядро зошита та виконайте всі клітинки заново.

---

### 🔴 Model Not Found in Catalog

**Повідомлення про помилку:**
```
ValueError: Model phi-3.5-mini-cpu not found in the catalog.
[ERROR] Model 'phi-4-mini' not found in the catalog
```

**Причина:** Модель не завантажена або не активована у Foundry Local.

**Рішення:**

#### Варіант 1: Завантажте та активуйте моделі
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

#### Варіант 2: Використовуйте режим автоматичного вибору
Оновіть ваш CATALOG, щоб використовувати базові назви моделей (без суфікса `-cpu`):

```python
CATALOG = {
    'phi-4-mini': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini': {'capabilities':['code','refactor'],'priority':3},
}
```

Foundry Local SDK автоматично вибере найкращий варіант (CPU, GPU або NPU) для вашого обладнання.

---

### 🔴 HttpResponseError: 500 - Failed Loading Model

**Повідомлення про помилку:**
```
HttpResponseError: 500 - Failed loading model
```

**Причина:** Файл моделі пошкоджений або несумісний з обладнанням.

**Рішення:**

#### Перезавантажте модель
```bash
# Remove corrupted model
foundry model remove phi-3.5-mini

# Download fresh copy
foundry model download phi-3.5-mini
```

#### Використовуйте інший варіант
```bash
# Try CPU variant instead
foundry model download phi-3.5-mini-cpu
```

---

### 🔴 ImportError: No Module Found

**Повідомлення про помилку:**
```
ModuleNotFoundError: No module named 'foundry_local'
```

**Причина:** Пакет foundry-local-sdk не встановлений.

**Рішення:**

```bash
# Install SDK
pip install foundry-local-sdk

# Verify installation
pip show foundry-local-sdk
python -c "from foundry_local import FoundryLocalManager; print('SDK OK')"
```

---

### � Повільний перший запит

**Симптом:** Перше завершення займає понад 30 секунд, наступні запити виконуються швидко.

**Причина:** Це нормальна поведінка - сервіс завантажує модель у пам'ять під час першого запиту.

**Рішення:**

#### Попередньо завантажте моделі
```bash
# Download and load all models you'll use before running notebooks
foundry model download phi-4-mini
foundry model download qwen2.5-3b
foundry model download phi-3.5-mini

foundry model run phi-4-mini
foundry model run qwen2.5-3b
```

#### Тримайте сервіс активним
```bash
# Start service manually and leave it running
foundry service start
```

---

## Проблеми, специфічні для сесії 04

### Неправильна конфігурація порту

**Проблема:** Зошит підключається до неправильного порту (55769 vs 59959 vs 57127)

**Рішення:**

1. Перевірте, який порт використовує Foundry Local:
```bash
foundry service status
# Note the port number displayed
```

2. Оновіть клітинку 10 у зошиті:
```python
ENDPOINT = os.getenv('FOUNDRY_LOCAL_ENDPOINT', 'http://localhost:59959/v1')
# Replace 59959 with your actual port
```

3. Перезапустіть ядро та виконайте клітинки 6, 8, 10, 12, 16, 20, 22

---

### Неправильний вибір моделі

**Проблема:** Зошит показує gpt-oss-20b або qwen2.5-7b замість qwen2.5-3b

**Рішення:**

1. Перезапустіть ядро зошита (очищує старий стан змінних)
2. Виконайте клітинку 10 (Встановлення псевдонімів моделі)
3. Виконайте клітинку 12 (Відображення конфігурації)
4. **Перевірте:** Клітинка 12 повинна показувати `LLM Model: qwen2.5-3b`

---

### Діагностична клітинка не працює

**Проблема:** Клітинка 16 показує "❌ Foundry Local service not found!"

**Рішення:**

1. Перевірте, чи сервіс працює:
```bash
foundry service status
```

2. Перевірте кінцеву точку вручну:
```bash
curl http://localhost:59959/v1/models
```

3. Якщо curl працює, але зошит не працює:
   - Перезапустіть ядро зошита
   - Виконайте клітинки у порядку: 6, 8, 10, 12, 14, 16

4. Якщо curl не працює:
   - Запустіть сервіс: `foundry service start`
   - Завантажте моделі: `foundry model run phi-4-mini` та `foundry model run qwen2.5-3b`

---

### Перевірка перед запуском не вдалася

**Проблема:** Клітинка 20 показує помилки з'єднання, хоча діагностика пройшла успішно

**Рішення:**

1. Перевірте, чи моделі завантажені:
```bash
foundry model ls
# Should show phi-4-mini and qwen2.5-3b
```

2. Якщо моделі відсутні:
```bash
foundry model run phi-4-mini
foundry model run qwen2.5-3b
```

3. Виконайте клітинку 20 після завантаження моделей

---

### Порівняння не працює через значення None

**Проблема:** Клітинка 22 завершується, але показує затримку як None

**Рішення:**

1. Перевірте, чи перевірка перед запуском пройшла успішно (Клітинка 20)
2. Виконайте клітинку 22 ще раз - моделі можуть потребувати прогрівання під час першого запиту
3. Перевірте, чи обидві моделі завантажені: `foundry model ls`

---

## Проблеми, специфічні для сесії 05

### Агент використовує неправильну модель

**Проблема:** Агент не використовує очікувану модель

**Рішення:**

Перевірте конфігурацію:
```python
# Check which models are assigned
print(f"Researcher: {researcher.model_id}")
print(f"Editor: {editor.model_id}")
```

Перезапустіть ядро, якщо моделі неправильні.

---

### Переповнення контексту пам'яті

**Проблема:** Відповіді агента погіршуються з часом

**Рішення:** Вже автоматично вирішено - агенти зберігають лише останні 6 повідомлень у пам'яті.

---

## Проблеми, специфічні для сесії 06

### Плутанина між моделями для CPU та GPU

**Проблема:** Помилки CUDA при використанні конфігурації за замовчуванням

**Рішення:** Конфігурація за замовчуванням тепер використовує моделі для CPU. Якщо ви бачите помилки CUDA:

1. Перевірте, чи ви використовуєте каталог для CPU за замовчуванням:
```python
# Cell should show CPU variants
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```

2. Перезапустіть ядро та виконайте всі клітинки заново

---

### Неправильне визначення намірів

**Проблема:** Запити спрямовуються до неправильних моделей

**Рішення:**

Перевірте визначення намірів:
```python
# Run the intent detection test cell
for prompt in test_prompts:
    intent = detect_intent(prompt)
    print(f"{prompt[:50]}... → {intent}")
```

Оновіть RULES, якщо шаблони потребують коригування.

---

## Проблеми, пов'язані з обладнанням

### NVIDIA GPU

**Перевірте статус GPU:**
```bash
nvidia-smi
```

**Поширені проблеми:**
- **Застарілий драйвер:** Оновіть драйвери NVIDIA
- **Невідповідність версії CUDA:** Перевстановіть Foundry Local
- **Фрагментація пам'яті GPU:** Перезавантажте систему

### Qualcomm NPU

**Перевірте статус NPU:**
```bash
foundry device info
```

**Поширені проблеми:**
- **Драйвери NPU не встановлені:** Встановіть драйвери Qualcomm NPU
- **Варіант NPU недоступний:** Використовуйте варіант для CPU
- **Застаріла версія Windows:** Оновіть до останньої версії Windows 11

### Системи лише з CPU

**Рекомендовані моделі:**
```python
CATALOG = {
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','general'],'priority':2},
}
```

**Поради щодо продуктивності:**
- Використовуйте найменші моделі
- Зменшіть max_tokens
- Збільшіть терпіння для першого запиту

---

## Діагностичні команди

### Перевірте все
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

### У Python
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

## Отримання допомоги

### 1. Перевірте журнали
```bash
# Windows
foundry service logs

# Or check Windows Event Viewer
# Application Logs -> Microsoft-FoundryLocal
```

### 2. Проблеми на GitHub
- Шукайте існуючі проблеми: https://github.com/microsoft/Foundry-Local/issues
- Створіть нову проблему, додавши:
  - Повідомлення про помилку (повний текст)
  - Вивід `foundry service status`
  - Вивід `foundry --version`
  - Інформацію про GPU/NPU (nvidia-smi тощо)
  - Кроки для відтворення

### 3. Документація
- **Основний репозиторій:** https://github.com/microsoft/Foundry-Local
- **Python SDK:** https://github.com/microsoft/Foundry-Local/tree/main/sdk/python
- **Довідник CLI:** https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-cli.md
- **Усунення несправностей:** https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-troubleshooting.md

---

## Контрольний список швидких виправлень

Коли щось йде не так, спробуйте наступне по черзі:

- [ ] Перевірте, чи сервіс працює: `foundry service status`
- [ ] Перезапустіть сервіс: `foundry service stop && foundry service start`
- [ ] Перевірте, чи модель існує: `foundry model ls | grep phi-4-mini`
- [ ] Завантажте необхідні моделі: `foundry model run phi-4-mini`
- [ ] Перевірте пам'ять GPU: `nvidia-smi` (якщо NVIDIA)
- [ ] Спробуйте варіант для CPU: Використовуйте `phi-4-mini-cpu` замість `phi-4-mini`
- [ ] Перезапустіть ядро зошита
- [ ] Очистіть виводи зошита та виконайте всі клітинки заново
- [ ] Перевстановіть SDK: `pip install --upgrade --force-reinstall foundry-local-sdk`
- [ ] Перезавантажте систему (як останній засіб)

---

## Поради щодо запобігання проблемам

### Найкращі практики

1. **Завжди перевіряйте сервіс спочатку:**
   ```bash
   foundry service status
   ```

2. **Використовуйте варіанти для CPU за замовчуванням:**
   ```python
   CATALOG = {
       'phi-4-mini-cpu': {...},
       'qwen2.5-0.5b-cpu': {...},
   }
   ```

3. **Попередньо завантажуйте моделі перед запуском зошитів:**
   ```bash
   foundry model run phi-4-mini
   foundry model run qwen2.5-3b
   ```

4. **Тримайте сервіс активним:**
   - Не зупиняйте/запускайте сервіс без необхідності
   - Дозвольте йому працювати у фоновому режимі між сесіями

5. **Моніторьте ресурси:**
   - Перевіряйте пам'ять GPU перед запуском
   - Закривайте непотрібні програми, що використовують GPU
   - Використовуйте Диспетчер завдань / nvidia-smi

6. **Оновлюйте регулярно:**
   ```bash
   winget upgrade Microsoft.FoundryLocal
   pip install --upgrade foundry-local-sdk
   ```

---

**Останнє оновлення:** 8 жовтня 2025 року

---

**Відмова від відповідальності**:  
Цей документ був перекладений за допомогою сервісу автоматичного перекладу [Co-op Translator](https://github.com/Azure/co-op-translator). Хоча ми прагнемо до точності, будь ласка, майте на увазі, що автоматичні переклади можуть містити помилки або неточності. Оригінальний документ на його рідній мові слід вважати авторитетним джерелом. Для критичної інформації рекомендується професійний людський переклад. Ми не несемо відповідальності за будь-які непорозуміння або неправильні тлумачення, що виникають внаслідок використання цього перекладу.