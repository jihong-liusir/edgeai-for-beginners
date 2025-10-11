<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "e88a16101de37838f7cf256a9cd0f199",
  "translation_date": "2025-10-11T12:08:03+00:00",
  "source_file": "Workshop/notebooks/TROUBLESHOOTING.md",
  "language_code": "ta"
}
-->
# வொர்க்ஷாப் நோட்புக் - பிரச்சினைகளை சரிசெய்யும் வழிகாட்டி

## உள்ளடக்க அட்டவணை

- [பொதுவான பிரச்சினைகள் மற்றும் தீர்வுகள்](../../../../Workshop/notebooks)
- [அமர்வு 04 குறிப்பிட்ட பிரச்சினைகள்](../../../../Workshop/notebooks)
- [அமர்வு 05 குறிப்பிட்ட பிரச்சினைகள்](../../../../Workshop/notebooks)
- [அமர்வு 06 குறிப்பிட்ட பிரச்சினைகள்](../../../../Workshop/notebooks)
- [ஹார்ட்வேருக்கு தொடர்பான பிரச்சினைகள்](../../../../Workshop/notebooks)
- [டயக்னோஸ்டிக் கட்டளைகள்](../../../../Workshop/notebooks)
- [உதவி பெறுதல்](../../../../Workshop/notebooks)

---

## பொதுவான பிரச்சினைகள் மற்றும் தீர்வுகள்

### 🔴 CUDA நினைவகம் இல்லை

**பிழை செய்தி:**
```
CUDA failure 2: out of memory
```

**மூல காரணம்:** GPU-க்கு மாடலை ஏற்ற VRAM போதுமான அளவில் இல்லை.

**தீர்வுகள்:**

#### விருப்பம் 1: CPU மாறுபாடுகளை பயன்படுத்தவும் (பரிந்துரைக்கப்படுகிறது)
```python
# In your notebook, update the CATALOG to use CPU variants
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```

#### விருப்பம் 2: GPU-வில் சிறிய மாடல்களை பயன்படுத்தவும்
```python
# Use only the smallest model
CATALOG = {
    'qwen2.5-0.5b': {'capabilities':['general','code','summarize','classification'],'priority':1},
}
```

#### விருப்பம் 3: GPU நினைவகத்தை அழிக்கவும்
```bash
# Close other GPU-intensive applications
# Check GPU memory usage
nvidia-smi

# Restart Foundry Local service
foundry service stop
foundry service start
```

#### விருப்பம் 4: GPU நினைவகத்தை அதிகரிக்கவும் (சாத்தியமானால்)
- உலாவி தாவல்கள், வீடியோ எடிட்டர்கள் அல்லது பிற GPU பயன்பாடுகளை மூடவும்
- Windows காட்சித் தோற்றங்களை குறைக்கவும்
- ஒருங்கிணைந்த + தனித்துவமான GPU இருந்தால், தனித்துவமான GPU-வை பயன்படுத்தவும்

---

### 🔴 APIConnectionError: இணைப்பு பிழை

**பிழை செய்தி:**
```
APIConnectionError: Connection error
[Retry 1/2] Setup failed for 'phi-4-mini': APIConnectionError: Connection error.
```

**மூல காரணம்:** Foundry Local சேவை இயங்கவில்லை அல்லது அணுக முடியவில்லை.

**தீர்வுகள்:**

#### படி 1: சேவை நிலையை சரிபார்க்கவும்
```bash
foundry service status
```

#### படி 2: சேவை நிறுத்தப்பட்டிருந்தால் தொடங்கவும்
```bash
foundry service start
```

#### படி 3: இறுதிப்புள்ளியை சரிபார்க்கவும்
```bash
# Check what port the service is using
foundry service status

# Test with curl (adjust port if different)
curl http://localhost:59959/health
curl http://localhost:55769/health
```

#### படி 4: தேவையான மாடல்களை ஏற்றவும்
```bash
foundry model run phi-4-mini
foundry model run qwen2.5-3b
foundry model run phi-3.5-mini
```

#### படி 5: நோட்புக் கர்னலை மீண்டும் தொடங்கவும்
சேவையை தொடங்கி மாடல்களை ஏற்றிய பிறகு, நோட்புக் கர்னலை மீண்டும் தொடங்கி அனைத்து செல்களையும் மீண்டும் இயக்கவும்.

---

### 🔴 மாடல் பட்டியலில் காணப்படவில்லை

**பிழை செய்தி:**
```
ValueError: Model phi-3.5-mini-cpu not found in the catalog.
[ERROR] Model 'phi-4-mini' not found in the catalog
```

**மூல காரணம்:** மாடல் பதிவிறக்கம் செய்யப்படவில்லை அல்லது Foundry Local-ல் ஏற்றப்படவில்லை.

**தீர்வுகள்:**

#### விருப்பம் 1: மாடல்களை பதிவிறக்கம் செய்து ஏற்றவும்
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

#### விருப்பம் 2: தானியங்கி தேர்வு முறையை பயன்படுத்தவும்
உங்கள் CATALOG-ஐ அடிப்படை மாடல் பெயர்களைப் பயன்படுத்த புதுப்பிக்கவும் (`-cpu` பின்வெட்டியை இல்லாமல்):

```python
CATALOG = {
    'phi-4-mini': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini': {'capabilities':['code','refactor'],'priority':3},
}
```

Foundry Local SDK உங்கள் ஹார்ட்வேருக்கு சிறந்த மாறுபாட்டை (CPU, GPU, அல்லது NPU) தானாகவே தேர்ந்தெடுக்கும்.

---

### 🔴 HttpResponseError: 500 - மாடலை ஏற்றுவதில் தோல்வி

**பிழை செய்தி:**
```
HttpResponseError: 500 - Failed loading model
```

**மூல காரணம்:** மாடல் கோப்பு சேதமடைந்தது அல்லது ஹார்ட்வேருடன் பொருந்தவில்லை.

**தீர்வுகள்:**

#### மாடலை மீண்டும் பதிவிறக்கவும்
```bash
# Remove corrupted model
foundry model remove phi-3.5-mini

# Download fresh copy
foundry model download phi-3.5-mini
```

#### வேறு மாறுபாட்டைப் பயன்படுத்தவும்
```bash
# Try CPU variant instead
foundry model download phi-3.5-mini-cpu
```

---

### 🔴 ImportError: எந்த மாட்யூலும் காணப்படவில்லை

**பிழை செய்தி:**
```
ModuleNotFoundError: No module named 'foundry_local'
```

**மூல காரணம்:** foundry-local-sdk தொகுப்பு நிறுவப்படவில்லை.

**தீர்வுகள்:**

```bash
# Install SDK
pip install foundry-local-sdk

# Verify installation
pip show foundry-local-sdk
python -c "from foundry_local import FoundryLocalManager; print('SDK OK')"
```

---

### � முதல் கோரிக்கை மெதுவாக உள்ளது

**அறிகுறி:** முதல் முடிவு 30+ விநாடிகள் ஆகிறது, அதற்குப் பிறகு கோரிக்கைகள் வேகமாக உள்ளன.

**மூல காரணம்:** இது சாதாரணமாக உள்ளது - சேவை முதல் கோரிக்கையில் மாடலை நினைவகத்தில் ஏற்றுகிறது.

**தீர்வுகள்:**

#### மாடல்களை முன்கூட்டியே ஏற்றவும்
```bash
# Download and load all models you'll use before running notebooks
foundry model download phi-4-mini
foundry model download qwen2.5-3b
foundry model download phi-3.5-mini

foundry model run phi-4-mini
foundry model run qwen2.5-3b
```

#### சேவையை இயக்கவிடவும்
```bash
# Start service manually and leave it running
foundry service start
```

---

## அமர்வு 04 குறிப்பிட்ட பிரச்சினைகள்

### தவறான போர்ட் கட்டமைப்பு

**பிரச்சினை:** நோட்புக் தவறான போர்ட்டுடன் இணைக்கிறது (55769 vs 59959 vs 57127)

**தீர்வு:**

1. Foundry Local எந்த போர்ட்டைப் பயன்படுத்துகிறது என்பதை சரிபார்க்கவும்:
```bash
foundry service status
# Note the port number displayed
```

2. நோட்புக்கில் செல்கள் 10-ஐ புதுப்பிக்கவும்:
```python
ENDPOINT = os.getenv('FOUNDRY_LOCAL_ENDPOINT', 'http://localhost:59959/v1')
# Replace 59959 with your actual port
```

3. கர்னலை மீண்டும் தொடங்கி செல்கள் 6, 8, 10, 12, 16, 20, 22-ஐ மீண்டும் இயக்கவும்

---

### தவறான மாடல் தேர்வு

**பிரச்சினை:** நோட்புக் gpt-oss-20b அல்லது qwen2.5-7b-ஐ காட்டுகிறது qwen2.5-3b-க்கு பதிலாக

**தீர்வு:**

1. நோட்புக் கர்னலை மீண்டும் தொடங்கவும் (பழைய மாறி நிலையை அழிக்கிறது)
2. செல்கள் 10-ஐ மீண்டும் இயக்கவும் (மாடல் அலியாஸ்களை அமைக்கவும்)
3. செல்கள் 12-ஐ மீண்டும் இயக்கவும் (கட்டமைப்பை காட்டவும்)
4. **சரிபார்க்கவும்:** செல்கள் 12 `LLM Model: qwen2.5-3b` என்பதை காட்ட வேண்டும்

---

### டயக்னோஸ்டிக் செல்கள் தோல்வி

**பிரச்சினை:** செல்கள் 16 "❌ Foundry Local service not found!" என்று காட்டுகிறது

**தீர்வு:**

1. சேவை இயங்குகிறதா என்பதை சரிபார்க்கவும்:
```bash
foundry service status
```

2. இறுதிப்புள்ளியை கையேடு மூலம் சோதிக்கவும்:
```bash
curl http://localhost:59959/v1/models
```

3. curl வேலை செய்கிறது ஆனால் நோட்புக் வேலை செய்யவில்லை என்றால்:
   - நோட்புக் கர்னலை மீண்டும் தொடங்கவும்
   - செல்களை வரிசையாக மீண்டும் இயக்கவும்: 6, 8, 10, 12, 14, 16

4. curl தோல்வியடைந்தால்:
   - சேவையை தொடங்கவும்: `foundry service start`
   - மாடல்களை ஏற்றவும்: `foundry model run phi-4-mini` மற்றும் `foundry model run qwen2.5-3b`

---

### முன்-பறக்க சோதனை தோல்வி

**பிரச்சினை:** செல்கள் 20 இணைப்பு பிழைகளை காட்டுகிறது, டயக்னோஸ்டிக் பாஸ் ஆனாலும்

**தீர்வு:**

1. மாடல்கள் ஏற்றப்பட்டுள்ளனவா என்பதை சரிபார்க்கவும்:
```bash
foundry model ls
# Should show phi-4-mini and qwen2.5-3b
```

2. மாடல்கள் காணப்படவில்லை என்றால்:
```bash
foundry model run phi-4-mini
foundry model run qwen2.5-3b
```

3. மாடல்கள் ஏற்றப்பட்ட பிறகு செல்கள் 20-ஐ மீண்டும் இயக்கவும்

---

### ஒப்பீடு None மதிப்புகளுடன் தோல்வி

**பிரச்சினை:** செல்கள் 22 முடிவடைகிறது ஆனால் latency None என்று காட்டுகிறது

**தீர்வு:**

1. முதலில் முன்-பறக்க பாஸ் ஆனதா என்பதை சரிபார்க்கவும் (செல்கள் 20)
2. செல்கள் 22-ஐ மீண்டும் இயக்கவும் - மாடல்கள் முதல் கோரிக்கையில் சூடுபிடிக்க தேவைப்படலாம்
3. இரு மாடல்களும் ஏற்றப்பட்டுள்ளனவா என்பதை சரிபார்க்கவும்: `foundry model ls`

---

## அமர்வு 05 குறிப்பிட்ட பிரச்சினைகள்

### ஏஜென்ட் தவறான மாடலைப் பயன்படுத்துகிறது

**பிரச்சினை:** ஏஜென்ட் எதிர்பார்க்கப்பட்ட மாடலைப் பயன்படுத்தவில்லை

**தீர்வு:**

கட்டமைப்பை சரிபார்க்கவும்:
```python
# Check which models are assigned
print(f"Researcher: {researcher.model_id}")
print(f"Editor: {editor.model_id}")
```

மாடல்கள் தவறாக இருந்தால் கர்னலை மீண்டும் தொடங்கவும்.

---

### நினைவக சூழல் அதிகப்படுத்தல்

**பிரச்சினை:** ஏஜென்ட் பதில்கள் காலப்போக்கில் குறைவாக உள்ளன

**தீர்வு:** இது தானாகவே கையாளப்படுகிறது - ஏஜென்ட்கள் நினைவகத்தில் கடைசி 6 செய்திகளை மட்டுமே வைத்திருக்கின்றன.

---

## அமர்வு 06 குறிப்பிட்ட பிரச்சினைகள்

### CPU vs GPU மாடல் குழப்பம்

**பிரச்சினை:** இயல்புநிலை கட்டமைப்பைப் பயன்படுத்தும்போது CUDA பிழைகள் ஏற்படுகின்றன

**தீர்வு:** இயல்புநிலை கட்டமைப்பு தற்போது CPU மாடல்களைப் பயன்படுத்துகிறது. நீங்கள் CUDA பிழைகளைப் பார்க்கிறீர்கள் என்றால்:

1. நீங்கள் இயல்புநிலை CPU பட்டியலைப் பயன்படுத்துகிறீர்களா என்பதை சரிபார்க்கவும்:
```python
# Cell should show CPU variants
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```

2. கர்னலை மீண்டும் தொடங்கி அனைத்து செல்களையும் மீண்டும் இயக்கவும்

---

### நோக்கத்தை கண்டறிதல் வேலை செய்யவில்லை

**பிரச்சினை:** கேள்விகள் தவறான மாடல்களுக்கு அனுப்பப்படுகின்றன

**தீர்வு:**

நோக்கத்தை கண்டறிதலை சோதிக்கவும்:
```python
# Run the intent detection test cell
for prompt in test_prompts:
    intent = detect_intent(prompt)
    print(f"{prompt[:50]}... → {intent}")
```

முறைகள் சரிசெய்ய தேவைப்பட்டால் RULES-ஐ புதுப்பிக்கவும்.

---

## ஹார்ட்வேருக்கு தொடர்பான பிரச்சினைகள்

### NVIDIA GPU

**GPU நிலையை சரிபார்க்கவும்:**
```bash
nvidia-smi
```

**பொதுவான பிரச்சினைகள்:**
- **டிரைவர் பழமையானது**: NVIDIA டிரைவர்களை புதுப்பிக்கவும்
- **CUDA பதிப்பு பொருந்தவில்லை**: Foundry Local-ஐ மீண்டும் நிறுவவும்
- **GPU நினைவகம் சிதறியுள்ளது**: கணினியை மீண்டும் தொடங்கவும்

### Qualcomm NPU

**NPU நிலையை சரிபார்க்கவும்:**
```bash
foundry device info
```

**பொதுவான பிரச்சினைகள்:**
- **NPU டிரைவர்கள் நிறுவப்படவில்லை**: Qualcomm NPU டிரைவர்களை நிறுவவும்
- **NPU மாறுபாடு கிடைக்கவில்லை**: CPU மாறுபாட்டைப் பயன்படுத்தவும்
- **Windows பதிப்பு பழமையானது**: Windows 11-இன் சமீபத்திய பதிப்புக்கு புதுப்பிக்கவும்

### CPU-மட்டும் அமைப்புகள்

**பரிந்துரைக்கப்பட்ட மாடல்கள்:**
```python
CATALOG = {
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','general'],'priority':2},
}
```

**செயல்திறன் குறிப்புகள்:**
- சிறிய மாடல்களை பயன்படுத்தவும்
- max_tokens-ஐ குறைக்கவும்
- முதல் கோரிக்கைக்கு பொறுமையை அதிகரிக்கவும்

---

## டயக்னோஸ்டிக் கட்டளைகள்

### அனைத்தையும் சரிபார்க்கவும்
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

### Python-ல்
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

## உதவி பெறுதல்

### 1. பதிவு கோப்புகளை சரிபார்க்கவும்
```bash
# Windows
foundry service logs

# Or check Windows Event Viewer
# Application Logs -> Microsoft-FoundryLocal
```

### 2. GitHub பிரச்சினைகள்
- உள்ள பிரச்சினைகளை தேடவும்: https://github.com/microsoft/Foundry-Local/issues
- புதிய பிரச்சினையை உருவாக்கவும்:
  - பிழை செய்தி (முழு உரை)
  - `foundry service status`-இன் வெளியீடு
  - `foundry --version`-இன் வெளியீடு
  - GPU/NPU தகவல் (nvidia-smi, etc.)
  - மீண்டும் உருவாக்குவதற்கான படிகள்

### 3. ஆவணங்கள்
- **முக்கிய களஞ்சியம்**: https://github.com/microsoft/Foundry-Local
- **Python SDK**: https://github.com/microsoft/Foundry-Local/tree/main/sdk/python
- **CLI குறிப்பு**: https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-cli.md
- **பிரச்சினைகளை சரிசெய்தல்**: https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-troubleshooting.md

---

## விரைவான சரிசெய்தல் சோதனை பட்டியல்

பிரச்சினைகள் ஏற்பட்டால், வரிசையாக இதை முயற்சிக்கவும்:

- [ ] சேவை இயங்குகிறதா என்பதை சரிபார்க்கவும்: `foundry service status`
- [ ] சேவையை மீண்டும் தொடங்கவும்: `foundry service stop && foundry service start`
- [ ] மாடல் உள்ளது என்பதை சரிபார்க்கவும்: `foundry model ls | grep phi-4-mini`
- [ ] தேவையான மாடல்களை ஏற்றவும்: `foundry model run phi-4-mini`
- [ ] GPU நினைவகத்தை சரிபார்க்கவும்: `nvidia-smi` (NVIDIA இருந்தால்)
- [ ] CPU மாறுபாட்டை முயற்சிக்கவும்: `phi-4-mini-cpu`-ஐ `phi-4-mini`-க்கு பதிலாக பயன்படுத்தவும்
- [ ] நோட்புக் கர்னலை மீண்டும் தொடங்கவும்
- [ ] நோட்புக் வெளியீடுகளை அழித்து அனைத்து செல்களையும் மீண்டும் இயக்கவும்
- [ ] SDK-ஐ மீண்டும் நிறுவவும்: `pip install --upgrade --force-reinstall foundry-local-sdk`
- [ ] கணினியை மீண்டும் தொடங்கவும் (கடைசி முயற்சி)

---

## தடுப்பு குறிப்புகள்

### சிறந்த நடைமுறைகள்

1. **முதலில் சேவையை எப்போதும் சரிபார்க்கவும்:**
   ```bash
   foundry service status
   ```

2. **இயல்புநிலை CPU மாறுபாடுகளை பயன்படுத்தவும்:**
   ```python
   CATALOG = {
       'phi-4-mini-cpu': {...},
       'qwen2.5-0.5b-cpu': {...},
   }
   ```

3. **நோட்புக் இயக்குவதற்கு முன் மாடல்களை ஏற்றவும்:**
   ```bash
   foundry model run phi-4-mini
   foundry model run qwen2.5-3b
   ```

4. **சேவையை இயக்கவிடவும்:**
   - தேவையற்ற முறையில் சேவையை நிறுத்த/தொடங்க வேண்டாம்
   - அமர்வுகளுக்கு இடையில் பின்னணியில் இயக்கவிடவும்

5. **வளங்களை கண்காணிக்கவும்:**
   - இயக்குவதற்கு முன் GPU நினைவகத்தை சரிபார்க்கவும்
   - தேவையற்ற GPU பயன்பாடுகளை மூடவும்
   - Task Manager / nvidia-smi-ஐ பயன்படுத்தவும்

6. **தினசரி புதுப்பிக்கவும்:**
   ```bash
   winget upgrade Microsoft.FoundryLocal
   pip install --upgrade foundry-local-sdk
   ```

---

**கடைசியாக புதுப்பிக்கப்பட்ட தேதி:** அக்டோபர் 8, 2025

---

**அறிவிப்பு**:  
இந்த ஆவணம் [Co-op Translator](https://github.com/Azure/co-op-translator) என்ற AI மொழிபெயர்ப்பு சேவையை பயன்படுத்தி மொழிபெயர்க்கப்பட்டுள்ளது. நாங்கள் துல்லியத்திற்காக முயற்சிக்கிறோம், ஆனால் தானியங்கி மொழிபெயர்ப்புகளில் பிழைகள் அல்லது தவறுகள் இருக்கக்கூடும் என்பதை கவனத்தில் கொள்ளவும். அதன் சொந்த மொழியில் உள்ள மூல ஆவணம் அதிகாரப்பூர்வ ஆதாரமாக கருதப்பட வேண்டும். முக்கியமான தகவல்களுக்கு, தொழில்முறை மனித மொழிபெயர்ப்பு பரிந்துரைக்கப்படுகிறது. இந்த மொழிபெயர்ப்பைப் பயன்படுத்துவதால் ஏற்படும் எந்த தவறான புரிதல்களுக்கும் அல்லது தவறான விளக்கங்களுக்கும் நாங்கள் பொறுப்பல்ல.