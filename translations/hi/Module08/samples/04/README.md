<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "2f1754a482b6a84e07287a5b775e65b6",
  "translation_date": "2025-09-30T23:42:45+00:00",
  "source_file": "Module08/samples/04/README.md",
  "language_code": "hi"
}
-->
# नमूना 04: Chainlit के साथ प्रोडक्शन चैट एप्लिकेशन

Microsoft Foundry Local का उपयोग करके प्रोडक्शन-रेडी चैट एप्लिकेशन बनाने के कई तरीकों को दिखाने वाला एक व्यापक नमूना, जिसमें आधुनिक वेब इंटरफेस, स्ट्रीमिंग प्रतिक्रियाएँ, और नवीनतम ब्राउज़र तकनीकें शामिल हैं।

## क्या शामिल है

- **🚀 Chainlit चैट ऐप** (`app.py`): स्ट्रीमिंग के साथ प्रोडक्शन-रेडी चैट एप्लिकेशन
- **🌐 WebGPU डेमो** (`webgpu-demo/`): हार्डवेयर एक्सेलेरेशन के साथ ब्राउज़र-आधारित AI इंफेरेंस
- **🎨 Open WebUI इंटीग्रेशन** (`open-webui-guide.md`): पेशेवर ChatGPT जैसा इंटरफेस
- **📚 शैक्षिक नोटबुक** (`chainlit_app.ipynb`): इंटरएक्टिव लर्निंग सामग्री

## त्वरित शुरुआत

### 1. Chainlit चैट एप्लिकेशन

```cmd
# Navigate to Module08 directory
cd Module08

# Start your model
foundry model run phi-4-mini

# Run Chainlit app (using port 8080 to avoid conflicts)
chainlit run samples\04\app.py -w --port 8080
```

खुलता है: `http://localhost:8080`

### 2. WebGPU ब्राउज़र डेमो

```cmd
# Navigate to WebGPU demo
cd Module08\samples\04\webgpu-demo

# Serve the demo
python -m http.server 5173
```

खुलता है: `http://localhost:5173`

### 3. Open WebUI सेटअप

```cmd
# Run Open WebUI with Docker
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```

खुलता है: `http://localhost:3000`

## आर्किटेक्चर पैटर्न

### लोकल बनाम क्लाउड निर्णय मैट्रिक्स

| परिदृश्य | सिफारिश | कारण |
|----------|---------|------|
| **गोपनीय डेटा** | 🏠 लोकल (Foundry) | डेटा डिवाइस से बाहर नहीं जाता |
| **जटिल तर्क** | ☁️ क्लाउड (Azure OpenAI) | बड़े मॉडल तक पहुंच |
| **रियल-टाइम चैट** | 🏠 लोकल (Foundry) | कम विलंबता, तेज प्रतिक्रियाएँ |
| **दस्तावेज़ विश्लेषण** | 🔄 हाइब्रिड | निष्कर्षण के लिए लोकल, विश्लेषण के लिए क्लाउड |
| **कोड जनरेशन** | 🏠 लोकल (Foundry) | गोपनीयता + विशेष मॉडल |
| **अनुसंधान कार्य** | ☁️ क्लाउड (Azure OpenAI) | व्यापक ज्ञान आधार की आवश्यकता |

### तकनीकी तुलना

| तकनीक | उपयोग का मामला | फायदे | नुकसान |
|-------|----------------|-------|--------|
| **Chainlit** | Python डेवलपर्स, त्वरित प्रोटोटाइप | आसान सेटअप, स्ट्रीमिंग सपोर्ट | केवल Python |
| **WebGPU** | अधिकतम गोपनीयता, ऑफलाइन परिदृश्य | ब्राउज़र-नेटिव, सर्वर की आवश्यकता नहीं | सीमित मॉडल आकार |
| **Open WebUI** | प्रोडक्शन डिप्लॉयमेंट, टीमें | पेशेवर UI, उपयोगकर्ता प्रबंधन | Docker की आवश्यकता |

## आवश्यकताएँ

- **Foundry Local**: इंस्टॉल और चल रहा ([डाउनलोड करें](https://aka.ms/foundry-local-installer))
- **Python**: 3.10+ वर्चुअल एनवायरनमेंट के साथ
- **मॉडल**: कम से कम एक लोडेड (`foundry model run phi-4-mini`)
- **ब्राउज़र**: Chrome/Edge WebGPU सपोर्ट के साथ डेमो के लिए
- **Docker**: Open WebUI के लिए (वैकल्पिक)

## इंस्टॉलेशन और सेटअप

### 1. Python एनवायरनमेंट सेटअप

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

## नमूना एप्लिकेशन

### Chainlit चैट एप्लिकेशन

**विशेषताएँ:**
- 🚀 **रियल-टाइम स्ट्रीमिंग**: टोकन उत्पन्न होते ही दिखाई देते हैं
- 🛡️ **मजबूत त्रुटि प्रबंधन**: ग्रेसफुल डिग्रेडेशन और रिकवरी
- 🎨 **आधुनिक UI**: बॉक्स से बाहर पेशेवर चैट इंटरफेस
- 🔧 **लचीला कॉन्फ़िगरेशन**: एनवायरनमेंट वेरिएबल्स और ऑटो-डिटेक्शन
- 📱 **उत्तरदायी डिज़ाइन**: डेस्कटॉप और मोबाइल डिवाइस पर काम करता है

**त्वरित शुरुआत:**
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

### WebGPU ब्राउज़र डेमो

**विशेषताएँ:**
- 🌐 **ब्राउज़र-नेटिव AI**: सर्वर की आवश्यकता नहीं, पूरी तरह से ब्राउज़र में चलता है
- ⚡ **WebGPU एक्सेलेरेशन**: हार्डवेयर एक्सेलेरेशन उपलब्ध होने पर
- 🔒 **अधिकतम गोपनीयता**: आपका डेटा कभी भी डिवाइस से बाहर नहीं जाता
- 🎯 **शून्य इंस्टॉल**: किसी भी संगत ब्राउज़र में काम करता है
- 🔄 **ग्रेसफुल फॉलबैक**: WebGPU अनुपलब्ध होने पर CPU पर वापस जाता है

**चलाना:**
```cmd
cd samples\04\webgpu-demo
python -m http.server 5173
# Open http://localhost:5173
```

### Open WebUI इंटीग्रेशन

**विशेषताएँ:**
- 🎨 **ChatGPT जैसा इंटरफेस**: पेशेवर, परिचित UI
- 👥 **मल्टी-यूजर सपोर्ट**: उपयोगकर्ता खाते और बातचीत का इतिहास
- 📁 **फाइल प्रोसेसिंग**: दस्तावेज़ अपलोड और विश्लेषण
- 🔄 **मॉडल स्विचिंग**: विभिन्न मॉडलों के बीच आसानी से स्विच करें
- 🐳 **Docker डिप्लॉयमेंट**: प्रोडक्शन-रेडी कंटेनराइज्ड सेटअप

**त्वरित सेटअप:**
```cmd
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```

## कॉन्फ़िगरेशन संदर्भ

### एनवायरनमेंट वेरिएबल्स

| वेरिएबल | विवरण | डिफ़ॉल्ट | उदाहरण |
|---------|-------|---------|--------|
| `MODEL` | उपयोग करने के लिए मॉडल का उपनाम | `phi-4-mini` | `qwen2.5-7b` |
| `BASE_URL` | Foundry Local एंडपॉइंट | ऑटो-डिटेक्टेड | `http://localhost:51211` |
| `API_KEY` | API कुंजी (लोकल के लिए वैकल्पिक) | `""` | `your-api-key` |

## समस्या निवारण

### सामान्य समस्याएँ

**Chainlit एप्लिकेशन:**

1. **सेवा उपलब्ध नहीं:**
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

3. **Python एनवायरनमेंट समस्याएँ:**
   ```cmd
   # Verify correct interpreter in VS Code
   # Ctrl+Shift+P → Python: Select Interpreter
   # Choose: Module08/.venv/Scripts/python.exe
   
   # Reinstall dependencies
   pip install -r requirements.txt
   ```

**WebGPU डेमो:**

1. **WebGPU समर्थित नहीं:**
   - Chrome/Edge 113+ में अपडेट करें
   - WebGPU सक्षम करें: `chrome://flags/#enable-unsafe-webgpu`
   - GPU स्थिति जांचें: `chrome://gpu`
   - डेमो स्वचालित रूप से CPU पर वापस जाएगा

2. **मॉडल लोडिंग त्रुटियाँ:**
   - मॉडल डाउनलोड के लिए इंटरनेट कनेक्शन सुनिश्चित करें
   - ब्राउज़र कंसोल में CORS त्रुटियाँ जांचें
   - सुनिश्चित करें कि आप HTTP के माध्यम से सेवा दे रहे हैं (file:// नहीं)

**Open WebUI:**

1. **कनेक्शन अस्वीकृत:**
   ```cmd
   # Check Docker is running
   docker --version
   
   # Check container status
   docker ps | findstr open-webui
   
   # View container logs
   docker logs open-webui
   ```

2. **मॉडल दिखाई नहीं दे रहे:**
   ```cmd
   # Verify Foundry Local endpoint
   curl http://localhost:51211/v1/models
   
   # Restart Open WebUI
   docker restart open-webui
   ```

### वैलिडेशन चेकलिस्ट

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

## उन्नत उपयोग

### प्रदर्शन अनुकूलन

**Chainlit:**
- बेहतर अनुभव के लिए स्ट्रीमिंग का उपयोग करें
- उच्च समवर्तीता के लिए कनेक्शन पूलिंग लागू करें
- बार-बार पूछे जाने वाले प्रश्नों के लिए मॉडल प्रतिक्रियाओं को कैश करें
- बड़े बातचीत इतिहास के साथ मेमोरी उपयोग की निगरानी करें

**WebGPU:**
- अधिकतम गोपनीयता और गति के लिए WebGPU का उपयोग करें
- छोटे मॉडलों के लिए मॉडल क्वांटाइजेशन लागू करें
- बैकग्राउंड प्रोसेसिंग के लिए Web Workers का उपयोग करें
- ब्राउज़र स्टोरेज में संकलित मॉडलों को कैश करें

**Open WebUI:**
- बातचीत इतिहास के लिए स्थायी वॉल्यूम का उपयोग करें
- Docker कंटेनर के लिए संसाधन सीमाएँ कॉन्फ़िगर करें
- उपयोगकर्ता डेटा के लिए बैकअप रणनीतियाँ लागू करें
- SSL समाप्ति के लिए रिवर्स प्रॉक्सी सेट करें

### इंटीग्रेशन पैटर्न

**हाइब्रिड लोकल/क्लाउड:**
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

## प्रोडक्शन डिप्लॉयमेंट

### सुरक्षा विचार

- **API कुंजियाँ**: एनवायरनमेंट वेरिएबल्स का उपयोग करें, कभी हार्डकोड न करें
- **नेटवर्क**: प्रोडक्शन में HTTPS का उपयोग करें, टीम एक्सेस के लिए VPN पर विचार करें
- **एक्सेस कंट्रोल**: Open WebUI के लिए प्रमाणीकरण लागू करें
- **डेटा गोपनीयता**: यह ऑडिट करें कि कौन सा डेटा लोकल रहता है और कौन सा क्लाउड में जाता है
- **अपडेट्स**: Foundry Local और कंटेनरों को अपडेट रखें

### मॉनिटरिंग और रखरखाव

- **हेल्थ चेक्स**: एंडपॉइंट मॉनिटरिंग लागू करें
- **लॉगिंग**: सभी घटकों से लॉग्स को केंद्रीकृत करें
- **मेट्रिक्स**: प्रतिक्रिया समय, त्रुटि दर, संसाधन उपयोग को ट्रैक करें
- **बैकअप**: बातचीत डेटा और कॉन्फ़िगरेशन का नियमित बैकअप

## संदर्भ और संसाधन

### दस्तावेज़ीकरण
- [Chainlit दस्तावेज़ीकरण](https://docs.chainlit.io/) - पूरा फ्रेमवर्क गाइड
- [Foundry Local दस्तावेज़ीकरण](https://learn.microsoft.com/azure/ai-foundry/foundry-local/) - आधिकारिक Microsoft दस्तावेज़
- [ONNX Runtime Web](https://onnxruntime.ai/docs/get-started/with-javascript/web.html) - WebGPU इंटीग्रेशन
- [Open WebUI दस्तावेज़ीकरण](https://docs.openwebui.com/) - उन्नत कॉन्फ़िगरेशन

### नमूना फाइलें
- [`app.py`](../../../../../Module08/samples/04/app.py) - प्रोडक्शन Chainlit एप्लिकेशन
- [`chainlit_app.ipynb`](./chainlit_app.ipynb) - शैक्षिक नोटबुक
- [`webgpu-demo/`](../../../../../Module08/samples/04/webgpu-demo) - ब्राउज़र-आधारित AI इंफेरेंस
- [`open-webui-guide.md`](./open-webui-guide.md) - पूरा Open WebUI सेटअप

### संबंधित नमूने
- [सत्र 4 दस्तावेज़ीकरण](../../04.CuttingEdgeModels.md) - पूरा सत्र गाइड
- [Foundry Local नमूने](https://github.com/microsoft/foundry-local/tree/main/samples) - आधिकारिक नमूने

---

**अस्वीकरण**:  
यह दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) का उपयोग करके अनुवादित किया गया है। जबकि हम सटीकता सुनिश्चित करने का प्रयास करते हैं, कृपया ध्यान दें कि स्वचालित अनुवाद में त्रुटियां या अशुद्धियां हो सकती हैं। मूल भाषा में उपलब्ध मूल दस्तावेज़ को प्रामाणिक स्रोत माना जाना चाहिए। महत्वपूर्ण जानकारी के लिए, पेशेवर मानव अनुवाद की सिफारिश की जाती है। इस अनुवाद के उपयोग से उत्पन्न किसी भी गलतफहमी या गलत व्याख्या के लिए हम उत्तरदायी नहीं हैं।