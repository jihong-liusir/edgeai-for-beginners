<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "562ac0eae12d808c9f45fbb77eb5c84f",
  "translation_date": "2025-09-24T21:12:55+00:00",
  "source_file": "Module08/samples/04/README.md",
  "language_code": "pa"
}
-->
# Sample 04: ਪ੍ਰੋਡਕਸ਼ਨ ਚੈਟ ਐਪਲੀਕੇਸ਼ਨਜ਼ ਚੇਨਲਿਟ ਨਾਲ

ਇਹ ਇੱਕ ਵਿਸਤ੍ਰਿਤ ਨਮੂਨਾ ਹੈ ਜੋ ਮਾਈਕਰੋਸਾਫਟ ਫਾਊਂਡਰੀ ਲੋਕਲ ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਪ੍ਰੋਡਕਸ਼ਨ-ਤਿਆਰ ਚੈਟ ਐਪਲੀਕੇਸ਼ਨ ਬਣਾਉਣ ਦੇ ਕਈ ਤਰੀਕੇ ਦਿਖਾਉਂਦਾ ਹੈ, ਜਿਸ ਵਿੱਚ ਆਧੁਨਿਕ ਵੈੱਬ ਇੰਟਰਫੇਸ, ਸਟ੍ਰੀਮਿੰਗ ਜਵਾਬ, ਅਤੇ ਅਗਲੇ ਪੱਧਰ ਦੀ ਬ੍ਰਾਊਜ਼ਰ ਤਕਨਾਲੋਜੀ ਸ਼ਾਮਲ ਹੈ।

## ਕੀ ਸ਼ਾਮਲ ਹੈ

- **🚀 ਚੇਨਲਿਟ ਚੈਟ ਐਪ** (`app.py`): ਸਟ੍ਰੀਮਿੰਗ ਨਾਲ ਪ੍ਰੋਡਕਸ਼ਨ-ਤਿਆਰ ਚੈਟ ਐਪਲੀਕੇਸ਼ਨ
- **🌐 ਵੈੱਬGPU ਡੈਮੋ** (`webgpu-demo/`): ਹਾਰਡਵੇਅਰ ਐਕਸਲੇਰੇਸ਼ਨ ਨਾਲ ਬ੍ਰਾਊਜ਼ਰ-ਅਧਾਰਿਤ AI ਇੰਫਰੈਂਸ
- **🎨 ਓਪਨ ਵੈੱਬUI ਇੰਟੀਗ੍ਰੇਸ਼ਨ** (`open-webui-guide.md`): ਪ੍ਰੋਫੈਸ਼ਨਲ ChatGPT-ਜਿਵੇਂ ਇੰਟਰਫੇਸ
- **📚 ਸਿੱਖਣ ਲਈ ਨੋਟਬੁੱਕ** (`chainlit_app.ipynb`): ਇੰਟਰਐਕਟਿਵ ਸਿੱਖਣ ਸਮੱਗਰੀ

## ਤੁਰੰਤ ਸ਼ੁਰੂਆਤ

### 1. ਚੇਨਲਿਟ ਚੈਟ ਐਪਲੀਕੇਸ਼ਨ

```cmd
# Navigate to Module08 directory
cd Module08

# Start your model
foundry model run phi-4-mini

# Run Chainlit app (using port 8080 to avoid conflicts)
chainlit run samples\04\app.py -w --port 8080
```
  
ਖੁਲਦਾ ਹੈ: `http://localhost:8080`

### 2. ਵੈੱਬGPU ਬ੍ਰਾਊਜ਼ਰ ਡੈਮੋ

```cmd
# Navigate to WebGPU demo
cd Module08\samples\04\webgpu-demo

# Serve the demo
python -m http.server 5173
```
  
ਖੁਲਦਾ ਹੈ: `http://localhost:5173`

### 3. ਓਪਨ ਵੈੱਬUI ਸੈਟਅਪ

```cmd
# Run Open WebUI with Docker
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```
  
ਖੁਲਦਾ ਹੈ: `http://localhost:3000`

## ਆਰਕੀਟੈਕਚਰ ਪੈਟਰਨ

### ਲੋਕਲ ਵਿਰੁੱਧ ਕਲਾਉਡ ਫੈਸਲਾ ਮੈਟ੍ਰਿਕਸ

| ਸਥਿਤੀ | ਸਿਫਾਰਸ਼ | ਕਾਰਨ |
|--------|----------|------|
| **ਗੋਪਨੀਯਤਾ-ਸੰਵੇਦਨਸ਼ੀਲ ਡਾਟਾ** | 🏠 ਲੋਕਲ (Foundry) | ਡਾਟਾ ਕਦੇ ਵੀ ਡਿਵਾਈਸ ਤੋਂ ਬਾਹਰ ਨਹੀਂ ਜਾਂਦਾ |
| **ਜਟਿਲ ਤਰਕ** | ☁️ ਕਲਾਉਡ (Azure OpenAI) | ਵੱਡੇ ਮਾਡਲਾਂ ਤੱਕ ਪਹੁੰਚ |
| **ਰਿਅਲ-ਟਾਈਮ ਚੈਟ** | 🏠 ਲੋਕਲ (Foundry) | ਘੱਟ ਲੈਟੈਂਸੀ, ਤੇਜ਼ ਜਵਾਬ |
| **ਦਸਤਾਵੇਜ਼ ਵਿਸ਼ਲੇਸ਼ਣ** | 🔄 ਹਾਈਬ੍ਰਿਡ | ਨਿਕਾਲਣ ਲਈ ਲੋਕਲ, ਵਿਸ਼ਲੇਸ਼ਣ ਲਈ ਕਲਾਉਡ |
| **ਕੋਡ ਜਨਰੇਸ਼ਨ** | 🏠 ਲੋਕਲ (Foundry) | ਗੋਪਨੀਯਤਾ + ਵਿਸ਼ੇਸ਼ ਮਾਡਲ |
| **ਗਵਾਚੀ ਕਾਰਜ** | ☁️ ਕਲਾਉਡ (Azure OpenAI) | ਵਿਸ਼ਾਲ ਗਿਆਨ ਅਧਾਰ ਦੀ ਲੋੜ |

### ਤਕਨਾਲੋਜੀ ਤੁਲਨਾ

| ਤਕਨਾਲੋਜੀ | ਵਰਤੋਂ ਦਾ ਕੇਸ | ਫਾਇਦੇ | ਨੁਕਸਾਨ |
|----------|--------------|-------|--------|
| **ਚੇਨਲਿਟ** | ਪਾਇਥਨ ਡਿਵੈਲਪਰ, ਤੇਜ਼ ਪ੍ਰੋਟੋਟਾਈਪਿੰਗ | ਆਸਾਨ ਸੈਟਅਪ, ਸਟ੍ਰੀਮਿੰਗ ਸਹਾਇਤਾ | ਸਿਰਫ ਪਾਇਥਨ |
| **ਵੈੱਬGPU** | ਵੱਧ ਤੋਂ ਵੱਧ ਗੋਪਨੀਯਤਾ, ਆਫਲਾਈਨ ਸਥਿਤੀਆਂ | ਬ੍ਰਾਊਜ਼ਰ-ਮੂਲ, ਸਰਵਰ ਦੀ ਲੋੜ ਨਹੀਂ | ਸੀਮਤ ਮਾਡਲ ਆਕਾਰ |
| **ਓਪਨ ਵੈੱਬUI** | ਪ੍ਰੋਡਕਸ਼ਨ ਡਿਪਲੌਇਮੈਂਟ, ਟੀਮਾਂ | ਪ੍ਰੋਫੈਸ਼ਨਲ UI, ਯੂਜ਼ਰ ਮੈਨੇਜਮੈਂਟ | ਡੌਕਰ ਦੀ ਲੋੜ |

## ਪੂਰਵ ਸ਼ਰਤਾਂ

- **Foundry Local**: ਇੰਸਟਾਲ ਅਤੇ ਚਲ ਰਿਹਾ ([Download](https://aka.ms/foundry-local-installer))
- **Python**: 3.10+ ਨਾਲ ਵਰਚੁਅਲ ਐਨਵਾਇਰਮੈਂਟ
- **ਮਾਡਲ**: ਘੱਟੋ-ਘੱਟ ਇੱਕ ਲੋਡ ਕੀਤਾ (`foundry model run phi-4-mini`)
- **ਬ੍ਰਾਊਜ਼ਰ**: Chrome/Edge ਨਾਲ WebGPU ਸਹਾਇਤਾ ਲਈ ਡੈਮੋ
- **Docker**: ਓਪਨ ਵੈੱਬUI ਲਈ (ਵਿਕਲਪਿਕ)

## ਇੰਸਟਾਲੇਸ਼ਨ ਅਤੇ ਸੈਟਅਪ

### 1. ਪਾਇਥਨ ਐਨਵਾਇਰਮੈਂਟ ਸੈਟਅਪ

```cmd
# Navigate to Module08 directory
cd Module08

# Create and activate virtual environment
py -m venv .venv
.venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```
  
### 2. Foundry Local ਸੈਟਅਪ

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
  
## ਨਮੂਨਾ ਐਪਲੀਕੇਸ਼ਨ

### ਚੇਨਲਿਟ ਚੈਟ ਐਪਲੀਕੇਸ਼ਨ

**ਵਿਸ਼ੇਸ਼ਤਾਵਾਂ:**
- 🚀 **ਰਿਅਲ-ਟਾਈਮ ਸਟ੍ਰੀਮਿੰਗ**: ਟੋਕਨ ਜਿਵੇਂ ਹੀ ਜਨਰੇਟ ਹੁੰਦੇ ਹਨ, ਦਿਖਾਈ ਦਿੰਦੇ ਹਨ
- 🛡️ **ਮਜ਼ਬੂਤ ਗਲਤੀ ਸੰਭਾਲ**: ਗ੍ਰੇਸਫੁਲ ਡਿਗਰੇਡੇਸ਼ਨ ਅਤੇ ਰਿਕਵਰੀ
- 🎨 **ਆਧੁਨਿਕ UI**: ਬਾਕਸ ਤੋਂ ਬਾਹਰ ਪ੍ਰੋਫੈਸ਼ਨਲ ਚੈਟ ਇੰਟਰਫੇਸ
- 🔧 **ਲਚਕਦਾਰ ਸੰਰਚਨਾ**: ਵਾਤਾਵਰਣ ਚਰ ਅਤੇ ਆਟੋ-ਡਿਟੈਕਸ਼ਨ
- 📱 **ਰਿਸਪਾਂਸਿਵ ਡਿਜ਼ਾਈਨ**: ਡੈਸਕਟਾਪ ਅਤੇ ਮੋਬਾਈਲ ਡਿਵਾਈਸਾਂ 'ਤੇ ਕੰਮ ਕਰਦਾ ਹੈ

**ਤੁਰੰਤ ਸ਼ੁਰੂਆਤ:**
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
  
### ਵੈੱਬGPU ਬ੍ਰਾਊਜ਼ਰ ਡੈਮੋ

**ਵਿਸ਼ੇਸ਼ਤਾਵਾਂ:**
- 🌐 **ਬ੍ਰਾਊਜ਼ਰ-ਮੂਲ AI**: ਕੋਈ ਸਰਵਰ ਦੀ ਲੋੜ ਨਹੀਂ, ਪੂਰੀ ਤਰ੍ਹਾਂ ਬ੍ਰਾਊਜ਼ਰ ਵਿੱਚ ਚਲਦਾ ਹੈ
- ⚡ **ਵੈੱਬGPU ਐਕਸਲੇਰੇਸ਼ਨ**: ਜਿੱਥੇ ਉਪਲਬਧ ਹੋਵੇ, ਹਾਰਡਵੇਅਰ ਐਕਸਲੇਰੇਸ਼ਨ
- 🔒 **ਵੱਧ ਤੋਂ ਵੱਧ ਗੋਪਨੀਯਤਾ**: ਡਾਟਾ ਕਦੇ ਵੀ ਤੁਹਾਡੇ ਡਿਵਾਈਸ ਤੋਂ ਬਾਹਰ ਨਹੀਂ ਜਾਂਦਾ
- 🎯 **ਜ਼ੀਰੋ ਇੰਸਟਾਲ**: ਕਿਸੇ ਵੀ ਅਨੁਕੂਲ ਬ੍ਰਾਊਜ਼ਰ ਵਿੱਚ ਕੰਮ ਕਰਦਾ ਹੈ
- 🔄 **ਗ੍ਰੇਸਫੁਲ ਫਾਲਬੈਕ**: ਜੇ WebGPU ਉਪਲਬਧ ਨਹੀਂ, ਤਾਂ CPU 'ਤੇ ਵਾਪਸ ਆ ਜਾਂਦਾ ਹੈ

**ਚਲਾਉਣਾ:**
```cmd
cd samples\04\webgpu-demo
python -m http.server 5173
# Open http://localhost:5173
```
  
### ਓਪਨ ਵੈੱਬUI ਇੰਟੀਗ੍ਰੇਸ਼ਨ

**ਵਿਸ਼ੇਸ਼ਤਾਵਾਂ:**
- 🎨 **ChatGPT-ਜਿਵੇਂ ਇੰਟਰਫੇਸ**: ਪ੍ਰੋਫੈਸ਼ਨਲ, ਜਾਣ-ਪਛਾਣ ਵਾਲਾ UI
- 👥 **ਮਲਟੀ-ਯੂਜ਼ਰ ਸਹਾਇਤਾ**: ਯੂਜ਼ਰ ਅਕਾਊਂਟ ਅਤੇ ਗੱਲਬਾਤ ਦਾ ਇਤਿਹਾਸ
- 📁 **ਫਾਈਲ ਪ੍ਰੋਸੈਸਿੰਗ**: ਦਸਤਾਵੇਜ਼ ਅਪਲੋਡ ਅਤੇ ਵਿਸ਼ਲੇਸ਼ਣ
- 🔄 **ਮਾਡਲ ਸਵਿੱਚਿੰਗ**: ਵੱਖ-ਵੱਖ ਮਾਡਲਾਂ ਦੇ ਵਿਚਕਾਰ ਆਸਾਨ ਸਵਿੱਚਿੰਗ
- 🐳 **ਡੌਕਰ ਡਿਪਲੌਇਮੈਂਟ**: ਪ੍ਰੋਡਕਸ਼ਨ-ਤਿਆਰ ਕੰਟੇਨਰਾਈਜ਼ਡ ਸੈਟਅਪ

**ਤੁਰੰਤ ਸੈਟਅਪ:**
```cmd
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```
  
## ਸੰਰਚਨਾ ਸੰਦਰਭ

### ਵਾਤਾਵਰਣ ਚਰ

| ਚਰ | ਵੇਰਵਾ | ਡਿਫਾਲਟ | ਉਦਾਹਰਨ |
|----|-------|---------|---------|
| `MODEL` | ਵਰਤਣ ਲਈ ਮਾਡਲ ਉਪਨਾਮ | `phi-4-mini` | `qwen2.5-7b-instruct` |
| `BASE_URL` | Foundry Local ਐਂਡਪੌਇੰਟ | ਆਟੋ-ਡਿਟੈਕਟ ਕੀਤਾ | `http://localhost:51211` |
| `API_KEY` | API ਕੁੰਜੀ (ਲੋਕਲ ਲਈ ਵਿਕਲਪਿਕ) | `""` | `your-api-key` |

## ਸਮੱਸਿਆ ਹੱਲ

### ਆਮ ਸਮੱਸਿਆਵਾਂ

**ਚੇਨਲਿਟ ਐਪਲੀਕੇਸ਼ਨ:**

1. **ਸੇਵਾ ਉਪਲਬਧ ਨਹੀਂ:**
   ```cmd
   # Check Foundry Local status
   foundry service status
   foundry service ps
   
   # Validate API endpoint (note: port 51211)
   curl http://localhost:51211/v1/models
   ```
  
2. **ਪੋਰਟ ਸੰਘਰਸ਼:**
   ```cmd
   # Check what's using port 8080
   netstat -ano | findstr :8080
   
   # Use different port if needed
   chainlit run samples\04\app.py -w --port 3000
   ```
  
3. **ਪਾਇਥਨ ਐਨਵਾਇਰਮੈਂਟ ਸਮੱਸਿਆਵਾਂ:**
   ```cmd
   # Verify correct interpreter in VS Code
   # Ctrl+Shift+P → Python: Select Interpreter
   # Choose: Module08/.venv/Scripts/python.exe
   
   # Reinstall dependencies
   pip install -r requirements.txt
   ```
  
**ਵੈੱਬGPU ਡੈਮੋ:**

1. **ਵੈੱਬGPU ਸਹਾਇਤਾ ਨਹੀਂ:**
   - Chrome/Edge 113+ 'ਤੇ ਅਪਡੇਟ ਕਰੋ
   - WebGPU ਐਨੇਬਲ ਕਰੋ: `chrome://flags/#enable-unsafe-webgpu`
   - GPU ਸਥਿਤੀ ਚੈੱਕ ਕਰੋ: `chrome://gpu`
   - ਡੈਮੋ ਆਪਣੇ ਆਪ CPU 'ਤੇ ਵਾਪਸ ਆ ਜਾਵੇਗਾ

2. **ਮਾਡਲ ਲੋਡ ਕਰਨ ਦੀਆਂ ਗਲਤੀਆਂ:**
   - ਮਾਡਲ ਡਾਊਨਲੋਡ ਲਈ ਇੰਟਰਨੈਟ ਕਨੈਕਸ਼ਨ ਯਕੀਨੀ ਬਣਾਓ
   - ਬ੍ਰਾਊਜ਼ਰ ਕਨਸੋਲ ਵਿੱਚ CORS ਗਲਤੀਆਂ ਚੈੱਕ ਕਰੋ
   - ਯਕੀਨੀ ਬਣਾਓ ਕਿ ਤੁਸੀਂ HTTP ਦੁਆਰਾ ਸਰਵ ਕਰ ਰਹੇ ਹੋ (file:// ਨਹੀਂ)

**ਓਪਨ ਵੈੱਬUI:**

1. **ਕਨੈਕਸ਼ਨ ਰਿਫਿਊਜ਼ਡ:**
   ```cmd
   # Check Docker is running
   docker --version
   
   # Check container status
   docker ps | findstr open-webui
   
   # View container logs
   docker logs open-webui
   ```
  
2. **ਮਾਡਲ ਪ੍ਰਗਟ ਨਹੀਂ ਹੋ ਰਹੇ:**
   ```cmd
   # Verify Foundry Local endpoint
   curl http://localhost:51211/v1/models
   
   # Restart Open WebUI
   docker restart open-webui
   ```
  
### ਵੈਧਤਾ ਚੈੱਕਲਿਸਟ

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
  
## ਅਗਲੇ ਪੱਧਰ ਦੀ ਵਰਤੋਂ

### ਪ੍ਰਦਰਸ਼ਨ ਅਪਟਿਮਾਈਜ਼ੇਸ਼ਨ

**ਚੇਨਲਿਟ:**
- ਵਧੀਆ ਪ੍ਰਦਰਸ਼ਨ ਲਈ ਸਟ੍ਰੀਮਿੰਗ ਦੀ ਵਰਤੋਂ ਕਰੋ
- ਉੱਚ ਸਮਕਾਲੀਤਾ ਲਈ ਕਨੈਕਸ਼ਨ ਪੂਲਿੰਗ ਲਾਗੂ ਕਰੋ
- ਦੁਹਰਾਏ ਗਏ ਪ੍ਰਸ਼ਨਾਂ ਲਈ ਮਾਡਲ ਜਵਾਬਾਂ ਕੈਸ਼ ਕਰੋ
- ਵੱਡੇ ਗੱਲਬਾਤ ਇਤਿਹਾਸਾਂ ਨਾਲ ਮੈਮਰੀ ਦੀ ਵਰਤੋਂ ਦੀ ਨਿਗਰਾਨੀ ਕਰੋ

**ਵੈੱਬGPU:**
- ਵੱਧ ਤੋਂ ਵੱਧ ਗੋਪਨੀਯਤਾ ਅਤੇ ਗਤੀ ਲਈ WebGPU ਦੀ ਵਰਤੋਂ ਕਰੋ
- ਛੋਟੇ ਮਾਡਲਾਂ ਲਈ ਮਾਡਲ ਕੁਆੰਟਾਈਜ਼ੇਸ਼ਨ ਲਾਗੂ ਕਰੋ
- ਬੈਕਗ੍ਰਾਊਂਡ ਪ੍ਰੋਸੈਸਿੰਗ ਲਈ Web Workers ਦੀ ਵਰਤੋਂ ਕਰੋ
- ਬ੍ਰਾਊਜ਼ਰ ਸਟੋਰੇਜ ਵਿੱਚ ਕੈਸ਼ ਕੀਤੇ ਮਾਡਲਾਂ ਨੂੰ ਸੰਭਾਲੋ

**ਓਪਨ ਵੈੱਬUI:**
- ਗੱਲਬਾਤ ਇਤਿਹਾਸ ਲਈ ਸਥਾਈ ਵਾਲਿਊਮ ਦੀ ਵਰਤੋਂ ਕਰੋ
- ਡੌਕਰ ਕੰਟੇਨਰ ਲਈ ਸਰੋਤ ਸੀਮਾਵਾਂ ਸੰਰਚਿਤ ਕਰੋ
- ਯੂਜ਼ਰ ਡਾਟਾ ਲਈ ਬੈਕਅਪ ਰਣਨੀਤੀਆਂ ਲਾਗੂ ਕਰੋ
- SSL ਟਰਮੀਨੇਸ਼ਨ ਲਈ ਰਿਵਰਸ ਪ੍ਰੌਕਸੀ ਸੈਟਅਪ ਕਰੋ

### ਇੰਟੀਗ੍ਰੇਸ਼ਨ ਪੈਟਰਨ

**ਹਾਈਬ੍ਰਿਡ ਲੋਕਲ/ਕਲਾਉਡ:**
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
  
**ਮਲਟੀ-ਮੋਡਲ ਪਾਈਪਲਾਈਨ:**
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
  
## ਪ੍ਰੋਡਕਸ਼ਨ ਡਿਪਲੌਇਮੈਂਟ

### ਸੁਰੱਖਿਆ ਵਿਚਾਰ

- **API ਕੁੰਜੀਆਂ**: ਵਾਤਾਵਰਣ ਚਰ ਦੀ ਵਰਤੋਂ ਕਰੋ, ਕਦੇ ਵੀ ਹਾਰਡਕੋਡ ਨਾ ਕਰੋ
- **ਨੈਟਵਰਕ**: ਪ੍ਰੋਡਕਸ਼ਨ ਵਿੱਚ HTTPS ਦੀ ਵਰਤੋਂ ਕਰੋ, ਟੀਮ ਪਹੁੰਚ ਲਈ VPN 'ਤੇ ਵਿਚਾਰ ਕਰੋ
- **ਪਹੁੰਚ ਨਿਯੰਤਰਣ**: ਓਪਨ ਵੈੱਬUI ਲਈ ਪ੍ਰਮਾਣਿਕਤਾ ਲਾਗੂ ਕਰੋ
- **ਡਾਟਾ ਗੋਪਨੀਯਤਾ**: ਇਹ ਆਡਿਟ ਕਰੋ ਕਿ ਕਿਹੜਾ ਡਾਟਾ ਲੋਕਲ ਰਹਿੰਦਾ ਹੈ ਅਤੇ ਕਿਹੜਾ ਕਲਾਉਡ ਵਿੱਚ ਜਾਂਦਾ ਹੈ
- **ਅਪਡੇਟਸ**: Foundry Local ਅਤੇ ਕੰਟੇਨਰਾਂ ਨੂੰ ਅਪਡੇਟ ਰੱਖੋ

### ਨਿਗਰਾਨੀ ਅਤੇ ਰਖਰਖਾਅ

- **ਹੈਲਥ ਚੈੱਕਸ**: ਐਂਡਪੌਇੰਟ ਨਿਗਰਾਨੀ ਲਾਗੂ ਕਰੋ
- **ਲੌਗਿੰਗ**: ਸਾਰੇ ਕੰਪੋਨੈਂਟਾਂ ਤੋਂ ਲੌਗਸ ਨੂੰ ਕੇਂਦਰੀਕਰਿਤ ਕਰੋ
- **ਮੈਟ੍ਰਿਕਸ**: ਜਵਾਬ ਦੇ ਸਮੇਂ, ਗਲਤੀ ਦਰਾਂ, ਸਰੋਤ ਦੀ ਵਰਤੋਂ ਨੂੰ ਟ੍ਰੈਕ ਕਰੋ
- **ਬੈਕਅਪ**: ਗੱਲਬਾਤ ਡਾਟਾ ਅਤੇ ਸੰਰਚਨਾਵਾਂ ਦਾ ਨਿਯਮਿਤ ਬੈਕਅਪ

## ਸੰਦਰਭ ਅਤੇ ਸਰੋਤ

### ਦਸਤਾਵੇਜ਼

- [ਚੇਨਲਿਟ ਦਸਤਾਵੇਜ਼](https://docs.chainlit.io/) - ਪੂਰਾ ਫਰੇਮਵਰਕ ਗਾਈਡ
- [Foundry Local ਦਸਤਾਵੇਜ਼](https://learn.microsoft.com/azure/ai-foundry/foundry-local/) - ਅਧਿਕਾਰਤ ਮਾਈਕਰੋਸਾਫਟ ਡੌਕਸ
- [ONNX Runtime Web](https://onnxruntime.ai/docs/get-started/with-javascript/web.html) - ਵੈੱਬGPU ਇੰਟੀਗ੍ਰੇਸ਼ਨ
- [ਓਪਨ ਵੈੱਬUI ਦਸਤਾਵੇਜ਼](https://docs.openwebui.com/) - ਅਗਲੇ ਪੱਧਰ ਦੀ ਸੰਰਚਨਾ

### ਨਮੂਨਾ ਫਾਈਲਾਂ

- [`app.py`](../../../../../Module08/samples/04/app.py) - ਪ੍ਰੋਡਕਸ਼ਨ ਚੇਨਲਿਟ ਐਪਲੀਕੇਸ਼ਨ
- [`chainlit_app.ipynb`](./chainlit_app.ipynb) - ਸਿੱਖਣ ਲਈ ਨੋਟਬੁੱਕ
- [`webgpu-demo/`](../../../../../Module08/samples/04/webgpu-demo) - ਬ੍ਰਾਊਜ਼ਰ-ਅਧਾਰਿਤ AI ਇੰਫਰੈਂਸ
- [`open-webui-guide.md`](./open-webui-guide.md) - ਪੂਰਾ ਓਪਨ ਵੈੱਬUI ਸੈਟਅਪ

### ਸੰਬੰਧਿਤ ਨਮੂਨੇ

- [ਸੈਸ਼ਨ 4 ਦਸਤਾਵੇਜ਼](../../04.CuttingEdgeModels.md) - ਪੂਰਾ ਸੈਸ਼ਨ ਗਾਈਡ
- [Foundry Local ਨਮੂਨੇ](https://github.com/microsoft/foundry-local/tree/main/samples) - ਅਧਿਕਾਰਤ ਨਮੂਨੇ

---

