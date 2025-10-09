<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "ddaad917d0c16fc3d498a6b4eabc8088",
  "translation_date": "2025-10-09T09:51:25+00:00",
  "source_file": "Workshop/notebooks/quickstart.md",
  "language_code": "mr"
}
-->
# वर्कशॉप नोटबुक्स - जलद प्रारंभ मार्गदर्शिका

## विषय सूची

- [पूर्वतयारी](../../../../Workshop/notebooks)
- [प्रारंभिक सेटअप](../../../../Workshop/notebooks)
- [सत्र 04: मॉडेल तुलना](../../../../Workshop/notebooks)
- [सत्र 05: मल्टी-एजंट ऑर्केस्ट्रेटर](../../../../Workshop/notebooks)
- [सत्र 06: हेतूनुसार मॉडेल रूटिंग](../../../../Workshop/notebooks)
- [पर्यावरणीय व्हेरिएबल्स](../../../../Workshop/notebooks)
- [सामान्य कमांड्स](../../../../Workshop/notebooks)

---

## पूर्वतयारी

### 1. फाउंड्री लोकल स्थापित करा

**Windows:**
```bash
winget install Microsoft.FoundryLocal
```

**macOS:**
```bash
brew tap microsoft/foundrylocal
brew install foundrylocal
```

**स्थापना सत्यापित करा:**
```bash
foundry --version
```

### 2. Python डिपेंडन्सी स्थापित करा

```bash
cd Workshop
pip install -r requirements.txt
```

किंवा स्वतंत्रपणे स्थापित करा:
```bash
pip install foundry-local-sdk openai numpy requests
```

---

## प्रारंभिक सेटअप

### फाउंड्री लोकल सेवा सुरू करा

**कोणत्याही नोटबुक चालवण्यापूर्वी आवश्यक:**

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

### मॉडेल्स डाउनलोड आणि लोड करा

नोटबुक्स खालील मॉडेल्स वापरतात:

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

### सेटअप सत्यापित करा

```bash
# List loaded models
foundry model ls

# Check service health
curl http://localhost:59959/v1/models
```

---

## सत्र 04: मॉडेल तुलना

### उद्देश
लहान भाषा मॉडेल्स (SLM) आणि मोठ्या भाषा मॉडेल्स (LLM) यांच्यातील कार्यक्षमता तुलना करा.

### जलद सेटअप

```bash
# Start service (if not already running)
foundry service start

# Load required models
foundry model run phi-4-mini
foundry model run qwen2.5-3b
```

### नोटबुक चालवणे

1. **उघडा** `session04_model_compare.ipynb` VS Code किंवा Jupyter मध्ये
2. **कर्नल रीस्टार्ट करा** (Kernel → Restart Kernel)
3. **सर्व सेल्स चालवा** क्रमाने

### मुख्य कॉन्फिगरेशन

**डिफॉल्ट मॉडेल्स:**
- **SLM:** `phi-4-mini` (~4GB RAM, जलद)
- **LLM:** `qwen2.5-3b` (~3GB RAM, मेमरी-ऑप्टिमाइझ्ड)

**पर्यावरणीय व्हेरिएबल्स (पर्यायी):**
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

### सानुकूलन

**वेगळे मॉडेल्स वापरा:**
```python
os.environ['SLM_ALIAS'] = 'phi-3.5-mini'
os.environ['LLM_ALIAS'] = 'qwen2.5-1.5b'
```

**सानुकूल प्रॉम्प्ट:**
```python
os.environ['COMPARE_PROMPT'] = 'Explain quantum computing in simple terms'
```

### सत्यापन चेकलिस्ट

- [ ] सेल 12 योग्य मॉडेल्स दर्शवते (phi-4-mini, qwen2.5-3b)
- [ ] सेल 12 योग्य एंडपॉइंट दर्शवते (पोर्ट 59959)
- [ ] सेल 16 डायग्नोस्टिक पास होते (✅ सेवा चालू आहे)
- [ ] सेल 20 प्री-फ्लाइट चेक पास होते (दोन्ही मॉडेल्स ठीक)
- [ ] सेल 22 तुलना पूर्ण होते लेटन्सी व्हॅल्यूससह
- [ ] सेल 24 सत्यापन दर्शवते 🎉 सर्व चेक्स पास झाले!

### वेळ अंदाज
- **पहिला रन:** 5-10 मिनिटे (मॉडेल डाउनलोडसह)
- **पुढील रन:** 1-2 मिनिटे

---

## सत्र 05: मल्टी-एजंट ऑर्केस्ट्रेटर

### उद्देश
फाउंड्री लोकल SDK वापरून मल्टी-एजंट सहकार्याचे प्रदर्शन - एजंट्स एकत्रितपणे परिष्कृत आउटपुट तयार करतात.

### जलद सेटअप

```bash
# Start service
foundry service start

# Load models
foundry model run phi-4-mini  # Primary model
foundry model run qwen2.5-7b  # Optional: higher quality editor
```

### नोटबुक चालवणे

1. **उघडा** `session05_agents_orchestrator.ipynb`
2. **कर्नल रीस्टार्ट करा**
3. **सर्व सेल्स चालवा** क्रमाने

### मुख्य कॉन्फिगरेशन

**डिफॉल्ट सेटअप (दोन्ही एजंट्ससाठी समान मॉडेल):**
```python
PRIMARY_ALIAS = 'phi-4-mini'
EDITOR_ALIAS = 'phi-4-mini'  # Uses same model
```

**प्रगत सेटअप (वेगळे मॉडेल्स):**
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

### विस्तार

**अधिक एजंट्स जोडा:**
```python
critic = Agent(
    name='Critic',
    system='Review content for accuracy',
    client=client,
    model_id=model_id
)
```

**बॅच टेस्टिंग:**
```python
test_questions = [
    "What are benefits of local AI?",
    "How does RAG improve accuracy?",
]

for q in test_questions:
    result = pipeline(q, verbose=False)
    print(result['final'])
```

### वेळ अंदाज
- **पहिला रन:** 3-5 मिनिटे
- **पुढील रन:** प्रति प्रश्न 1-2 मिनिटे

---

## सत्र 06: हेतूनुसार मॉडेल रूटिंग

### उद्देश
आढळलेल्या हेतूनुसार प्रॉम्प्ट्स विशेष मॉडेल्सकडे बुद्धिमत्तेने रूट करा.

### जलद सेटअप

```bash
# Start service
foundry service start

# Load all routing models (CPU variants recommended)
foundry model run phi-4-mini-cpu
foundry model run qwen2.5-0.5b-cpu
foundry model run phi-3.5-mini-cpu
```

**टीप:** सत्र 06 CPU मॉडेल्सवर डिफॉल्ट आहे जास्तीत जास्त सुसंगततेसाठी.

### नोटबुक चालवणे

1. **उघडा** `session06_models_router.ipynb`
2. **कर्नल रीस्टार्ट करा**
3. **सर्व सेल्स चालवा** क्रमाने

### मुख्य कॉन्फिगरेशन

**डिफॉल्ट कॅटलॉग (CPU मॉडेल्स):**
```python
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```

**पर्यायी (GPU मॉडेल्स):**
```python
# Uncomment GPU catalog in Cell #6 if you have sufficient VRAM (8GB+)
CATALOG = {
    'phi-4-mini': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini': {'capabilities':['code','refactor'],'priority':3},
}
```

### हेतू ओळख

राउटर हेतू ओळखण्यासाठी regex पॅटर्न्स वापरतो:

| हेतू | पॅटर्न उदाहरणे | रूटेड टू |
|------|-----------------|----------|
| `code` | "refactor", "implement function" | phi-3.5-mini-cpu |
| `classification` | "categorize", "classify this" | qwen2.5-0.5b-cpu |
| `summarize` | "summarize", "tl;dr" | phi-4-mini-cpu |
| `general` | बाकी सर्व | phi-4-mini-cpu |

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

### सानुकूलन

**सानुकूल हेतू जोडा:**
```python
import re

# Add to RULES
RULES.append((re.compile('translate|翻译', re.I), 'translation'))

# Add capability to catalog
CATALOG['phi-4-mini-cpu']['capabilities'].append('translation')
```

**टोकन ट्रॅकिंग सक्षम करा:**
```python
import os
os.environ['SHOW_USAGE'] = '1'
```

### GPU मॉडेल्सवर स्विच करणे

जर तुमच्याकडे 8GB+ VRAM असेल:

1. **Cell #6** मध्ये CPU कॅटलॉग कॉमेंट करा
2. GPU कॅटलॉग अनकॉमेंट करा
3. GPU मॉडेल्स लोड करा:
   ```bash
   foundry model run phi-4-mini
   foundry model run qwen2.5-0.5b
   foundry model run phi-3.5-mini
   ```
4. कर्नल रीस्टार्ट करा आणि नोटबुक पुन्हा चालवा

### वेळ अंदाज
- **पहिला रन:** 5-10 मिनिटे (मॉडेल लोडिंग)
- **पुढील रन:** प्रति चाचणी 30-60 सेकंद

---

## पर्यावरणीय व्हेरिएबल्स

### ग्लोबल कॉन्फिगरेशन

Jupyter/VS Code सुरू करण्यापूर्वी सेट करा:

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

### नोटबुकमधील कॉन्फिगरेशन

कोणत्याही नोटबुकच्या सुरुवातीला सेट करा:

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

### सेवा व्यवस्थापन

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

### मॉडेल व्यवस्थापन

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

### एंडपॉइंट्स चाचणी

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

## सर्वोत्तम पद्धती

### कोणतेही नोटबुक सुरू करण्यापूर्वी

1. **सेवा चालू आहे का ते तपासा:**
   ```bash
   foundry service status
   ```

2. **मॉडेल्स लोड झाले आहेत का ते सत्यापित करा:**
   ```bash
   foundry model ls
   ```

3. **नोटबुक कर्नल रीस्टार्ट करा** जर पुन्हा चालवत असाल

4. **सर्व आउटपुट क्लिअर करा** स्वच्छ रनसाठी

### संसाधन व्यवस्थापन

1. **डिफॉल्टने CPU मॉडेल्स वापरा** सुसंगततेसाठी
2. **GPU मॉडेल्सवर स्विच करा** फक्त 8GB+ VRAM असल्यास
3. **इतर GPU अॅप्लिकेशन्स बंद करा** चालवण्यापूर्वी
4. **सेवा चालू ठेवा** नोटबुक सत्रांदरम्यान
5. **संसाधन वापर मॉनिटर करा** Task Manager / nvidia-smi सह

### समस्या निवारण

1. **कोड डीबग करण्यापूर्वी नेहमी सेवा तपासा**
2. **कर्नल रीस्टार्ट करा** जर जुन्या कॉन्फिगरेशन दिसत असेल
3. **डायग्नोस्टिक सेल्स पुन्हा चालवा** कोणत्याही बदलानंतर
4. **मॉडेल नावे तपासा** लोड केलेल्या मॉडेल्सशी जुळतात का
5. **एंडपॉइंट पोर्ट सत्यापित करा** सेवा स्थितीशी जुळते का

---

## जलद संदर्भ: मॉडेल उपनाम

### सामान्य मॉडेल्स

| उपनाम | आकार | सर्वोत्तम उपयोग | RAM/VRAM | प्रकार |
|-------|------|----------------|----------|-------|
| `phi-4-mini` | ~4B | सामान्य चॅट, सारांश | 4-6GB | `-cpu`, `-cuda-gpu`, `-npu` |
| `phi-3.5-mini` | ~3.5B | कोड जनरेशन, रीफॅक्टरिंग | 3-5GB | `-cpu`, `-cuda-gpu`, `-npu` |
| `qwen2.5-3b` | ~3B | सामान्य कार्य, कार्यक्षम | 3-4GB | `-cpu`, `-cuda-gpu` |
| `qwen2.5-1.5b` | ~1.5B | जलद, कमी संसाधन | 2-3GB | `-cpu`, `-cuda-gpu` |
| `qwen2.5-0.5b` | ~0.5B | वर्गीकरण, किमान संसाधन | 1-2GB | `-cpu`, `-cuda-gpu` |

### प्रकार नामकरण

- **मूल नाव** (उदा., `phi-4-mini`): तुमच्या हार्डवेअरसाठी सर्वोत्तम प्रकार आपोआप निवडते
- **`-cpu`**: CPU-ऑप्टिमाइझ्ड, सर्वत्र कार्य करते
- **`-cuda-gpu`**: NVIDIA GPU ऑप्टिमाइझ्ड, 8GB+ VRAM आवश्यक
- **`-npu`**: Qualcomm NPU ऑप्टिमाइझ्ड, NPU ड्रायव्हर्स आवश्यक

**शिफारस:** मूल नावे (शेवटचा प्रत्यय न लावता) वापरा आणि फाउंड्री लोकल सर्वोत्तम प्रकार आपोआप निवडू दे.

---

## यशाचे संकेत

तुम्ही तयार आहात जेव्हा तुम्हाला दिसते:

✅ `foundry service status` "running" दर्शवते  
✅ `foundry model ls` तुमच्यासाठी आवश्यक मॉडेल्स दर्शवते  
✅ सेवा योग्य एंडपॉइंटवर प्रवेशयोग्य आहे  
✅ हेल्थ चेक 200 OK परत करते  
✅ नोटबुक डायग्नोस्टिक सेल्स पास होतात  
✅ आउटपुटमध्ये कोणतीही कनेक्शन त्रुटी नाही  

---

## मदत मिळवा

### दस्तऐवजीकरण
- **मुख्य रिपॉझिटरी:** https://github.com/microsoft/Foundry-Local  
- **Python SDK:** https://github.com/microsoft/Foundry-Local/tree/main/sdk/python  
- **CLI संदर्भ:** https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-cli.md  
- **समस्या निवारण:** या डिरेक्टरीतील `troubleshooting.md` पहा  

### GitHub समस्या
- https://github.com/microsoft/Foundry-Local/issues  
- https://github.com/microsoft/edgeai-for-beginners/issues  

---

**शेवटचे अद्यतन:** 8 ऑक्टोबर, 2025  
**आवृत्ती:** वर्कशॉप नोटबुक्स 2.0  

---

**अस्वीकरण**:  
हा दस्तऐवज [Co-op Translator](https://github.com/Azure/co-op-translator) या एआय भाषांतर सेवेचा वापर करून भाषांतरित करण्यात आला आहे. आम्ही अचूकतेसाठी प्रयत्नशील असलो तरी कृपया लक्षात घ्या की स्वयंचलित भाषांतरांमध्ये त्रुटी किंवा अचूकतेचा अभाव असू शकतो. मूळ भाषेतील दस्तऐवज हा अधिकृत स्रोत मानला जावा. महत्त्वाच्या माहितीसाठी व्यावसायिक मानवी भाषांतराची शिफारस केली जाते. या भाषांतराचा वापर केल्यामुळे उद्भवणाऱ्या कोणत्याही गैरसमज किंवा चुकीच्या अर्थासाठी आम्ही जबाबदार राहणार नाही.