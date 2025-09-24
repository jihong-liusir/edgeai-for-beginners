<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "562ac0eae12d808c9f45fbb77eb5c84f",
  "translation_date": "2025-09-24T15:28:58+00:00",
  "source_file": "Module08/samples/04/README.md",
  "language_code": "ne"
}
-->
# नमूना ०४: उत्पादन स्तरको च्याट एप्लिकेसनहरू Chainlit प्रयोग गरेर

Microsoft Foundry Local प्रयोग गरी उत्पादन-तयार च्याट एप्लिकेसन निर्माण गर्ने विभिन्न तरिकाहरूको विस्तृत नमूना, जसमा आधुनिक वेब इन्टरफेस, स्ट्रिमिङ प्रतिक्रिया, र अत्याधुनिक ब्राउजर प्रविधिहरू समावेश छन्।

## समावेश गरिएको सामग्री

- **🚀 Chainlit च्याट एप** (`app.py`): स्ट्रिमिङसहित उत्पादन-तयार च्याट एप्लिकेसन
- **🌐 WebGPU डेमो** (`webgpu-demo/`): हार्डवेयर एक्सेलेरेशनसहित ब्राउजर-आधारित AI इनफरेन्स
- **🎨 Open WebUI एकीकरण** (`open-webui-guide.md`): व्यावसायिक ChatGPT-जस्तै इन्टरफेस
- **📚 शैक्षिक नोटबुक** (`chainlit_app.ipynb`): अन्तरक्रियात्मक सिकाइ सामग्री

## छिटो सुरु गर्ने तरिका

### १. Chainlit च्याट एप्लिकेसन

```cmd
# Navigate to Module08 directory
cd Module08

# Start your model
foundry model run phi-4-mini

# Run Chainlit app (using port 8080 to avoid conflicts)
chainlit run samples\04\app.py -w --port 8080
```

खुल्छ: `http://localhost:8080`

### २. WebGPU ब्राउजर डेमो

```cmd
# Navigate to WebGPU demo
cd Module08\samples\04\webgpu-demo

# Serve the demo
python -m http.server 5173
```

खुल्छ: `http://localhost:5173`

### ३. Open WebUI सेटअप

```cmd
# Run Open WebUI with Docker
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```

खुल्छ: `http://localhost:3000`

## आर्किटेक्चर ढाँचा

### स्थानीय बनाम क्लाउड निर्णय म्याट्रिक्स

| परिदृश्य | सिफारिस | कारण |
|----------|---------|------|
| **गोपनीयता-संवेदनशील डाटा** | 🏠 स्थानीय (Foundry) | डाटा कहिल्यै उपकरण बाहिर जान्दैन |
| **जटिल तर्क** | ☁️ क्लाउड (Azure OpenAI) | ठूला मोडेलहरूको पहुँच |
| **रियल-टाइम च्याट** | 🏠 स्थानीय (Foundry) | कम विलम्बता, छिटो प्रतिक्रिया |
| **डकुमेन्ट विश्लेषण** | 🔄 हाइब्रिड | स्थानीयमा एक्स्ट्र्याक्सन, क्लाउडमा विश्लेषण |
| **कोड जेनेरेशन** | 🏠 स्थानीय (Foundry) | गोपनीयता + विशेष मोडेलहरू |
| **अनुसन्धान कार्यहरू** | ☁️ क्लाउड (Azure OpenAI) | व्यापक ज्ञान आधार आवश्यक |

### प्रविधि तुलना

| प्रविधि | प्रयोग केस | फाइदा | कमजोरी |
|--------|------------|-------|--------|
| **Chainlit** | Python डेभलपर्स, छिटो प्रोटोटाइप | सजिलो सेटअप, स्ट्रिमिङ समर्थन | केवल Python |
| **WebGPU** | अधिकतम गोपनीयता, अफलाइन परिदृश्य | ब्राउजर-नेभेटिभ, सर्भर आवश्यक छैन | सीमित मोडेल आकार |
| **Open WebUI** | उत्पादन परिनियोजन, टिमहरू | व्यावसायिक UI, प्रयोगकर्ता व्यवस्थापन | Docker आवश्यक |

## पूर्वापेक्षाहरू

- **Foundry Local**: स्थापना गरिएको र चलिरहेको ([डाउनलोड](https://aka.ms/foundry-local-installer))
- **Python**: ३.१०+ भर्चुअल वातावरणसहित
- **मोडेल**: कम्तीमा एउटा लोड गरिएको (`foundry model run phi-4-mini`)
- **ब्राउजर**: Chrome/Edge WebGPU समर्थनसहित डेमोहरूको लागि
- **Docker**: Open WebUI को लागि (वैकल्पिक)

## स्थापना र सेटअप

### १. Python वातावरण सेटअप

```cmd
# Navigate to Module08 directory
cd Module08

# Create and activate virtual environment
py -m venv .venv
.venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### २. Foundry Local सेटअप

```cmd
# Verify Foundry Local installation
foundry --version

# Start the service
foundry service start

# Load a model
foundry model run phi-4-mini

# Verify model is running
foundry service ps
```

## नमूना एप्लिकेसनहरू

### Chainlit च्याट एप्लिकेसन

**विशेषताहरू:**
- 🚀 **रियल-टाइम स्ट्रिमिङ**: टोकनहरू उत्पन्न हुनेबित्तिकै देखिन्छन्
- 🛡️ **मजबुत त्रुटि व्यवस्थापन**: सहज डिग्रेडेसन र पुन: प्राप्ति
- 🎨 **आधुनिक UI**: व्यावसायिक च्याट इन्टरफेस
- 🔧 **लचिलो कन्फिगरेसन**: वातावरण भेरिएबलहरू र स्वत: पत्ता लगाउने क्षमता
- 📱 **उत्तरदायी डिजाइन**: डेस्कटप र मोबाइल उपकरणमा काम गर्दछ

**छिटो सुरु गर्ने तरिका:**
```cmd
# Run with default settings (recommended)
chainlit run samples\04\app.py -w --port 8080

# Use specific model
set MODEL=qwen2.5-7b-instruct
chainlit run samples\04\app.py -w --port 8080

# Manual endpoint configuration
set BASE_URL=http://localhost:51211
set API_KEY=your-api-key
chainlit run samples\04\app.py -w --port 8080
```

### WebGPU ब्राउजर डेमो

**विशेषताहरू:**
- 🌐 **ब्राउजर-नेभेटिभ AI**: कुनै सर्भर आवश्यक छैन, पूर्ण रूपमा ब्राउजरमा चल्छ
- ⚡ **WebGPU एक्सेलेरेशन**: हार्डवेयर एक्सेलेरेशन उपलब्ध हुँदा
- 🔒 **अधिकतम गोपनीयता**: डाटा कहिल्यै उपकरण बाहिर जान्दैन
- 🎯 **शून्य स्थापना**: कुनै पनि उपयुक्त ब्राउजरमा काम गर्दछ
- 🔄 **सहज फलब्याक**: WebGPU उपलब्ध नभए CPU मा फलब्याक हुन्छ

**चलाउने तरिका:**
```cmd
cd samples\04\webgpu-demo
python -m http.server 5173
# Open http://localhost:5173
```

### Open WebUI एकीकरण

**विशेषताहरू:**
- 🎨 **ChatGPT-जस्तै इन्टरफेस**: व्यावसायिक, परिचित UI
- 👥 **बहु-प्रयोगकर्ता समर्थन**: प्रयोगकर्ता खाता र संवाद इतिहास
- 📁 **फाइल प्रशोधन**: अपलोड र डकुमेन्ट विश्लेषण
- 🔄 **मोडेल स्विचिङ**: विभिन्न मोडेलहरू बीच सजिलो स्विचिङ
- 🐳 **Docker परिनियोजन**: उत्पादन-तयार कन्टेनराइज्ड सेटअप

**छिटो सेटअप:**
```cmd
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```

## कन्फिगरेसन सन्दर्भ

### वातावरण भेरिएबलहरू

| भेरिएबल | विवरण | डिफल्ट | उदाहरण |
|---------|-------|--------|--------|
| `MODEL` | प्रयोग गर्न मोडेल उपनाम | `phi-4-mini` | `qwen2.5-7b-instruct` |
| `BASE_URL` | Foundry Local अन्तर्क्रियाको अन्त्य बिन्दु | स्वत: पत्ता लगाइएको | `http://localhost:51211` |
| `API_KEY` | API कुञ्जी (स्थानीयको लागि वैकल्पिक) | `""` | `your-api-key` |

## समस्या समाधान

### सामान्य समस्याहरू

**Chainlit एप्लिकेसन:**

१. **सेवा उपलब्ध छैन:**
   ```cmd
   # Check Foundry Local status
   foundry service status
   foundry service ps
   
   # Validate API endpoint (note: port 51211)
   curl http://localhost:51211/v1/models
   ```

२. **पोर्ट द्वन्द्व:**
   ```cmd
   # Check what's using port 8080
   netstat -ano | findstr :8080
   
   # Use different port if needed
   chainlit run samples\04\app.py -w --port 3000
   ```

३. **Python वातावरण समस्याहरू:**
   ```cmd
   # Verify correct interpreter in VS Code
   # Ctrl+Shift+P → Python: Select Interpreter
   # Choose: Module08/.venv/Scripts/python.exe
   
   # Reinstall dependencies
   pip install -r requirements.txt
   ```

**WebGPU डेमो:**

१. **WebGPU समर्थित छैन:**
   - Chrome/Edge ११३+ मा अपडेट गर्नुहोस्
   - WebGPU सक्षम गर्नुहोस्: `chrome://flags/#enable-unsafe-webgpu`
   - GPU स्थिति जाँच गर्नुहोस्: `chrome://gpu`
   - डेमो स्वत: CPU मा फलब्याक हुनेछ

२. **मोडेल लोडिङ त्रुटिहरू:**
   - मोडेल डाउनलोडको लागि इन्टरनेट कनेक्शन सुनिश्चित गर्नुहोस्
   - ब्राउजर कन्सोलमा CORS त्रुटिहरू जाँच गर्नुहोस्
   - HTTP मार्फत सेवा सुनिश्चित गर्नुहोस् (file:// होइन)

**Open WebUI:**

१. **कनेक्शन अस्वीकृत:**
   ```cmd
   # Check Docker is running
   docker --version
   
   # Check container status
   docker ps | findstr open-webui
   
   # View container logs
   docker logs open-webui
   ```

२. **मोडेलहरू देखिँदैनन्:**
   ```cmd
   # Verify Foundry Local endpoint
   curl http://localhost:51211/v1/models
   
   # Restart Open WebUI
   docker restart open-webui
   ```

### मान्यता जाँच सूची

```cmd
# ✅ 1. Foundry Local Setup
foundry --version                    # Should show version
foundry service status               # Should show "running"
foundry model list                   # Should show loaded models
curl http://localhost:51211/v1/models  # Should return JSON

# ✅ 2. Python Environment  
python --version                     # Should be 3.10+
pip list | findstr chainlit         # Should show chainlit package
pip list | findstr openai           # Should show openai package

# ✅ 3. Application Testing
chainlit run samples\04\app.py -w --port 8080  # Should open browser
# Test WebGPU demo at localhost:5173
# Test Open WebUI at localhost:3000
```

## उन्नत प्रयोग

### प्रदर्शन अनुकूलन

**Chainlit:**
- राम्रो अनुभवको लागि स्ट्रिमिङ प्रयोग गर्नुहोस्
- उच्च समवर्तीता लागि कनेक्शन पूलिङ कार्यान्वयन गर्नुहोस्
- दोहोरिएका प्रश्नहरूको लागि मोडेल प्रतिक्रिया क्यास गर्नुहोस्
- ठूलो संवाद इतिहासको साथ मेमोरी प्रयोग निगरानी गर्नुहोस्

**WebGPU:**
- अधिकतम गोपनीयता र गति लागि WebGPU प्रयोग गर्नुहोस्
- साना मोडेलहरूको लागि मोडेल क्वान्टाइजेसन कार्यान्वयन गर्नुहोस्
- पृष्ठभूमि प्रशोधनको लागि Web Workers प्रयोग गर्नुहोस्
- ब्राउजर स्टोरेजमा कम्पाइल गरिएको मोडेलहरू क्यास गर्नुहोस्

**Open WebUI:**
- संवाद इतिहासको लागि स्थायी भोल्युमहरू प्रयोग गर्नुहोस्
- Docker कन्टेनरको लागि स्रोत सीमा कन्फिगर गर्नुहोस्
- प्रयोगकर्ता डाटाको लागि ब्याकअप रणनीतिहरू कार्यान्वयन गर्नुहोस्
- SSL टर्मिनेसनको लागि रिभर्स प्रोक्सी सेटअप गर्नुहोस्

### एकीकरण ढाँचा

**हाइब्रिड स्थानीय/क्लाउड:**
```python
# Route based on complexity and privacy requirements
async def intelligent_routing(prompt: str, metadata: dict):
    if metadata.get("contains_pii"):
        return await foundry_local_completion(prompt)  # Privacy-sensitive
    elif len(prompt.split()) > 200:
        return await azure_openai_completion(prompt)   # Complex reasoning
    else:
        return await foundry_local_completion(prompt)  # Default local
```

**मल्टि-मोडल पाइपलाइन:**
```python
# Combine different AI capabilities
async def analyze_document(file_path: str):
    # 1. OCR with WebGPU (browser-based)
    text = await webgpu_ocr(file_path)
    
    # 2. Analysis with Foundry Local (private)
    summary = await foundry_local_analyze(text)
    
    # 3. Enhancement with cloud (if needed)
    if summary.confidence < 0.8:
        summary = await azure_openai_enhance(summary)
    
    return summary
```

## उत्पादन परिनियोजन

### सुरक्षा विचारहरू

- **API कुञ्जीहरू**: वातावरण भेरिएबलहरू प्रयोग गर्नुहोस्, कहिल्यै हार्डकोड नगर्नुहोस्
- **नेटवर्क**: उत्पादनमा HTTPS प्रयोग गर्नुहोस्, टिम पहुँचको लागि VPN विचार गर्नुहोस्
- **पहुँच नियन्त्रण**: Open WebUI को लागि प्रमाणीकरण कार्यान्वयन गर्नुहोस्
- **डाटा गोपनीयता**: कुन डाटा स्थानीय रहन्छ र क्लाउडमा जान्छ भनेर अडिट गर्नुहोस्
- **अपडेटहरू**: Foundry Local र कन्टेनरहरू अद्यावधिक राख्नुहोस्

### निगरानी र मर्मत

- **स्वास्थ्य जाँचहरू**: अन्त्य बिन्दु निगरानी कार्यान्वयन गर्नुहोस्
- **लगिङ**: सबै कम्पोनेन्टहरूबाट लगहरू केन्द्रीकृत गर्नुहोस्
- **मेट्रिक्स**: प्रतिक्रिया समय, त्रुटि दर, स्रोत प्रयोग ट्र्याक गर्नुहोस्
- **ब्याकअप**: संवाद डाटा र कन्फिगरेसनहरूको नियमित ब्याकअप गर्नुहोस्

## सन्दर्भ र स्रोतहरू

### दस्तावेजहरू
- [Chainlit दस्तावेज](https://docs.chainlit.io/) - पूर्ण फ्रेमवर्क गाइड
- [Foundry Local दस्तावेज](https://learn.microsoft.com/azure/ai-foundry/foundry-local/) - आधिकारिक Microsoft दस्तावेज
- [ONNX Runtime Web](https://onnxruntime.ai/docs/get-started/with-javascript/web.html) - WebGPU एकीकरण
- [Open WebUI दस्तावेज](https://docs.openwebui.com/) - उन्नत कन्फिगरेसन

### नमूना फाइलहरू
- [`app.py`](../../../../../Module08/samples/04/app.py) - उत्पादन Chainlit एप्लिकेसन
- [`chainlit_app.ipynb`](./chainlit_app.ipynb) - शैक्षिक नोटबुक
- [`webgpu-demo/`](../../../../../Module08/samples/04/webgpu-demo) - ब्राउजर-आधारित AI इनफरेन्स
- [`open-webui-guide.md`](./open-webui-guide.md) - पूर्ण Open WebUI सेटअप

### सम्बन्धित नमूनाहरू
- [सत्र ४ दस्तावेज](../../04.CuttingEdgeModels.md) - पूर्ण सत्र गाइड
- [Foundry Local नमूनाहरू](https://github.com/microsoft/foundry-local/tree/main/samples) - आधिकारिक नमूनाहरू

---

