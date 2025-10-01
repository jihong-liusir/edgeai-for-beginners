<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "2f1754a482b6a84e07287a5b775e65b6",
  "translation_date": "2025-10-01T00:03:43+00:00",
  "source_file": "Module08/samples/04/README.md",
  "language_code": "pa"
}
-->
# ਨਮੂਨਾ 04: ਚੇਨਲਿਟ ਨਾਲ ਉਤਪਾਦਨ ਚੈਟ ਐਪਲੀਕੇਸ਼ਨ

ਇਹ ਇੱਕ ਵਿਸਤ੍ਰਿਤ ਨਮੂਨਾ ਹੈ ਜੋ ਮਾਈਕਰੋਸਾਫਟ ਫਾਊਂਡਰੀ ਲੋਕਲ ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਉਤਪਾਦਨ-ਤਿਆਰ ਚੈਟ ਐਪਲੀਕੇਸ਼ਨ ਬਣਾਉਣ ਦੇ ਕਈ ਤਰੀਕਿਆਂ ਨੂੰ ਦਰਸਾਉਂਦਾ ਹੈ, ਜਿਸ ਵਿੱਚ ਆਧੁਨਿਕ ਵੈੱਬ ਇੰਟਰਫੇਸ, ਸਟ੍ਰੀਮਿੰਗ ਜਵਾਬ, ਅਤੇ ਅਗੇਤਨ ਬ੍ਰਾਊਜ਼ਰ ਤਕਨਾਲੋਜੀਆਂ ਸ਼ਾਮਲ ਹਨ।

## ਕੀ ਸ਼ਾਮਲ ਹੈ

- **🚀 ਚੇਨਲਿਟ ਚੈਟ ਐਪ** (`app.py`): ਸਟ੍ਰੀਮਿੰਗ ਵਾਲੀ ਉਤਪਾਦਨ-ਤਿਆਰ ਚੈਟ ਐਪਲੀਕੇਸ਼ਨ  
- **🌐 ਵੈੱਬਜੀਪੀਯੂ ਡੈਮੋ** (`webgpu-demo/`): ਹਾਰਡਵੇਅਰ ਐਕਸਲੇਰੇਸ਼ਨ ਨਾਲ ਬ੍ਰਾਊਜ਼ਰ-ਅਧਾਰਿਤ AI ਇੰਫਰੈਂਸ  
- **🎨 ਓਪਨ ਵੈੱਬਯੂਆਈ ਇੰਟੀਗ੍ਰੇਸ਼ਨ** (`open-webui-guide.md`): ਪ੍ਰੋਫੈਸ਼ਨਲ ChatGPT ਵਰਗਾ ਇੰਟਰਫੇਸ  
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
  
ਖੁਲ੍ਹਦਾ ਹੈ: `http://localhost:8080`

### 2. ਵੈੱਬਜੀਪੀਯੂ ਬ੍ਰਾਊਜ਼ਰ ਡੈਮੋ

```cmd
# Navigate to WebGPU demo
cd Module08\samples\04\webgpu-demo

# Serve the demo
python -m http.server 5173
```
  
ਖੁਲ੍ਹਦਾ ਹੈ: `http://localhost:5173`

### 3. ਓਪਨ ਵੈੱਬਯੂਆਈ ਸੈਟਅੱਪ

```cmd
# Run Open WebUI with Docker
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```
  
ਖੁਲ੍ਹਦਾ ਹੈ: `http://localhost:3000`

## ਆਰਕੀਟੈਕਚਰ ਪੈਟਰਨ

### ਲੋਕਲ ਵਿਰੁੱਧ ਕਲਾਉਡ ਫੈਸਲਾ ਮੈਟ੍ਰਿਕਸ

| ਸਥਿਤੀ | ਸਿਫਾਰਸ਼ | ਕਾਰਨ |
|--------|----------|-------|
| **ਗੋਪਨੀਯਤਾ-ਸੰਵੇਦਨਸ਼ੀਲ ਡਾਟਾ** | 🏠 ਲੋਕਲ (ਫਾਊਂਡਰੀ) | ਡਾਟਾ ਕਦੇ ਵੀ ਡਿਵਾਈਸ ਤੋਂ ਬਾਹਰ ਨਹੀਂ ਜਾਂਦਾ |
| **ਜਟਿਲ ਤਰਕ** | ☁️ ਕਲਾਉਡ (Azure OpenAI) | ਵੱਡੇ ਮਾਡਲਾਂ ਤੱਕ ਪਹੁੰਚ |
| **ਰਿਅਲ-ਟਾਈਮ ਚੈਟ** | 🏠 ਲੋਕਲ (ਫਾਊਂਡਰੀ) | ਘੱਟ ਲੈਟੈਂਸੀ, ਤੇਜ਼ ਜਵਾਬ |
| **ਦਸਤਾਵੇਜ਼ ਵਿਸ਼ਲੇਸ਼ਣ** | 🔄 ਹਾਈਬ੍ਰਿਡ | ਨਿਕਾਲਣ ਲਈ ਲੋਕਲ, ਵਿਸ਼ਲੇਸ਼ਣ ਲਈ ਕਲਾਉਡ |
| **ਕੋਡ ਜਨਰੇਸ਼ਨ** | 🏠 ਲੋਕਲ (ਫਾਊਂਡਰੀ) | ਗੋਪਨੀਯਤਾ + ਵਿਸ਼ੇਸ਼ ਮਾਡਲ |
| **ਗਵੈਸ਼ਣਾ ਕਾਰਜ** | ☁️ ਕਲਾਉਡ (Azure OpenAI) | ਵਿਸ਼ਾਲ ਗਿਆਨ ਅਧਾਰ ਦੀ ਲੋੜ |

### ਤਕਨਾਲੋਜੀ ਦੀ ਤੁਲਨਾ

| ਤਕਨਾਲੋਜੀ | ਵਰਤੋਂ ਦਾ ਕੇਸ | ਫਾਇਦੇ | ਨੁਕਸਾਨ |
|----------|--------------|--------|--------|
| **ਚੇਨਲਿਟ** | ਪਾਇਥਨ ਡਿਵੈਲਪਰ, ਤੇਜ਼ ਪ੍ਰੋਟੋਟਾਈਪਿੰਗ | ਆਸਾਨ ਸੈਟਅੱਪ, ਸਟ੍ਰੀਮਿੰਗ ਸਹਾਇਤਾ | ਸਿਰਫ ਪਾਇਥਨ |
| **ਵੈੱਬਜੀਪੀਯੂ** | ਵੱਧ ਤੋਂ ਵੱਧ ਗੋਪਨੀਯਤਾ, ਆਫਲਾਈਨ ਸਥਿਤੀਆਂ | ਬ੍ਰਾਊਜ਼ਰ-ਮੂਲ, ਸਰਵਰ ਦੀ ਲੋੜ ਨਹੀਂ | ਸੀਮਤ ਮਾਡਲ ਆਕਾਰ |
| **ਓਪਨ ਵੈੱਬਯੂਆਈ** | ਉਤਪਾਦਨ ਤੈਨਾਤੀ, ਟੀਮਾਂ | ਪ੍ਰੋਫੈਸ਼ਨਲ UI, ਯੂਜ਼ਰ ਪ੍ਰਬੰਧਨ | ਡੌਕਰ ਦੀ ਲੋੜ |

## ਪੂਰਵ ਸ਼ਰਤਾਂ

- **ਫਾਊਂਡਰੀ ਲੋਕਲ**: ਇੰਸਟਾਲ ਅਤੇ ਚੱਲ ਰਿਹਾ ([ਡਾਊਨਲੋਡ ਕਰੋ](https://aka.ms/foundry-local-installer))  
- **ਪਾਇਥਨ**: 3.10+ ਨਾਲ ਵਰਚੁਅਲ ਐਨਵਾਇਰਮੈਂਟ  
- **ਮਾਡਲ**: ਘੱਟੋ-ਘੱਟ ਇੱਕ ਲੋਡ ਕੀਤਾ ਹੋਇਆ (`foundry model run phi-4-mini`)  
- **ਬ੍ਰਾਊਜ਼ਰ**: Chrome/Edge ਜਿਸ ਵਿੱਚ ਵੈੱਬਜੀਪੀਯੂ ਸਹਾਇਤਾ ਹੈ ਡੈਮੋ ਲਈ  
- **ਡੌਕਰ**: ਓਪਨ ਵੈੱਬਯੂਆਈ ਲਈ (ਵਿਕਲਪਿਕ)  

## ਇੰਸਟਾਲੇਸ਼ਨ ਅਤੇ ਸੈਟਅੱਪ

### 1. ਪਾਇਥਨ ਐਨਵਾਇਰਮੈਂਟ ਸੈਟਅੱਪ

```cmd
# Navigate to Module08 directory
cd Module08

# Create and activate virtual environment
py -m venv .venv
.venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```
  
### 2. ਫਾਊਂਡਰੀ ਲੋਕਲ ਸੈਟਅੱਪ

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
- 🚀 **ਰਿਅਲ-ਟਾਈਮ ਸਟ੍ਰੀਮਿੰਗ**: ਟੋਕਨ ਜਿਵੇਂ-ਜਿਵੇਂ ਜਨਰੇਟ ਹੁੰਦੇ ਹਨ, ਤੁਰੰਤ ਦਿਖਾਈ ਦਿੰਦੇ ਹਨ  
- 🛡️ **ਮਜ਼ਬੂਤ ਗਲਤੀ ਸੰਭਾਲ**: ਗ੍ਰੇਸਫੁਲ ਡਿਗਰੇਡੇਸ਼ਨ ਅਤੇ ਰਿਕਵਰੀ  
- 🎨 **ਆਧੁਨਿਕ UI**: ਬਾਕਸ ਤੋਂ ਬਾਹਰ ਪ੍ਰੋਫੈਸ਼ਨਲ ਚੈਟ ਇੰਟਰਫੇਸ  
- 🔧 **ਲਚਕੀਲਾ ਕਨਫਿਗਰੇਸ਼ਨ**: ਐਨਵਾਇਰਮੈਂਟ ਵੈਰੀਏਬਲ ਅਤੇ ਆਟੋ-ਡਿਟੈਕਸ਼ਨ  
- 📱 **ਰਿਸਪਾਂਸਿਵ ਡਿਜ਼ਾਈਨ**: ਡੈਸਕਟਾਪ ਅਤੇ ਮੋਬਾਈਲ ਡਿਵਾਈਸਾਂ 'ਤੇ ਕੰਮ ਕਰਦਾ ਹੈ  

**ਤੁਰੰਤ ਸ਼ੁਰੂਆਤ:**  
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
  
### ਵੈੱਬਜੀਪੀਯੂ ਬ੍ਰਾਊਜ਼ਰ ਡੈਮੋ

**ਵਿਸ਼ੇਸ਼ਤਾਵਾਂ:**  
- 🌐 **ਬ੍ਰਾਊਜ਼ਰ-ਮੂਲ AI**: ਕੋਈ ਸਰਵਰ ਲੋੜੀਂਦਾ ਨਹੀਂ, ਪੂਰੀ ਤਰ੍ਹਾਂ ਬ੍ਰਾਊਜ਼ਰ ਵਿੱਚ ਚੱਲਦਾ ਹੈ  
- ⚡ **ਵੈੱਬਜੀਪੀਯੂ ਐਕਸਲੇਰੇਸ਼ਨ**: ਜਿੱਥੇ ਉਪਲਬਧ ਹੋਵੇ, ਹਾਰਡਵੇਅਰ ਐਕਸਲੇਰੇਸ਼ਨ  
- 🔒 **ਵੱਧ ਤੋਂ ਵੱਧ ਗੋਪਨੀਯਤਾ**: ਡਾਟਾ ਕਦੇ ਵੀ ਤੁਹਾਡੇ ਡਿਵਾਈਸ ਤੋਂ ਬਾਹਰ ਨਹੀਂ ਜਾਂਦਾ  
- 🎯 **ਜ਼ੀਰੋ ਇੰਸਟਾਲ**: ਕਿਸੇ ਵੀ ਅਨੁਕੂਲ ਬ੍ਰਾਊਜ਼ਰ ਵਿੱਚ ਕੰਮ ਕਰਦਾ ਹੈ  
- 🔄 **ਗ੍ਰੇਸਫੁਲ ਫਾਲਬੈਕ**: ਜੇ ਵੈੱਬਜੀਪੀਯੂ ਉਪਲਬਧ ਨਹੀਂ, ਤਾਂ CPU 'ਤੇ ਚੱਲਦਾ ਹੈ  

**ਚਲਾਉਣਾ:**  
```cmd
cd samples\04\webgpu-demo
python -m http.server 5173
# Open http://localhost:5173
```
  
### ਓਪਨ ਵੈੱਬਯੂਆਈ ਇੰਟੀਗ੍ਰੇਸ਼ਨ

**ਵਿਸ਼ੇਸ਼ਤਾਵਾਂ:**  
- 🎨 **ChatGPT ਵਰਗਾ ਇੰਟਰਫੇਸ**: ਪ੍ਰੋਫੈਸ਼ਨਲ, ਜਾਣ-ਪਛਾਣ ਵਾਲਾ UI  
- 👥 **ਮਲਟੀ-ਯੂਜ਼ਰ ਸਹਾਇਤਾ**: ਯੂਜ਼ਰ ਅਕਾਊਂਟ ਅਤੇ ਗੱਲਬਾਤ ਦਾ ਇਤਿਹਾਸ  
- 📁 **ਫਾਈਲ ਪ੍ਰੋਸੈਸਿੰਗ**: ਦਸਤਾਵੇਜ਼ ਅਪਲੋਡ ਅਤੇ ਵਿਸ਼ਲੇਸ਼ਣ  
- 🔄 **ਮਾਡਲ ਸਵਿੱਚਿੰਗ**: ਵੱਖ-ਵੱਖ ਮਾਡਲਾਂ ਵਿੱਚ ਆਸਾਨੀ ਨਾਲ ਬਦਲਾਅ  
- 🐳 **ਡੌਕਰ ਤੈਨਾਤੀ**: ਉਤਪਾਦਨ-ਤਿਆਰ ਕੰਟੇਨਰਾਈਜ਼ਡ ਸੈਟਅੱਪ  

**ਤੁਰੰਤ ਸੈਟਅੱਪ:**  
```cmd
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```
  
## ਕਨਫਿਗਰੇਸ਼ਨ ਰਿਫਰੈਂਸ

### ਐਨਵਾਇਰਮੈਂਟ ਵੈਰੀਏਬਲ

| ਵੈਰੀਏਬਲ | ਵੇਰਵਾ | ਡਿਫਾਲਟ | ਉਦਾਹਰਨ |
|----------|--------|---------|---------|
| `MODEL` | ਵਰਤਣ ਲਈ ਮਾਡਲ ਉਪਨਾਮ | `phi-4-mini` | `qwen2.5-7b` |
| `BASE_URL` | ਫਾਊਂਡਰੀ ਲੋਕਲ ਐਂਡਪੌਇੰਟ | ਆਟੋ-ਡਿਟੈਕਟ ਕੀਤਾ | `http://localhost:51211` |
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
  
**ਵੈੱਬਜੀਪੀਯੂ ਡੈਮੋ:**  

1. **ਵੈੱਬਜੀਪੀਯੂ ਸਹਾਇਤਾ ਨਹੀਂ:**  
   - Chrome/Edge 113+ 'ਤੇ ਅਪਡੇਟ ਕਰੋ  
   - ਵੈੱਬਜੀਪੀਯੂ ਐਨੇਬਲ ਕਰੋ: `chrome://flags/#enable-unsafe-webgpu`  
   - GPU ਸਥਿਤੀ ਚੈੱਕ ਕਰੋ: `chrome://gpu`  
   - ਡੈਮੋ ਆਪਣੇ ਆਪ CPU 'ਤੇ ਫਾਲਬੈਕ ਕਰੇਗਾ  

2. **ਮਾਡਲ ਲੋਡ ਕਰਨ ਦੀਆਂ ਗਲਤੀਆਂ:**  
   - ਮਾਡਲ ਡਾਊਨਲੋਡ ਲਈ ਇੰਟਰਨੈਟ ਕਨੈਕਸ਼ਨ ਯਕੀਨੀ ਬਣਾਓ  
   - ਬ੍ਰਾਊਜ਼ਰ ਕਨਸੋਲ ਵਿੱਚ CORS ਗਲਤੀਆਂ ਚੈੱਕ ਕਰੋ  
   - ਯਕੀਨੀ ਬਣਾਓ ਕਿ ਤੁਸੀਂ HTTP ਰਾਹੀਂ ਸਰਵ ਕਰ ਰਹੇ ਹੋ (file:// ਨਹੀਂ)  

**ਓਪਨ ਵੈੱਬਯੂਆਈ:**  

1. **ਕਨੈਕਸ਼ਨ ਰਿਫਿਊਜ਼ਡ:**  
   ```cmd
   # Check Docker is running
   docker --version
   
   # Check container status
   docker ps | findstr open-webui
   
   # View container logs
   docker logs open-webui
   ```
  
2. **ਮਾਡਲ ਦਿਖਾਈ ਨਹੀਂ ਦੇ ਰਹੇ:**  
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
  
## ਉੱਚ-ਪੱਧਰੀ ਵਰਤੋਂ

### ਪ੍ਰਦਰਸ਼ਨ ਅਪਗ੍ਰੇਡ

**ਚੇਨਲਿਟ:**  
- ਵਧੀਆ ਪ੍ਰਤੀਤ ਪ੍ਰਦਰਸ਼ਨ ਲਈ ਸਟ੍ਰੀਮਿੰਗ ਵਰਤੋ  
- ਉੱਚ ਸਮਕਾਲੀਤਾ ਲਈ ਕਨੈਕਸ਼ਨ ਪੂਲਿੰਗ ਲਾਗੂ ਕਰੋ  
- ਦੁਹਰਾਏ ਗਏ ਪ੍ਰਸ਼ਨਾਂ ਲਈ ਮਾਡਲ ਜਵਾਬ ਕੈਸ਼ ਕਰੋ  
- ਵੱਡੇ ਗੱਲਬਾਤ ਇਤਿਹਾਸਾਂ ਨਾਲ ਮੈਮੋਰੀ ਦੀ ਵਰਤੋਂ ਦੀ ਨਿਗਰਾਨੀ ਕਰੋ  

**ਵੈੱਬਜੀਪੀਯੂ:**  
- ਵੱਧ ਤੋਂ ਵੱਧ ਗੋਪਨੀਯਤਾ ਅਤੇ ਗਤੀ ਲਈ ਵੈੱਬਜੀਪੀਯੂ ਵਰਤੋ  
- ਛੋਟੇ ਮਾਡਲਾਂ ਲਈ ਮਾਡਲ ਕਵਾਂਟੀਜ਼ੇਸ਼ਨ ਲਾਗੂ ਕਰੋ  
- ਬੈਕਗ੍ਰਾਊਂਡ ਪ੍ਰੋਸੈਸਿੰਗ ਲਈ ਵੈੱਬ ਵਰਕਰ ਵਰਤੋ  
- ਬ੍ਰਾਊਜ਼ਰ ਸਟੋਰੇਜ ਵਿੱਚ ਕੈਸ਼ ਕੀਤੇ ਮਾਡਲਾਂ ਨੂੰ ਸਟੋਰ ਕਰੋ  

**ਓਪਨ ਵੈੱਬਯੂਆਈ:**  
- ਗੱਲਬਾਤ ਇਤਿਹਾਸ ਲਈ ਸਥਾਈ ਵਾਲਿਊਮ ਵਰਤੋ  
- ਡੌਕਰ ਕੰਟੇਨਰ ਲਈ ਸਰੋਤ ਸੀਮਾਵਾਂ ਕਨਫਿਗਰ ਕਰੋ  
- ਯੂਜ਼ਰ ਡਾਟਾ ਲਈ ਬੈਕਅੱਪ ਰਣਨੀਤੀਆਂ ਲਾਗੂ ਕਰੋ  
- SSL ਟਰਮੀਨੇਸ਼ਨ ਲਈ ਰਿਵਰਸ ਪ੍ਰੌਕਸੀ ਸੈਟਅੱਪ ਕਰੋ  

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
  
## ਉਤਪਾਦਨ ਤੈਨਾਤੀ

### ਸੁਰੱਖਿਆ ਵਿਚਾਰ

- **API ਕੁੰਜੀਆਂ**: ਐਨਵਾਇਰਮੈਂਟ ਵੈਰੀਏਬਲ ਵਰਤੋ, ਕਦੇ ਵੀ ਹਾਰਡਕੋਡ ਨਾ ਕਰੋ  
- **ਨੈੱਟਵਰਕ**: ਉਤਪਾਦਨ ਵਿੱਚ HTTPS ਵਰਤੋ, ਟੀਮ ਪਹੁੰਚ ਲਈ VPN ਬਾਰੇ ਸੋਚੋ  
- **ਪਹੁੰਚ ਨਿਯੰਤਰਣ**: ਓਪਨ ਵੈੱਬਯੂਆਈ ਲਈ ਪ੍ਰਮਾਣਿਕਤਾ ਲਾਗੂ ਕਰੋ  
- **ਡਾਟਾ ਗੋਪਨੀਯਤਾ**: ਇਹ ਆਡੀਟ ਕਰੋ ਕਿ ਕਿਹੜਾ ਡਾਟਾ ਲੋਕਲ ਰਹਿੰਦਾ ਹੈ ਅਤੇ ਕਿਹੜਾ ਕਲਾਉਡ ਵਿੱਚ ਜਾਂਦਾ ਹੈ  
- **ਅਪਡੇਟਸ**: ਫਾਊਂਡਰੀ ਲੋਕਲ ਅਤੇ ਕੰਟੇਨਰਾਂ ਨੂੰ ਅਪਡੇਟ ਰੱਖੋ  

### ਨਿਗਰਾਨੀ ਅਤੇ ਰਖਰਖਾਅ

- **ਹੈਲਥ ਚੈੱਕਸ**: ਐਂਡਪੌਇੰਟ ਨਿਗਰਾਨੀ ਲਾਗੂ ਕਰੋ  
- **ਲੌਗਿੰਗ**: ਸਾਰੇ ਕੰਪੋਨੈਂਟਾਂ ਤੋਂ ਲੌਗਸ ਨੂੰ ਕੇਂਦਰੀਕ੍ਰਿਤ ਕਰੋ  
- **ਮੀਟ੍ਰਿਕਸ**: ਜਵਾਬ ਦੇ ਸਮੇਂ, ਗਲਤੀ ਦਰਾਂ, ਸਰੋਤ ਦੀ ਵਰਤੋਂ ਨੂੰ ਟ੍ਰੈਕ ਕਰੋ  
- **ਬੈਕਅੱਪ**: ਗੱਲਬਾਤ ਡਾਟਾ ਅਤੇ ਕਨਫਿਗਰੇਸ਼ਨ ਦੀ ਨਿਯਮਤ ਬੈਕਅੱਪ  

## ਹਵਾਲੇ ਅਤੇ ਸਰੋਤ

### ਦਸਤਾਵੇਜ਼

- [ਚੇਨਲਿਟ ਦਸਤਾਵੇਜ਼](https://docs.chainlit.io/) - ਪੂਰਾ ਫਰੇਮਵਰਕ ਗਾਈਡ  
- [ਫਾਊਂਡਰੀ ਲੋਕਲ ਦਸਤਾਵੇਜ਼](https://learn.microsoft.com/azure/ai-foundry/foundry-local/) - ਮਾਈਕਰੋਸਾਫਟ ਦੀ ਅਧਿਕਾਰਕ ਦਸਤਾਵੇਜ਼  
- [ONNX ਰਨਟਾਈਮ ਵੈੱਬ](https://onnxruntime.ai/docs/get-started/with-javascript/web.html) - ਵੈੱਬਜੀਪੀਯੂ ਇੰਟੀਗ੍ਰੇਸ਼ਨ  
- [ਓਪਨ ਵੈੱਬਯੂਆਈ ਦਸਤਾਵੇਜ਼](https://docs.openwebui.com/) - ਉੱਚ-ਪੱਧਰੀ ਕਨਫਿਗਰੇਸ਼ਨ  

### ਨਮੂਨਾ ਫਾਈਲਾਂ

- [`app.py`](../../../../../Module08/samples/04/app.py) - ਉਤਪਾਦਨ ਚੇਨਲਿਟ ਐਪਲੀਕੇਸ਼ਨ  
- [`chainlit_app.ipynb`](./chainlit_app.ipynb) - ਸਿੱਖਣ ਲਈ ਨੋਟਬੁੱਕ  
- [`webgpu-demo/`](../../../../../Module08/samples/04/webgpu-demo) - ਬ੍ਰਾਊਜ਼ਰ-ਅਧਾਰਿਤ AI ਇੰਫਰੈਂਸ  
- [`open-webui-guide.md`](./open-webui-guide.md) - ਪੂਰਾ ਓਪਨ ਵੈੱਬਯੂਆਈ ਸੈਟਅੱਪ  

### ਸੰਬੰਧਿਤ ਨਮੂਨੇ

- [ਸੈਸ਼ਨ 4 ਦਸਤਾਵੇਜ਼](../../04.CuttingEdgeModels.md) - ਪੂਰੀ ਸੈਸ਼ਨ ਗਾਈਡ  
- [ਫਾਊਂਡਰੀ ਲੋਕਲ ਨਮੂਨੇ](https://github.com/microsoft/foundry-local/tree/main/samples) - ਅਧਿਕਾਰਕ ਨਮੂਨੇ  

---

**ਅਸਵੀਕਰਤਾ**:  
ਇਹ ਦਸਤਾਵੇਜ਼ AI ਅਨੁਵਾਦ ਸੇਵਾ [Co-op Translator](https://github.com/Azure/co-op-translator) ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਅਨੁਵਾਦ ਕੀਤਾ ਗਿਆ ਹੈ। ਹਾਲਾਂਕਿ ਅਸੀਂ ਸਹੀ ਹੋਣ ਦੀ ਕੋਸ਼ਿਸ਼ ਕਰਦੇ ਹਾਂ, ਕਿਰਪਾ ਕਰਕੇ ਧਿਆਨ ਦਿਓ ਕਿ ਸਵੈਚਾਲਿਤ ਅਨੁਵਾਦਾਂ ਵਿੱਚ ਗਲਤੀਆਂ ਜਾਂ ਅਸੁਚੱਜੇਪਣ ਹੋ ਸਕਦੇ ਹਨ। ਇਸ ਦੀ ਮੂਲ ਭਾਸ਼ਾ ਵਿੱਚ ਮੌਜੂਦ ਦਸਤਾਵੇਜ਼ ਨੂੰ ਅਧਿਕਾਰਤ ਸਰੋਤ ਮੰਨਿਆ ਜਾਣਾ ਚਾਹੀਦਾ ਹੈ। ਮਹੱਤਵਪੂਰਨ ਜਾਣਕਾਰੀ ਲਈ, ਪੇਸ਼ੇਵਰ ਮਨੁੱਖੀ ਅਨੁਵਾਦ ਦੀ ਸਿਫਾਰਸ਼ ਕੀਤੀ ਜਾਂਦੀ ਹੈ। ਇਸ ਅਨੁਵਾਦ ਦੀ ਵਰਤੋਂ ਤੋਂ ਪੈਦਾ ਹੋਣ ਵਾਲੇ ਕਿਸੇ ਵੀ ਗਲਤਫਹਿਮੀ ਜਾਂ ਗਲਤ ਵਿਆਖਿਆ ਲਈ ਅਸੀਂ ਜ਼ਿੰਮੇਵਾਰ ਨਹੀਂ ਹਾਂ।