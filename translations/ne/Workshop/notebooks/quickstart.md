<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "ddaad917d0c16fc3d498a6b4eabc8088",
  "translation_date": "2025-10-09T09:52:32+00:00",
  "source_file": "Workshop/notebooks/quickstart.md",
  "language_code": "ne"
}
-->
# कार्यशाला नोटबुकहरू - छिटो सुरु गर्ने मार्गदर्शन

## सामग्री तालिका

- [पूर्वापेक्षाहरू](../../../../Workshop/notebooks)
- [प्रारम्भिक सेटअप](../../../../Workshop/notebooks)
- [सत्र ०४: मोडेल तुलना](../../../../Workshop/notebooks)
- [सत्र ०५: बहु-एजेन्ट समन्वयकर्ता](../../../../Workshop/notebooks)
- [सत्र ०६: उद्देश्य-आधारित मोडेल रुटिङ](../../../../Workshop/notebooks)
- [पर्यावरण चरहरू](../../../../Workshop/notebooks)
- [सामान्य आदेशहरू](../../../../Workshop/notebooks)

---

## पूर्वापेक्षाहरू

### १. फाउन्ड्री लोकल स्थापना गर्नुहोस्

**विन्डोज:**
```bash
winget install Microsoft.FoundryLocal
```

**म्याकओएस:**
```bash
brew tap microsoft/foundrylocal
brew install foundrylocal
```

**स्थापना प्रमाणित गर्नुहोस्:**
```bash
foundry --version
```

### २. पाइथन निर्भरता स्थापना गर्नुहोस्

```bash
cd Workshop
pip install -r requirements.txt
```

वा व्यक्तिगत रूपमा स्थापना गर्नुहोस्:
```bash
pip install foundry-local-sdk openai numpy requests
```

---

## प्रारम्भिक सेटअप

### फाउन्ड्री लोकल सेवा सुरु गर्नुहोस्

**कुनै पनि नोटबुक चलाउनु अघि आवश्यक:**

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

### मोडेलहरू डाउनलोड र लोड गर्नुहोस्

नोटबुकहरूले यी मोडेलहरूलाई डिफल्ट रूपमा प्रयोग गर्छन्:

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

### सेटअप प्रमाणित गर्नुहोस्

```bash
# List loaded models
foundry model ls

# Check service health
curl http://localhost:59959/v1/models
```

---

## सत्र ०४: मोडेल तुलना

### उद्देश्य
साना भाषा मोडेल (SLM) र ठूला भाषा मोडेल (LLM) बीचको प्रदर्शन तुलना गर्नुहोस्।

### छिटो सेटअप

```bash
# Start service (if not already running)
foundry service start

# Load required models
foundry model run phi-4-mini
foundry model run qwen2.5-3b
```

### नोटबुक चलाउने

1. **खोल्नुहोस्** `session04_model_compare.ipynb` VS Code वा Jupyter मा
2. **कर्नेल पुनः सुरु गर्नुहोस्** (कर्नेल → कर्नेल पुनः सुरु गर्नुहोस्)
3. **सबै सेलहरू क्रम अनुसार चलाउनुहोस्**

### मुख्य कन्फिगरेसन

**डिफल्ट मोडेलहरू:**
- **SLM:** `phi-4-mini` (~4GB RAM, छिटो)
- **LLM:** `qwen2.5-3b` (~3GB RAM, मेमोरी-अप्टिमाइज्ड)

**पर्यावरण चरहरू (वैकल्पिक):**
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

**विभिन्न मोडेलहरू प्रयोग गर्नुहोस्:**
```python
os.environ['SLM_ALIAS'] = 'phi-3.5-mini'
os.environ['LLM_ALIAS'] = 'qwen2.5-1.5b'
```

**अनुकूलित प्रम्प्ट:**
```python
os.environ['COMPARE_PROMPT'] = 'Explain quantum computing in simple terms'
```

### मान्यकरण चेकलिस्ट

- [ ] सेल १२ सही मोडेलहरू देखाउँछ (phi-4-mini, qwen2.5-3b)
- [ ] सेल १२ सही अन्त बिन्दु देखाउँछ (पोर्ट 59959)
- [ ] सेल १६ डायग्नोस्टिक पास हुन्छ (✅ सेवा चलिरहेको छ)
- [ ] सेल २० प्रि-फ्लाइट चेक पास हुन्छ (दुबै मोडेल ठीक छन्)
- [ ] सेल २२ तुलना पूरा हुन्छ विलम्ब मानहरूसँग
- [ ] सेल २४ मान्यकरण देखाउँछ 🎉 सबै चेक पास भयो!

### समय अनुमान
- **पहिलो रन:** ५-१० मिनेट (मोडेल डाउनलोड सहित)
- **पछिल्ला रनहरू:** १-२ मिनेट

---

## सत्र ०५: बहु-एजेन्ट समन्वयकर्ता

### उद्देश्य
फाउन्ड्री लोकल SDK प्रयोग गरेर बहु-एजेन्ट सहयोग प्रदर्शन गर्नुहोस् - एजेन्टहरूले परिष्कृत आउटपुट उत्पादन गर्न सँगै काम गर्छन्।

### छिटो सेटअप

```bash
# Start service
foundry service start

# Load models
foundry model run phi-4-mini  # Primary model
foundry model run qwen2.5-7b  # Optional: higher quality editor
```

### नोटबुक चलाउने

1. **खोल्नुहोस्** `session05_agents_orchestrator.ipynb`
2. **कर्नेल पुनः सुरु गर्नुहोस्**
3. **सबै सेलहरू क्रम अनुसार चलाउनुहोस्**

### मुख्य कन्फिगरेसन

**डिफल्ट सेटअप (दुबै एजेन्टहरूको लागि समान मोडेल):**
```python
PRIMARY_ALIAS = 'phi-4-mini'
EDITOR_ALIAS = 'phi-4-mini'  # Uses same model
```

**उन्नत सेटअप (विभिन्न मोडेलहरू):**
```python
import os
os.environ['AGENT_MODEL_PRIMARY'] = 'phi-4-mini'     # Fast for research
os.environ['AGENT_MODEL_EDITOR'] = 'qwen2.5-7b'      # High quality for editing
```

### वास्तुकला

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

### विस्तारहरू

**थप एजेन्टहरू थप्नुहोस्:**
```python
critic = Agent(
    name='Critic',
    system='Review content for accuracy',
    client=client,
    model_id=model_id
)
```

**ब्याच परीक्षण:**
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
- **पहिलो रन:** ३-५ मिनेट
- **पछिल्ला रनहरू:** प्रति प्रश्न १-२ मिनेट

---

## सत्र ०६: उद्देश्य-आधारित मोडेल रुटिङ

### उद्देश्य
पत्ता लागेको उद्देश्यको आधारमा प्रम्प्टहरूलाई विशेष मोडेलहरूमा बुद्धिमानीपूर्वक रुट गर्नुहोस्।

### छिटो सेटअप

```bash
# Start service
foundry service start

# Load all routing models (CPU variants recommended)
foundry model run phi-4-mini-cpu
foundry model run qwen2.5-0.5b-cpu
foundry model run phi-3.5-mini-cpu
```

**नोट:** सत्र ०६ CPU मोडेलहरूमा डिफल्ट हुन्छ अधिकतम अनुकूलताका लागि।

### नोटबुक चलाउने

1. **खोल्नुहोस्** `session06_models_router.ipynb`
2. **कर्नेल पुनः सुरु गर्नुहोस्**
3. **सबै सेलहरू क्रम अनुसार चलाउनुहोस्**

### मुख्य कन्फिगरेसन

**डिफल्ट क्याटलग (CPU मोडेलहरू):**
```python
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```

**वैकल्पिक (GPU मोडेलहरू):**
```python
# Uncomment GPU catalog in Cell #6 if you have sufficient VRAM (8GB+)
CATALOG = {
    'phi-4-mini': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini': {'capabilities':['code','refactor'],'priority':3},
}
```

### उद्देश्य पत्ता लगाउने

राउटरले उद्देश्य पत्ता लगाउन regex ढाँचाहरू प्रयोग गर्दछ:

| उद्देश्य | ढाँचा उदाहरणहरू | रुट गरिएको मोडेल |
|---------|------------------|------------------|
| `code` | "refactor", "implement function" | phi-3.5-mini-cpu |
| `classification` | "categorize", "classify this" | qwen2.5-0.5b-cpu |
| `summarize` | "summarize", "tl;dr" | phi-4-mini-cpu |
| `general` | अन्य सबै | phi-4-mini-cpu |

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

**अनुकूलित उद्देश्य थप्नुहोस्:**
```python
import re

# Add to RULES
RULES.append((re.compile('translate|翻译', re.I), 'translation'))

# Add capability to catalog
CATALOG['phi-4-mini-cpu']['capabilities'].append('translation')
```

**टोकन ट्र्याकिङ सक्षम गर्नुहोस्:**
```python
import os
os.environ['SHOW_USAGE'] = '1'
```

### GPU मोडेलहरूमा स्विच गर्दै

यदि तपाईंसँग ८GB+ VRAM छ भने:

1. **सेल #६** मा, CPU क्याटलगलाई टिप्पणी गर्नुहोस्
2. GPU क्याटलग अनटिप्पणी गर्नुहोस्
3. GPU मोडेलहरू लोड गर्नुहोस्:
   ```bash
   foundry model run phi-4-mini
   foundry model run qwen2.5-0.5b
   foundry model run phi-3.5-mini
   ```
4. कर्नेल पुनः सुरु गर्नुहोस् र नोटबुक पुनः चलाउनुहोस्

### समय अनुमान
- **पहिलो रन:** ५-१० मिनेट (मोडेल लोड गर्दै)
- **पछिल्ला रनहरू:** प्रति परीक्षण ३०-६० सेकेन्ड

---

## पर्यावरण चरहरू

### ग्लोबल कन्फिगरेसन

Jupyter/VS Code सुरु गर्नु अघि सेट गर्नुहोस्:

**विन्डोज (कमाण्ड प्रम्प्ट):**
```cmd
set FOUNDRY_LOCAL_ENDPOINT=http://localhost:59959/v1
set SHOW_USAGE=1
set RETRY_ON_FAIL=1
```

**विन्डोज (पावरशेल):**
```powershell
$env:FOUNDRY_LOCAL_ENDPOINT="http://localhost:59959/v1"
$env:SHOW_USAGE="1"
$env:RETRY_ON_FAIL="1"
```

**म्याकओएस/लिनक्स:**
```bash
export FOUNDRY_LOCAL_ENDPOINT=http://localhost:59959/v1
export SHOW_USAGE=1
export RETRY_ON_FAIL=1
```

### नोटबुकमा कन्फिगरेसन

कुनै पनि नोटबुकको सुरुमा सेट गर्नुहोस्:

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

## सामान्य आदेशहरू

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

### मोडेल व्यवस्थापन

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

### अन्त बिन्दु परीक्षण

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

### डायग्नोस्टिक आदेशहरू

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

## उत्कृष्ट अभ्यासहरू

### कुनै पनि नोटबुक सुरु गर्नु अघि

1. **सेवा चलिरहेको छ जाँच गर्नुहोस्:**
   ```bash
   foundry service status
   ```

2. **मोडेलहरू लोड गरिएको छ प्रमाणित गर्नुहोस्:**
   ```bash
   foundry model ls
   ```

3. **नोटबुक कर्नेल पुनः सुरु गर्नुहोस्** यदि पुनः चलाउँदै

4. **सबै आउटपुटहरू खाली गर्नुहोस्** सफा रनको लागि

### स्रोत व्यवस्थापन

1. **CPU मोडेलहरू डिफल्ट रूपमा प्रयोग गर्नुहोस्** अनुकूलताका लागि
2. **GPU मोडेलहरूमा स्विच गर्नुहोस्** यदि तपाईंसँग ८GB+ VRAM छ भने
3. **GPU अनुप्रयोगहरू बन्द गर्नुहोस्** नोटबुक चलाउनु अघि
4. **सेवा चलिरहेको राख्नुहोस्** नोटबुक सत्रहरू बीच
5. **स्रोत उपयोग निगरानी गर्नुहोस्** टास्क म्यानेजर / nvidia-smi प्रयोग गरेर

### समस्या समाधान

1. **कोड डिबगिङ गर्नु अघि सधैं सेवा जाँच गर्नुहोस्**
2. **कर्नेल पुनः सुरु गर्नुहोस्** यदि पुरानो कन्फिगरेसन देखिन्छ
3. **कुनै पनि परिवर्तनपछि डायग्नोस्टिक सेलहरू पुनः चलाउनुहोस्**
4. **मोडेल नामहरू जाँच गर्नुहोस्** लोड गरिएकोसँग मेल खान्छ
5. **अन्त बिन्दु पोर्ट प्रमाणित गर्नुहोस्** सेवा स्थितिसँग मेल खान्छ

---

## छिटो सन्दर्भ: मोडेल उपनामहरू

### सामान्य मोडेलहरू

| उपनाम | आकार | उत्तम प्रयोग | RAM/VRAM | भेरियन्टहरू |
|-------|------|--------------|----------|-------------|
| `phi-4-mini` | ~4B | सामान्य च्याट, संक्षेपण | 4-6GB | `-cpu`, `-cuda-gpu`, `-npu` |
| `phi-3.5-mini` | ~3.5B | कोड उत्पादन, पुनः संरचना | 3-5GB | `-cpu`, `-cuda-gpu`, `-npu` |
| `qwen2.5-3b` | ~3B | सामान्य कार्यहरू, कुशल | 3-4GB | `-cpu`, `-cuda-gpu` |
| `qwen2.5-1.5b` | ~1.5B | छिटो, कम स्रोत | 2-3GB | `-cpu`, `-cuda-gpu` |
| `qwen2.5-0.5b` | ~0.5B | वर्गीकरण, न्यूनतम स्रोत | 1-2GB | `-cpu`, `-cuda-gpu` |

### भेरियन्ट नामकरण

- **आधार नाम** (जस्तै, `phi-4-mini`): तपाईंको हार्डवेयरको लागि उत्तम भेरियन्ट स्वतः चयन गर्दछ
- **`-cpu`**: CPU-अप्टिमाइज्ड, सबै ठाउँमा काम गर्छ
- **`-cuda-gpu`**: NVIDIA GPU-अप्टिमाइज्ड, ८GB+ VRAM आवश्यक
- **`-npu`**: Qualcomm NPU-अप्टिमाइज्ड, NPU ड्राइभरहरू आवश्यक

**सिफारिस:** आधार नामहरू प्रयोग गर्नुहोस् (सफिक्स बिना) र फाउन्ड्री लोकललाई उत्तम भेरियन्ट स्वतः चयन गर्न दिनुहोस्।

---

## सफलता संकेतकहरू

तपाईं तयार हुनुहुन्छ जब तपाईं देख्नुहुन्छ:

✅ `foundry service status` "running" देखाउँछ  
✅ `foundry model ls` तपाईंको आवश्यक मोडेलहरू देखाउँछ  
✅ सेवा सही अन्त बिन्दुमा पहुँचयोग्य छ  
✅ स्वास्थ्य जाँच २०० OK फर्काउँछ  
✅ नोटबुक डायग्नोस्टिक सेलहरू पास हुन्छ  
✅ आउटपुटमा कुनै जडान त्रुटिहरू छैनन्  

---

## सहयोग प्राप्त गर्दै

### दस्तावेजीकरण
- **मुख्य रिपोजिटरी**: https://github.com/microsoft/Foundry-Local  
- **पाइथन SDK**: https://github.com/microsoft/Foundry-Local/tree/main/sdk/python  
- **CLI सन्दर्भ**: https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-cli.md  
- **समस्या समाधान**: यस निर्देशिकामा `troubleshooting.md` हेर्नुहोस्  

### GitHub मुद्दाहरू
- https://github.com/microsoft/Foundry-Local/issues  
- https://github.com/microsoft/edgeai-for-beginners/issues  

---

**अन्तिम अद्यावधिक:** अक्टोबर ८, २०२५  
**संस्करण:** कार्यशाला नोटबुकहरू २.०  

---

**अस्वीकरण**:  
यो दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) प्रयोग गरी अनुवाद गरिएको हो। हामी यथासम्भव सटीकता सुनिश्चित गर्न प्रयास गर्छौं, तर कृपया ध्यान दिनुहोस् कि स्वचालित अनुवादहरूमा त्रुटिहरू वा अशुद्धताहरू हुन सक्छन्। यसको मूल भाषामा रहेको मूल दस्तावेज़लाई आधिकारिक स्रोत मानिनुपर्छ। महत्वपूर्ण जानकारीका लागि, व्यावसायिक मानव अनुवाद सिफारिस गरिन्छ। यस अनुवादको प्रयोगबाट उत्पन्न हुने कुनै पनि गलतफहमी वा गलत व्याख्याका लागि हामी जिम्मेवार हुने छैनौं।