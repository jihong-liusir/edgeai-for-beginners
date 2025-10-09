<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "e88a16101de37838f7cf256a9cd0f199",
  "translation_date": "2025-10-09T11:17:22+00:00",
  "source_file": "Workshop/notebooks/TROUBLESHOOTING.md",
  "language_code": "pa"
}
-->
# ਵਰਕਸ਼ਾਪ ਨੋਟਬੁੱਕਸ - ਟਰਬਲਸ਼ੂਟਿੰਗ ਗਾਈਡ

## ਸੂਚੀ

- [ਆਮ ਸਮੱਸਿਆਵਾਂ ਅਤੇ ਹੱਲ](../../../../Workshop/notebooks)
- [ਸੈਸ਼ਨ 04 ਨਾਲ ਸੰਬੰਧਿਤ ਸਮੱਸਿਆਵਾਂ](../../../../Workshop/notebooks)
- [ਸੈਸ਼ਨ 05 ਨਾਲ ਸੰਬੰਧਿਤ ਸਮੱਸਿਆਵਾਂ](../../../../Workshop/notebooks)
- [ਸੈਸ਼ਨ 06 ਨਾਲ ਸੰਬੰਧਿਤ ਸਮੱਸਿਆਵਾਂ](../../../../Workshop/notebooks)
- [ਹਾਰਡਵੇਅਰ-ਸਪੈਸਿਫਿਕ ਸਮੱਸਿਆਵਾਂ](../../../../Workshop/notebooks)
- [ਡਾਇਗਨੋਸਟਿਕ ਕਮਾਂਡ](../../../../Workshop/notebooks)
- [ਮਦਦ ਪ੍ਰਾਪਤ ਕਰਨਾ](../../../../Workshop/notebooks)

---

## ਆਮ ਸਮੱਸਿਆਵਾਂ ਅਤੇ ਹੱਲ

### 🔴 CUDA ਮੈਮਰੀ ਖਤਮ ਹੋਣਾ

**ਐਰਰ ਮੈਸੇਜ:**
```
CUDA failure 2: out of memory
```
  
**ਮੂਲ ਕਾਰਨ:** GPU ਵਿੱਚ ਮਾਡਲ ਲੋਡ ਕਰਨ ਲਈ ਕਾਫ਼ੀ VRAM ਨਹੀਂ ਹੈ।

**ਹੱਲ:**

#### ਵਿਕਲਪ 1: CPU ਵਰਜਨ ਵਰਤੋ (ਸਿਫਾਰਸ਼ੀ)
```python
# In your notebook, update the CATALOG to use CPU variants
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```
  
#### ਵਿਕਲਪ 2: GPU 'ਤੇ ਛੋਟੇ ਮਾਡਲ ਵਰਤੋ
```python
# Use only the smallest model
CATALOG = {
    'qwen2.5-0.5b': {'capabilities':['general','code','summarize','classification'],'priority':1},
}
```
  
#### ਵਿਕਲਪ 3: GPU ਮੈਮਰੀ ਕਲੀਅਰ ਕਰੋ
```bash
# Close other GPU-intensive applications
# Check GPU memory usage
nvidia-smi

# Restart Foundry Local service
foundry service stop
foundry service start
```
  
#### ਵਿਕਲਪ 4: GPU ਮੈਮਰੀ ਵਧਾਓ (ਜੇ ਸੰਭਵ ਹੋਵੇ)
- ਬ੍ਰਾਊਜ਼ਰ ਟੈਬ, ਵੀਡੀਓ ਐਡੀਟਰ ਜਾਂ ਹੋਰ GPU ਐਪਸ ਬੰਦ ਕਰੋ  
- Windows ਵਿਜ਼ੁਅਲ ਇਫੈਕਟ ਘਟਾਓ  
- ਜੇ ਤੁਹਾਡੇ ਕੋਲ ਇੰਟੀਗ੍ਰੇਟਡ + ਡਿਡੀਕੇਟਡ GPU ਹੈ ਤਾਂ ਡਿਡੀਕੇਟਡ GPU ਵਰਤੋ  

---

### 🔴 APIConnectionError: ਕਨੈਕਸ਼ਨ ਐਰਰ

**ਐਰਰ ਮੈਸੇਜ:**
```
APIConnectionError: Connection error
[Retry 1/2] Setup failed for 'phi-4-mini': APIConnectionError: Connection error.
```
  
**ਮੂਲ ਕਾਰਨ:** Foundry Local ਸੇਵਾ ਚੱਲ ਰਹੀ ਨਹੀਂ ਜਾਂ ਪਹੁੰਚਯੋਗ ਨਹੀਂ ਹੈ।

**ਹੱਲ:**

#### ਪੜਾਅ 1: ਸੇਵਾ ਦੀ ਸਥਿਤੀ ਚੈੱਕ ਕਰੋ
```bash
foundry service status
```
  
#### ਪੜਾਅ 2: ਜੇ ਸੇਵਾ ਬੰਦ ਹੈ ਤਾਂ ਸ਼ੁਰੂ ਕਰੋ
```bash
foundry service start
```
  
#### ਪੜਾਅ 3: ਐਂਡਪੌਇੰਟ ਦੀ ਪੁਸ਼ਟੀ ਕਰੋ
```bash
# Check what port the service is using
foundry service status

# Test with curl (adjust port if different)
curl http://localhost:59959/health
curl http://localhost:55769/health
```
  
#### ਪੜਾਅ 4: ਲੋੜੀਂਦੇ ਮਾਡਲ ਲੋਡ ਕਰੋ
```bash
foundry model run phi-4-mini
foundry model run qwen2.5-3b
foundry model run phi-3.5-mini
```
  
#### ਪੜਾਅ 5: ਨੋਟਬੁੱਕ ਕਰਨਲ ਰੀਸਟਾਰਟ ਕਰੋ  
ਸੇਵਾ ਸ਼ੁਰੂ ਕਰਨ ਅਤੇ ਮਾਡਲ ਲੋਡ ਕਰਨ ਤੋਂ ਬਾਅਦ, ਨੋਟਬੁੱਕ ਕਰਨਲ ਰੀਸਟਾਰਟ ਕਰੋ ਅਤੇ ਸਾਰੇ ਸੈਲ ਦੁਬਾਰਾ ਚਲਾਓ।  

---

### 🔴 ਮਾਡਲ ਕੈਟਾਲੌਗ ਵਿੱਚ ਨਹੀਂ ਮਿਲਿਆ

**ਐਰਰ ਮੈਸੇਜ:**
```
ValueError: Model phi-3.5-mini-cpu not found in the catalog.
[ERROR] Model 'phi-4-mini' not found in the catalog
```
  
**ਮੂਲ ਕਾਰਨ:** ਮਾਡਲ ਡਾਊਨਲੋਡ ਨਹੀਂ ਕੀਤਾ ਗਿਆ ਜਾਂ Foundry Local ਵਿੱਚ ਲੋਡ ਨਹੀਂ ਕੀਤਾ ਗਿਆ।

**ਹੱਲ:**

#### ਵਿਕਲਪ 1: ਮਾਡਲ ਡਾਊਨਲੋਡ ਅਤੇ ਲੋਡ ਕਰੋ
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
  
#### ਵਿਕਲਪ 2: ਆਟੋ-ਸਿਲੈਕਸ਼ਨ ਮੋਡ ਵਰਤੋ  
ਆਪਣੇ CATALOG ਨੂੰ ਬੇਸ ਮਾਡਲ ਨਾਮ (ਬਿਨਾਂ `-cpu` ਸੁਫਿਕਸ) ਨਾਲ ਅਪਡੇਟ ਕਰੋ:

```python
CATALOG = {
    'phi-4-mini': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini': {'capabilities':['code','refactor'],'priority':3},
}
```
  
Foundry Local SDK ਤੁਹਾਡੇ ਹਾਰਡਵੇਅਰ ਲਈ ਸਬ ਤੋਂ ਵਧੀਆ ਵਰਜਨ (CPU, GPU, ਜਾਂ NPU) ਆਟੋਮੈਟਿਕ ਤੌਰ 'ਤੇ ਚੁਣੇਗਾ।  

---

### 🔴 HttpResponseError: 500 - ਮਾਡਲ ਲੋਡ ਕਰਨ ਵਿੱਚ ਅਸਫਲ

**ਐਰਰ ਮੈਸੇਜ:**
```
HttpResponseError: 500 - Failed loading model
```
  
**ਮੂਲ ਕਾਰਨ:** ਮਾਡਲ ਫਾਈਲ ਕਰਪਟ ਹੋ ਗਈ ਹੈ ਜਾਂ ਹਾਰਡਵੇਅਰ ਨਾਲ ਅਨੁਕੂਲ ਨਹੀਂ ਹੈ।

**ਹੱਲ:**

#### ਮਾਡਲ ਦੁਬਾਰਾ ਡਾਊਨਲੋਡ ਕਰੋ
```bash
# Remove corrupted model
foundry model remove phi-3.5-mini

# Download fresh copy
foundry model download phi-3.5-mini
```
  
#### ਵੱਖਰੇ ਵਰਜਨ ਦੀ ਵਰਤੋਂ ਕਰੋ
```bash
# Try CPU variant instead
foundry model download phi-3.5-mini-cpu
```
  
---

### 🔴 ImportError: ਕੋਈ ਮੋਡਿਊਲ ਨਹੀਂ ਮਿਲਿਆ

**ਐਰਰ ਮੈਸੇਜ:**
```
ModuleNotFoundError: No module named 'foundry_local'
```
  
**ਮੂਲ ਕਾਰਨ:** foundry-local-sdk ਪੈਕੇਜ ਇੰਸਟਾਲ ਨਹੀਂ ਹੈ।

**ਹੱਲ:**

```bash
# Install SDK
pip install foundry-local-sdk

# Verify installation
pip show foundry-local-sdk
python -c "from foundry_local import FoundryLocalManager; print('SDK OK')"
```
  
---

### � ਪਹਿਲੀ ਬੇਨਤੀ ਧੀਮੀ

**ਲੱਛਣ:** ਪਹਿਲੀ completion ਵਿੱਚ 30+ ਸਕਿੰਟ ਲੱਗਦੇ ਹਨ, ਬਾਅਦ ਦੀਆਂ ਬੇਨਤੀਆਂ ਤੇਜ਼ ਹੁੰਦੀਆਂ ਹਨ।

**ਮੂਲ ਕਾਰਨ:** ਇਹ ਆਮ ਵਿਵਹਾਰ ਹੈ - ਸੇਵਾ ਪਹਿਲੀ ਬੇਨਤੀ 'ਤੇ ਮਾਡਲ ਨੂੰ ਮੈਮਰੀ ਵਿੱਚ ਲੋਡ ਕਰ ਰਹੀ ਹੈ।

**ਹੱਲ:**

#### ਮਾਡਲ ਪਹਿਲਾਂ ਹੀ ਲੋਡ ਕਰੋ
```bash
# Download and load all models you'll use before running notebooks
foundry model download phi-4-mini
foundry model download qwen2.5-3b
foundry model download phi-3.5-mini

foundry model run phi-4-mini
foundry model run qwen2.5-3b
```
  
#### ਸੇਵਾ ਚੱਲਦੀ ਰਹਿਣ ਦਿਓ
```bash
# Start service manually and leave it running
foundry service start
```
  
---

## ਸੈਸ਼ਨ 04 ਨਾਲ ਸੰਬੰਧਿਤ ਸਮੱਸਿਆਵਾਂ

### ਗਲਤ ਪੋਰਟ ਕਨਫਿਗਰੇਸ਼ਨ

**ਸਮੱਸਿਆ:** ਨੋਟਬੁੱਕ ਗਲਤ ਪੋਰਟ (55769 vs 59959 vs 57127) ਨਾਲ ਜੁੜ ਰਹੀ ਹੈ।

**ਹੱਲ:**

1. ਚੈੱਕ ਕਰੋ ਕਿ Foundry Local ਕਿਹੜੀ ਪੋਰਟ ਵਰਤ ਰਿਹਾ ਹੈ:
```bash
foundry service status
# Note the port number displayed
```
  
2. ਨੋਟਬੁੱਕ ਵਿੱਚ ਸੈਲ 10 ਅਪਡੇਟ ਕਰੋ:
```python
ENDPOINT = os.getenv('FOUNDRY_LOCAL_ENDPOINT', 'http://localhost:59959/v1')
# Replace 59959 with your actual port
```
  
3. ਕਰਨਲ ਰੀਸਟਾਰਟ ਕਰੋ ਅਤੇ ਸੈਲ 6, 8, 10, 12, 16, 20, 22 ਦੁਬਾਰਾ ਚਲਾਓ।  

---

### ਗਲਤ ਮਾਡਲ ਚੋਣ

**ਸਮੱਸਿਆ:** ਨੋਟਬੁੱਕ gpt-oss-20b ਜਾਂ qwen2.5-7b ਦਿਖਾ ਰਿਹਾ ਹੈ ਬਜਾਏ qwen2.5-3b ਦੇ।

**ਹੱਲ:**

1. ਨੋਟਬੁੱਕ ਕਰਨਲ ਰੀਸਟਾਰਟ ਕਰੋ (ਪੁਰਾਣੀ ਵੈਰੀਏਬਲ ਸਥਿਤੀ ਸਾਫ਼ ਕਰਦਾ ਹੈ)।  
2. ਸੈਲ 10 ਦੁਬਾਰਾ ਚਲਾਓ (Set Model Aliases)।  
3. ਸੈਲ 12 ਦੁਬਾਰਾ ਚਲਾਓ (Display Configuration)।  
4. **ਪੁਸ਼ਟੀ ਕਰੋ:** ਸੈਲ 12 'ਤੇ `LLM Model: qwen2.5-3b` ਦਿਖਣਾ ਚਾਹੀਦਾ ਹੈ।  

---

### ਡਾਇਗਨੋਸਟਿਕ ਸੈਲ ਫੇਲ

**ਸਮੱਸਿਆ:** ਸੈਲ 16 "❌ Foundry Local service not found!" ਦਿਖਾਉਂਦਾ ਹੈ।

**ਹੱਲ:**

1. ਪੁਸ਼ਟੀ ਕਰੋ ਕਿ ਸੇਵਾ ਚੱਲ ਰਹੀ ਹੈ:
```bash
foundry service status
```
  
2. ਐਂਡਪੌਇੰਟ ਨੂੰ ਮੈਨੁਅਲੀ ਤੌਰ 'ਤੇ ਟੈਸਟ ਕਰੋ:
```bash
curl http://localhost:59959/v1/models
```
  
3. ਜੇ curl ਕੰਮ ਕਰਦਾ ਹੈ ਪਰ ਨੋਟਬੁੱਕ ਨਹੀਂ:
   - ਨੋਟਬੁੱਕ ਕਰਨਲ ਰੀਸਟਾਰਟ ਕਰੋ  
   - ਸੈਲ 6, 8, 10, 12, 14, 16 ਨੂੰ ਕ੍ਰਮਵਾਰ ਦੁਬਾਰਾ ਚਲਾਓ।  

4. ਜੇ curl ਫੇਲ ਹੁੰਦਾ ਹੈ:
   - ਸੇਵਾ ਸ਼ੁਰੂ ਕਰੋ: `foundry service start`  
   - ਮਾਡਲ ਲੋਡ ਕਰੋ: `foundry model run phi-4-mini` ਅਤੇ `foundry model run qwen2.5-3b`  

---

### ਪ੍ਰੀ-ਫਲਾਈਟ ਚੈੱਕ ਫੇਲ

**ਸਮੱਸਿਆ:** ਸੈਲ 20 ਕਨੈਕਸ਼ਨ ਐਰਰ ਦਿਖਾਉਂਦਾ ਹੈ ਹਾਲਾਂਕਿ ਡਾਇਗਨੋਸਟਿਕ ਪਾਸ ਹੋ ਗਿਆ।

**ਹੱਲ:**

1. ਚੈੱਕ ਕਰੋ ਕਿ ਮਾਡਲ ਲੋਡ ਹੋਏ ਹਨ:
```bash
foundry model ls
# Should show phi-4-mini and qwen2.5-3b
```
  
2. ਜੇ ਮਾਡਲ ਗੁੰਮ ਹਨ:
```bash
foundry model run phi-4-mini
foundry model run qwen2.5-3b
```
  
3. ਮਾਡਲ ਲੋਡ ਹੋਣ ਤੋਂ ਬਾਅਦ ਸੈਲ 20 ਦੁਬਾਰਾ ਚਲਾਓ।  

---

### None ਵੈਲਿਊਜ਼ ਨਾਲ ਤੁਲਨਾ ਫੇਲ

**ਸਮੱਸਿਆ:** ਸੈਲ 22 ਪੂਰਾ ਹੋ ਜਾਂਦਾ ਹੈ ਪਰ latency ਨੂੰ None ਦਿਖਾਉਂਦਾ ਹੈ।

**ਹੱਲ:**

1. ਪਹਿਲਾਂ ਪ੍ਰੀ-ਫਲਾਈਟ ਪਾਸ ਹੋਣ ਦੀ ਪੁਸ਼ਟੀ ਕਰੋ (ਸੈਲ 20)।  
2. ਸੈਲ 22 ਦੁਬਾਰਾ ਚਲਾਓ - ਮਾਡਲ ਨੂੰ ਪਹਿਲੀ ਬੇਨਤੀ 'ਤੇ ਗਰਮ ਹੋਣ ਦੀ ਲੋੜ ਹੋ ਸਕਦੀ ਹੈ।  
3. ਦੋਵੇਂ ਮਾਡਲ ਲੋਡ ਹੋਣ ਦੀ ਪੁਸ਼ਟੀ ਕਰੋ: `foundry model ls`  

---

## ਸੈਸ਼ਨ 05 ਨਾਲ ਸੰਬੰਧਿਤ ਸਮੱਸਿਆਵਾਂ

### ਏਜੰਟ ਗਲਤ ਮਾਡਲ ਵਰਤ ਰਿਹਾ ਹੈ

**ਸਮੱਸਿਆ:** ਏਜੰਟ ਉਮੀਦ ਕੀਤੇ ਮਾਡਲ ਦੀ ਵਰਤੋਂ ਨਹੀਂ ਕਰ ਰਿਹਾ।

**ਹੱਲ:**

ਕਨਫਿਗਰੇਸ਼ਨ ਦੀ ਪੁਸ਼ਟੀ ਕਰੋ:
```python
# Check which models are assigned
print(f"Researcher: {researcher.model_id}")
print(f"Editor: {editor.model_id}")
```
  
ਜੇ ਮਾਡਲ ਗਲਤ ਹਨ ਤਾਂ ਕਰਨਲ ਰੀਸਟਾਰਟ ਕਰੋ।  

---

### ਮੈਮਰੀ ਕਨਟੈਕਸਟ ਓਵਰਫਲੋ

**ਸਮੱਸਿਆ:** ਸਮੇਂ ਦੇ ਨਾਲ ਏਜੰਟ ਦੇ ਜਵਾਬ ਖਰਾਬ ਹੋ ਰਹੇ ਹਨ।

**ਹੱਲ:** ਇਹ ਪਹਿਲਾਂ ਹੀ ਆਟੋਮੈਟਿਕ ਤੌਰ 'ਤੇ ਹੱਲ ਕੀਤਾ ਗਿਆ ਹੈ - ਏਜੰਟ ਮੈਮਰੀ ਵਿੱਚ ਸਿਰਫ਼ ਪਿਛਲੇ 6 ਸੁਨੇਹੇ ਰੱਖਦੇ ਹਨ।  

---

## ਸੈਸ਼ਨ 06 ਨਾਲ ਸੰਬੰਧਿਤ ਸਮੱਸਿਆਵਾਂ

### CPU vs GPU ਮਾਡਲ ਦਾ ਗੁੰਝਲ

**ਸਮੱਸਿਆ:** ਡਿਫਾਲਟ ਕਨਫਿਗਰੇਸ਼ਨ ਵਰਤਦੇ ਸਮੇਂ CUDA ਐਰਰ ਆ ਰਹੇ ਹਨ।

**ਹੱਲ:** ਡਿਫਾਲਟ ਕਨਫਿਗਰੇਸ਼ਨ ਹੁਣ CPU ਮਾਡਲ ਵਰਤਦਾ ਹੈ। ਜੇ CUDA ਐਰਰ ਆਉਂਦੇ ਹਨ:

1. ਪੁਸ਼ਟੀ ਕਰੋ ਕਿ ਤੁਸੀਂ ਡਿਫਾਲਟ CPU ਕੈਟਾਲੌਗ ਵਰਤ ਰਹੇ ਹੋ:
```python
# Cell should show CPU variants
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```
  
2. ਕਰਨਲ ਰੀਸਟਾਰਟ ਕਰੋ ਅਤੇ ਸਾਰੇ ਸੈਲ ਦੁਬਾਰਾ ਚਲਾਓ।  

---

### ਇੰਟੈਂਟ ਡਿਟੈਕਸ਼ਨ ਕੰਮ ਨਹੀਂ ਕਰ ਰਿਹਾ

**ਸਮੱਸਿਆ:** ਪ੍ਰੋਮਪਟ ਗਲਤ ਮਾਡਲਾਂ ਵੱਲ ਰੂਟ ਹੋ ਰਹੇ ਹਨ।

**ਹੱਲ:**

ਇੰਟੈਂਟ ਡਿਟੈਕਸ਼ਨ ਟੈਸਟ ਕਰੋ:
```python
# Run the intent detection test cell
for prompt in test_prompts:
    intent = detect_intent(prompt)
    print(f"{prompt[:50]}... → {intent}")
```
  
ਜੇ ਪੈਟਰਨਸ ਨੂੰ ਸਮਾਧਾਨ ਦੀ ਲੋੜ ਹੈ ਤਾਂ RULES ਅਪਡੇਟ ਕਰੋ।  

---

## ਹਾਰਡਵੇਅਰ-ਸਪੈਸਿਫਿਕ ਸਮੱਸਿਆਵਾਂ

### NVIDIA GPU

**GPU ਸਥਿਤੀ ਚੈੱਕ ਕਰੋ:**
```bash
nvidia-smi
```
  
**ਆਮ ਸਮੱਸਿਆਵਾਂ:**
- **ਡ੍ਰਾਈਵਰ ਪੁਰਾਣੇ ਹਨ:** NVIDIA ਡ੍ਰਾਈਵਰ ਅਪਡੇਟ ਕਰੋ।  
- **CUDA ਵਰਜਨ ਮਿਸਮੈਚ:** Foundry Local ਨੂੰ ਦੁਬਾਰਾ ਇੰਸਟਾਲ ਕਰੋ।  
- **GPU ਮੈਮਰੀ ਫ੍ਰੈਗਮੈਂਟਡ:** ਸਿਸਟਮ ਰੀਸਟਾਰਟ ਕਰੋ।  

### Qualcomm NPU

**NPU ਸਥਿਤੀ ਚੈੱਕ ਕਰੋ:**
```bash
foundry device info
```
  
**ਆਮ ਸਮੱਸਿਆਵਾਂ:**
- **NPU ਡ੍ਰਾਈਵਰ ਇੰਸਟਾਲ ਨਹੀਂ ਹਨ:** Qualcomm NPU ਡ੍ਰਾਈਵਰ ਇੰਸਟਾਲ ਕਰੋ।  
- **NPU ਵਰਜਨ ਉਪਲਬਧ ਨਹੀਂ:** CPU ਵਰਜਨ ਦੀ ਵਰਤੋਂ ਕਰੋ।  
- **Windows ਵਰਜਨ ਬਹੁਤ ਪੁਰਾਣਾ:** ਨਵੀਂਤਮ Windows 11 'ਤੇ ਅਪਡੇਟ ਕਰੋ।  

### ਸਿਰਫ਼ CPU ਸਿਸਟਮ

**ਸਿਫਾਰਸ਼ੀ ਮਾਡਲ:**
```python
CATALOG = {
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','general'],'priority':2},
}
```
  
**ਪਰਫਾਰਮੈਂਸ ਟਿਪਸ:**
- ਸਭ ਤੋਂ ਛੋਟੇ ਮਾਡਲ ਵਰਤੋ।  
- max_tokens ਘਟਾਓ।  
- ਪਹਿਲੀ ਬੇਨਤੀ ਲਈ ਧੀਰਜ ਰੱਖੋ।  

---

## ਡਾਇਗਨੋਸਟਿਕ ਕਮਾਂਡ

### ਸਭ ਕੁਝ ਚੈੱਕ ਕਰੋ
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
  
### Python ਵਿੱਚ
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

## ਮਦਦ ਪ੍ਰਾਪਤ ਕਰਨਾ

### 1. ਲੌਗਸ ਚੈੱਕ ਕਰੋ
```bash
# Windows
foundry service logs

# Or check Windows Event Viewer
# Application Logs -> Microsoft-FoundryLocal
```
  
### 2. GitHub Issues
- ਮੌਜੂਦਾ ਸਮੱਸਿਆਵਾਂ ਦੀ ਖੋਜ ਕਰੋ: https://github.com/microsoft/Foundry-Local/issues  
- ਨਵੀਂ ਸਮੱਸਿਆ ਬਣਾਓ:  
  - ਐਰਰ ਮੈਸੇਜ (ਪੂਰਾ ਟੈਕਸਟ)  
  - `foundry service status` ਦਾ ਆਉਟਪੁੱਟ  
  - `foundry --version` ਦਾ ਆਉਟਪੁੱਟ  
  - GPU/NPU ਜਾਣਕਾਰੀ (nvidia-smi, ਆਦਿ)  
  - ਦੁਹਰਾਉਣ ਦੇ ਕਦਮ  

### 3. ਦਸਤਾਵੇਜ਼
- **ਮੁੱਖ ਰਿਪੋਜ਼ਟਰੀ:** https://github.com/microsoft/Foundry-Local  
- **Python SDK:** https://github.com/microsoft/Foundry-Local/tree/main/sdk/python  
- **CLI ਰਿਫਰੈਂਸ:** https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-cli.md  
- **ਟਰਬਲਸ਼ੂਟਿੰਗ:** https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-troubleshooting.md  

---

## ਕਵਿਕ ਫਿਕਸ ਚੈੱਕਲਿਸਟ

ਜਦੋਂ ਕੁਝ ਗਲਤ ਹੋਵੇ, ਇਹ ਕਦਮ ਲਗਾਤਾਰ ਅਜ਼ਮਾਓ:

- [ ] ਸੇਵਾ ਚੱਲ ਰਹੀ ਹੈ ਜਾਂ ਨਹੀਂ ਚੈੱਕ ਕਰੋ: `foundry service status`  
- [ ] ਸੇਵਾ ਰੀਸਟਾਰਟ ਕਰੋ: `foundry service stop && foundry service start`  
- [ ] ਮਾਡਲ ਮੌਜੂਦ ਹੈ ਜਾਂ ਨਹੀਂ ਚੈੱਕ ਕਰੋ: `foundry model ls | grep phi-4-mini`  
- [ ] ਲੋੜੀਂਦੇ ਮਾਡਲ ਲੋਡ ਕਰੋ: `foundry model run phi-4-mini`  
- [ ] GPU ਮੈਮਰੀ ਚੈੱਕ ਕਰੋ: `nvidia-smi` (ਜੇ NVIDIA ਹੈ)  
- [ ] CPU ਵਰਜਨ ਅਜ਼ਮਾਓ: `phi-4-mini-cpu` ਦੀ ਵਰਤੋਂ ਕਰੋ।  
- [ ] ਨੋਟਬੁੱਕ ਕਰਨਲ ਰੀਸਟਾਰਟ ਕਰੋ।  
- [ ] ਨੋਟਬੁੱਕ ਆਉਟਪੁੱਟ ਸਾਫ਼ ਕਰੋ ਅਤੇ ਸਾਰੇ ਸੈਲ ਦੁਬਾਰਾ ਚਲਾਓ।  
- [ ] SDK ਦੁਬਾਰਾ ਇੰਸਟਾਲ ਕਰੋ: `pip install --upgrade --force-reinstall foundry-local-sdk`  
- [ ] ਸਿਸਟਮ ਰੀਬੂਟ ਕਰੋ (ਆਖਰੀ ਵਿਕਲਪ)।  

---

## ਰੋਕਥਾਮ ਟਿਪਸ

### ਸ੍ਰੇਸ਼ਠ ਅਭਿਆਸ

1. **ਸਭ ਤੋਂ ਪਹਿਲਾਂ ਸੇਵਾ ਚੈੱਕ ਕਰੋ:**
   ```bash
   foundry service status
   ```
  
2. **ਡਿਫਾਲਟ ਤੌਰ 'ਤੇ CPU ਵਰਜਨ ਦੀ ਵਰਤੋਂ ਕਰੋ:**
   ```python
   CATALOG = {
       'phi-4-mini-cpu': {...},
       'qwen2.5-0.5b-cpu': {...},
   }
   ```
  
3. **ਨੋਟਬੁੱਕ ਚਲਾਉਣ ਤੋਂ ਪਹਿਲਾਂ ਮਾਡਲ ਲੋਡ ਕਰੋ:**
   ```bash
   foundry model run phi-4-mini
   foundry model run qwen2.5-3b
   ```
  
4. **ਸੇਵਾ ਚੱਲਦੀ ਰਹਿਣ ਦਿਓ:**
   - ਸੇਵਾ ਨੂੰ ਬੇਵਜ੍ਹਾ ਬੰਦ/ਸ਼ੁਰੂ ਨਾ ਕਰੋ।  
   - ਸੈਸ਼ਨ ਦੇ ਵਿਚਕਾਰ ਇਸਨੂੰ ਬੈਕਗ੍ਰਾਊਂਡ ਵਿੱਚ ਚੱਲਣ ਦਿਓ।  

5. **ਸੰਸਾਧਨਾਂ ਦੀ ਨਿਗਰਾਨੀ ਕਰੋ:**
   - ਨੋਟਬੁੱਕ ਚਲਾਉਣ ਤੋਂ ਪਹਿਲਾਂ GPU ਮੈਮਰੀ ਚੈੱਕ ਕਰੋ।  
   - ਬੇਵਜ੍ਹਾ GPU ਐਪਲੀਕੇਸ਼ਨ ਬੰਦ ਕਰੋ।  
   - Task Manager / nvidia-smi ਦੀ ਵਰਤੋਂ ਕਰੋ।  

6. **ਨਿਯਮਿਤ ਅਪਡੇਟ ਕਰੋ:**
   ```bash
   winget upgrade Microsoft.FoundryLocal
   pip install --upgrade foundry-local-sdk
   ```
  
---

**ਆਖਰੀ ਅਪਡੇਟ:** ਅਕਤੂਬਰ 8, 2025  

---

**ਅਸਵੀਕਰਤਾ**:  
ਇਹ ਦਸਤਾਵੇਜ਼ AI ਅਨੁਵਾਦ ਸੇਵਾ [Co-op Translator](https://github.com/Azure/co-op-translator) ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਅਨੁਵਾਦ ਕੀਤਾ ਗਿਆ ਹੈ। ਹਾਲਾਂਕਿ ਅਸੀਂ ਸਹੀਤਾ ਲਈ ਯਤਨਸ਼ੀਲ ਹਾਂ, ਕਿਰਪਾ ਕਰਕੇ ਧਿਆਨ ਦਿਓ ਕਿ ਸਵੈਚਾਲਿਤ ਅਨੁਵਾਦਾਂ ਵਿੱਚ ਗਲਤੀਆਂ ਜਾਂ ਅਸੁਚਨਾਵਾਂ ਹੋ ਸਕਦੀਆਂ ਹਨ। ਇਸ ਦੀ ਮੂਲ ਭਾਸ਼ਾ ਵਿੱਚ ਮੌਜੂਦ ਦਸਤਾਵੇਜ਼ ਨੂੰ ਅਧਿਕਾਰਤ ਸਰੋਤ ਮੰਨਿਆ ਜਾਣਾ ਚਾਹੀਦਾ ਹੈ। ਮਹੱਤਵਪੂਰਨ ਜਾਣਕਾਰੀ ਲਈ, ਪੇਸ਼ੇਵਰ ਮਨੁੱਖੀ ਅਨੁਵਾਦ ਦੀ ਸਿਫਾਰਸ਼ ਕੀਤੀ ਜਾਂਦੀ ਹੈ। ਇਸ ਅਨੁਵਾਦ ਦੀ ਵਰਤੋਂ ਤੋਂ ਪੈਦਾ ਹੋਣ ਵਾਲੇ ਕਿਸੇ ਵੀ ਗਲਤਫਹਿਮੀ ਜਾਂ ਗਲਤ ਵਿਆਖਿਆ ਲਈ ਅਸੀਂ ਜ਼ਿੰਮੇਵਾਰ ਨਹੀਂ ਹਾਂ।