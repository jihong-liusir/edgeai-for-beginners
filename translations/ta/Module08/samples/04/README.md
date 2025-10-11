<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "2f1754a482b6a84e07287a5b775e65b6",
  "translation_date": "2025-10-11T12:57:49+00:00",
  "source_file": "Module08/samples/04/README.md",
  "language_code": "ta"
}
-->
# மாதிரி 04: Chainlit மூலம் உற்பத்தி தரமான உரையாடல் பயன்பாடுகள்

Microsoft Foundry Local பயன்படுத்தி உற்பத்தி தரமான உரையாடல் பயன்பாடுகளை உருவாக்க பல்வேறு அணுகுமுறைகளை விளக்கும் முழுமையான மாதிரி. இதில் நவீன வலை இடைமுகங்கள், ஸ்ட்ரீமிங் பதில்கள் மற்றும் முன்னணி உலாவி தொழில்நுட்பங்கள் அடங்கும்.

## உள்ளடக்கம்

- **🚀 Chainlit Chat App** (`app.py`): ஸ்ட்ரீமிங் கொண்ட உற்பத்தி தரமான உரையாடல் பயன்பாடு
- **🌐 WebGPU டெமோ** (`webgpu-demo/`): உலாவி அடிப்படையிலான AI முடிவெடுப்பு, ஹார்ட்வேரின் வேகத்தை அதிகரிக்கும்
- **🎨 Open WebUI ஒருங்கிணைப்பு** (`open-webui-guide.md`): தொழில்முறை ChatGPT போன்ற இடைமுகம்
- **📚 கல்வி நோட்புக்** (`chainlit_app.ipynb`): இடைமுகக் கற்றல் பொருட்கள்

## விரைவான தொடக்கம்

### 1. Chainlit உரையாடல் பயன்பாடு

```cmd
# Navigate to Module08 directory
cd Module08

# Start your model
foundry model run phi-4-mini

# Run Chainlit app (using port 8080 to avoid conflicts)
chainlit run samples\04\app.py -w --port 8080
```

திறக்கப்படும் இடம்: `http://localhost:8080`

### 2. WebGPU உலாவி டெமோ

```cmd
# Navigate to WebGPU demo
cd Module08\samples\04\webgpu-demo

# Serve the demo
python -m http.server 5173
```

திறக்கப்படும் இடம்: `http://localhost:5173`

### 3. Open WebUI அமைப்பு

```cmd
# Run Open WebUI with Docker
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```

திறக்கப்படும் இடம்: `http://localhost:3000`

## கட்டமைப்பு முறை

### உள்ளூர் vs கிளவுட் முடிவு அட்டவணை

| சூழல் | பரிந்துரை | காரணம் |
|-------|-----------|--------|
| **தனியுரிமை-முக்கியமான தரவுகள்** | 🏠 உள்ளூர் (Foundry) | தரவுகள் சாதனத்தை விட்டு வெளியே செல்லாது |
| **சிக்கலான காரணங்கள்** | ☁️ கிளவுட் (Azure OpenAI) | பெரிய மாதிரிகளுக்கான அணுகல் |
| **நேரடி உரையாடல்** | 🏠 உள்ளூர் (Foundry) | குறைந்த தாமதம், வேகமான பதில்கள் |
| **ஆவண பகுப்பாய்வு** | 🔄 கலப்பு | எடுக்கும் பணிக்கு உள்ளூர், பகுப்பாய்வுக்கு கிளவுட் |
| **கோடு உருவாக்கம்** | 🏠 உள்ளூர் (Foundry) | தனியுரிமை + சிறப்பு மாதிரிகள் |
| **ஆராய்ச்சி பணிகள்** | ☁️ கிளவுட் (Azure OpenAI) | பரந்த அறிவு அடிப்படை தேவை |

### தொழில்நுட்ப ஒப்பீடு

| தொழில்நுட்பம் | பயன்பாட்டு வழக்கு | நன்மைகள் | குறைகள் |
|---------------|------------------|----------|---------|
| **Chainlit** | Python டெவலப்பர்கள், விரைவான மாதிரி உருவாக்கம் | எளிய அமைப்பு, ஸ்ட்ரீமிங் ஆதரவு | Python மட்டும் |
| **WebGPU** | அதிகபட்ச தனியுரிமை, ஆஃப்லைன் சூழல்கள் | உலாவி-இயல்பானது, சர்வர் தேவையில்லை | வரையறுக்கப்பட்ட மாதிரி அளவு |
| **Open WebUI** | உற்பத்தி பயன்பாடு, குழுக்கள் | தொழில்முறை UI, பயனர் மேலாண்மை | Docker தேவை |

## முன் தேவைகள்

- **Foundry Local**: நிறுவப்பட்டு இயங்கும் நிலையில் ([Download](https://aka.ms/foundry-local-installer))
- **Python**: 3.10+ மற்றும் மெய்நிகர் சூழல்
- **மாதிரி**: குறைந்தது ஒன்று ஏற்றப்பட்ட (`foundry model run phi-4-mini`)
- **உலாவி**: Chrome/Edge WebGPU ஆதரவு கொண்டது
- **Docker**: Open WebUI க்கானது (விருப்பம்)

## நிறுவல் மற்றும் அமைப்பு

### 1. Python சூழல் அமைப்பு

```cmd
# Navigate to Module08 directory
cd Module08

# Create and activate virtual environment
py -m venv .venv
.venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### 2. Foundry Local அமைப்பு

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

## மாதிரி பயன்பாடுகள்

### Chainlit உரையாடல் பயன்பாடு

**அம்சங்கள்:**
- 🚀 **நேரடி ஸ்ட்ரீமிங்**: உருவாக்கப்படும் போது டோக்கன்கள் தோன்றும்
- 🛡️ **வலுவான பிழை கையாளுதல்**: சீரழிவு மற்றும் மீட்பு
- 🎨 **நவீன UI**: தொழில்முறை உரையாடல் இடைமுகம்
- 🔧 **நெகிழ்வான கட்டமைப்பு**: சூழல் மாறிகள் மற்றும் தானியங்கி கண்டறிதல்
- 📱 **பதிலளிக்கும் வடிவமைப்பு**: டெஸ்க்டாப் மற்றும் மொபைல் சாதனங்களில் வேலை செய்கிறது

**விரைவான தொடக்கம்:**
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

### WebGPU உலாவி டெமோ

**அம்சங்கள்:**
- 🌐 **உலாவி-இயல்பான AI**: சர்வர் தேவையில்லை, முழுவதும் உலாவியில் இயங்குகிறது
- ⚡ **WebGPU வேகத்தை அதிகரித்தல்**: ஹார்ட்வேரின் வேகத்தை அதிகரிக்கும்
- 🔒 **அதிகபட்ச தனியுரிமை**: தரவுகள் சாதனத்தை விட்டு வெளியே செல்லாது
- 🎯 **ப صفر நிறுவல்**: எந்த இணக்கமான உலாவியிலும் வேலை செய்கிறது
- 🔄 **சீரான மாற்று**: WebGPU கிடைக்காதால் CPU க்கு மாறுகிறது

**இயக்குதல்:**
```cmd
cd samples\04\webgpu-demo
python -m http.server 5173
# Open http://localhost:5173
```

### Open WebUI ஒருங்கிணைப்பு

**அம்சங்கள்:**
- 🎨 **ChatGPT போன்ற இடைமுகம்**: தொழில்முறை, பரிச்சயமான UI
- 👥 **பல பயனர் ஆதரவு**: பயனர் கணக்குகள் மற்றும் உரையாடல் வரலாறு
- 📁 **கோப்பு செயலாக்கம்**: கோப்புகளை பதிவேற்றம் செய்து பகுப்பாய்வு செய்யுங்கள்
- 🔄 **மாதிரி மாற்றம்**: வெவ்வேறு மாதிரிகளுக்கு இடையே எளிதாக மாறுதல்
- 🐳 **Docker அமைப்பு**: உற்பத்தி தரமான கெண்டைனர் அமைப்பு

**விரைவான அமைப்பு:**
```cmd
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```

## கட்டமைப்பு குறிப்புகள்

### சூழல் மாறிகள்

| மாறி | விளக்கம் | இயல்புநிலை | உதாரணம் |
|------|----------|------------|----------|
| `MODEL` | பயன்படுத்த வேண்டிய மாதிரி பெயர் | `phi-4-mini` | `qwen2.5-7b` |
| `BASE_URL` | Foundry Local முடிவெடுப்பு | தானாக கண்டறியப்படும் | `http://localhost:51211` |
| `API_KEY` | API விசை (உள்ளூருக்கு விருப்பம்) | `""` | `your-api-key` |

## பிழை தீர்வு

### பொதுவான பிரச்சினைகள்

**Chainlit பயன்பாடு:**

1. **சேவை கிடைக்கவில்லை:**
   ```cmd
   # Check Foundry Local status
   foundry service status
   foundry service ps
   
   # Validate API endpoint (note: port 51211)
   curl http://localhost:51211/v1/models
   ```

2. **போர்ட் மோதல்கள்:**
   ```cmd
   # Check what's using port 8080
   netstat -ano | findstr :8080
   
   # Use different port if needed
   chainlit run samples\04\app.py -w --port 3000
   ```

3. **Python சூழல் பிரச்சினைகள்:**
   ```cmd
   # Verify correct interpreter in VS Code
   # Ctrl+Shift+P → Python: Select Interpreter
   # Choose: Module08/.venv/Scripts/python.exe
   
   # Reinstall dependencies
   pip install -r requirements.txt
   ```

**WebGPU டெமோ:**

1. **WebGPU ஆதரவு இல்லை:**
   - Chrome/Edge 113+ க்கு மேம்படுத்தவும்
   - WebGPU ஐ இயக்கவும்: `chrome://flags/#enable-unsafe-webgpu`
   - GPU நிலையை சரிபார்க்கவும்: `chrome://gpu`
   - டெமோ தானாக CPU க்கு மாறும்

2. **மாதிரி ஏற்றுதல் பிழைகள்:**
   - மாதிரி பதிவிறக்கத்திற்கான இணைய இணைப்பு உறுதிப்படுத்தவும்
   - உலாவி கன்சோலில் CORS பிழைகளை சரிபார்க்கவும்
   - HTTP மூலம் சேவை செய்கிறீர்கள் என்பதை உறுதிப்படுத்தவும் (file:// அல்ல)

**Open WebUI:**

1. **இணைப்பு மறுக்கப்பட்டது:**
   ```cmd
   # Check Docker is running
   docker --version
   
   # Check container status
   docker ps | findstr open-webui
   
   # View container logs
   docker logs open-webui
   ```

2. **மாதிரிகள் தோன்றவில்லை:**
   ```cmd
   # Verify Foundry Local endpoint
   curl http://localhost:51211/v1/models
   
   # Restart Open WebUI
   docker restart open-webui
   ```

### சரிபார்ப்பு சோதனை பட்டியல்

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

## மேம்பட்ட பயன்பாடு

### செயல்திறன் மேம்பாடு

**Chainlit:**
- perceived performance ஐ மேம்படுத்த ஸ்ட்ரீமிங் பயன்படுத்தவும்
- அதிக இணக்கத்திற்கான இணைப்பு குளங்களை செயல்படுத்தவும்
- மீண்டும் மீண்டும் கேள்விகளுக்கு மாதிரி பதில்களை சேமிக்கவும்
- பெரிய உரையாடல் வரலாற்றுடன் நினைவக பயன்பாட்டை கண்காணிக்கவும்

**WebGPU:**
- அதிகபட்ச தனியுரிமை மற்றும் வேகத்திற்காக WebGPU ஐ பயன்படுத்தவும்
- சிறிய மாதிரிகளுக்காக மாதிரி அளவீட்டை செயல்படுத்தவும்
- பின்னணி செயலாக்கத்திற்காக Web Workers ஐ பயன்படுத்தவும்
- உலாவி சேமிப்பகத்தில் தொகுக்கப்பட்ட மாதிரிகளை சேமிக்கவும்

**Open WebUI:**
- உரையாடல் வரலாற்றிற்காக நிலையான தொகுதிகளை பயன்படுத்தவும்
- Docker கெண்டைனருக்கான வள வரம்புகளை அமைக்கவும்
- பயனர் தரவிற்கான காப்பு உத்திகளை செயல்படுத்தவும்
- SSL முடிவுக்கு ரிவர்ஸ் ப்ராக்ஸி அமைக்கவும்

### ஒருங்கிணைப்பு முறை

**கலப்பு உள்ளூர்/கிளவுட்:**
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

**பலவகை முறைமைகள்:**
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

## உற்பத்தி அமைப்பு

### பாதுகாப்பு கருத்துக்கள்

- **API விசைகள்**: சூழல் மாறிகளை பயன்படுத்தவும், நேரடியாக குறியாக்க வேண்டாம்
- **நெட்வொர்க்**: உற்பத்தியில் HTTPS ஐ பயன்படுத்தவும், குழு அணுகலுக்கான VPN ஐ பரிசீலிக்கவும்
- **அணுகல் கட்டுப்பாடு**: Open WebUI க்கான அங்கீகாரத்தை செயல்படுத்தவும்
- **தரவு தனியுரிமை**: உள்ளூர் மற்றும் கிளவுட் தரவுகளை ஆய்வு செய்யவும்
- **மேம்படுத்தல்கள்**: Foundry Local மற்றும் கெண்டைனர்களை புதுப்பித்து வைத்திருக்கவும்

### கண்காணிப்பு மற்றும் பராமரிப்பு

- **ஆரோக்கிய சோதனைகள்**: முடிவெடுப்பு கண்காணிப்பை செயல்படுத்தவும்
- **பதிவுகள்**: அனைத்து கூறுகளிலிருந்து பதிவுகளை மையமாக்கவும்
- **அளவீடுகள்**: பதில் நேரங்கள், பிழை விகிதங்கள், வள பயன்பாட்டை கண்காணிக்கவும்
- **காப்பு**: உரையாடல் தரவுகள் மற்றும் கட்டமைப்புகளின் வழக்கமான காப்பு

## குறிப்புகள் மற்றும் வளங்கள்

### ஆவணங்கள்
- [Chainlit ஆவணங்கள்](https://docs.chainlit.io/) - முழுமையான கட்டமைப்பு வழிகாட்டி
- [Foundry Local ஆவணங்கள்](https://learn.microsoft.com/azure/ai-foundry/foundry-local/) - Microsoft அதிகாரப்பூர்வ ஆவணங்கள்
- [ONNX Runtime Web](https://onnxruntime.ai/docs/get-started/with-javascript/web.html) - WebGPU ஒருங்கிணைப்பு
- [Open WebUI ஆவணங்கள்](https://docs.openwebui.com/) - மேம்பட்ட கட்டமைப்பு

### மாதிரி கோப்புகள்
- [`app.py`](../../../../../Module08/samples/04/app.py) - உற்பத்தி Chainlit பயன்பாடு
- [`chainlit_app.ipynb`](./chainlit_app.ipynb) - கல்வி நோட்புக்
- [`webgpu-demo/`](../../../../../Module08/samples/04/webgpu-demo) - உலாவி அடிப்படையிலான AI முடிவெடுப்பு
- [`open-webui-guide.md`](./open-webui-guide.md) - முழுமையான Open WebUI அமைப்பு

### தொடர்புடைய மாதிரிகள்
- [அமர்வு 4 ஆவணங்கள்](../../04.CuttingEdgeModels.md) - முழுமையான அமர்வு வழிகாட்டி
- [Foundry Local மாதிரிகள்](https://github.com/microsoft/foundry-local/tree/main/samples) - அதிகாரப்பூர்வ மாதிரிகள்

---

**குறிப்பு**:  
இந்த ஆவணம் [Co-op Translator](https://github.com/Azure/co-op-translator) என்ற AI மொழிபெயர்ப்பு சேவையைப் பயன்படுத்தி மொழிபெயர்க்கப்பட்டுள்ளது. நாங்கள் துல்லியத்திற்காக முயற்சிக்கிறோம், ஆனால் தானியங்கி மொழிபெயர்ப்புகளில் பிழைகள் அல்லது தவறான தகவல்கள் இருக்கக்கூடும் என்பதை தயவுசெய்து கவனத்தில் கொள்ளுங்கள். அதன் தாய்மொழியில் உள்ள மூல ஆவணம் அதிகாரப்பூர்வ ஆதாரமாக கருதப்பட வேண்டும். முக்கியமான தகவல்களுக்கு, தொழில்முறை மனித மொழிபெயர்ப்பு பரிந்துரைக்கப்படுகிறது. இந்த மொழிபெயர்ப்பைப் பயன்படுத்துவதால் ஏற்படும் எந்த தவறான புரிதல்கள் அல்லது தவறான விளக்கங்களுக்கு நாங்கள் பொறுப்பல்ல.