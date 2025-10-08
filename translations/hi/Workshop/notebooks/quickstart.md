<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "ddaad917d0c16fc3d498a6b4eabc8088",
  "translation_date": "2025-10-08T22:04:44+00:00",
  "source_file": "Workshop/notebooks/quickstart.md",
  "language_code": "hi"
}
-->
# वर्कशॉप नोटबुक्स - त्वरित प्रारंभ गाइड

## सामग्री तालिका

- [पूर्व आवश्यकताएँ](../../../../Workshop/notebooks)
- [प्रारंभिक सेटअप](../../../../Workshop/notebooks)
- [सत्र 04: मॉडल तुलना](../../../../Workshop/notebooks)
- [सत्र 05: मल्टी-एजेंट ऑर्केस्ट्रेटर](../../../../Workshop/notebooks)
- [सत्र 06: इरादे-आधारित मॉडल रूटिंग](../../../../Workshop/notebooks)
- [पर्यावरण चर](../../../../Workshop/notebooks)
- [सामान्य कमांड्स](../../../../Workshop/notebooks)

---

## पूर्व आवश्यकताएँ

### 1. Foundry Local इंस्टॉल करें

**Windows:**
```bash
winget install Microsoft.FoundryLocal
```

**macOS:**
```bash
brew tap microsoft/foundrylocal
brew install foundrylocal
```

**इंस्टॉलेशन सत्यापित करें:**
```bash
foundry --version
```

### 2. Python डिपेंडेंसी इंस्टॉल करें

```bash
cd Workshop
pip install -r requirements.txt
```

या व्यक्तिगत रूप से इंस्टॉल करें:
```bash
pip install foundry-local-sdk openai numpy requests
```

---

## प्रारंभिक सेटअप

### Foundry Local सेवा शुरू करें

**किसी भी नोटबुक को चलाने से पहले आवश्यक:**

```bash
# Start the service
foundry service start

# Verify it's running
foundry service status
```

अपेक्षित आउटपुट:
```
✅ Service started successfully
Endpoint: http://localhost:59959
```

### मॉडल डाउनलोड और लोड करें

नोटबुक्स डिफ़ॉल्ट रूप से इन मॉडलों का उपयोग करते हैं:

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

### सेटअप सत्यापित करें

```bash
# List loaded models
foundry model ls

# Check service health
curl http://localhost:59959/v1/models
```

---

## सत्र 04: मॉडल तुलना

### उद्देश्य
छोटे भाषा मॉडल (SLM) और बड़े भाषा मॉडल (LLM) के प्रदर्शन की तुलना करें।

### त्वरित सेटअप

```bash
# Start service (if not already running)
foundry service start

# Load required models
foundry model run phi-4-mini
foundry model run qwen2.5-3b
```

### नोटबुक चलाना

1. **खोलें** `session04_model_compare.ipynb` VS Code या Jupyter में
2. **कर्नेल रीस्टार्ट करें** (Kernel → Restart Kernel)
3. **सभी सेल्स क्रम में चलाएँ**

### मुख्य कॉन्फ़िगरेशन

**डिफ़ॉल्ट मॉडल्स:**
- **SLM:** `phi-4-mini` (~4GB RAM, तेज़)
- **LLM:** `qwen2.5-3b` (~3GB RAM, मेमोरी-ऑप्टिमाइज़्ड)

**पर्यावरण चर (वैकल्पिक):**
```python
import os
os.environ['SLM_ALIAS'] = 'phi-4-mini'
os.environ['LLM_ALIAS'] = 'qwen2.5-3b'
os.environ['FOUNDRY_LOCAL_ENDPOINT'] = 'http://localhost:59959/v1'
```

### अपेक्षित आउटपुट

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

### अनुकूलन

**विभिन्न मॉडल्स का उपयोग करें:**
```python
os.environ['SLM_ALIAS'] = 'phi-3.5-mini'
os.environ['LLM_ALIAS'] = 'qwen2.5-1.5b'
```

**कस्टम प्रॉम्प्ट:**
```python
os.environ['COMPARE_PROMPT'] = 'Explain quantum computing in simple terms'
```

### सत्यापन चेकलिस्ट

- [ ] सेल 12 सही मॉडल्स दिखाता है (phi-4-mini, qwen2.5-3b)
- [ ] सेल 12 सही एंडपॉइंट दिखाता है (पोर्ट 59959)
- [ ] सेल 16 डायग्नोस्टिक पास करता है (✅ सेवा चल रही है)
- [ ] सेल 20 प्री-फ्लाइट चेक पास करता है (दोनों मॉडल्स ठीक हैं)
- [ ] सेल 22 तुलना पूरी होती है लेटेंसी मानों के साथ
- [ ] सेल 24 सत्यापन दिखाता है 🎉 सभी चेक पास हुए!

### समय अनुमान
- **पहली बार चलाना:** 5-10 मिनट (मॉडल डाउनलोड सहित)
- **अगली बार चलाना:** 1-2 मिनट

---

## सत्र 05: मल्टी-एजेंट ऑर्केस्ट्रेटर

### उद्देश्य
Foundry Local SDK का उपयोग करके मल्टी-एजेंट सहयोग प्रदर्शित करें - एजेंट्स मिलकर परिष्कृत आउटपुट तैयार करते हैं।

### त्वरित सेटअप

```bash
# Start service
foundry service start

# Load models
foundry model run phi-4-mini  # Primary model
foundry model run qwen2.5-7b  # Optional: higher quality editor
```

### नोटबुक चलाना

1. **खोलें** `session05_agents_orchestrator.ipynb`
2. **कर्नेल रीस्टार्ट करें**
3. **सभी सेल्स क्रम में चलाएँ**

### मुख्य कॉन्फ़िगरेशन

**डिफ़ॉल्ट सेटअप (दोनों एजेंट्स के लिए समान मॉडल):**
```python
PRIMARY_ALIAS = 'phi-4-mini'
EDITOR_ALIAS = 'phi-4-mini'  # Uses same model
```

**उन्नत सेटअप (विभिन्न मॉडल्स):**
```python
import os
os.environ['AGENT_MODEL_PRIMARY'] = 'phi-4-mini'     # Fast for research
os.environ['AGENT_MODEL_EDITOR'] = 'qwen2.5-7b'      # High quality for editing
```

### आर्किटेक्चर

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

### अपेक्षित आउटपुट

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

### एक्सटेंशन

**अधिक एजेंट्स जोड़ें:**
```python
critic = Agent(
    name='Critic',
    system='Review content for accuracy',
    client=client,
    model_id=model_id
)
```

**बैच परीक्षण:**
```python
test_questions = [
    "What are benefits of local AI?",
    "How does RAG improve accuracy?",
]

for q in test_questions:
    result = pipeline(q, verbose=False)
    print(result['final'])
```

### समय अनुमान
- **पहली बार चलाना:** 3-5 मिनट
- **अगली बार चलाना:** प्रति प्रश्न 1-2 मिनट

---

## सत्र 06: इरादे-आधारित मॉडल रूटिंग

### उद्देश्य
पता लगाए गए इरादे के आधार पर प्रॉम्प्ट्स को विशेष मॉडल्स की ओर बुद्धिमानी से रूट करें।

### त्वरित सेटअप

```bash
# Start service
foundry service start

# Load all routing models (CPU variants recommended)
foundry model run phi-4-mini-cpu
foundry model run qwen2.5-0.5b-cpu
foundry model run phi-3.5-mini-cpu
```

**नोट:** सत्र 06 अधिकतम संगतता के लिए CPU मॉडल्स पर डिफ़ॉल्ट है।

### नोटबुक चलाना

1. **खोलें** `session06_models_router.ipynb`
2. **कर्नेल रीस्टार्ट करें**
3. **सभी सेल्स क्रम में चलाएँ**

### मुख्य कॉन्फ़िगरेशन

**डिफ़ॉल्ट कैटलॉग (CPU मॉडल्स):**
```python
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```

**वैकल्पिक (GPU मॉडल्स):**
```python
# Uncomment GPU catalog in Cell #6 if you have sufficient VRAM (8GB+)
CATALOG = {
    'phi-4-mini': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini': {'capabilities':['code','refactor'],'priority':3},
}
```

### इरादा पहचान

राउटर इरादे का पता लगाने के लिए regex पैटर्न का उपयोग करता है:

| इरादा | पैटर्न उदाहरण | रूट किया गया |
|-------|---------------|-------------|
| `code` | "refactor", "implement function" | phi-3.5-mini-cpu |
| `classification` | "categorize", "classify this" | qwen2.5-0.5b-cpu |
| `summarize` | "summarize", "tl;dr" | phi-4-mini-cpu |
| `general` | अन्य सभी | phi-4-mini-cpu |

### अपेक्षित आउटपुट

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

### अनुकूलन

**कस्टम इरादा जोड़ें:**
```python
import re

# Add to RULES
RULES.append((re.compile('translate|翻译', re.I), 'translation'))

# Add capability to catalog
CATALOG['phi-4-mini-cpu']['capabilities'].append('translation')
```

**टोकन ट्रैकिंग सक्षम करें:**
```python
import os
os.environ['SHOW_USAGE'] = '1'
```

### GPU मॉडल्स पर स्विच करना

यदि आपके पास 8GB+ VRAM है:

1. **सेल #6** में, CPU कैटलॉग को कमेंट करें
2. GPU कैटलॉग को अनकमेंट करें
3. GPU मॉडल्स लोड करें:
   ```bash
   foundry model run phi-4-mini
   foundry model run qwen2.5-0.5b
   foundry model run phi-3.5-mini
   ```
4. कर्नेल रीस्टार्ट करें और नोटबुक फिर से चलाएँ

### समय अनुमान
- **पहली बार चलाना:** 5-10 मिनट (मॉडल लोडिंग)
- **अगली बार चलाना:** प्रति परीक्षण 30-60 सेकंड

---

## पर्यावरण चर

### वैश्विक कॉन्फ़िगरेशन

Jupyter/VS Code शुरू करने से पहले सेट करें:

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

### नोटबुक में कॉन्फ़िगरेशन

किसी भी नोटबुक की शुरुआत में सेट करें:

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

## सामान्य कमांड्स

### सेवा प्रबंधन

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

### मॉडल प्रबंधन

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

### एंडपॉइंट परीक्षण

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

### डायग्नोस्टिक कमांड्स

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

## सर्वोत्तम प्रथाएँ

### किसी भी नोटबुक को शुरू करने से पहले

1. **जाँचें कि सेवा चल रही है:**
   ```bash
   foundry service status
   ```

2. **सत्यापित करें कि मॉडल्स लोड हो चुके हैं:**
   ```bash
   foundry model ls
   ```

3. **नोटबुक कर्नेल रीस्टार्ट करें** यदि फिर से चला रहे हैं

4. **सभी आउटपुट साफ़ करें** एक साफ़ रन के लिए

### संसाधन प्रबंधन

1. **डिफ़ॉल्ट रूप से CPU मॉडल्स का उपयोग करें** संगतता के लिए
2. **GPU मॉडल्स पर स्विच करें** केवल यदि आपके पास 8GB+ VRAM है
3. **GPU एप्लिकेशन बंद करें** चलाने से पहले
4. **सेवा चालू रखें** नोटबुक सत्रों के बीच
5. **संसाधन उपयोग की निगरानी करें** Task Manager / nvidia-smi के साथ

### समस्या निवारण

1. **कोड डिबग करने से पहले हमेशा सेवा की जाँच करें**
2. **कर्नेल रीस्टार्ट करें** यदि पुरानी कॉन्फ़िगरेशन दिखती है
3. **डायग्नोस्टिक सेल्स फिर से चलाएँ** किसी भी बदलाव के बाद
4. **मॉडल नाम सत्यापित करें** जो लोड हो चुके हैं
5. **एंडपॉइंट पोर्ट सत्यापित करें** जो सेवा स्थिति से मेल खाता है

---

## त्वरित संदर्भ: मॉडल उपनाम

### सामान्य मॉडल्स

| उपनाम | आकार | सर्वश्रेष्ठ उपयोग | RAM/VRAM | वेरिएंट्स |
|-------|------|------------------|----------|-----------|
| `phi-4-mini` | ~4B | सामान्य चैट, सारांश | 4-6GB | `-cpu`, `-cuda-gpu`, `-npu` |
| `phi-3.5-mini` | ~3.5B | कोड जनरेशन, रिफैक्टरिंग | 3-5GB | `-cpu`, `-cuda-gpu`, `-npu` |
| `qwen2.5-3b` | ~3B | सामान्य कार्य, कुशल | 3-4GB | `-cpu`, `-cuda-gpu` |
| `qwen2.5-1.5b` | ~1.5B | तेज़, कम संसाधन | 2-3GB | `-cpu`, `-cuda-gpu` |
| `qwen2.5-0.5b` | ~0.5B | वर्गीकरण, न्यूनतम संसाधन | 1-2GB | `-cpu`, `-cuda-gpu` |

### वेरिएंट नामकरण

- **बेस नाम** (जैसे, `phi-4-mini`): आपके हार्डवेयर के लिए सर्वश्रेष्ठ वेरिएंट को ऑटो-चुनता है
- **`-cpu`**: CPU-ऑप्टिमाइज़्ड, हर जगह काम करता है
- **`-cuda-gpu`**: NVIDIA GPU ऑप्टिमाइज़्ड, 8GB+ VRAM की आवश्यकता
- **`-npu`**: Qualcomm NPU ऑप्टिमाइज़्ड, NPU ड्राइवर्स की आवश्यकता

**सिफारिश:** बेस नाम (बिना उपसर्ग) का उपयोग करें और Foundry Local को सर्वश्रेष्ठ वेरिएंट ऑटो-चुनने दें।

---

## सफलता संकेतक

आप तैयार हैं जब आप देखें:

✅ `foundry service status` "running" दिखाता है  
✅ `foundry model ls` आपके आवश्यक मॉडल्स दिखाता है  
✅ सेवा सही एंडपॉइंट पर सुलभ है  
✅ हेल्थ चेक 200 OK लौटाता है  
✅ नोटबुक डायग्नोस्टिक सेल्स पास करते हैं  
✅ आउटपुट में कोई कनेक्शन त्रुटि नहीं है  

---

## सहायता प्राप्त करना

### दस्तावेज़ीकरण
- **मुख्य रिपॉजिटरी**: https://github.com/microsoft/Foundry-Local
- **Python SDK**: https://github.com/microsoft/Foundry-Local/tree/main/sdk/python
- **CLI संदर्भ**: https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-cli.md
- **समस्या निवारण**: इस निर्देशिका में `troubleshooting.md` देखें

### GitHub Issues
- https://github.com/microsoft/Foundry-Local/issues
- https://github.com/microsoft/edgeai-for-beginners/issues

---

**अंतिम अपडेट:** 8 अक्टूबर, 2025  
**संस्करण:** वर्कशॉप नोटबुक्स 2.0

---

**अस्वीकरण**:  
यह दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) का उपयोग करके अनुवादित किया गया है। जबकि हम सटीकता के लिए प्रयास करते हैं, कृपया ध्यान दें कि स्वचालित अनुवाद में त्रुटियां या अशुद्धियां हो सकती हैं। मूल भाषा में उपलब्ध मूल दस्तावेज़ को आधिकारिक स्रोत माना जाना चाहिए। महत्वपूर्ण जानकारी के लिए, पेशेवर मानव अनुवाद की सिफारिश की जाती है। इस अनुवाद के उपयोग से उत्पन्न किसी भी गलतफहमी या गलत व्याख्या के लिए हम उत्तरदायी नहीं हैं।