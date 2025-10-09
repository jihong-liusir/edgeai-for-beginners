<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "e88a16101de37838f7cf256a9cd0f199",
  "translation_date": "2025-10-09T09:54:15+00:00",
  "source_file": "Workshop/notebooks/TROUBLESHOOTING.md",
  "language_code": "ne"
}
-->
# कार्यशाला नोटबुकहरू - समस्या समाधान मार्गदर्शिका

## सामग्री तालिका

- [सामान्य समस्या र समाधानहरू](../../../../Workshop/notebooks)
- [सत्र ०४ विशेष समस्या](../../../../Workshop/notebooks)
- [सत्र ०५ विशेष समस्या](../../../../Workshop/notebooks)
- [सत्र ०६ विशेष समस्या](../../../../Workshop/notebooks)
- [हार्डवेयर-विशेष समस्या](../../../../Workshop/notebooks)
- [डायग्नोस्टिक कमाण्डहरू](../../../../Workshop/notebooks)
- [मद्दत प्राप्त गर्ने तरिका](../../../../Workshop/notebooks)

---

## सामान्य समस्या र समाधानहरू

### 🔴 CUDA मेमोरी सकियो

**त्रुटि सन्देश:**
```
CUDA failure 2: out of memory
```
  
**मूल कारण:** GPU मा मोडेल लोड गर्न पर्याप्त VRAM छैन।

**समाधानहरू:**

#### विकल्प १: CPU भेरियन्ट प्रयोग गर्नुहोस् (सिफारिस गरिएको)
```python
# In your notebook, update the CATALOG to use CPU variants
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```
  
#### विकल्प २: GPU मा साना मोडेलहरू प्रयोग गर्नुहोस्
```python
# Use only the smallest model
CATALOG = {
    'qwen2.5-0.5b': {'capabilities':['general','code','summarize','classification'],'priority':1},
}
```
  
#### विकल्प ३: GPU मेमोरी खाली गर्नुहोस्
```bash
# Close other GPU-intensive applications
# Check GPU memory usage
nvidia-smi

# Restart Foundry Local service
foundry service stop
foundry service start
```
  
#### विकल्प ४: GPU मेमोरी बढाउनुहोस् (यदि सम्भव छ)
- ब्राउजर ट्याबहरू, भिडियो एडिटरहरू वा अन्य GPU एपहरू बन्द गर्नुहोस्
- Windows दृश्य प्रभावहरू घटाउनुहोस्
- यदि तपाईंसँग समर्पित + एकीकृत GPU छ भने समर्पित GPU प्रयोग गर्नुहोस्

---

### 🔴 APIConnectionError: कनेक्शन त्रुटि

**त्रुटि सन्देश:**
```
APIConnectionError: Connection error
[Retry 1/2] Setup failed for 'phi-4-mini': APIConnectionError: Connection error.
```
  
**मूल कारण:** Foundry Local सेवा चलिरहेको छैन वा पहुँचयोग्य छैन।

**समाधानहरू:**

#### चरण १: सेवा स्थिति जाँच गर्नुहोस्
```bash
foundry service status
```
  
#### चरण २: सेवा बन्द भएमा सुरु गर्नुहोस्
```bash
foundry service start
```
  
#### चरण ३: अन्त बिन्दु प्रमाणित गर्नुहोस्
```bash
# Check what port the service is using
foundry service status

# Test with curl (adjust port if different)
curl http://localhost:59959/health
curl http://localhost:55769/health
```
  
#### चरण ४: आवश्यक मोडेलहरू लोड गर्नुहोस्
```bash
foundry model run phi-4-mini
foundry model run qwen2.5-3b
foundry model run phi-3.5-mini
```
  
#### चरण ५: नोटबुक कर्नेल पुनः सुरु गर्नुहोस्
सेवा सुरु गरेपछि र मोडेलहरू लोड गरेपछि, नोटबुक कर्नेल पुनः सुरु गर्नुहोस् र सबै सेलहरू पुनः चलाउनुहोस्।

---

### 🔴 क्याटलगमा मोडेल फेला परेन

**त्रुटि सन्देश:**
```
ValueError: Model phi-3.5-mini-cpu not found in the catalog.
[ERROR] Model 'phi-4-mini' not found in the catalog
```
  
**मूल कारण:** मोडेल डाउनलोड गरिएको छैन वा Foundry Local मा लोड गरिएको छैन।

**समाधानहरू:**

#### विकल्प १: मोडेलहरू डाउनलोड र लोड गर्नुहोस्
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
  
#### विकल्प २: स्वतः चयन मोड प्रयोग गर्नुहोस्
तपाईंको CATALOG लाई आधार मोडेल नामहरू (बिना `-cpu` प्रत्यय) प्रयोग गर्न अद्यावधिक गर्नुहोस्:

```python
CATALOG = {
    'phi-4-mini': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini': {'capabilities':['code','refactor'],'priority':3},
}
```
  
Foundry Local SDK ले तपाईंको हार्डवेयरका लागि स्वतः उत्तम भेरियन्ट (CPU, GPU, वा NPU) चयन गर्नेछ।

---

### 🔴 HttpResponseError: 500 - मोडेल लोड गर्न असफल

**त्रुटि सन्देश:**
```
HttpResponseError: 500 - Failed loading model
```
  
**मूल कारण:** मोडेल फाइल बिग्रिएको छ वा हार्डवेयरसँग असंगत छ।

**समाधानहरू:**

#### मोडेल पुनः डाउनलोड गर्नुहोस्
```bash
# Remove corrupted model
foundry model remove phi-3.5-mini

# Download fresh copy
foundry model download phi-3.5-mini
```
  
#### फरक भेरियन्ट प्रयोग गर्नुहोस्
```bash
# Try CPU variant instead
foundry model download phi-3.5-mini-cpu
```
  
---

### 🔴 ImportError: कुनै मोड्युल फेला परेन

**त्रुटि सन्देश:**
```
ModuleNotFoundError: No module named 'foundry_local'
```
  
**मूल कारण:** foundry-local-sdk प्याकेज स्थापना गरिएको छैन।

**समाधानहरू:**

```bash
# Install SDK
pip install foundry-local-sdk

# Verify installation
pip show foundry-local-sdk
python -c "from foundry_local import FoundryLocalManager; print('SDK OK')"
```
  
---

### � पहिलो अनुरोध ढिलो

**लक्षण:** पहिलो कम्प्लिशनमा ३०+ सेकेन्ड लाग्छ, त्यसपछि अन्य अनुरोधहरू छिटो हुन्छन्।

**मूल कारण:** यो सामान्य व्यवहार हो - सेवा पहिलो अनुरोधमा मोडेललाई मेमोरीमा लोड गर्दैछ।

**समाधानहरू:**

#### मोडेलहरू पहिले नै लोड गर्नुहोस्
```bash
# Download and load all models you'll use before running notebooks
foundry model download phi-4-mini
foundry model download qwen2.5-3b
foundry model download phi-3.5-mini

foundry model run phi-4-mini
foundry model run qwen2.5-3b
```
  
#### सेवा चलिरहेको राख्नुहोस्
```bash
# Start service manually and leave it running
foundry service start
```
  
---

## सत्र ०४ विशेष समस्या

### गलत पोर्ट कन्फिगरेसन

**समस्या:** नोटबुक गलत पोर्टमा जडान गर्दैछ (५५७६९ बनाम ५९९५९ बनाम ५७१२७)

**समाधान:**

1. Foundry Local कुन पोर्ट प्रयोग गर्दैछ जाँच गर्नुहोस्:
```bash
foundry service status
# Note the port number displayed
```
  
2. नोटबुकको सेल १० अद्यावधिक गर्नुहोस्:
```python
ENDPOINT = os.getenv('FOUNDRY_LOCAL_ENDPOINT', 'http://localhost:59959/v1')
# Replace 59959 with your actual port
```
  
3. कर्नेल पुनः सुरु गर्नुहोस् र सेलहरू ६, ८, १०, १२, १६, २०, २२ पुनः चलाउनुहोस्

---

### गलत मोडेल चयन

**समस्या:** नोटबुकले gpt-oss-20b वा qwen2.5-7b देखाउँदैछ qwen2.5-3b को सट्टा

**समाधान:**

1. नोटबुक कर्नेल पुनः सुरु गर्नुहोस् (पुरानो भेरिएबल स्थिति खाली गर्दछ)
2. सेल १० पुनः चलाउनुहोस् (मोडेल उपनाम सेट गर्नुहोस्)
3. सेल १२ पुनः चलाउनुहोस् (कन्फिगरेसन प्रदर्शन गर्नुहोस्)
4. **प्रमाणित गर्नुहोस्:** सेल १२ ले `LLM Model: qwen2.5-3b` देखाउनुपर्छ

---

### डायग्नोस्टिक सेल असफल

**समस्या:** सेल १६ ले "❌ Foundry Local सेवा फेला परेन!" देखाउँछ

**समाधान:**

1. सेवा चलिरहेको छ कि छैन प्रमाणित गर्नुहोस्:
```bash
foundry service status
```
  
2. अन्त बिन्दु म्यानुअली परीक्षण गर्नुहोस्:
```bash
curl http://localhost:59959/v1/models
```
  
3. यदि curl काम गर्छ तर नोटबुकले गर्दैन:
   - नोटबुक कर्नेल पुनः सुरु गर्नुहोस्
   - सेलहरू क्रममा पुनः चलाउनुहोस्: ६, ८, १०, १२, १४, १६

4. यदि curl असफल हुन्छ:
   - सेवा सुरु गर्नुहोस्: `foundry service start`
   - मोडेलहरू लोड गर्नुहोस्: `foundry model run phi-4-mini` र `foundry model run qwen2.5-3b`

---

### प्रि-फ्लाइट चेक असफल

**समस्या:** सेल २० ले कनेक्शन त्रुटिहरू देखाउँछ यद्यपि डायग्नोस्टिक पास भयो

**समाधान:**

1. मोडेलहरू लोड गरिएको छ कि छैन जाँच गर्नुहोस्:
```bash
foundry model ls
# Should show phi-4-mini and qwen2.5-3b
```
  
2. यदि मोडेलहरू हराइरहेका छन्:
```bash
foundry model run phi-4-mini
foundry model run qwen2.5-3b
```
  
3. मोडेलहरू लोड भएपछि सेल २० पुनः चलाउनुहोस्

---

### तुलना असफल None मानहरूसँग

**समस्या:** सेल २२ पूरा हुन्छ तर विलम्बता None देखाउँछ

**समाधान:**

1. पहिले प्रि-फ्लाइट पास भएको छ कि छैन जाँच गर्नुहोस् (सेल २०)
2. सेल २२ पुनः चलाउनुहोस् - मोडेलहरू पहिलो अनुरोधमा तातो हुन आवश्यक हुन सक्छ
3. दुवै मोडेलहरू लोड गरिएको छ कि छैन प्रमाणित गर्नुहोस्: `foundry model ls`

---

## सत्र ०५ विशेष समस्या

### एजेन्टले गलत मोडेल प्रयोग गर्दैछ

**समस्या:** एजेन्टले अपेक्षित मोडेल प्रयोग गरिरहेको छैन

**समाधान:**

कन्फिगरेसन प्रमाणित गर्नुहोस्:
```python
# Check which models are assigned
print(f"Researcher: {researcher.model_id}")
print(f"Editor: {editor.model_id}")
```
  
यदि मोडेलहरू गलत छन् भने कर्नेल पुनः सुरु गर्नुहोस्।

---

### मेमोरी सन्दर्भ ओभरफ्लो

**समस्या:** एजेन्ट प्रतिक्रियाहरू समयसँगै बिग्रँदै जान्छन्

**समाधान:** यो पहिले नै स्वचालित रूपमा ह्यान्डल गरिएको छ - एजेन्टहरूले मेमोरीमा केवल पछिल्ला ६ सन्देशहरू राख्छन्।

---

## सत्र ०६ विशेष समस्या

### CPU बनाम GPU मोडेल भ्रम

**समस्या:** डिफल्ट कन्फिगरेसन प्रयोग गर्दा CUDA त्रुटिहरू देखिन्छन्

**समाधान:** डिफल्ट कन्फिगरेसन अब CPU मोडेलहरू प्रयोग गर्दछ। यदि तपाईंले CUDA त्रुटिहरू देख्नुभयो भने:

1. तपाईं डिफल्ट CPU क्याटलग प्रयोग गर्दै हुनुहुन्छ कि छैन प्रमाणित गर्नुहोस्:
```python
# Cell should show CPU variants
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```
  
2. कर्नेल पुनः सुरु गर्नुहोस् र सबै सेलहरू पुनः चलाउनुहोस्

---

### उद्देश्य पत्ता लगाउन काम गरिरहेको छैन

**समस्या:** प्रम्प्टहरू गलत मोडेलहरूमा रुट गरिँदैछ

**समाधान:**

उद्देश्य पत्ता लगाउने परीक्षण गर्नुहोस्:
```python
# Run the intent detection test cell
for prompt in test_prompts:
    intent = detect_intent(prompt)
    print(f"{prompt[:50]}... → {intent}")
```
  
यदि ढाँचाहरू समायोजन गर्न आवश्यक छ भने RULES अद्यावधिक गर्नुहोस्।

---

## हार्डवेयर-विशेष समस्या

### NVIDIA GPU

**GPU स्थिति जाँच गर्नुहोस्:**
```bash
nvidia-smi
```
  
**सामान्य समस्या:**
- **ड्राइभर पुरानो:** NVIDIA ड्राइभरहरू अद्यावधिक गर्नुहोस्
- **CUDA संस्करण असंगत:** Foundry Local पुनः स्थापना गर्नुहोस्
- **GPU मेमोरी खण्डित:** प्रणाली पुनः सुरु गर्नुहोस्

### Qualcomm NPU

**NPU स्थिति जाँच गर्नुहोस्:**
```bash
foundry device info
```
  
**सामान्य समस्या:**
- **NPU ड्राइभरहरू स्थापना गरिएको छैन:** Qualcomm NPU ड्राइभरहरू स्थापना गर्नुहोस्
- **NPU भेरियन्ट उपलब्ध छैन:** CPU भेरियन्ट प्रयोग गर्नुहोस्
- **Windows संस्करण धेरै पुरानो:** Windows 11 को नवीनतम संस्करणमा अद्यावधिक गर्नुहोस्

### CPU-मात्र प्रणालीहरू

**सिफारिस गरिएको मोडेलहरू:**
```python
CATALOG = {
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','general'],'priority':2},
}
```
  
**प्रदर्शन सुझावहरू:**
- साना मोडेलहरू प्रयोग गर्नुहोस्
- max_tokens घटाउनुहोस्
- पहिलो अनुरोधका लागि धैर्य बढाउनुहोस्

---

## डायग्नोस्टिक कमाण्डहरू

### सबै कुरा जाँच गर्नुहोस्
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
  
### Python मा
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

## मद्दत प्राप्त गर्ने तरिका

### १. लगहरू जाँच गर्नुहोस्
```bash
# Windows
foundry service logs

# Or check Windows Event Viewer
# Application Logs -> Microsoft-FoundryLocal
```
  
### २. GitHub समस्याहरू
- विद्यमान समस्याहरू खोज्नुहोस्: https://github.com/microsoft/Foundry-Local/issues  
- नयाँ समस्या सिर्जना गर्नुहोस्:
  - त्रुटि सन्देश (पूर्ण पाठ)
  - `foundry service status` को आउटपुट
  - `foundry --version` को आउटपुट
  - GPU/NPU जानकारी (nvidia-smi, आदि)
  - पुनः उत्पादन गर्न चरणहरू

### ३. दस्तावेजहरू
- **मुख्य रिपोजिटरी:** https://github.com/microsoft/Foundry-Local  
- **Python SDK:** https://github.com/microsoft/Foundry-Local/tree/main/sdk/python  
- **CLI सन्दर्भ:** https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-cli.md  
- **समस्या समाधान:** https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-troubleshooting.md  

---

## छिटो समाधान चेकलिस्ट

जब समस्या आउँछ, यी क्रममा प्रयास गर्नुहोस्:

- [ ] सेवा चलिरहेको छ कि छैन जाँच गर्नुहोस्: `foundry service status`
- [ ] सेवा पुनः सुरु गर्नुहोस्: `foundry service stop && foundry service start`
- [ ] मोडेल अवस्थित छ कि छैन प्रमाणित गर्नुहोस्: `foundry model ls | grep phi-4-mini`
- [ ] आवश्यक मोडेलहरू लोड गर्नुहोस्: `foundry model run phi-4-mini`
- [ ] GPU मेमोरी जाँच गर्नुहोस्: `nvidia-smi` (यदि NVIDIA हो भने)
- [ ] CPU भेरियन्ट प्रयास गर्नुहोस्: `phi-4-mini-cpu` प्रयोग गर्नुहोस् `phi-4-mini` को सट्टा
- [ ] नोटबुक कर्नेल पुनः सुरु गर्नुहोस्
- [ ] नोटबुक आउटपुटहरू खाली गर्नुहोस् र सबै सेलहरू पुनः चलाउनुहोस्
- [ ] SDK पुनः स्थापना गर्नुहोस्: `pip install --upgrade --force-reinstall foundry-local-sdk`
- [ ] प्रणाली पुनः सुरु गर्नुहोस् (अन्तिम उपाय)

---

## रोकथाम सुझावहरू

### उत्तम अभ्यासहरू

1. **पहिले सेवा जाँच गर्नुहोस्:**
   ```bash
   foundry service status
   ```
  
2. **डिफल्ट रूपमा CPU भेरियन्टहरू प्रयोग गर्नुहोस्:**
   ```python
   CATALOG = {
       'phi-4-mini-cpu': {...},
       'qwen2.5-0.5b-cpu': {...},
   }
   ```
  
3. **नोटबुकहरू चलाउनु अघि मोडेलहरू पहिले नै लोड गर्नुहोस्:**
   ```bash
   foundry model run phi-4-mini
   foundry model run qwen2.5-3b
   ```
  
4. **सेवा चलिरहेको राख्नुहोस्:**
   - सेवा अनावश्यक रूपमा बन्द/सुरु नगर्नुहोस्
   - सत्रहरू बीचमा पृष्ठभूमिमा चल्न दिनुहोस्

5. **स्रोतहरू निगरानी गर्नुहोस्:**
   - GPU मेमोरी नोटबुक चलाउनु अघि जाँच गर्नुहोस्
   - अनावश्यक GPU एप्लिकेसनहरू बन्द गर्नुहोस्
   - Task Manager / nvidia-smi प्रयोग गर्नुहोस्

6. **नियमित रूपमा अद्यावधिक गर्नुहोस्:**
   ```bash
   winget upgrade Microsoft.FoundryLocal
   pip install --upgrade foundry-local-sdk
   ```
  
---

**अन्तिम अद्यावधिक:** अक्टोबर ८, २०२५

---

**अस्वीकरण**:  
यो दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) प्रयोग गरी अनुवाद गरिएको हो। हामी यथासम्भव सटीकता सुनिश्चित गर्न प्रयास गर्छौं, तर कृपया ध्यान दिनुहोस् कि स्वचालित अनुवादहरूमा त्रुटिहरू वा अशुद्धताहरू हुन सक्छन्। यसको मूल भाषामा रहेको मूल दस्तावेज़लाई आधिकारिक स्रोत मानिनुपर्छ। महत्त्वपूर्ण जानकारीका लागि, व्यावसायिक मानव अनुवाद सिफारिस गरिन्छ। यस अनुवादको प्रयोगबाट उत्पन्न हुने कुनै पनि गलतफहमी वा गलत व्याख्याका लागि हामी जिम्मेवार हुने छैनौं।