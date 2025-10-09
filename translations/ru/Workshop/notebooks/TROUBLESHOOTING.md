<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "e88a16101de37838f7cf256a9cd0f199",
  "translation_date": "2025-10-09T07:10:25+00:00",
  "source_file": "Workshop/notebooks/TROUBLESHOOTING.md",
  "language_code": "ru"
}
-->
# Рабочие тетради - Руководство по устранению неполадок

## Содержание

- [Общие проблемы и их решения](../../../../Workshop/notebooks)
- [Проблемы, специфичные для сессии 04](../../../../Workshop/notebooks)
- [Проблемы, специфичные для сессии 05](../../../../Workshop/notebooks)
- [Проблемы, специфичные для сессии 06](../../../../Workshop/notebooks)
- [Проблемы, связанные с оборудованием](../../../../Workshop/notebooks)
- [Диагностические команды](../../../../Workshop/notebooks)
- [Получение помощи](../../../../Workshop/notebooks)

---

## Общие проблемы и их решения

### 🔴 CUDA Out of Memory

**Сообщение об ошибке:**
```
CUDA failure 2: out of memory
```

**Причина:** На GPU недостаточно видеопамяти для загрузки модели.

**Решения:**

#### Вариант 1: Использовать CPU-версии (рекомендуется)
```python
# In your notebook, update the CATALOG to use CPU variants
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```

#### Вариант 2: Использовать более компактные модели на GPU
```python
# Use only the smallest model
CATALOG = {
    'qwen2.5-0.5b': {'capabilities':['general','code','summarize','classification'],'priority':1},
}
```

#### Вариант 3: Очистить память GPU
```bash
# Close other GPU-intensive applications
# Check GPU memory usage
nvidia-smi

# Restart Foundry Local service
foundry service stop
foundry service start
```

#### Вариант 4: Увеличить объем памяти GPU (если возможно)
- Закройте вкладки браузера, видеоредакторы или другие приложения, использующие GPU
- Уменьшите визуальные эффекты Windows
- Используйте выделенный GPU, если у вас есть интегрированный и выделенный GPU

---

### 🔴 APIConnectionError: Connection Error

**Сообщение об ошибке:**
```
APIConnectionError: Connection error
[Retry 1/2] Setup failed for 'phi-4-mini': APIConnectionError: Connection error.
```

**Причина:** Служба Foundry Local не запущена или недоступна.

**Решения:**

#### Шаг 1: Проверьте статус службы
```bash
foundry service status
```

#### Шаг 2: Запустите службу, если она остановлена
```bash
foundry service start
```

#### Шаг 3: Проверьте конечную точку
```bash
# Check what port the service is using
foundry service status

# Test with curl (adjust port if different)
curl http://localhost:59959/health
curl http://localhost:55769/health
```

#### Шаг 4: Загрузите необходимые модели
```bash
foundry model run phi-4-mini
foundry model run qwen2.5-3b
foundry model run phi-3.5-mini
```

#### Шаг 5: Перезапустите ядро тетради
После запуска службы и загрузки моделей перезапустите ядро тетради и выполните все ячейки заново.

---

### 🔴 Model Not Found in Catalog

**Сообщение об ошибке:**
```
ValueError: Model phi-3.5-mini-cpu not found in the catalog.
[ERROR] Model 'phi-4-mini' not found in the catalog
```

**Причина:** Модель не загружена или не добавлена в Foundry Local.

**Решения:**

#### Вариант 1: Загрузите и добавьте модели
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

#### Вариант 2: Используйте режим автоматического выбора
Обновите ваш CATALOG, чтобы использовать базовые названия моделей (без суффикса `-cpu`):

```python
CATALOG = {
    'phi-4-mini': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini': {'capabilities':['code','refactor'],'priority':3},
}
```

Foundry Local SDK автоматически выберет лучший вариант (CPU, GPU или NPU) для вашего оборудования.

---

### 🔴 HttpResponseError: 500 - Failed Loading Model

**Сообщение об ошибке:**
```
HttpResponseError: 500 - Failed loading model
```

**Причина:** Файл модели поврежден или несовместим с оборудованием.

**Решения:**

#### Перезагрузите модель
```bash
# Remove corrupted model
foundry model remove phi-3.5-mini

# Download fresh copy
foundry model download phi-3.5-mini
```

#### Используйте другой вариант
```bash
# Try CPU variant instead
foundry model download phi-3.5-mini-cpu
```

---

### 🔴 ImportError: No Module Found

**Сообщение об ошибке:**
```
ModuleNotFoundError: No module named 'foundry_local'
```

**Причина:** Пакет foundry-local-sdk не установлен.

**Решения:**

```bash
# Install SDK
pip install foundry-local-sdk

# Verify installation
pip show foundry-local-sdk
python -c "from foundry_local import FoundryLocalManager; print('SDK OK')"
```

---

### � Медленный первый запрос

**Симптом:** Первое выполнение занимает более 30 секунд, последующие запросы выполняются быстрее.

**Причина:** Это нормальное поведение — служба загружает модель в память при первом запросе.

**Решения:**

#### Предварительная загрузка моделей
```bash
# Download and load all models you'll use before running notebooks
foundry model download phi-4-mini
foundry model download qwen2.5-3b
foundry model download phi-3.5-mini

foundry model run phi-4-mini
foundry model run qwen2.5-3b
```

#### Держите службу запущенной
```bash
# Start service manually and leave it running
foundry service start
```

---

## Проблемы, специфичные для сессии 04

### Неправильная конфигурация порта

**Проблема:** Тетрадь подключается к неправильному порту (55769 вместо 59959 или 57127)

**Решение:**

1. Проверьте, какой порт использует Foundry Local:
```bash
foundry service status
# Note the port number displayed
```

2. Обновите ячейку 10 в тетради:
```python
ENDPOINT = os.getenv('FOUNDRY_LOCAL_ENDPOINT', 'http://localhost:59959/v1')
# Replace 59959 with your actual port
```

3. Перезапустите ядро и выполните ячейки 6, 8, 10, 12, 16, 20, 22

---

### Неправильный выбор модели

**Проблема:** Тетрадь показывает gpt-oss-20b или qwen2.5-7b вместо qwen2.5-3b

**Решение:**

1. Перезапустите ядро тетради (очищает старые переменные)
2. Выполните ячейку 10 (установите псевдонимы моделей)
3. Выполните ячейку 12 (показать конфигурацию)
4. **Проверьте:** Ячейка 12 должна показывать `LLM Model: qwen2.5-3b`

---

### Диагностическая ячейка не работает

**Проблема:** Ячейка 16 показывает "❌ Foundry Local service not found!"

**Решение:**

1. Убедитесь, что служба запущена:
```bash
foundry service status
```

2. Проверьте конечную точку вручную:
```bash
curl http://localhost:59959/v1/models
```

3. Если curl работает, но тетрадь нет:
   - Перезапустите ядро тетради
   - Выполните ячейки в порядке: 6, 8, 10, 12, 14, 16

4. Если curl не работает:
   - Запустите службу: `foundry service start`
   - Загрузите модели: `foundry model run phi-4-mini` и `foundry model run qwen2.5-3b`

---

### Предварительная проверка не проходит

**Проблема:** Ячейка 20 показывает ошибки подключения, хотя диагностика прошла успешно

**Решение:**

1. Проверьте, загружены ли модели:
```bash
foundry model ls
# Should show phi-4-mini and qwen2.5-3b
```

2. Если модели отсутствуют:
```bash
foundry model run phi-4-mini
foundry model run qwen2.5-3b
```

3. Выполните ячейку 20 после загрузки моделей

---

### Сравнение завершается с None

**Проблема:** Ячейка 22 завершается, но показывает задержку как None

**Решение:**

1. Убедитесь, что предварительная проверка прошла (ячейка 20)
2. Выполните ячейку 22 заново — модели могут требовать прогрева при первом запросе
3. Убедитесь, что обе модели загружены: `foundry model ls`

---

## Проблемы, специфичные для сессии 05

### Агент использует неправильную модель

**Проблема:** Агент использует не ту модель, которую ожидали

**Решение:**

Проверьте конфигурацию:
```python
# Check which models are assigned
print(f"Researcher: {researcher.model_id}")
print(f"Editor: {editor.model_id}")
```

Перезапустите ядро, если модели указаны неверно.

---

### Переполнение контекста памяти

**Проблема:** Ответы агента ухудшаются со временем

**Решение:** Уже автоматически обработано — агенты хранят только последние 6 сообщений в памяти.

---

## Проблемы, специфичные для сессии 06

### Путаница между моделями CPU и GPU

**Проблема:** Ошибки CUDA при использовании конфигурации по умолчанию

**Решение:** Конфигурация по умолчанию теперь использует модели для CPU. Если вы видите ошибки CUDA:

1. Убедитесь, что вы используете каталог CPU по умолчанию:
```python
# Cell should show CPU variants
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```

2. Перезапустите ядро и выполните все ячейки заново

---

### Неработающий детектор намерений

**Проблема:** Запросы направляются к неправильным моделям

**Решение:**

Проверьте детектор намерений:
```python
# Run the intent detection test cell
for prompt in test_prompts:
    intent = detect_intent(prompt)
    print(f"{prompt[:50]}... → {intent}")
```

Обновите RULES, если необходимо скорректировать шаблоны.

---

## Проблемы, связанные с оборудованием

### NVIDIA GPU

**Проверка статуса GPU:**
```bash
nvidia-smi
```

**Распространенные проблемы:**
- **Устаревший драйвер:** Обновите драйверы NVIDIA
- **Несоответствие версии CUDA:** Переустановите Foundry Local
- **Фрагментация памяти GPU:** Перезагрузите систему

### Qualcomm NPU

**Проверка статуса NPU:**
```bash
foundry device info
```

**Распространенные проблемы:**
- **Драйверы NPU не установлены:** Установите драйверы Qualcomm NPU
- **Вариант NPU недоступен:** Используйте вариант для CPU
- **Старая версия Windows:** Обновите до последней версии Windows 11

### Системы только с CPU

**Рекомендуемые модели:**
```python
CATALOG = {
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','general'],'priority':2},
}
```

**Советы по производительности:**
- Используйте самые компактные модели
- Уменьшите max_tokens
- Будьте терпеливы при первом запросе

---

## Диагностические команды

### Проверить всё
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

### На Python
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

## Получение помощи

### 1. Проверьте логи
```bash
# Windows
foundry service logs

# Or check Windows Event Viewer
# Application Logs -> Microsoft-FoundryLocal
```

### 2. Вопросы на GitHub
- Ищите существующие вопросы: https://github.com/microsoft/Foundry-Local/issues
- Создайте новый вопрос с:
  - Сообщением об ошибке (полный текст)
  - Выводом команды `foundry service status`
  - Выводом команды `foundry --version`
  - Информацией о GPU/NPU (nvidia-smi и т.д.)
  - Шагами для воспроизведения

### 3. Документация
- **Основной репозиторий:** https://github.com/microsoft/Foundry-Local
- **Python SDK:** https://github.com/microsoft/Foundry-Local/tree/main/sdk/python
- **Справочник CLI:** https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-cli.md
- **Устранение неполадок:** https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-troubleshooting.md

---

## Контрольный список быстрых решений

Когда что-то идет не так, попробуйте следующее по порядку:

- [ ] Проверьте, запущена ли служба: `foundry service status`
- [ ] Перезапустите службу: `foundry service stop && foundry service start`
- [ ] Убедитесь, что модель существует: `foundry model ls | grep phi-4-mini`
- [ ] Загрузите необходимые модели: `foundry model run phi-4-mini`
- [ ] Проверьте память GPU: `nvidia-smi` (если NVIDIA)
- [ ] Попробуйте вариант для CPU: Используйте `phi-4-mini-cpu` вместо `phi-4-mini`
- [ ] Перезапустите ядро тетради
- [ ] Очистите выводы тетради и выполните все ячейки заново
- [ ] Переустановите SDK: `pip install --upgrade --force-reinstall foundry-local-sdk`
- [ ] Перезагрузите систему (в крайнем случае)

---

## Советы по предотвращению проблем

### Лучшие практики

1. **Всегда сначала проверяйте службу:**
   ```bash
   foundry service status
   ```

2. **Используйте варианты для CPU по умолчанию:**
   ```python
   CATALOG = {
       'phi-4-mini-cpu': {...},
       'qwen2.5-0.5b-cpu': {...},
   }
   ```

3. **Предварительно загружайте модели перед запуском тетрадей:**
   ```bash
   foundry model run phi-4-mini
   foundry model run qwen2.5-3b
   ```

4. **Держите службу запущенной:**
   - Не останавливайте/запускайте службу без необходимости
   - Пусть она работает в фоновом режиме между сессиями

5. **Контролируйте ресурсы:**
   - Проверьте память GPU перед запуском
   - Закройте ненужные приложения, использующие GPU
   - Используйте Диспетчер задач / nvidia-smi

6. **Регулярно обновляйтесь:**
   ```bash
   winget upgrade Microsoft.FoundryLocal
   pip install --upgrade foundry-local-sdk
   ```

---

**Последнее обновление:** 8 октября 2025 года

---

**Отказ от ответственности**:  
Этот документ был переведен с помощью сервиса автоматического перевода [Co-op Translator](https://github.com/Azure/co-op-translator). Несмотря на наши усилия обеспечить точность перевода, автоматические переводы могут содержать ошибки или неточности. Оригинальный документ на его родном языке следует считать авторитетным источником. Для получения критически важной информации рекомендуется профессиональный перевод человеком. Мы не несем ответственности за любые недоразумения или неправильные интерпретации, возникшие в результате использования данного перевода.