<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "e88a16101de37838f7cf256a9cd0f199",
  "translation_date": "2025-10-09T09:53:47+00:00",
  "source_file": "Workshop/notebooks/TROUBLESHOOTING.md",
  "language_code": "mr"
}
-->
# वर्कशॉप नोटबुक्स - समस्या निराकरण मार्गदर्शक

## विषय सूची

- [सामान्य समस्या आणि उपाय](../../../../Workshop/notebooks)
- [सेशन 04 संबंधित समस्या](../../../../Workshop/notebooks)
- [सेशन 05 संबंधित समस्या](../../../../Workshop/notebooks)
- [सेशन 06 संबंधित समस्या](../../../../Workshop/notebooks)
- [हार्डवेअर-संबंधित समस्या](../../../../Workshop/notebooks)
- [डायग्नोस्टिक कमांड्स](../../../../Workshop/notebooks)
- [मदत मिळवणे](../../../../Workshop/notebooks)

---

## सामान्य समस्या आणि उपाय

### 🔴 CUDA आउट ऑफ मेमरी

**त्रुटी संदेश:**
```
CUDA failure 2: out of memory
```

**मूळ कारण:** GPU कडे मॉडेल लोड करण्यासाठी पुरेशी VRAM नाही.

**उपाय:**

#### पर्याय 1: CPU व्हेरियंट वापरा (शिफारस केलेले)
```python
# In your notebook, update the CATALOG to use CPU variants
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```

#### पर्याय 2: GPU वर छोटे मॉडेल वापरा
```python
# Use only the smallest model
CATALOG = {
    'qwen2.5-0.5b': {'capabilities':['general','code','summarize','classification'],'priority':1},
}
```

#### पर्याय 3: GPU मेमरी साफ करा
```bash
# Close other GPU-intensive applications
# Check GPU memory usage
nvidia-smi

# Restart Foundry Local service
foundry service stop
foundry service start
```

#### पर्याय 4: GPU मेमरी वाढवा (जर शक्य असेल)
- ब्राउझर टॅब्स, व्हिडिओ एडिटर्स किंवा इतर GPU अ‍ॅप्स बंद करा
- विंडोज व्हिज्युअल इफेक्ट्स कमी करा
- तुमच्याकडे इंटिग्रेटेड + डेडिकेटेड GPU असल्यास डेडिकेटेड GPU वापरा

---

### 🔴 APIConnectionError: कनेक्शन त्रुटी

**त्रुटी संदेश:**
```
APIConnectionError: Connection error
[Retry 1/2] Setup failed for 'phi-4-mini': APIConnectionError: Connection error.
```

**मूळ कारण:** Foundry Local सेवा चालू नाही किंवा प्रवेशयोग्य नाही.

**उपाय:**

#### चरण 1: सेवा स्थिती तपासा
```bash
foundry service status
```

#### चरण 2: सेवा बंद असल्यास सुरू करा
```bash
foundry service start
```

#### चरण 3: एंडपॉइंट सत्यापित करा
```bash
# Check what port the service is using
foundry service status

# Test with curl (adjust port if different)
curl http://localhost:59959/health
curl http://localhost:55769/health
```

#### चरण 4: आवश्यक मॉडेल्स लोड करा
```bash
foundry model run phi-4-mini
foundry model run qwen2.5-3b
foundry model run phi-3.5-mini
```

#### चरण 5: नोटबुक कर्नल रीस्टार्ट करा
सेवा सुरू केल्यानंतर आणि मॉडेल्स लोड केल्यानंतर, नोटबुक कर्नल रीस्टार्ट करा आणि सर्व सेल्स पुन्हा चालवा.

---

### 🔴 कॅटलॉगमध्ये मॉडेल सापडले नाही

**त्रुटी संदेश:**
```
ValueError: Model phi-3.5-mini-cpu not found in the catalog.
[ERROR] Model 'phi-4-mini' not found in the catalog
```

**मूळ कारण:** मॉडेल डाउनलोड केलेले नाही किंवा Foundry Local मध्ये लोड केलेले नाही.

**उपाय:**

#### पर्याय 1: मॉडेल्स डाउनलोड आणि लोड करा
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

#### पर्याय 2: ऑटो-सेलेक्शन मोड वापरा
तुमचा CATALOG बेस मॉडेल नावांवर अपडेट करा (जसे `-cpu` प्रत्ययाशिवाय):

```python
CATALOG = {
    'phi-4-mini': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini': {'capabilities':['code','refactor'],'priority':3},
}
```

Foundry Local SDK तुमच्या हार्डवेअरसाठी सर्वोत्तम व्हेरियंट (CPU, GPU, किंवा NPU) आपोआप निवडेल.

---

### 🔴 HttpResponseError: 500 - मॉडेल लोड करण्यात अयशस्वी

**त्रुटी संदेश:**
```
HttpResponseError: 500 - Failed loading model
```

**मूळ कारण:** मॉडेल फाइल खराब झाली आहे किंवा हार्डवेअरशी सुसंगत नाही.

**उपाय:**

#### मॉडेल पुन्हा डाउनलोड करा
```bash
# Remove corrupted model
foundry model remove phi-3.5-mini

# Download fresh copy
foundry model download phi-3.5-mini
```

#### वेगळा व्हेरियंट वापरा
```bash
# Try CPU variant instead
foundry model download phi-3.5-mini-cpu
```

---

### 🔴 ImportError: मॉड्यूल सापडले नाही

**त्रुटी संदेश:**
```
ModuleNotFoundError: No module named 'foundry_local'
```

**मूळ कारण:** foundry-local-sdk पॅकेज स्थापित केलेले नाही.

**उपाय:**

```bash
# Install SDK
pip install foundry-local-sdk

# Verify installation
pip show foundry-local-sdk
python -c "from foundry_local import FoundryLocalManager; print('SDK OK')"
```

---

### � पहिल्या विनंतीसाठी धीमापन

**लक्षण:** पहिली पूर्णता 30+ सेकंद घेते, त्यानंतरच्या विनंत्या वेगवान असतात.

**मूळ कारण:** ही सामान्य गोष्ट आहे - सेवा पहिल्या विनंतीवर मॉडेल मेमरीमध्ये लोड करत आहे.

**उपाय:**

#### मॉडेल्स प्री-लोड करा
```bash
# Download and load all models you'll use before running notebooks
foundry model download phi-4-mini
foundry model download qwen2.5-3b
foundry model download phi-3.5-mini

foundry model run phi-4-mini
foundry model run qwen2.5-3b
```

#### सेवा चालू ठेवा
```bash
# Start service manually and leave it running
foundry service start
```

---

## सेशन 04 संबंधित समस्या

### चुकीचे पोर्ट कॉन्फिगरेशन

**समस्या:** नोटबुक चुकीच्या पोर्टशी कनेक्ट होत आहे (55769 vs 59959 vs 57127)

**उपाय:**

1. Foundry Local कोणता पोर्ट वापरत आहे ते तपासा:
```bash
foundry service status
# Note the port number displayed
```

2. नोटबुकमधील सेल 10 अपडेट करा:
```python
ENDPOINT = os.getenv('FOUNDRY_LOCAL_ENDPOINT', 'http://localhost:59959/v1')
# Replace 59959 with your actual port
```

3. कर्नल रीस्टार्ट करा आणि सेल्स 6, 8, 10, 12, 16, 20, 22 पुन्हा चालवा

---

### चुकीचे मॉडेल निवड

**समस्या:** नोटबुक gpt-oss-20b किंवा qwen2.5-7b दर्शवत आहे, qwen2.5-3b ऐवजी

**उपाय:**

1. नोटबुक कर्नल रीस्टार्ट करा (जुना व्हेरिएबल स्टेट साफ करतो)
2. सेल 10 पुन्हा चालवा (मॉडेल उपनाम सेट करा)
3. सेल 12 पुन्हा चालवा (कॉन्फिगरेशन दर्शवा)
4. **सत्यापित करा:** सेल 12 मध्ये `LLM Model: qwen2.5-3b` दिसले पाहिजे

---

### डायग्नोस्टिक सेल अयशस्वी

**समस्या:** सेल 16 "❌ Foundry Local सेवा सापडली नाही!" असे दर्शवते

**उपाय:**

1. सेवा चालू आहे का ते सत्यापित करा:
```bash
foundry service status
```

2. एंडपॉइंट मॅन्युअली तपासा:
```bash
curl http://localhost:59959/v1/models
```

3. जर curl कार्य करत असेल पण नोटबुक कार्य करत नसेल:
   - नोटबुक कर्नल रीस्टार्ट करा
   - सेल्स क्रमाने पुन्हा चालवा: 6, 8, 10, 12, 14, 16

4. जर curl अयशस्वी झाले:
   - सेवा सुरू करा: `foundry service start`
   - मॉडेल्स लोड करा: `foundry model run phi-4-mini` आणि `foundry model run qwen2.5-3b`

---

### प्री-फ्लाइट चेक अयशस्वी

**समस्या:** सेल 20 कनेक्शन त्रुटी दर्शवते जरी डायग्नोस्टिक पास झाले असले तरी

**उपाय:**

1. मॉडेल्स लोड झाली आहेत का ते तपासा:
```bash
foundry model ls
# Should show phi-4-mini and qwen2.5-3b
```

2. जर मॉडेल्स गायब असतील:
```bash
foundry model run phi-4-mini
foundry model run qwen2.5-3b
```

3. मॉडेल्स लोड झाल्यानंतर सेल 20 पुन्हा चालवा

---

### तुलना None व्हॅल्यूससह अयशस्वी

**समस्या:** सेल 22 पूर्ण होते पण लेटन्सी None म्हणून दर्शवते

**उपाय:**

1. प्रथम प्री-फ्लाइट पास झाले आहे का ते तपासा (सेल 20)
2. सेल 22 पुन्हा चालवा - मॉडेल्स पहिल्या विनंतीवर गरम होण्याची आवश्यकता असू शकते
3. दोन्ही मॉडेल्स लोड झाली आहेत का ते सत्यापित करा: `foundry model ls`

---

## सेशन 05 संबंधित समस्या

### एजंट चुकीचे मॉडेल वापरत आहे

**समस्या:** एजंट अपेक्षित मॉडेल वापरत नाही

**उपाय:**

कॉन्फिगरेशन सत्यापित करा:
```python
# Check which models are assigned
print(f"Researcher: {researcher.model_id}")
print(f"Editor: {editor.model_id}")
```

जर मॉडेल्स चुकीचे असतील तर कर्नल रीस्टार्ट करा.

---

### मेमरी कॉन्टेक्स्ट ओव्हरफ्लो

**समस्या:** एजंट प्रतिसाद वेळोवेळी खराब होत आहेत

**उपाय:** आधीच स्वयंचलितपणे हाताळलेले आहे - एजंट्स मेमरीमध्ये फक्त शेवटचे 6 संदेश ठेवतात.

---

## सेशन 06 संबंधित समस्या

### CPU vs GPU मॉडेल गोंधळ

**समस्या:** डिफॉल्ट कॉन्फिगरेशन वापरताना CUDA त्रुटी येत आहेत

**उपाय:** डिफॉल्ट कॉन्फिगरेशन आता CPU मॉडेल्स वापरते. जर तुम्हाला CUDA त्रुटी दिसत असतील:

1. तुम्ही डिफॉल्ट CPU कॅटलॉग वापरत आहात का ते सत्यापित करा:
```python
# Cell should show CPU variants
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```

2. कर्नल रीस्टार्ट करा आणि सर्व सेल्स पुन्हा चालवा

---

### हेतू ओळख कार्य करत नाही

**समस्या:** प्रॉम्प्ट्स चुकीच्या मॉडेल्सकडे रूट होत आहेत

**उपाय:**

हेतू ओळख तपासा:
```python
# Run the intent detection test cell
for prompt in test_prompts:
    intent = detect_intent(prompt)
    print(f"{prompt[:50]}... → {intent}")
```

जर पॅटर्न्समध्ये बदल आवश्यक असेल तर RULES अपडेट करा.

---

## हार्डवेअर-संबंधित समस्या

### NVIDIA GPU

**GPU स्थिती तपासा:**
```bash
nvidia-smi
```

**सामान्य समस्या:**
- **ड्रायव्हर जुना आहे:** NVIDIA ड्रायव्हर्स अपडेट करा
- **CUDA आवृत्ती जुळत नाही:** Foundry Local पुन्हा स्थापित करा
- **GPU मेमरी तुकडे झाले आहे:** सिस्टम रीस्टार्ट करा

### Qualcomm NPU

**NPU स्थिती तपासा:**
```bash
foundry device info
```

**सामान्य समस्या:**
- **NPU ड्रायव्हर्स स्थापित नाहीत:** Qualcomm NPU ड्रायव्हर्स स्थापित करा
- **NPU व्हेरियंट उपलब्ध नाही:** CPU व्हेरियंट वापरा
- **विंडोज आवृत्ती खूप जुनी आहे:** नवीनतम Windows 11 वर अपडेट करा

### फक्त CPU असलेली सिस्टम

**शिफारस केलेली मॉडेल्स:**
```python
CATALOG = {
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','general'],'priority':2},
}
```

**कामगिरी टिप्स:**
- सर्वात छोटे मॉडेल्स वापरा
- max_tokens कमी करा
- पहिल्या विनंतीसाठी थोडा संयम ठेवा

---

## डायग्नोस्टिक कमांड्स

### सर्व काही तपासा
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

### Python मध्ये
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

## मदत मिळवणे

### 1. लॉग्स तपासा
```bash
# Windows
foundry service logs

# Or check Windows Event Viewer
# Application Logs -> Microsoft-FoundryLocal
```

### 2. GitHub समस्यांवर जा
- विद्यमान समस्यांचा शोध घ्या: https://github.com/microsoft/Foundry-Local/issues
- नवीन समस्या तयार करा:
  - त्रुटी संदेश (पूर्ण मजकूर)
  - `foundry service status` चे आउटपुट
  - `foundry --version` चे आउटपुट
  - GPU/NPU माहिती (nvidia-smi, इ.)
  - समस्या पुनरुत्पादित करण्याचे चरण

### 3. दस्तऐवज
- **मुख्य रिपॉझिटरी:** https://github.com/microsoft/Foundry-Local
- **Python SDK:** https://github.com/microsoft/Foundry-Local/tree/main/sdk/python
- **CLI संदर्भ:** https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-cli.md
- **समस्या निराकरण:** https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-troubleshooting.md

---

## जलद निराकरण चेकलिस्ट

जेव्हा समस्या उद्भवतात, तेव्हा खालील क्रमाने प्रयत्न करा:

- [ ] सेवा चालू आहे का तपासा: `foundry service status`
- [ ] सेवा रीस्टार्ट करा: `foundry service stop && foundry service start`
- [ ] मॉडेल अस्तित्वात आहे का तपासा: `foundry model ls | grep phi-4-mini`
- [ ] आवश्यक मॉडेल्स लोड करा: `foundry model run phi-4-mini`
- [ ] GPU मेमरी तपासा: `nvidia-smi` (जर NVIDIA असेल)
- [ ] CPU व्हेरियंट वापरून पहा: `phi-4-mini-cpu` ऐवजी `phi-4-mini` वापरा
- [ ] नोटबुक कर्नल रीस्टार्ट करा
- [ ] नोटबुक आउटपुट्स साफ करा आणि सर्व सेल्स पुन्हा चालवा
- [ ] SDK पुन्हा स्थापित करा: `pip install --upgrade --force-reinstall foundry-local-sdk`
- [ ] सिस्टम रीबूट करा (शेवटचा उपाय)

---

## प्रतिबंध टिप्स

### सर्वोत्तम पद्धती

1. **नेहमी प्रथम सेवा तपासा:**
   ```bash
   foundry service status
   ```

2. **डिफॉल्टनुसार CPU व्हेरियंट वापरा:**
   ```python
   CATALOG = {
       'phi-4-mini-cpu': {...},
       'qwen2.5-0.5b-cpu': {...},
   }
   ```

3. **नोटबुक चालवण्यापूर्वी मॉडेल्स प्री-लोड करा:**
   ```bash
   foundry model run phi-4-mini
   foundry model run qwen2.5-3b
   ```

4. **सेवा चालू ठेवा:**
   - सेवा अनावश्यकपणे थांबवू/सुरू करू नका
   - सत्रांदरम्यान ती पार्श्वभूमीत चालू ठेवा

5. **संसाधने मॉनिटर करा:**
   - चालवण्यापूर्वी GPU मेमरी तपासा
   - अनावश्यक GPU अ‍ॅप्स बंद करा
   - Task Manager / nvidia-smi वापरा

6. **नियमितपणे अपडेट करा:**
   ```bash
   winget upgrade Microsoft.FoundryLocal
   pip install --upgrade foundry-local-sdk
   ```

---

**शेवटचे अपडेट:** 8 ऑक्टोबर, 2025

---

**अस्वीकरण**:  
हा दस्तऐवज AI भाषांतर सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) वापरून भाषांतरित केला आहे. आम्ही अचूकतेसाठी प्रयत्नशील असलो तरी, कृपया लक्षात घ्या की स्वयंचलित भाषांतरांमध्ये चुका किंवा अचूकतेचा अभाव असू शकतो. मूळ भाषेतील मूळ दस्तऐवज हा अधिकृत स्रोत मानला जावा. महत्त्वाच्या माहितीसाठी, व्यावसायिक मानवी भाषांतराची शिफारस केली जाते. या भाषांतराचा वापर करून उद्भवलेल्या कोणत्याही गैरसमज किंवा चुकीच्या अर्थासाठी आम्ही जबाबदार राहणार नाही.