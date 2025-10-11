<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "ddaad917d0c16fc3d498a6b4eabc8088",
  "translation_date": "2025-10-11T12:07:14+00:00",
  "source_file": "Workshop/notebooks/quickstart.md",
  "language_code": "ta"
}
-->
# வேலைநிறுத்த நோட்புக் - விரைவான தொடக்க வழிகாட்டி

## உள்ளடக்க அட்டவணை

- [முன் தேவைகள்](../../../../Workshop/notebooks)
- [ஆரம்ப அமைப்பு](../../../../Workshop/notebooks)
- [அமர்வு 04: மாடல் ஒப்பீடு](../../../../Workshop/notebooks)
- [அமர்வு 05: பல முகவர் ஒருங்கிணைப்பாளர்](../../../../Workshop/notebooks)
- [அமர்வு 06: நோக்கத்தை அடிப்படையாகக் கொண்ட மாடல் வழிமுறை](../../../../Workshop/notebooks)
- [சுற்றுச்சூழல் மாறிகள்](../../../../Workshop/notebooks)
- [பொது கட்டளைகள்](../../../../Workshop/notebooks)

---

## முன் தேவைகள்

### 1. Foundry Local ஐ நிறுவவும்

**Windows:**
```bash
winget install Microsoft.FoundryLocal
```

**macOS:**
```bash
brew tap microsoft/foundrylocal
brew install foundrylocal
```

**நிறுவலை சரிபார்க்கவும்:**
```bash
foundry --version
```

### 2. Python சார்ந்த தேவைகளை நிறுவவும்

```bash
cd Workshop
pip install -r requirements.txt
```

அல்லது தனித்தனியாக நிறுவவும்:
```bash
pip install foundry-local-sdk openai numpy requests
```

---

## ஆரம்ப அமைப்பு

### Foundry Local சேவையை தொடங்கவும்

**எந்த நோட்புக் இயக்குவதற்கு முன் தேவை:**

```bash
# Start the service
foundry service start

# Verify it's running
foundry service status
```

எதிர்பார்க்கப்படும் வெளியீடு:
```
✅ Service started successfully
Endpoint: http://localhost:59959
```

### மாடல்களை பதிவிறக்கி ஏற்றவும்

இந்த நோட்புக் இயல்பாக இந்த மாடல்களை பயன்படுத்துகிறது:

```bash
# Download models (first time only - may take several minutes)
foundry model download phi-4-mini
foundry model download qwen2.5-3b
foundry model download phi-3.5-mini
foundry model download qwen2.5-0.5b

# Load models into memory
foundry model run phi-4-mini
foundry model run qwen2.5-3b
foundry model run phi-3.5-mini
```

### அமைப்பை சரிபார்க்கவும்

```bash
# List loaded models
foundry model ls

# Check service health
curl http://localhost:59959/v1/models
```

---

## அமர்வு 04: மாடல் ஒப்பீடு

### நோக்கம்
சிறிய மொழி மாடல்கள் (SLM) மற்றும் பெரிய மொழி மாடல்கள் (LLM) இடையிலான செயல்திறனை ஒப்பிடுங்கள்.

### விரைவான அமைப்பு

```bash
# Start service (if not already running)
foundry service start

# Load required models
foundry model run phi-4-mini
foundry model run qwen2.5-3b
```

### நோட்புக் இயக்குதல்

1. **திறக்கவும்** `session04_model_compare.ipynb` ஐ VS Code அல்லது Jupyter இல்
2. **கேர்னலை மீண்டும் தொடங்கவும்** (Kernel → Restart Kernel)
3. **அனைத்து செல்களை** வரிசையாக இயக்கவும்

### முக்கிய அமைப்பு

**இயல்புநிலை மாடல்கள்:**
- **SLM:** `phi-4-mini` (~4GB RAM, வேகமானது)
- **LLM:** `qwen2.5-3b` (~3GB RAM, நினைவகத்தைச் சேமிக்கும்)

**சுற்றுச்சூழல் மாறிகள் (விருப்பத்தேர்வு):**
```python
import os
os.environ['SLM_ALIAS'] = 'phi-4-mini'
os.environ['LLM_ALIAS'] = 'qwen2.5-3b'
os.environ['FOUNDRY_LOCAL_ENDPOINT'] = 'http://localhost:59959/v1'
```

### எதிர்பார்க்கப்படும் வெளியீடு

```
================================================================================
COMPARISON SUMMARY
================================================================================
Alias                Latency(s)      Tokens     Route               
--------------------------------------------------------------------------------
phi-4-mini           1.234           150        chat.completions    
qwen2.5-3b           2.456           180        chat.completions    
================================================================================

💡 SLM is 1.99x faster than LLM for this prompt
```

### தனிப்பயனாக்கம்

**வேறு மாடல்களைப் பயன்படுத்தவும்:**
```python
os.environ['SLM_ALIAS'] = 'phi-3.5-mini'
os.environ['LLM_ALIAS'] = 'qwen2.5-1.5b'
```

**தனிப்பயன் உந்துதல்:**
```python
os.environ['COMPARE_PROMPT'] = 'Explain quantum computing in simple terms'
```

### சரிபார்ப்பு சோதனை பட்டியல்

- [ ] செல்கள் 12 சரியான மாடல்களை காட்டுகிறது (phi-4-mini, qwen2.5-3b)
- [ ] செல்கள் 12 சரியான முடிவுகளை (port 59959) காட்டுகிறது
- [ ] செல்கள் 16 டயக்னோஸ்டிக் சோதனை வெற்றி (✅ சேவை இயங்குகிறது)
- [ ] செல்கள் 20 முன்-பயண சோதனை வெற்றி (இரண்டு மாடல்களும் சரி)
- [ ] செல்கள் 22 ஒப்பீடு முடிவடைகிறது தாமத மதிப்புகளுடன்
- [ ] செல்கள் 24 சரிபார்ப்பு 🎉 அனைத்து சோதனைகளும் வெற்றி பெற்றது என்று காட்டுகிறது!

### நேர மதிப்பீடு
- **முதல் இயக்கம்:** 5-10 நிமிடங்கள் (மாடல் பதிவிறக்கங்களை உள்ளடக்கியது)
- **பின்னர் இயக்கங்கள்:** 1-2 நிமிடங்கள்

---

## அமர்வு 05: பல முகவர் ஒருங்கிணைப்பாளர்

### நோக்கம்
Foundry Local SDK ஐப் பயன்படுத்தி பல முகவர்களின் ஒத்துழைப்பை விளக்குகிறது - முகவர்கள் இணைந்து மேம்பட்ட வெளியீடுகளை உருவாக்குகிறார்கள்.

### விரைவான அமைப்பு

```bash
# Start service
foundry service start

# Load models
foundry model run phi-4-mini  # Primary model
foundry model run qwen2.5-7b  # Optional: higher quality editor
```

### நோட்புக் இயக்குதல்

1. **திறக்கவும்** `session05_agents_orchestrator.ipynb`
2. **கேர்னலை மீண்டும் தொடங்கவும்**
3. **அனைத்து செல்களை** வரிசையாக இயக்கவும்

### முக்கிய அமைப்பு

**இயல்புநிலை அமைப்பு (இரு முகவர்களுக்கும் ஒரே மாடல்):**
```python
PRIMARY_ALIAS = 'phi-4-mini'
EDITOR_ALIAS = 'phi-4-mini'  # Uses same model
```

**மேம்பட்ட அமைப்பு (வேறு மாடல்கள்):**
```python
import os
os.environ['AGENT_MODEL_PRIMARY'] = 'phi-4-mini'     # Fast for research
os.environ['AGENT_MODEL_EDITOR'] = 'qwen2.5-7b'      # High quality for editing
```

### கட்டமைப்பு

```
User Question
    ↓
Researcher Agent (phi-4-mini)
  → Gathers bullet points
    ↓
Editor Agent (phi-4-mini or qwen2.5-7b)
  → Refines into executive summary
    ↓
Final Output
```

### எதிர்பார்க்கப்படும் வெளியீடு

```
================================================================================
[Pipeline] Question: Explain why edge AI matters for compliance.
================================================================================

[Stage 1: Research]
Output: • Edge AI processes data locally, reducing transmission...

[Stage 2: Editorial Refinement]
Output: Executive Summary: Edge AI enhances compliance by keeping data...

[FINAL OUTPUT]
Executive Summary: Edge AI enhances compliance by keeping sensitive data 
on-premises and reduces latency through local processing.

[METADATA]
Models used: {'researcher': 'phi-4-mini', 'editor': 'phi-4-mini'}
```

### விரிவாக்கங்கள்

**மேலும் முகவர்களைச் சேர்க்கவும்:**
```python
critic = Agent(
    name='Critic',
    system='Review content for accuracy',
    client=client,
    model_id=model_id
)
```

**தொகுதி சோதனை:**
```python
test_questions = [
    "What are benefits of local AI?",
    "How does RAG improve accuracy?",
]

for q in test_questions:
    result = pipeline(q, verbose=False)
    print(result['final'])
```

### நேர மதிப்பீடு
- **முதல் இயக்கம்:** 3-5 நிமிடங்கள்
- **பின்னர் இயக்கங்கள்:** கேள்விக்கு 1-2 நிமிடங்கள்

---

## அமர்வு 06: நோக்கத்தை அடிப்படையாகக் கொண்ட மாடல் வழிமுறை

### நோக்கம்
கண்டறியப்பட்ட நோக்கத்தின் அடிப்படையில் சிறப்பு மாடல்களுக்கு உந்துதல்களை புத்திசாலித்தனமாக வழிமாற்றம் செய்யுங்கள்.

### விரைவான அமைப்பு

```bash
# Start service
foundry service start

# Load all routing models (CPU variants recommended)
foundry model run phi-4-mini-cpu
foundry model run qwen2.5-0.5b-cpu
foundry model run phi-3.5-mini-cpu
```

**குறிப்பு:** Session 06 அதிகபட்ச இணக்கத்திற்காக CPU மாடல்களை இயல்புநிலையாக அமைக்கிறது.

### நோட்புக் இயக்குதல்

1. **திறக்கவும்** `session06_models_router.ipynb`
2. **கேர்னலை மீண்டும் தொடங்கவும்**
3. **அனைத்து செல்களை** வரிசையாக இயக்கவும்

### முக்கிய அமைப்பு

**இயல்புநிலை பட்டியல் (CPU மாடல்கள்):**
```python
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```

**மாற்று (GPU மாடல்கள்):**
```python
# Uncomment GPU catalog in Cell #6 if you have sufficient VRAM (8GB+)
CATALOG = {
    'phi-4-mini': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini': {'capabilities':['code','refactor'],'priority':3},
}
```

### நோக்க கண்டறிதல்

வழிமாற்றி நோக்கத்தை கண்டறிய regex மாதிரிகளைப் பயன்படுத்துகிறது:

| நோக்கம் | மாதிரி உதாரணங்கள் | வழிமாற்றப்பட்டது |
|--------|-----------------|-----------|
| `code` | "refactor", "implement function" | phi-3.5-mini-cpu |
| `classification` | "categorize", "classify this" | qwen2.5-0.5b-cpu |
| `summarize` | "summarize", "tl;dr" | phi-4-mini-cpu |
| `general` | மற்றவை அனைத்தும் | phi-4-mini-cpu |

### எதிர்பார்க்கப்படும் வெளியீடு

```
✓ Using CPU-optimized models (default configuration)
  Models: phi-4-mini-cpu, qwen2.5-0.5b-cpu, phi-3.5-mini-cpu

Routing prompts to specialized models...
============================================================

Prompt: Refactor this Python function for readability
  Intent: code           | Model: phi-3.5-mini-cpu
  Output: Here's a refactored version...
  Tokens: 156

Prompt: Categorize this email as urgent or normal
  Intent: classification | Model: qwen2.5-0.5b-cpu
  Output: Category: Normal
  Tokens: 45

✓ Success! All prompts routed correctly.
```

### தனிப்பயனாக்கம்

**தனிப்பயன் நோக்கத்தைச் சேர்க்கவும்:**
```python
import re

# Add to RULES
RULES.append((re.compile('translate|翻译', re.I), 'translation'))

# Add capability to catalog
CATALOG['phi-4-mini-cpu']['capabilities'].append('translation')
```

**டோக்கன் கண்காணிப்பை இயக்கவும்:**
```python
import os
os.environ['SHOW_USAGE'] = '1'
```

### GPU மாடல்களுக்கு மாறுதல்

உங்களிடம் 8GB+ VRAM இருந்தால்:

1. **Cell #6** இல், CPU பட்டியலை கருத்துரையாக மாற்றவும்
2. GPU பட்டியலை கருத்துரையற்றதாக மாற்றவும்
3. GPU மாடல்களை ஏற்றவும்:
   ```bash
   foundry model run phi-4-mini
   foundry model run qwen2.5-0.5b
   foundry model run phi-3.5-mini
   ```
4. கேர்னலை மீண்டும் தொடங்கி நோட்புக் இயக்கவும்

### நேர மதிப்பீடு
- **முதல் இயக்கம்:** 5-10 நிமிடங்கள் (மாடல் ஏற்றுதல்)
- **பின்னர் சோதனைகள்:** 30-60 விநாடிகள்

---

## சுற்றுச்சூழல் மாறிகள்

### உலகளாவிய அமைப்பு

Jupyter/VS Code ஐத் தொடங்குவதற்கு முன் அமைக்கவும்:

**Windows (Command Prompt):**
```cmd
set FOUNDRY_LOCAL_ENDPOINT=http://localhost:59959/v1
set SHOW_USAGE=1
set RETRY_ON_FAIL=1
```

**Windows (PowerShell):**
```powershell
$env:FOUNDRY_LOCAL_ENDPOINT="http://localhost:59959/v1"
$env:SHOW_USAGE="1"
$env:RETRY_ON_FAIL="1"
```

**macOS/Linux:**
```bash
export FOUNDRY_LOCAL_ENDPOINT=http://localhost:59959/v1
export SHOW_USAGE=1
export RETRY_ON_FAIL=1
```

### நோட்புக் உள்ளமைப்பு

எந்த நோட்புக்கின் தொடக்கத்தில் அமைக்கவும்:

```python
import os

# Foundry Local configuration
os.environ['FOUNDRY_LOCAL_ENDPOINT'] = 'http://localhost:59959/v1'

# Model selection
os.environ['SLM_ALIAS'] = 'phi-4-mini'
os.environ['LLM_ALIAS'] = 'qwen2.5-3b'

# Agent models
os.environ['AGENT_MODEL_PRIMARY'] = 'phi-4-mini'
os.environ['AGENT_MODEL_EDITOR'] = 'qwen2.5-7b'

# Debugging
os.environ['SHOW_USAGE'] = '1'       # Show token usage
os.environ['RETRY_ON_FAIL'] = '1'    # Enable retries
os.environ['RETRY_BACKOFF'] = '2.0'  # Retry delay
```

---

## பொதுக் கட்டளைகள்

### சேவை மேலாண்மை

```bash
# Start service
foundry service start

# Check status
foundry service status

# Stop service
foundry service stop

# View logs
foundry service logs
```

### மாடல் மேலாண்மை

```bash
# List all available models in catalog
foundry model catalog

# List loaded models
foundry model ls

# Download a model
foundry model download phi-4-mini

# Load a model
foundry model run phi-4-mini

# Unload a model
foundry model unload phi-4-mini

# Remove a model
foundry model remove phi-4-mini

# Get model info
foundry model info phi-4-mini
```

### முடிவுகளை சோதித்தல்

```bash
# Check service health
curl http://localhost:59959/health

# List available models via API
curl http://localhost:59959/v1/models

# Test model completion
curl http://localhost:59959/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "phi-4-mini",
    "messages": [{"role":"user","content":"Hello"}],
    "max_tokens": 50
  }'
```

### டயக்னோஸ்டிக் கட்டளைகள்

```bash
# Check everything
foundry --version
foundry service status
foundry model ls
foundry device info

# GPU status (NVIDIA)
nvidia-smi

# NPU status (Qualcomm)
foundry device info
```

---

## சிறந்த நடைமுறைகள்

### எந்த நோட்புக் தொடங்குவதற்கு முன்

1. **சேவை இயங்குகிறதா என்பதைச் சரிபார்க்கவும்:**
   ```bash
   foundry service status
   ```

2. **மாடல்கள் ஏற்றப்பட்டுள்ளனவா என்பதைச் சரிபார்க்கவும்:**
   ```bash
   foundry model ls
   ```

3. **நோட்புக் கேர்னலை மீண்டும் தொடங்கவும்** மீண்டும் இயக்கும்போது

4. **அனைத்து வெளியீடுகளையும் அழிக்கவும்** சுத்தமான இயக்கத்திற்காக

### வள மேலாண்மை

1. **இயல்புநிலை CPU மாடல்களைப் பயன்படுத்தவும்** இணக்கத்திற்காக
2. **GPU மாடல்களுக்கு மாறவும்** 8GB+ VRAM இருந்தால் மட்டுமே
3. **மற்ற GPU பயன்பாடுகளை மூடவும்** இயக்குவதற்கு முன்
4. **சேவையை இயக்கவும்** நோட்புக் அமர்வுகளுக்கு இடையில்
5. **வள பயன்பாட்டை கண்காணிக்கவும்** Task Manager / nvidia-smi மூலம்

### சிக்கல் தீர்வு

1. **முதலில் சேவையைச் சரிபார்க்கவும்** குறியீட்டை சரிசெய்வதற்கு முன்
2. **கேர்னலை மீண்டும் தொடங்கவும்** பழைய அமைப்பைக் காண்பித்தால்
3. **எந்த மாற்றங்களுக்குப் பிறகும் டயக்னோஸ்டிக் செல்களை மீண்டும் இயக்கவும்**
4. **மாடல் பெயர்கள்** ஏற்றப்பட்டவற்றுடன் பொருந்துகிறதா என்பதைச் சரிபார்க்கவும்
5. **முடிவு போர்ட்** சேவை நிலையைப் பொருந்துகிறதா என்பதைச் சரிபார்க்கவும்

---

## விரைவான குறிப்புகள்: மாடல் பெயர்கள்

### பொதுவான மாடல்கள்

| பெயர் | அளவு | சிறந்த பயன்பாடு | RAM/VRAM | மாறுபாடுகள் |
|-------|------|----------|----------|----------|
| `phi-4-mini` | ~4B | பொதுவான உரையாடல், சுருக்கம் | 4-6GB | `-cpu`, `-cuda-gpu`, `-npu` |
| `phi-3.5-mini` | ~3.5B | குறியீடு உருவாக்கம், மறுசீரமைப்பு | 3-5GB | `-cpu`, `-cuda-gpu`, `-npu` |
| `qwen2.5-3b` | ~3B | பொதுவான பணிகள், திறமையானது | 3-4GB | `-cpu`, `-cuda-gpu` |
| `qwen2.5-1.5b` | ~1.5B | வேகமானது, குறைந்த வளம் | 2-3GB | `-cpu`, `-cuda-gpu` |
| `qwen2.5-0.5b` | ~0.5B | வகைப்படுத்தல், குறைந்த வளம் | 1-2GB | `-cpu`, `-cuda-gpu` |

### மாறுபாடு பெயரிடல்

- **அடிப்படை பெயர்** (எ.கா., `phi-4-mini`): உங்கள் ஹார்ட்வேருக்கு சிறந்த மாறுபாட்டை தானாகத் தேர்ந்தெடுக்கிறது
- **`-cpu`**: CPU-க்கு உகந்தது, எங்கும் வேலை செய்கிறது
- **`-cuda-gpu`**: NVIDIA GPU-க்கு உகந்தது, 8GB+ VRAM தேவை
- **`-npu`**: Qualcomm NPU-க்கு உகந்தது, NPU இயக்கிகள் தேவை

**பரிந்துரை:** அடிப்படை பெயர்களைப் பயன்படுத்தவும் (முடிவில்லாமல்) மற்றும் Foundry Local சிறந்த மாறுபாட்டை தானாகத் தேர்ந்தெடுக்க அனுமதிக்கவும்.

---

## வெற்றியின் அடையாளங்கள்

நீங்கள் தயாராக இருக்கிறீர்கள், நீங்கள் காணும்போது:

✅ `foundry service status` "இயங்குகிறது" என்று காட்டுகிறது  
✅ `foundry model ls` உங்கள் தேவையான மாடல்களை காட்டுகிறது  
✅ சேவை சரியான முடிவில் அணுகக்கூடியது  
✅ ஆரோக்கிய சோதனை 200 OK திரும்புகிறது  
✅ நோட்புக் டயக்னோஸ்டிக் செல்கள் வெற்றி பெறுகிறது  
✅ வெளியீட்டில் எந்த இணைப்பு பிழைகளும் இல்லை  

---

## உதவி பெறுதல்

### ஆவணங்கள்
- **முக்கிய களஞ்சியம்**: https://github.com/microsoft/Foundry-Local  
- **Python SDK**: https://github.com/microsoft/Foundry-Local/tree/main/sdk/python  
- **CLI குறிப்பு**: https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-cli.md  
- **சிக்கல் தீர்வு**: இந்த கோப்பகத்தில் உள்ள `troubleshooting.md` ஐப் பார்க்கவும்  

### GitHub பிரச்சினைகள்
- https://github.com/microsoft/Foundry-Local/issues  
- https://github.com/microsoft/edgeai-for-beginners/issues  

---

**கடைசியாக புதுப்பிக்கப்பட்டது:** அக்டோபர் 8, 2025  
**பதிப்பு:** வேலைநிறுத்த நோட்புக் 2.0  

---

**குறிப்பு**:  
இந்த ஆவணம் [Co-op Translator](https://github.com/Azure/co-op-translator) என்ற AI மொழிபெயர்ப்பு சேவையைப் பயன்படுத்தி மொழிபெயர்க்கப்பட்டுள்ளது. நாங்கள் துல்லியத்திற்காக முயற்சிக்கிறோம், ஆனால் தானியக்க மொழிபெயர்ப்புகளில் பிழைகள் அல்லது தவறான தகவல்கள் இருக்கக்கூடும் என்பதை தயவுசெய்து கவனத்தில் கொள்ளுங்கள். அதன் தாய்மொழியில் உள்ள மூல ஆவணம் அதிகாரப்பூர்வ ஆதாரமாக கருதப்பட வேண்டும். முக்கியமான தகவல்களுக்கு, தொழில்முறை மனித மொழிபெயர்ப்பு பரிந்துரைக்கப்படுகிறது. இந்த மொழிபெயர்ப்பைப் பயன்படுத்துவதால் ஏற்படும் எந்த தவறான புரிதல்கள் அல்லது தவறான விளக்கங்களுக்கு நாங்கள் பொறுப்பல்ல.