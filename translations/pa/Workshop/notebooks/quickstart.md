<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "ddaad917d0c16fc3d498a6b4eabc8088",
  "translation_date": "2025-10-09T11:15:15+00:00",
  "source_file": "Workshop/notebooks/quickstart.md",
  "language_code": "pa"
}
-->
# ਵਰਕਸ਼ਾਪ ਨੋਟਬੁੱਕਸ - ਤੁਰੰਤ ਸ਼ੁਰੂਆਤ ਗਾਈਡ

## ਸਮੱਗਰੀ ਦੀ ਸੂਚੀ

- [ਪੂਰਵ ਸ਼ਰਤਾਂ](../../../../Workshop/notebooks)
- [ਸ਼ੁਰੂਆਤੀ ਸੈਟਅਪ](../../../../Workshop/notebooks)
- [ਸੈਸ਼ਨ 04: ਮਾਡਲ ਤੁਲਨਾ](../../../../Workshop/notebooks)
- [ਸੈਸ਼ਨ 05: ਮਲਟੀ-ਏਜੰਟ ਆਰਕਿਸਟਰੇਟਰ](../../../../Workshop/notebooks)
- [ਸੈਸ਼ਨ 06: ਇਰਾਦਾ-ਅਧਾਰਿਤ ਮਾਡਲ ਰੂਟਿੰਗ](../../../../Workshop/notebooks)
- [ਵਾਤਾਵਰਣ ਵੈਰੀਏਬਲ](../../../../Workshop/notebooks)
- [ਆਮ ਕਮਾਂਡ](../../../../Workshop/notebooks)

---

## ਪੂਰਵ ਸ਼ਰਤਾਂ

### 1. Foundry Local ਇੰਸਟਾਲ ਕਰੋ

**Windows:**
```bash
winget install Microsoft.FoundryLocal
```

**macOS:**
```bash
brew tap microsoft/foundrylocal
brew install foundrylocal
```

**ਇੰਸਟਾਲੇਸ਼ਨ ਦੀ ਪੁਸ਼ਟੀ ਕਰੋ:**
```bash
foundry --version
```

### 2. Python Dependencies ਇੰਸਟਾਲ ਕਰੋ

```bash
cd Workshop
pip install -r requirements.txt
```

ਜਾਂ ਵੱਖ-ਵੱਖ ਇੰਸਟਾਲ ਕਰੋ:
```bash
pip install foundry-local-sdk openai numpy requests
```

---

## ਸ਼ੁਰੂਆਤੀ ਸੈਟਅਪ

### Foundry Local ਸੇਵਾ ਸ਼ੁਰੂ ਕਰੋ

**ਕੋਈ ਵੀ ਨੋਟਬੁੱਕ ਚਲਾਉਣ ਤੋਂ ਪਹਿਲਾਂ ਲਾਜ਼ਮੀ:**

```bash
# Start the service
foundry service start

# Verify it's running
foundry service status
```

ਉਮੀਦ ਕੀਤੀ ਆਉਟਪੁੱਟ:
```
✅ Service started successfully
Endpoint: http://localhost:59959
```

### ਮਾਡਲ ਡਾਊਨਲੋਡ ਅਤੇ ਲੋਡ ਕਰੋ

ਨੋਟਬੁੱਕਸ ਡਿਫਾਲਟ ਰੂਪ ਵਿੱਚ ਇਹ ਮਾਡਲ ਵਰਤਦੇ ਹਨ:

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

### ਸੈਟਅਪ ਦੀ ਪੁਸ਼ਟੀ ਕਰੋ

```bash
# List loaded models
foundry model ls

# Check service health
curl http://localhost:59959/v1/models
```

---

## ਸੈਸ਼ਨ 04: ਮਾਡਲ ਤੁਲਨਾ

### ਉਦੇਸ਼
ਛੋਟੇ ਭਾਸ਼ਾ ਮਾਡਲ (SLM) ਅਤੇ ਵੱਡੇ ਭਾਸ਼ਾ ਮਾਡਲ (LLM) ਦੇ ਪ੍ਰਦਰਸ਼ਨ ਦੀ ਤੁਲਨਾ ਕਰੋ।

### ਤੁਰੰਤ ਸੈਟਅਪ

```bash
# Start service (if not already running)
foundry service start

# Load required models
foundry model run phi-4-mini
foundry model run qwen2.5-3b
```

### ਨੋਟਬੁੱਕ ਚਲਾਉਣਾ

1. **ਖੋਲ੍ਹੋ** `session04_model_compare.ipynb` VS Code ਜਾਂ Jupyter ਵਿੱਚ
2. **ਕਰਨਲ ਰੀਸਟਾਰਟ ਕਰੋ** (Kernel → Restart Kernel)
3. **ਸਾਰੇ ਸੈਲ ਚਲਾਓ** ਕ੍ਰਮਵਾਰ

### ਮੁੱਖ ਸੰਰਚਨਾ

**ਡਿਫਾਲਟ ਮਾਡਲ:**
- **SLM:** `phi-4-mini` (~4GB RAM, ਤੇਜ਼)
- **LLM:** `qwen2.5-3b` (~3GB RAM, ਮੈਮਰੀ-ਆਪਟੀਮਾਈਜ਼ਡ)

**ਵਾਤਾਵਰਣ ਵੈਰੀਏਬਲ (ਵਿਕਲਪਿਕ):**
```python
import os
os.environ['SLM_ALIAS'] = 'phi-4-mini'
os.environ['LLM_ALIAS'] = 'qwen2.5-3b'
os.environ['FOUNDRY_LOCAL_ENDPOINT'] = 'http://localhost:59959/v1'
```

### ਉਮੀਦ ਕੀਤੀ ਆਉਟਪੁੱਟ

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

### ਕਸਟਮਾਈਜ਼ੇਸ਼ਨ

**ਵੱਖਰੇ ਮਾਡਲ ਵਰਤੋ:**
```python
os.environ['SLM_ALIAS'] = 'phi-3.5-mini'
os.environ['LLM_ALIAS'] = 'qwen2.5-1.5b'
```

**ਕਸਟਮ ਪ੍ਰੋੰਪਟ:**
```python
os.environ['COMPARE_PROMPT'] = 'Explain quantum computing in simple terms'
```

### ਵੈਧਤਾ ਚੈੱਕਲਿਸਟ

- [ ] ਸੈਲ 12 ਸਹੀ ਮਾਡਲ ਦਿਖਾਉਂਦਾ ਹੈ (phi-4-mini, qwen2.5-3b)
- [ ] ਸੈਲ 12 ਸਹੀ ਐਂਡਪੌਇੰਟ ਦਿਖਾਉਂਦਾ ਹੈ (port 59959)
- [ ] ਸੈਲ 16 ਡਾਇਗਨੋਸਟਿਕ ਪਾਸ ਕਰਦਾ ਹੈ (✅ ਸੇਵਾ ਚੱਲ ਰਹੀ ਹੈ)
- [ ] ਸੈਲ 20 ਪ੍ਰੀ-ਫਲਾਈਟ ਚੈੱਕ ਪਾਸ ਕਰਦਾ ਹੈ (ਦੋਵੇਂ ਮਾਡਲ ਠੀਕ ਹਨ)
- [ ] ਸੈਲ 22 ਤੁਲਨਾ ਪੂਰੀ ਹੁੰਦੀ ਹੈ ਲੇਟੈਂਸੀ ਵੈਲਿਊਜ਼ ਨਾਲ
- [ ] ਸੈਲ 24 ਵੈਧਤਾ ਦਿਖਾਉਂਦਾ ਹੈ 🎉 ਸਾਰੇ ਚੈੱਕ ਪਾਸ!

### ਸਮਾਂ ਅਨੁਮਾਨ
- **ਪਹਿਲੀ ਵਾਰ ਚਲਾਉਣਾ:** 5-10 ਮਿੰਟ (ਮਾਡਲ ਡਾਊਨਲੋਡ ਸਮੇਤ)
- **ਅਗਲੀ ਵਾਰ ਚਲਾਉਣਾ:** 1-2 ਮਿੰਟ

---

## ਸੈਸ਼ਨ 05: ਮਲਟੀ-ਏਜੰਟ ਆਰਕਿਸਟਰੇਟਰ

### ਉਦੇਸ਼
Foundry Local SDK ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਮਲਟੀ-ਏਜੰਟ ਸਹਿਯੋਗ ਦਿਖਾਉਣਾ - ਏਜੰਟ ਮਿਲ ਕੇ ਸੁਧਾਰਿਤ ਨਤੀਜੇ ਪੈਦਾ ਕਰਦੇ ਹਨ।

### ਤੁਰੰਤ ਸੈਟਅਪ

```bash
# Start service
foundry service start

# Load models
foundry model run phi-4-mini  # Primary model
foundry model run qwen2.5-7b  # Optional: higher quality editor
```

### ਨੋਟਬੁੱਕ ਚਲਾਉਣਾ

1. **ਖੋਲ੍ਹੋ** `session05_agents_orchestrator.ipynb`
2. **ਕਰਨਲ ਰੀਸਟਾਰਟ ਕਰੋ**
3. **ਸਾਰੇ ਸੈਲ ਚਲਾਓ** ਕ੍ਰਮਵਾਰ

### ਮੁੱਖ ਸੰਰਚਨਾ

**ਡਿਫਾਲਟ ਸੈਟਅਪ (ਦੋਵੇਂ ਏਜੰਟ ਲਈ ਇੱਕੋ ਮਾਡਲ):**
```python
PRIMARY_ALIAS = 'phi-4-mini'
EDITOR_ALIAS = 'phi-4-mini'  # Uses same model
```

**ਉੱਚਤਮ ਸੈਟਅਪ (ਵੱਖਰੇ ਮਾਡਲ):**
```python
import os
os.environ['AGENT_MODEL_PRIMARY'] = 'phi-4-mini'     # Fast for research
os.environ['AGENT_MODEL_EDITOR'] = 'qwen2.5-7b'      # High quality for editing
```

### ਆਰਕੀਟੈਕਚਰ

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

### ਉਮੀਦ ਕੀਤੀ ਆਉਟਪੁੱਟ

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

### ਵਧਾਈਆਂ

**ਹੋਰ ਏਜੰਟ ਸ਼ਾਮਲ ਕਰੋ:**
```python
critic = Agent(
    name='Critic',
    system='Review content for accuracy',
    client=client,
    model_id=model_id
)
```

**ਬੈਚ ਟੈਸਟਿੰਗ:**
```python
test_questions = [
    "What are benefits of local AI?",
    "How does RAG improve accuracy?",
]

for q in test_questions:
    result = pipeline(q, verbose=False)
    print(result['final'])
```

### ਸਮਾਂ ਅਨੁਮਾਨ
- **ਪਹਿਲੀ ਵਾਰ ਚਲਾਉਣਾ:** 3-5 ਮਿੰਟ
- **ਅਗਲੀ ਵਾਰ ਚਲਾਉਣਾ:** ਪ੍ਰਸ਼ਨ ਪ੍ਰਤੀ 1-2 ਮਿੰਟ

---

## ਸੈਸ਼ਨ 06: ਇਰਾਦਾ-ਅਧਾਰਿਤ ਮਾਡਲ ਰੂਟਿੰਗ

### ਉਦੇਸ਼
ਪਤਾ ਲੱਗੇ ਇਰਾਦੇ ਦੇ ਅਧਾਰ 'ਤੇ ਵਿਸ਼ੇਸ਼ ਮਾਡਲਾਂ ਨੂੰ ਪ੍ਰੋੰਪਟਸ ਨੂੰ ਸਮਰਪਿਤ ਤੌਰ 'ਤੇ ਰੂਟ ਕਰੋ।

### ਤੁਰੰਤ ਸੈਟਅਪ

```bash
# Start service
foundry service start

# Load all routing models (CPU variants recommended)
foundry model run phi-4-mini-cpu
foundry model run qwen2.5-0.5b-cpu
foundry model run phi-3.5-mini-cpu
```

**ਨੋਟ:** ਸੈਸ਼ਨ 06 ਡਿਫਾਲਟ ਰੂਪ ਵਿੱਚ CPU ਮਾਡਲਾਂ ਨੂੰ ਵੱਧ ਤੋਂ ਵੱਧ ਅਨੁਕੂਲਤਾ ਲਈ ਵਰਤਦਾ ਹੈ।

### ਨੋਟਬੁੱਕ ਚਲਾਉਣਾ

1. **ਖੋਲ੍ਹੋ** `session06_models_router.ipynb`
2. **ਕਰਨਲ ਰੀਸਟਾਰਟ ਕਰੋ**
3. **ਸਾਰੇ ਸੈਲ ਚਲਾਓ** ਕ੍ਰਮਵਾਰ

### ਮੁੱਖ ਸੰਰਚਨਾ

**ਡਿਫਾਲਟ ਕੈਟਾਲੌਗ (CPU ਮਾਡਲ):**
```python
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```

**ਵਿਕਲਪ (GPU ਮਾਡਲ):**
```python
# Uncomment GPU catalog in Cell #6 if you have sufficient VRAM (8GB+)
CATALOG = {
    'phi-4-mini': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini': {'capabilities':['code','refactor'],'priority':3},
}
```

### ਇਰਾਦਾ ਪਤਾ ਲਗਾਉਣਾ

ਰੂਟਰ regex ਪੈਟਰਨ ਦੀ ਵਰਤੋਂ ਕਰਦਾ ਹੈ ਇਰਾਦਾ ਪਤਾ ਲਗਾਉਣ ਲਈ:

| ਇਰਾਦਾ | ਪੈਟਰਨ ਉਦਾਹਰਨ | ਰੂਟ ਕੀਤਾ |
|--------|-----------------|-----------|
| `code` | "refactor", "implement function" | phi-3.5-mini-cpu |
| `classification` | "categorize", "classify this" | qwen2.5-0.5b-cpu |
| `summarize` | "summarize", "tl;dr" | phi-4-mini-cpu |
| `general` | ਹੋਰ ਸਭ ਕੁਝ | phi-4-mini-cpu |

### ਉਮੀਦ ਕੀਤੀ ਆਉਟਪੁੱਟ

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

### ਕਸਟਮਾਈਜ਼ੇਸ਼ਨ

**ਕਸਟਮ ਇਰਾਦਾ ਸ਼ਾਮਲ ਕਰੋ:**
```python
import re

# Add to RULES
RULES.append((re.compile('translate|翻译', re.I), 'translation'))

# Add capability to catalog
CATALOG['phi-4-mini-cpu']['capabilities'].append('translation')
```

**ਟੋਕਨ ਟ੍ਰੈਕਿੰਗ ਚਾਲੂ ਕਰੋ:**
```python
import os
os.environ['SHOW_USAGE'] = '1'
```

### GPU ਮਾਡਲਾਂ ਵਿੱਚ ਸਵਿੱਚ ਕਰਨਾ

ਜੇ ਤੁਹਾਡੇ ਕੋਲ 8GB+ VRAM ਹੈ:

1. **ਸੈਲ #6** ਵਿੱਚ, CPU ਕੈਟਾਲੌਗ ਨੂੰ ਕਾਮੈਂਟ ਕਰੋ
2. GPU ਕੈਟਾਲੌਗ ਨੂੰ ਅਨਕਾਮੈਂਟ ਕਰੋ
3. GPU ਮਾਡਲ ਲੋਡ ਕਰੋ:
   ```bash
   foundry model run phi-4-mini
   foundry model run qwen2.5-0.5b
   foundry model run phi-3.5-mini
   ```
4. ਕਰਨਲ ਰੀਸਟਾਰਟ ਕਰੋ ਅਤੇ ਨੋਟਬੁੱਕ ਦੁਬਾਰਾ ਚਲਾਓ

### ਸਮਾਂ ਅਨੁਮਾਨ
- **ਪਹਿਲੀ ਵਾਰ ਚਲਾਉਣਾ:** 5-10 ਮਿੰਟ (ਮਾਡਲ ਲੋਡਿੰਗ)
- **ਅਗਲੀ ਵਾਰ ਚਲਾਉਣਾ:** ਪ੍ਰਤੀ ਟੈਸਟ 30-60 ਸਕਿੰਟ

---

## ਵਾਤਾਵਰਣ ਵੈਰੀਏਬਲ

### ਗਲੋਬਲ ਸੰਰਚਨਾ

Jupyter/VS Code ਸ਼ੁਰੂ ਕਰਨ ਤੋਂ ਪਹਿਲਾਂ ਸੈਟ ਕਰੋ:

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

### ਨੋਟਬੁੱਕ ਵਿੱਚ ਸੰਰਚਨਾ

ਕਿਸੇ ਵੀ ਨੋਟਬੁੱਕ ਦੇ ਸ਼ੁਰੂ ਵਿੱਚ ਸੈਟ ਕਰੋ:

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

## ਆਮ ਕਮਾਂਡ

### ਸੇਵਾ ਪ੍ਰਬੰਧਨ

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

### ਮਾਡਲ ਪ੍ਰਬੰਧਨ

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

### ਐਂਡਪੌਇੰਟ ਟੈਸਟਿੰਗ

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

### ਡਾਇਗਨੋਸਟਿਕ ਕਮਾਂਡ

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

## ਸਰਵੋਤਮ ਅਭਿਆਸ

### ਕਿਸੇ ਵੀ ਨੋਟਬੁੱਕ ਸ਼ੁਰੂ ਕਰਨ ਤੋਂ ਪਹਿਲਾਂ

1. **ਸੇਵਾ ਚੱਲ ਰਹੀ ਹੈ ਜਾਂ ਨਹੀਂ ਚੈੱਕ ਕਰੋ:**
   ```bash
   foundry service status
   ```

2. **ਮਾਡਲ ਲੋਡ ਹੋਏ ਹਨ ਜਾਂ ਨਹੀਂ ਚੈੱਕ ਕਰੋ:**
   ```bash
   foundry model ls
   ```

3. **ਨੋਟਬੁੱਕ ਕਰਨਲ ਰੀਸਟਾਰਟ ਕਰੋ** ਜੇ ਦੁਬਾਰਾ ਚਲਾਉਣਾ ਹੈ

4. **ਸਾਰੇ ਆਉਟਪੁੱਟ ਸਾਫ਼ ਕਰੋ** ਸਾਫ਼ ਚਲਾਉਣ ਲਈ

### ਸਰੋਤ ਪ੍ਰਬੰਧਨ

1. **ਡਿਫਾਲਟ ਰੂਪ ਵਿੱਚ CPU ਮਾਡਲ ਵਰਤੋ** ਅਨੁਕੂਲਤਾ ਲਈ
2. **GPU ਮਾਡਲਾਂ ਵਿੱਚ ਸਵਿੱਚ ਕਰੋ** ਜੇ ਤੁਹਾਡੇ ਕੋਲ 8GB+ VRAM ਹੈ
3. **GPU ਐਪਲੀਕੇਸ਼ਨ ਬੰਦ ਕਰੋ** ਨੋਟਬੁੱਕ ਚਲਾਉਣ ਤੋਂ ਪਹਿਲਾਂ
4. **ਨੋਟਬੁੱਕ ਸੈਸ਼ਨ ਦੇ ਵਿਚਕਾਰ ਸੇਵਾ ਚੱਲ ਰਹੀ ਰੱਖੋ**
5. **ਸਰੋਤ ਦੀ ਵਰਤੋਂ ਦੀ ਨਿਗਰਾਨੀ ਕਰੋ** Task Manager / nvidia-smi ਨਾਲ

### ਸਮੱਸਿਆ ਹੱਲ

1. **ਸੇਵਾ ਦੀ ਸਥਿਤੀ ਪਹਿਲਾਂ ਚੈੱਕ ਕਰੋ** ਕੋਡ ਡਿਬੱਗ ਕਰਨ ਤੋਂ ਪਹਿਲਾਂ
2. **ਕਰਨਲ ਰੀਸਟਾਰਟ ਕਰੋ** ਜੇ ਪੁਰਾਣੀ ਸੰਰਚਨਾ ਦਿਖਾਈ ਦੇਵੇ
3. **ਕੋਈ ਵੀ ਬਦਲਾਅ ਤੋਂ ਬਾਅਦ ਡਾਇਗਨੋਸਟਿਕ ਸੈਲ ਦੁਬਾਰਾ ਚਲਾਓ**
4. **ਮਾਡਲ ਦੇ ਨਾਮ ਚੈੱਕ ਕਰੋ** ਜੋ ਲੋਡ ਹੋਏ ਹਨ
5. **ਐਂਡਪੌਇੰਟ ਪੋਰਟ ਦੀ ਪੁਸ਼ਟੀ ਕਰੋ** ਸੇਵਾ ਸਥਿਤੀ ਨਾਲ ਮਿਲਦਾ ਹੈ

---

## ਤੁਰੰਤ ਸੰਦਰਭ: ਮਾਡਲ ਅਲੀਅਸ

### ਆਮ ਮਾਡਲ

| ਅਲੀਅਸ | ਆਕਾਰ | ਸਭ ਤੋਂ ਵਧੀਆ | RAM/VRAM | ਵੈਰੀਐਂਟ |
|-------|------|----------|----------|----------|
| `phi-4-mini` | ~4B | ਜਨਰਲ ਚੈਟ, ਸੰਖੇਪ | 4-6GB | `-cpu`, `-cuda-gpu`, `-npu` |
| `phi-3.5-mini` | ~3.5B | ਕੋਡ ਜਨਰੇਸ਼ਨ, ਰੀਫੈਕਟਰੀੰਗ | 3-5GB | `-cpu`, `-cuda-gpu`, `-npu` |
| `qwen2.5-3b` | ~3B | ਜਨਰਲ ਟਾਸਕ, ਕੁਸ਼ਲ | 3-4GB | `-cpu`, `-cuda-gpu` |
| `qwen2.5-1.5b` | ~1.5B | ਤੇਜ਼, ਘੱਟ ਸਰੋਤ | 2-3GB | `-cpu`, `-cuda-gpu` |
| `qwen2.5-0.5b` | ~0.5B | ਵਰਗੀਕਰਨ, ਘੱਟ ਸਰੋਤ | 1-2GB | `-cpu`, `-cuda-gpu` |

### ਵੈਰੀਐਂਟ ਨਾਮਕਰਨ

- **ਬੇਸ ਨਾਮ** (ਜਿਵੇਂ `phi-4-mini`): ਤੁਹਾਡੇ ਹਾਰਡਵੇਅਰ ਲਈ ਸਭ ਤੋਂ ਵਧੀਆ ਵੈਰੀਐਂਟ ਆਟੋ-ਚੁਣਦਾ ਹੈ
- **`-cpu`**: CPU-ਆਪਟੀਮਾਈਜ਼ਡ, ਹਰ ਜਗ੍ਹਾ ਕੰਮ ਕਰਦਾ ਹੈ
- **`-cuda-gpu`**: NVIDIA GPU-ਆਪਟੀਮਾਈਜ਼ਡ, 8GB+ VRAM ਦੀ ਲੋੜ ਹੈ
- **`-npu`**: Qualcomm NPU-ਆਪਟੀਮਾਈਜ਼ਡ, NPU ਡਰਾਈਵਰ ਦੀ ਲੋੜ ਹੈ

**ਸਿਫਾਰਸ਼:** ਬੇਸ ਨਾਮ (ਬਿਨਾਂ ਸੁਫਿਕਸ) ਵਰਤੋ ਅਤੇ Foundry Local ਨੂੰ ਸਭ ਤੋਂ ਵਧੀਆ ਵੈਰੀਐਂਟ ਚੁਣਨ ਦਿਓ।

---

## ਸਫਲਤਾ ਦੇ ਸੰਕੇਤ

ਤੁਸੀਂ ਤਿਆਰ ਹੋ ਜਦੋਂ ਤੁਸੀਂ ਵੇਖਦੇ ਹੋ:

✅ `foundry service status` "running" ਦਿਖਾਉਂਦਾ ਹੈ  
✅ `foundry model ls` ਤੁਹਾਡੇ ਲੋੜੀਂਦੇ ਮਾਡਲ ਦਿਖਾਉਂਦਾ ਹੈ  
✅ ਸੇਵਾ ਸਹੀ ਐਂਡਪੌਇੰਟ 'ਤੇ ਪਹੁੰਚਯੋਗ ਹੈ  
✅ ਹੈਲਥ ਚੈੱਕ 200 OK ਵਾਪਸ ਕਰਦਾ ਹੈ  
✅ ਨੋਟਬੁੱਕ ਡਾਇਗਨੋਸਟਿਕ ਸੈਲ ਪਾਸ ਕਰਦੇ ਹਨ  
✅ ਆਉਟਪੁੱਟ ਵਿੱਚ ਕੋਈ ਕਨੈਕਸ਼ਨ ਗਲਤੀ ਨਹੀਂ

---

## ਮਦਦ ਪ੍ਰਾਪਤ ਕਰਨਾ

### ਦਸਤਾਵੇਜ਼
- **ਮੁੱਖ ਰਿਪੋਜ਼ਟਰੀ**: https://github.com/microsoft/Foundry-Local  
- **Python SDK**: https://github.com/microsoft/Foundry-Local/tree/main/sdk/python  
- **CLI ਰਿਫਰੈਂਸ**: https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-cli.md  
- **ਸਮੱਸਿਆ ਹੱਲ**: ਇਸ ਡਾਇਰੈਕਟਰੀ ਵਿੱਚ `troubleshooting.md` ਵੇਖੋ  

### GitHub Issues
- https://github.com/microsoft/Foundry-Local/issues  
- https://github.com/microsoft/edgeai-for-beginners/issues  

---

**ਆਖਰੀ ਅਪਡੇਟ:** ਅਕਤੂਬਰ 8, 2025  
**ਵਰਜਨ:** ਵਰਕਸ਼ਾਪ ਨੋਟਬੁੱਕਸ 2.0  

---

**ਅਸਵੀਕਰਤੀ**:  
ਇਹ ਦਸਤਾਵੇਜ਼ AI ਅਨੁਵਾਦ ਸੇਵਾ [Co-op Translator](https://github.com/Azure/co-op-translator) ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਅਨੁਵਾਦ ਕੀਤਾ ਗਿਆ ਹੈ। ਹਾਲਾਂਕਿ ਅਸੀਂ ਸਹੀਅਤ ਲਈ ਯਤਨਸ਼ੀਲ ਹਾਂ, ਕਿਰਪਾ ਕਰਕੇ ਧਿਆਨ ਦਿਓ ਕਿ ਸਵੈਚਾਲਿਤ ਅਨੁਵਾਦਾਂ ਵਿੱਚ ਗਲਤੀਆਂ ਜਾਂ ਅਸੁਚਨਾਵਾਂ ਹੋ ਸਕਦੀਆਂ ਹਨ। ਇਸ ਦਸਤਾਵੇਜ਼ ਦਾ ਮੂਲ ਰੂਪ ਇਸਦੀ ਮੂਲ ਭਾਸ਼ਾ ਵਿੱਚ ਅਧਿਕਾਰਤ ਸਰੋਤ ਮੰਨਿਆ ਜਾਣਾ ਚਾਹੀਦਾ ਹੈ। ਮਹੱਤਵਪੂਰਨ ਜਾਣਕਾਰੀ ਲਈ, ਪੇਸ਼ੇਵਰ ਮਨੁੱਖੀ ਅਨੁਵਾਦ ਦੀ ਸਿਫਾਰਸ਼ ਕੀਤੀ ਜਾਂਦੀ ਹੈ। ਇਸ ਅਨੁਵਾਦ ਦੀ ਵਰਤੋਂ ਤੋਂ ਪੈਦਾ ਹੋਣ ਵਾਲੇ ਕਿਸੇ ਵੀ ਗਲਤ ਫਹਿਮੀ ਜਾਂ ਗਲਤ ਵਿਆਖਿਆ ਲਈ ਅਸੀਂ ਜ਼ਿੰਮੇਵਾਰ ਨਹੀਂ ਹਾਂ।