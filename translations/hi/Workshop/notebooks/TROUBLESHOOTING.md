<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "e88a16101de37838f7cf256a9cd0f199",
  "translation_date": "2025-10-08T22:06:11+00:00",
  "source_file": "Workshop/notebooks/TROUBLESHOOTING.md",
  "language_code": "hi"
}
-->
# वर्कशॉप नोटबुक्स - समस्या निवारण गाइड

## सामग्री सूची

- [सामान्य समस्याएं और समाधान](../../../../Workshop/notebooks)
- [सेशन 04 की विशेष समस्याएं](../../../../Workshop/notebooks)
- [सेशन 05 की विशेष समस्याएं](../../../../Workshop/notebooks)
- [सेशन 06 की विशेष समस्याएं](../../../../Workshop/notebooks)
- [हार्डवेयर से संबंधित समस्याएं](../../../../Workshop/notebooks)
- [डायग्नोस्टिक कमांड्स](../../../../Workshop/notebooks)
- [मदद प्राप्त करें](../../../../Workshop/notebooks)

---

## सामान्य समस्याएं और समाधान

### 🔴 CUDA आउट ऑफ मेमोरी

**एरर संदेश:**
```
CUDA failure 2: out of memory
```
  
**मूल कारण:** GPU में मॉडल लोड करने के लिए पर्याप्त VRAM नहीं है।

**समाधान:**

#### विकल्प 1: CPU वेरिएंट का उपयोग करें (अनुशंसित)
```python
# In your notebook, update the CATALOG to use CPU variants
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```
  
#### विकल्प 2: GPU पर छोटे मॉडल का उपयोग करें
```python
# Use only the smallest model
CATALOG = {
    'qwen2.5-0.5b': {'capabilities':['general','code','summarize','classification'],'priority':1},
}
```
  
#### विकल्प 3: GPU मेमोरी साफ करें
```bash
# Close other GPU-intensive applications
# Check GPU memory usage
nvidia-smi

# Restart Foundry Local service
foundry service stop
foundry service start
```
  
#### विकल्प 4: GPU मेमोरी बढ़ाएं (यदि संभव हो)
- ब्राउज़र टैब, वीडियो एडिटर्स, या अन्य GPU ऐप्स बंद करें
- विंडोज विजुअल इफेक्ट्स कम करें
- यदि आपके पास इंटीग्रेटेड + डेडिकेटेड GPU है, तो डेडिकेटेड GPU का उपयोग करें

---

### 🔴 APIConnectionError: कनेक्शन एरर

**एरर संदेश:**
```
APIConnectionError: Connection error
[Retry 1/2] Setup failed for 'phi-4-mini': APIConnectionError: Connection error.
```
  
**मूल कारण:** Foundry Local सेवा चल नहीं रही है या पहुंच योग्य नहीं है।

**समाधान:**

#### चरण 1: सेवा की स्थिति जांचें
```bash
foundry service status
```
  
#### चरण 2: सेवा शुरू करें यदि बंद हो
```bash
foundry service start
```
  
#### चरण 3: एंडपॉइंट सत्यापित करें
```bash
# Check what port the service is using
foundry service status

# Test with curl (adjust port if different)
curl http://localhost:59959/health
curl http://localhost:55769/health
```
  
#### चरण 4: आवश्यक मॉडल लोड करें
```bash
foundry model run phi-4-mini
foundry model run qwen2.5-3b
foundry model run phi-3.5-mini
```
  
#### चरण 5: नोटबुक कर्नेल को पुनः प्रारंभ करें  
सेवा शुरू करने और मॉडल लोड करने के बाद, नोटबुक कर्नेल को पुनः प्रारंभ करें और सभी सेल्स को फिर से चलाएं।

---

### 🔴 कैटलॉग में मॉडल नहीं मिला

**एरर संदेश:**
```
ValueError: Model phi-3.5-mini-cpu not found in the catalog.
[ERROR] Model 'phi-4-mini' not found in the catalog
```
  
**मूल कारण:** मॉडल डाउनलोड नहीं हुआ है या Foundry Local में लोड नहीं हुआ है।

**समाधान:**

#### विकल्प 1: मॉडल डाउनलोड और लोड करें
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
  
#### विकल्प 2: ऑटो-सेलेक्शन मोड का उपयोग करें  
अपने CATALOG को बेस मॉडल नाम (बिना `-cpu` प्रत्यय) के साथ अपडेट करें:

```python
CATALOG = {
    'phi-4-mini': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini': {'capabilities':['code','refactor'],'priority':3},
}
```
  
Foundry Local SDK आपके हार्डवेयर के लिए स्वचालित रूप से सबसे अच्छा वेरिएंट (CPU, GPU, या NPU) चुन लेगा।

---

### 🔴 HttpResponseError: 500 - मॉडल लोड करने में विफलता

**एरर संदेश:**
```
HttpResponseError: 500 - Failed loading model
```
  
**मूल कारण:** मॉडल फाइल खराब हो गई है या हार्डवेयर के साथ असंगत है।

**समाधान:**

#### मॉडल को पुनः डाउनलोड करें
```bash
# Remove corrupted model
foundry model remove phi-3.5-mini

# Download fresh copy
foundry model download phi-3.5-mini
```
  
#### अलग वेरिएंट का उपयोग करें
```bash
# Try CPU variant instead
foundry model download phi-3.5-mini-cpu
```
  
---

### 🔴 ImportError: कोई मॉड्यूल नहीं मिला

**एरर संदेश:**
```
ModuleNotFoundError: No module named 'foundry_local'
```
  
**मूल कारण:** foundry-local-sdk पैकेज इंस्टॉल नहीं है।

**समाधान:**

```bash
# Install SDK
pip install foundry-local-sdk

# Verify installation
pip show foundry-local-sdk
python -c "from foundry_local import FoundryLocalManager; print('SDK OK')"
```
  
---

### � पहली रिक्वेस्ट धीमी

**लक्षण:** पहली कंप्लीशन में 30+ सेकंड लगते हैं, बाद की रिक्वेस्ट तेज होती हैं।

**मूल कारण:** यह सामान्य व्यवहार है - सेवा पहली रिक्वेस्ट पर मॉडल को मेमोरी में लोड कर रही है।

**समाधान:**

#### मॉडल्स को पहले से लोड करें
```bash
# Download and load all models you'll use before running notebooks
foundry model download phi-4-mini
foundry model download qwen2.5-3b
foundry model download phi-3.5-mini

foundry model run phi-4-mini
foundry model run qwen2.5-3b
```
  
#### सेवा को चालू रखें
```bash
# Start service manually and leave it running
foundry service start
```
  
---

## सेशन 04 की विशेष समस्याएं

### गलत पोर्ट कॉन्फ़िगरेशन

**समस्या:** नोटबुक गलत पोर्ट से कनेक्ट हो रहा है (55769 बनाम 59959 बनाम 57127)

**समाधान:**

1. जांचें कि Foundry Local कौन सा पोर्ट उपयोग कर रहा है:
```bash
foundry service status
# Note the port number displayed
```
  
2. नोटबुक के सेल 10 को अपडेट करें:
```python
ENDPOINT = os.getenv('FOUNDRY_LOCAL_ENDPOINT', 'http://localhost:59959/v1')
# Replace 59959 with your actual port
```
  
3. कर्नेल को पुनः प्रारंभ करें और सेल्स 6, 8, 10, 12, 16, 20, 22 को फिर से चलाएं।

---

### गलत मॉडल चयन

**समस्या:** नोटबुक gpt-oss-20b या qwen2.5-7b दिखा रहा है बजाय qwen2.5-3b के।

**समाधान:**

1. नोटबुक कर्नेल को पुनः प्रारंभ करें (पुरानी वेरिएबल स्थिति साफ करता है)
2. सेल 10 को फिर से चलाएं (मॉडल उपनाम सेट करें)
3. सेल 12 को फिर से चलाएं (कॉन्फ़िगरेशन प्रदर्शित करें)
4. **सत्यापित करें:** सेल 12 को `LLM Model: qwen2.5-3b` दिखाना चाहिए।

---

### डायग्नोस्टिक सेल विफल

**समस्या:** सेल 16 "❌ Foundry Local सेवा नहीं मिली!" दिखा रहा है।

**समाधान:**

1. सुनिश्चित करें कि सेवा चल रही है:
```bash
foundry service status
```
  
2. एंडपॉइंट को मैन्युअली टेस्ट करें:
```bash
curl http://localhost:59959/v1/models
```
  
3. यदि curl काम करता है लेकिन नोटबुक नहीं:
   - नोटबुक कर्नेल को पुनः प्रारंभ करें
   - सेल्स को क्रम में फिर से चलाएं: 6, 8, 10, 12, 14, 16

4. यदि curl विफल:
   - सेवा शुरू करें: `foundry service start`
   - मॉडल लोड करें: `foundry model run phi-4-mini` और `foundry model run qwen2.5-3b`

---

### प्री-फ्लाइट चेक विफल

**समस्या:** सेल 20 कनेक्शन एरर दिखा रहा है जबकि डायग्नोस्टिक पास हो गया है।

**समाधान:**

1. जांचें कि मॉडल लोड हो चुके हैं:
```bash
foundry model ls
# Should show phi-4-mini and qwen2.5-3b
```
  
2. यदि मॉडल गायब हैं:
```bash
foundry model run phi-4-mini
foundry model run qwen2.5-3b
```
  
3. मॉडल लोड होने के बाद सेल 20 को फिर से चलाएं।

---

### तुलना None मानों के साथ विफल

**समस्या:** सेल 22 पूरा हो जाता है लेकिन लेटेंसी None दिखाता है।

**समाधान:**

1. पहले प्री-फ्लाइट पास सुनिश्चित करें (सेल 20)
2. सेल 22 को फिर से चलाएं - मॉडल को पहली रिक्वेस्ट पर वार्म अप करने की आवश्यकता हो सकती है।
3. सुनिश्चित करें कि दोनों मॉडल लोड हो चुके हैं: `foundry model ls`

---

## सेशन 05 की विशेष समस्याएं

### एजेंट गलत मॉडल का उपयोग कर रहा है

**समस्या:** एजेंट अपेक्षित मॉडल का उपयोग नहीं कर रहा है।

**समाधान:**

कॉन्फ़िगरेशन सत्यापित करें:
```python
# Check which models are assigned
print(f"Researcher: {researcher.model_id}")
print(f"Editor: {editor.model_id}")
```
  
यदि मॉडल गलत हैं तो कर्नेल को पुनः प्रारंभ करें।

---

### मेमोरी संदर्भ ओवरफ्लो

**समस्या:** समय के साथ एजेंट प्रतिक्रियाएं खराब हो रही हैं।

**समाधान:** पहले से स्वचालित रूप से संभाला गया है - एजेंट केवल अंतिम 6 संदेशों को मेमोरी में रखते हैं।

---

## सेशन 06 की विशेष समस्याएं

### CPU बनाम GPU मॉडल भ्रम

**समस्या:** डिफ़ॉल्ट कॉन्फ़िगरेशन का उपयोग करते समय CUDA एरर मिल रहे हैं।

**समाधान:** डिफ़ॉल्ट कॉन्फ़िगरेशन अब CPU मॉडल का उपयोग करता है। यदि आपको CUDA एरर मिलते हैं:

1. सत्यापित करें कि आप डिफ़ॉल्ट CPU कैटलॉग का उपयोग कर रहे हैं:
```python
# Cell should show CPU variants
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```
  
2. कर्नेल को पुनः प्रारंभ करें और सभी सेल्स को फिर से चलाएं।

---

### इंटेंट डिटेक्शन काम नहीं कर रहा है

**समस्या:** प्रॉम्प्ट्स गलत मॉडल्स पर रूट हो रहे हैं।

**समाधान:**

इंटेंट डिटेक्शन टेस्ट करें:
```python
# Run the intent detection test cell
for prompt in test_prompts:
    intent = detect_intent(prompt)
    print(f"{prompt[:50]}... → {intent}")
```
  
यदि पैटर्न को समायोजन की आवश्यकता हो तो RULES अपडेट करें।

---

## हार्डवेयर से संबंधित समस्याएं

### NVIDIA GPU

**GPU स्थिति जांचें:**
```bash
nvidia-smi
```
  
**सामान्य समस्याएं:**
- **ड्राइवर पुराना है:** NVIDIA ड्राइवर अपडेट करें
- **CUDA संस्करण असंगत:** Foundry Local को पुनः इंस्टॉल करें
- **GPU मेमोरी खंडित:** सिस्टम को पुनः प्रारंभ करें

### Qualcomm NPU

**NPU स्थिति जांचें:**
```bash
foundry device info
```
  
**सामान्य समस्याएं:**
- **NPU ड्राइवर इंस्टॉल नहीं हैं:** Qualcomm NPU ड्राइवर इंस्टॉल करें
- **NPU वेरिएंट उपलब्ध नहीं है:** CPU वेरिएंट का उपयोग करें
- **विंडोज संस्करण बहुत पुराना है:** नवीनतम विंडोज 11 में अपडेट करें

### केवल CPU सिस्टम

**अनुशंसित मॉडल:**
```python
CATALOG = {
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','general'],'priority':2},
}
```
  
**प्रदर्शन युक्तियाँ:**
- सबसे छोटे मॉडल का उपयोग करें
- max_tokens कम करें
- पहली रिक्वेस्ट के लिए धैर्य रखें

---

## डायग्नोस्टिक कमांड्स

### सब कुछ जांचें
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
  
### Python में
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

## मदद प्राप्त करें

### 1. लॉग्स जांचें
```bash
# Windows
foundry service logs

# Or check Windows Event Viewer
# Application Logs -> Microsoft-FoundryLocal
```
  
### 2. GitHub Issues
- मौजूदा समस्याओं को खोजें: https://github.com/microsoft/Foundry-Local/issues  
- नई समस्या बनाएं और शामिल करें:
  - एरर संदेश (पूरा टेक्स्ट)
  - `foundry service status` का आउटपुट
  - `foundry --version` का आउटपुट
  - GPU/NPU जानकारी (nvidia-smi, आदि)
  - समस्या को पुनः उत्पन्न करने के चरण

### 3. दस्तावेज़ीकरण
- **मुख्य रिपॉजिटरी:** https://github.com/microsoft/Foundry-Local  
- **Python SDK:** https://github.com/microsoft/Foundry-Local/tree/main/sdk/python  
- **CLI संदर्भ:** https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-cli.md  
- **समस्या निवारण:** https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-troubleshooting.md  

---

## त्वरित सुधार चेकलिस्ट

जब चीजें गलत हों, तो इन चरणों को क्रम में आज़माएं:

- [ ] जांचें कि सेवा चल रही है: `foundry service status`
- [ ] सेवा को पुनः प्रारंभ करें: `foundry service stop && foundry service start`
- [ ] सत्यापित करें कि मॉडल मौजूद है: `foundry model ls | grep phi-4-mini`
- [ ] आवश्यक मॉडल लोड करें: `foundry model run phi-4-mini`
- [ ] GPU मेमोरी जांचें: `nvidia-smi` (यदि NVIDIA)
- [ ] CPU वेरिएंट आज़माएं: `phi-4-mini-cpu` का उपयोग करें बजाय `phi-4-mini`
- [ ] नोटबुक कर्नेल को पुनः प्रारंभ करें
- [ ] नोटबुक आउटपुट साफ करें और सभी सेल्स को फिर से चलाएं
- [ ] SDK को पुनः इंस्टॉल करें: `pip install --upgrade --force-reinstall foundry-local-sdk`
- [ ] सिस्टम को पुनः चालू करें (अंतिम उपाय)

---

## रोकथाम युक्तियाँ

### सर्वोत्तम अभ्यास

1. **हमेशा पहले सेवा जांचें:**
   ```bash
   foundry service status
   ```
  
2. **डिफ़ॉल्ट रूप से CPU वेरिएंट का उपयोग करें:**
   ```python
   CATALOG = {
       'phi-4-mini-cpu': {...},
       'qwen2.5-0.5b-cpu': {...},
   }
   ```
  
3. **नोटबुक चलाने से पहले मॉडल्स को प्री-लोड करें:**
   ```bash
   foundry model run phi-4-mini
   foundry model run qwen2.5-3b
   ```
  
4. **सेवा को चालू रखें:**
   - सेवा को अनावश्यक रूप से बंद/चालू न करें
   - सत्रों के बीच इसे बैकग्राउंड में चलने दें

5. **संसाधनों की निगरानी करें:**
   - नोटबुक चलाने से पहले GPU मेमोरी जांचें
   - अनावश्यक GPU एप्लिकेशन बंद करें
   - टास्क मैनेजर / nvidia-smi का उपयोग करें

6. **नियमित रूप से अपडेट करें:**
   ```bash
   winget upgrade Microsoft.FoundryLocal
   pip install --upgrade foundry-local-sdk
   ```
  
---

**अंतिम अपडेट:** 8 अक्टूबर, 2025

---

**अस्वीकरण**:  
यह दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) का उपयोग करके अनुवादित किया गया है। जबकि हम सटीकता के लिए प्रयास करते हैं, कृपया ध्यान दें कि स्वचालित अनुवाद में त्रुटियां या अशुद्धियां हो सकती हैं। मूल भाषा में दस्तावेज़ को आधिकारिक स्रोत माना जाना चाहिए। महत्वपूर्ण जानकारी के लिए, पेशेवर मानव अनुवाद की सिफारिश की जाती है। इस अनुवाद के उपयोग से उत्पन्न किसी भी गलतफहमी या गलत व्याख्या के लिए हम उत्तरदायी नहीं हैं।