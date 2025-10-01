<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "2f1754a482b6a84e07287a5b775e65b6",
  "translation_date": "2025-09-30T23:53:16+00:00",
  "source_file": "Module08/samples/04/README.md",
  "language_code": "mr"
}
-->
# नमुना 04: Chainlit सह उत्पादन चॅट अनुप्रयोग

Microsoft Foundry Local वापरून उत्पादन-तयार चॅट अनुप्रयोग तयार करण्यासाठी विविध पद्धतींचे सविस्तर उदाहरण, ज्यामध्ये आधुनिक वेब इंटरफेस, स्ट्रीमिंग प्रतिसाद आणि अत्याधुनिक ब्राउझर तंत्रज्ञान समाविष्ट आहे.

## काय समाविष्ट आहे

- **🚀 Chainlit चॅट अ‍ॅप** (`app.py`): स्ट्रीमिंगसह उत्पादन-तयार चॅट अनुप्रयोग
- **🌐 WebGPU डेमो** (`webgpu-demo/`): हार्डवेअर प्रवेगासह ब्राउझर-आधारित AI इनफरन्स
- **🎨 Open WebUI एकत्रीकरण** (`open-webui-guide.md`): व्यावसायिक ChatGPT-सारखा इंटरफेस
- **📚 शैक्षणिक नोटबुक** (`chainlit_app.ipynb`): परस्पर शिकण्याची सामग्री

## जलद सुरुवात

### 1. Chainlit चॅट अनुप्रयोग

```cmd
# Navigate to Module08 directory
cd Module08

# Start your model
foundry model run phi-4-mini

# Run Chainlit app (using port 8080 to avoid conflicts)
chainlit run samples\04\app.py -w --port 8080
```

उघडते येथे: `http://localhost:8080`

### 2. WebGPU ब्राउझर डेमो

```cmd
# Navigate to WebGPU demo
cd Module08\samples\04\webgpu-demo

# Serve the demo
python -m http.server 5173
```

उघडते येथे: `http://localhost:5173`

### 3. Open WebUI सेटअप

```cmd
# Run Open WebUI with Docker
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```

उघडते येथे: `http://localhost:3000`

## आर्किटेक्चर नमुने

### स्थानिक विरुद्ध क्लाउड निर्णय मॅट्रिक्स

| परिस्थिती | शिफारस | कारण |
|-----------|---------|-------|
| **गोपनीय डेटा** | 🏠 स्थानिक (Foundry) | डेटा कधीही डिव्हाइस सोडत नाही |
| **जटिल विचारमंथन** | ☁️ क्लाउड (Azure OpenAI) | मोठ्या मॉडेल्सचा प्रवेश |
| **रिअल-टाइम चॅट** | 🏠 स्थानिक (Foundry) | कमी विलंब, जलद प्रतिसाद |
| **दस्तऐवज विश्लेषण** | 🔄 हायब्रिड | स्थानिक काढण्यासाठी, क्लाउड विश्लेषणासाठी |
| **कोड निर्मिती** | 🏠 स्थानिक (Foundry) | गोपनीयता + विशेष मॉडेल्स |
| **संशोधन कार्य** | ☁️ क्लाउड (Azure OpenAI) | विस्तृत ज्ञानसंच आवश्यक |

### तंत्रज्ञान तुलना

| तंत्रज्ञान | उपयोग प्रकरण | फायदे | तोटे |
|------------|--------------|-------|------|
| **Chainlit** | Python विकसक, जलद प्रोटोटायपिंग | सोपी सेटअप, स्ट्रीमिंग समर्थन | फक्त Python |
| **WebGPU** | जास्तीत जास्त गोपनीयता, ऑफलाइन परिस्थिती | ब्राउझर-नेटिव्ह, सर्व्हरची गरज नाही | मर्यादित मॉडेल आकार |
| **Open WebUI** | उत्पादन तैनाती, संघ | व्यावसायिक UI, वापरकर्ता व्यवस्थापन | Docker आवश्यक |

## पूर्वअटी

- **Foundry Local**: स्थापित आणि चालू ([डाउनलोड](https://aka.ms/foundry-local-installer))
- **Python**: 3.10+ वर्च्युअल वातावरणासह
- **मॉडेल**: किमान एक लोड केलेले (`foundry model run phi-4-mini`)
- **ब्राउझर**: Chrome/Edge WebGPU समर्थनासह डेमोसाठी
- **Docker**: Open WebUI साठी (पर्यायी)

## स्थापना आणि सेटअप

### 1. Python वातावरण सेटअप

```cmd
# Navigate to Module08 directory
cd Module08

# Create and activate virtual environment
py -m venv .venv
.venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### 2. Foundry Local सेटअप

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

## नमुना अनुप्रयोग

### Chainlit चॅट अनुप्रयोग

**वैशिष्ट्ये:**
- 🚀 **रिअल-टाइम स्ट्रीमिंग**: टोकन्स तयार होताच दिसतात
- 🛡️ **मजबूत त्रुटी हाताळणी**: सौम्य अपयश आणि पुनर्प्राप्ती
- 🎨 **आधुनिक UI**: व्यावसायिक चॅट इंटरफेस
- 🔧 **लवचिक कॉन्फिगरेशन**: पर्यावरणीय व्हेरिएबल्स आणि ऑटो-डिटेक्शन
- 📱 **प्रतिसादात्मक डिझाइन**: डेस्कटॉप आणि मोबाइल डिव्हाइसवर कार्य करते

**जलद सुरुवात:**
```cmd
# Run with default settings (recommended)
chainlit run samples\04\app.py -w --port 8080

# Use specific model
set MODEL=qwen2.5-7b
chainlit run samples\04\app.py -w --port 8080

# Manual endpoint configuration
set BASE_URL=http://localhost:51211
set API_KEY=your-api-key
chainlit run samples\04\app.py -w --port 8080
```

### WebGPU ब्राउझर डेमो

**वैशिष्ट्ये:**
- 🌐 **ब्राउझर-नेटिव्ह AI**: सर्व्हरची गरज नाही, पूर्णपणे ब्राउझरमध्ये चालते
- ⚡ **WebGPU प्रवेग**: हार्डवेअर प्रवेग उपलब्ध असल्यास
- 🔒 **जास्तीत जास्त गोपनीयता**: डेटा कधीही तुमच्या डिव्हाइसच्या बाहेर जात नाही
- 🎯 **शून्य स्थापना**: कोणत्याही सुसंगत ब्राउझरमध्ये कार्य करते
- 🔄 **सौम्य अपयश**: WebGPU अनुपलब्ध असल्यास CPU वर स्वयंचलितपणे स्विच करते

**चालवणे:**
```cmd
cd samples\04\webgpu-demo
python -m http.server 5173
# Open http://localhost:5173
```

### Open WebUI एकत्रीकरण

**वैशिष्ट्ये:**
- 🎨 **ChatGPT-सारखा इंटरफेस**: व्यावसायिक, परिचित UI
- 👥 **मल्टी-युजर समर्थन**: वापरकर्ता खाती आणि संभाषण इतिहास
- 📁 **फाइल प्रक्रिया**: दस्तऐवज अपलोड करा आणि विश्लेषण करा
- 🔄 **मॉडेल स्विचिंग**: वेगवेगळ्या मॉडेल्समध्ये सहज स्विचिंग
- 🐳 **Docker तैनाती**: उत्पादन-तयार कंटेनरयुक्त सेटअप

**जलद सेटअप:**
```cmd
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```

## कॉन्फिगरेशन संदर्भ

### पर्यावरणीय व्हेरिएबल्स

| व्हेरिएबल | वर्णन | डीफॉल्ट | उदाहरण |
|-----------|---------|---------|---------|
| `MODEL` | वापरण्यासाठी मॉडेल उपनाम | `phi-4-mini` | `qwen2.5-7b` |
| `BASE_URL` | Foundry Local एंडपॉइंट | स्वयंचलितपणे शोधलेले | `http://localhost:51211` |
| `API_KEY` | API की (स्थानिकसाठी पर्यायी) | `""` | `your-api-key` |

## समस्या निवारण

### सामान्य समस्या

**Chainlit अनुप्रयोग:**

1. **सेवा उपलब्ध नाही:**
   ```cmd
   # Check Foundry Local status
   foundry service status
   foundry service ps
   
   # Validate API endpoint (note: port 51211)
   curl http://localhost:51211/v1/models
   ```

2. **पोर्ट संघर्ष:**
   ```cmd
   # Check what's using port 8080
   netstat -ano | findstr :8080
   
   # Use different port if needed
   chainlit run samples\04\app.py -w --port 3000
   ```

3. **Python वातावरण समस्या:**
   ```cmd
   # Verify correct interpreter in VS Code
   # Ctrl+Shift+P → Python: Select Interpreter
   # Choose: Module08/.venv/Scripts/python.exe
   
   # Reinstall dependencies
   pip install -r requirements.txt
   ```

**WebGPU डेमो:**

1. **WebGPU समर्थित नाही:**
   - Chrome/Edge 113+ मध्ये अपडेट करा
   - WebGPU सक्षम करा: `chrome://flags/#enable-unsafe-webgpu`
   - GPU स्थिती तपासा: `chrome://gpu`
   - डेमो स्वयंचलितपणे CPU वर स्विच करेल

2. **मॉडेल लोडिंग त्रुटी:**
   - मॉडेल डाउनलोडसाठी इंटरनेट कनेक्शन सुनिश्चित करा
   - ब्राउझर कन्सोलमध्ये CORS त्रुटी तपासा
   - HTTP द्वारे सर्व्ह करत असल्याचे सत्यापित करा (file:// नाही)

**Open WebUI:**

1. **कनेक्शन नाकारले:**
   ```cmd
   # Check Docker is running
   docker --version
   
   # Check container status
   docker ps | findstr open-webui
   
   # View container logs
   docker logs open-webui
   ```

2. **मॉडेल्स दिसत नाहीत:**
   ```cmd
   # Verify Foundry Local endpoint
   curl http://localhost:51211/v1/models
   
   # Restart Open WebUI
   docker restart open-webui
   ```

### सत्यापन चेकलिस्ट

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

## प्रगत वापर

### कार्यक्षमता ऑप्टिमायझेशन

**Chainlit:**
- चांगल्या अनुभवासाठी स्ट्रीमिंग वापरा
- उच्च एकत्रिततेसाठी कनेक्शन पूलिंग अंमलात आणा
- पुनरावृत्ती क्वेरीसाठी मॉडेल प्रतिसाद कॅश करा
- मोठ्या संभाषण इतिहासासह मेमरी वापराचे निरीक्षण करा

**WebGPU:**
- जास्तीत जास्त गोपनीयता आणि वेगासाठी WebGPU वापरा
- लहान मॉडेल्ससाठी मॉडेल क्वांटायझेशन अंमलात आणा
- पार्श्वभूमी प्रक्रियेसाठी Web Workers वापरा
- ब्राउझर स्टोरेजमध्ये संकलित मॉडेल्स कॅश करा

**Open WebUI:**
- संभाषण इतिहासासाठी स्थिर व्हॉल्यूम्स वापरा
- Docker कंटेनरसाठी संसाधन मर्यादा कॉन्फिगर करा
- वापरकर्ता डेटासाठी बॅकअप धोरणे अंमलात आणा
- SSL समाप्तीसाठी रिव्हर्स प्रॉक्सी सेट करा

### एकत्रीकरण नमुने

**हायब्रिड स्थानिक/क्लाउड:**
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

**मल्टी-मोडल पाइपलाइन:**
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

## उत्पादन तैनाती

### सुरक्षा विचार

- **API कीज**: पर्यावरणीय व्हेरिएबल्स वापरा, कधीही हार्डकोड करू नका
- **नेटवर्क**: उत्पादनात HTTPS वापरा, संघ प्रवेशासाठी VPN विचार करा
- **प्रवेश नियंत्रण**: Open WebUI साठी प्रमाणीकरण अंमलात आणा
- **डेटा गोपनीयता**: कोणता डेटा स्थानिक राहतो आणि कोणता क्लाउडवर जातो याचे ऑडिट करा
- **अपडेट्स**: Foundry Local आणि कंटेनर्स अद्ययावत ठेवा

### निरीक्षण आणि देखभाल

- **हेल्थ चेक्स**: एंडपॉइंट मॉनिटरिंग अंमलात आणा
- **लॉगिंग**: सर्व घटकांमधून लॉग्स केंद्रीकृत करा
- **मेट्रिक्स**: प्रतिसाद वेळ, त्रुटी दर, संसाधन वापर ट्रॅक करा
- **बॅकअप**: संभाषण डेटा आणि कॉन्फिगरेशन्सचा नियमित बॅकअप

## संदर्भ आणि संसाधने

### दस्तऐवजीकरण
- [Chainlit दस्तऐवजीकरण](https://docs.chainlit.io/) - संपूर्ण फ्रेमवर्क मार्गदर्शक
- [Foundry Local दस्तऐवजीकरण](https://learn.microsoft.com/azure/ai-foundry/foundry-local/) - Microsoft अधिकृत दस्तऐवज
- [ONNX Runtime Web](https://onnxruntime.ai/docs/get-started/with-javascript/web.html) - WebGPU एकत्रीकरण
- [Open WebUI दस्तऐवजीकरण](https://docs.openwebui.com/) - प्रगत कॉन्फिगरेशन

### नमुना फाइल्स
- [`app.py`](../../../../../Module08/samples/04/app.py) - उत्पादन Chainlit अनुप्रयोग
- [`chainlit_app.ipynb`](./chainlit_app.ipynb) - शैक्षणिक नोटबुक
- [`webgpu-demo/`](../../../../../Module08/samples/04/webgpu-demo) - ब्राउझर-आधारित AI इनफरन्स
- [`open-webui-guide.md`](./open-webui-guide.md) - संपूर्ण Open WebUI सेटअप

### संबंधित नमुने
- [सत्र 4 दस्तऐवजीकरण](../../04.CuttingEdgeModels.md) - संपूर्ण सत्र मार्गदर्शक
- [Foundry Local नमुने](https://github.com/microsoft/foundry-local/tree/main/samples) - अधिकृत नमुने

---

**अस्वीकरण**:  
हा दस्तऐवज AI भाषांतर सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) वापरून भाषांतरित करण्यात आला आहे. आम्ही अचूकतेसाठी प्रयत्नशील असलो तरी, कृपया लक्षात ठेवा की स्वयंचलित भाषांतरांमध्ये त्रुटी किंवा अचूकतेचा अभाव असू शकतो. मूळ भाषेतील दस्तऐवज हा अधिकृत स्रोत मानला जावा. महत्त्वाच्या माहितीसाठी, व्यावसायिक मानवी भाषांतराची शिफारस केली जाते. या भाषांतराचा वापर करून उद्भवलेल्या कोणत्याही गैरसमज किंवा चुकीच्या अर्थासाठी आम्ही जबाबदार राहणार नाही.