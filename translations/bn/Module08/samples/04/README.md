<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "562ac0eae12d808c9f45fbb77eb5c84f",
  "translation_date": "2025-09-24T15:06:58+00:00",
  "source_file": "Module08/samples/04/README.md",
  "language_code": "bn"
}
-->
# নমুনা ০৪: চেইনলিট ব্যবহার করে প্রোডাকশন চ্যাট অ্যাপ্লিকেশন

মাইক্রোসফট ফাউন্ড্রি লোকাল ব্যবহার করে প্রোডাকশন-রেডি চ্যাট অ্যাপ্লিকেশন তৈরির বিভিন্ন পদ্ধতি প্রদর্শনকারী একটি বিস্তৃত নমুনা, যেখানে আধুনিক ওয়েব ইন্টারফেস, স্ট্রিমিং রেসপন্স এবং উন্নত ব্রাউজার প্রযুক্তি অন্তর্ভুক্ত রয়েছে।

## কী কী অন্তর্ভুক্ত

- **🚀 চেইনলিট চ্যাট অ্যাপ** (`app.py`): স্ট্রিমিং সহ প্রোডাকশন-রেডি চ্যাট অ্যাপ্লিকেশন
- **🌐 WebGPU ডেমো** (`webgpu-demo/`): হার্ডওয়্যার অ্যাক্সিলারেশন সহ ব্রাউজার-ভিত্তিক AI ইনফারেন্স
- **🎨 ওপেন WebUI ইন্টিগ্রেশন** (`open-webui-guide.md`): পেশাদার ChatGPT-এর মতো ইন্টারফেস
- **📚 শিক্ষামূলক নোটবুক** (`chainlit_app.ipynb`): ইন্টারঅ্যাকটিভ লার্নিং মেটেরিয়াল

## দ্রুত শুরু

### ১. চেইনলিট চ্যাট অ্যাপ্লিকেশন

```cmd
# Navigate to Module08 directory
cd Module08

# Start your model
foundry model run phi-4-mini

# Run Chainlit app (using port 8080 to avoid conflicts)
chainlit run samples\04\app.py -w --port 8080
```

খোলা হবে: `http://localhost:8080`

### ২. WebGPU ব্রাউজার ডেমো

```cmd
# Navigate to WebGPU demo
cd Module08\samples\04\webgpu-demo

# Serve the demo
python -m http.server 5173
```

খোলা হবে: `http://localhost:5173`

### ৩. ওপেন WebUI সেটআপ

```cmd
# Run Open WebUI with Docker
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```

খোলা হবে: `http://localhost:3000`

## আর্কিটেকচার প্যাটার্ন

### লোকাল বনাম ক্লাউড সিদ্ধান্ত ম্যাট্রিক্স

| পরিস্থিতি | সুপারিশ | কারণ |
|----------|----------------|--------|
| **গোপনীয় ডেটা** | 🏠 লোকাল (Foundry) | ডেটা ডিভাইসের বাইরে যায় না |
| **জটিল বিশ্লেষণ** | ☁️ ক্লাউড (Azure OpenAI) | বড় মডেলের অ্যাক্সেস |
| **রিয়েল-টাইম চ্যাট** | 🏠 লোকাল (Foundry) | কম লেটেন্সি, দ্রুত রেসপন্স |
| **ডকুমেন্ট বিশ্লেষণ** | 🔄 হাইব্রিড | লোকাল এক্সট্রাকশনের জন্য, ক্লাউড বিশ্লেষণের জন্য |
| **কোড জেনারেশন** | 🏠 লোকাল (Foundry) | গোপনীয়তা + বিশেষায়িত মডেল |
| **গবেষণা কাজ** | ☁️ ক্লাউড (Azure OpenAI) | বিস্তৃত জ্ঞানভিত্তিক প্রয়োজন |

### প্রযুক্তি তুলনা

| প্রযুক্তি | ব্যবহার ক্ষেত্র | সুবিধা | অসুবিধা |
|------------|----------|------|------|
| **চেইনলিট** | পাইথন ডেভেলপার, দ্রুত প্রোটোটাইপিং | সহজ সেটআপ, স্ট্রিমিং সাপোর্ট | শুধুমাত্র পাইথন |
| **WebGPU** | সর্বাধিক গোপনীয়তা, অফলাইন পরিস্থিতি | ব্রাউজার-নেটিভ, সার্ভার প্রয়োজন নেই | সীমিত মডেল সাইজ |
| **ওপেন WebUI** | প্রোডাকশন ডিপ্লয়মেন্ট, টিম | পেশাদার UI, ইউজার ম্যানেজমেন্ট | ডকার প্রয়োজন |

## প্রয়োজনীয়তা

- **Foundry Local**: ইনস্টল এবং চালু ([ডাউনলোড](https://aka.ms/foundry-local-installer))
- **পাইথন**: ৩.১০+ ভার্চুয়াল এনভায়রনমেন্ট সহ
- **মডেল**: অন্তত একটি লোড করা (`foundry model run phi-4-mini`)
- **ব্রাউজার**: Chrome/Edge WebGPU সাপোর্ট সহ ডেমোর জন্য
- **ডকার**: ওপেন WebUI-এর জন্য (ঐচ্ছিক)

## ইনস্টলেশন ও সেটআপ

### ১. পাইথন এনভায়রনমেন্ট সেটআপ

```cmd
# Navigate to Module08 directory
cd Module08

# Create and activate virtual environment
py -m venv .venv
.venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### ২. Foundry Local সেটআপ

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

## নমুনা অ্যাপ্লিকেশন

### চেইনলিট চ্যাট অ্যাপ্লিকেশন

**বৈশিষ্ট্য:**
- 🚀 **রিয়েল-টাইম স্ট্রিমিং**: টোকেন জেনারেট হওয়ার সাথে সাথে প্রদর্শিত হয়
- 🛡️ **শক্তিশালী ত্রুটি পরিচালনা**: গ্রেসফুল ডিগ্রেডেশন এবং পুনরুদ্ধার
- 🎨 **আধুনিক UI**: পেশাদার চ্যাট ইন্টারফেস
- 🔧 **ফ্লেক্সিবল কনফিগারেশন**: এনভায়রনমেন্ট ভেরিয়েবল এবং অটো-ডিটেকশন
- 📱 **রেসপন্সিভ ডিজাইন**: ডেস্কটপ এবং মোবাইল ডিভাইসে কাজ করে

**দ্রুত শুরু:**
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

### WebGPU ব্রাউজার ডেমো

**বৈশিষ্ট্য:**
- 🌐 **ব্রাউজার-নেটিভ AI**: কোনো সার্ভার প্রয়োজন নেই, সম্পূর্ণ ব্রাউজারে চলে
- ⚡ **WebGPU অ্যাক্সিলারেশন**: হার্ডওয়্যার অ্যাক্সিলারেশন উপলব্ধ থাকলে
- 🔒 **সর্বাধিক গোপনীয়তা**: ডেটা কখনোই আপনার ডিভাইসের বাইরে যায় না
- 🎯 **জিরো ইনস্টল**: যেকোনো সামঞ্জস্যপূর্ণ ব্রাউজারে কাজ করে
- 🔄 **গ্রেসফুল ফ্যালব্যাক**: WebGPU অনুপলব্ধ হলে CPU-তে ফিরে যায়

**চালানো:**
```cmd
cd samples\04\webgpu-demo
python -m http.server 5173
# Open http://localhost:5173
```

### ওপেন WebUI ইন্টিগ্রেশন

**বৈশিষ্ট্য:**
- 🎨 **ChatGPT-এর মতো ইন্টারফেস**: পেশাদার, পরিচিত UI
- 👥 **মাল্টি-ইউজার সাপোর্ট**: ইউজার অ্যাকাউন্ট এবং কথোপকথনের ইতিহাস
- 📁 **ফাইল প্রসেসিং**: ডকুমেন্ট আপলোড এবং বিশ্লেষণ
- 🔄 **মডেল সুইচিং**: বিভিন্ন মডেলের মধ্যে সহজে পরিবর্তন
- 🐳 **ডকার ডিপ্লয়মেন্ট**: প্রোডাকশন-রেডি কন্টেইনারাইজড সেটআপ

**দ্রুত সেটআপ:**
```cmd
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```

## কনফিগারেশন রেফারেন্স

### এনভায়রনমেন্ট ভেরিয়েবল

| ভেরিয়েবল | বিবরণ | ডিফল্ট | উদাহরণ |
|----------|-------------|---------|----------|
| `MODEL` | ব্যবহৃত মডেলের উপনাম | `phi-4-mini` | `qwen2.5-7b-instruct` |
| `BASE_URL` | Foundry Local এন্ডপয়েন্ট | অটো-ডিটেক্টেড | `http://localhost:51211` |
| `API_KEY` | API কী (লোকালের জন্য ঐচ্ছিক) | `""` | `your-api-key` |

## সমস্যা সমাধান

### সাধারণ সমস্যা

**চেইনলিট অ্যাপ্লিকেশন:**

1. **সার্ভিস উপলব্ধ নয়:**
   ```cmd
   # Check Foundry Local status
   foundry service status
   foundry service ps
   
   # Validate API endpoint (note: port 51211)
   curl http://localhost:51211/v1/models
   ```

2. **পোর্ট কনফ্লিক্ট:**
   ```cmd
   # Check what's using port 8080
   netstat -ano | findstr :8080
   
   # Use different port if needed
   chainlit run samples\04\app.py -w --port 3000
   ```

3. **পাইথন এনভায়রনমেন্ট সমস্যা:**
   ```cmd
   # Verify correct interpreter in VS Code
   # Ctrl+Shift+P → Python: Select Interpreter
   # Choose: Module08/.venv/Scripts/python.exe
   
   # Reinstall dependencies
   pip install -r requirements.txt
   ```

**WebGPU ডেমো:**

1. **WebGPU সমর্থিত নয়:**
   - Chrome/Edge 113+ আপডেট করুন
   - WebGPU সক্ষম করুন: `chrome://flags/#enable-unsafe-webgpu`
   - GPU স্ট্যাটাস পরীক্ষা করুন: `chrome://gpu`
   - ডেমো স্বয়ংক্রিয়ভাবে CPU-তে ফিরে যাবে

2. **মডেল লোডিং ত্রুটি:**
   - মডেল ডাউনলোডের জন্য ইন্টারনেট সংযোগ নিশ্চিত করুন
   - ব্রাউজার কনসোলে CORS ত্রুটি পরীক্ষা করুন
   - নিশ্চিত করুন আপনি HTTP-এর মাধ্যমে সার্ভ করছেন (file:// নয়)

**ওপেন WebUI:**

1. **সংযোগ প্রত্যাখ্যান:**
   ```cmd
   # Check Docker is running
   docker --version
   
   # Check container status
   docker ps | findstr open-webui
   
   # View container logs
   docker logs open-webui
   ```

2. **মডেল উপস্থিত নয়:**
   ```cmd
   # Verify Foundry Local endpoint
   curl http://localhost:51211/v1/models
   
   # Restart Open WebUI
   docker restart open-webui
   ```

### যাচাই চেকলিস্ট

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

## উন্নত ব্যবহার

### পারফরম্যান্স অপ্টিমাইজেশন

**চেইনলিট:**
- ভালো পারফরম্যান্সের জন্য স্ট্রিমিং ব্যবহার করুন
- উচ্চ কনকারেন্সির জন্য কানেকশন পুলিং বাস্তবায়ন করুন
- পুনরাবৃত্ত প্রশ্নের জন্য মডেল রেসপন্স ক্যাশ করুন
- বড় কথোপকথনের ইতিহাসের জন্য মেমরি ব্যবহার পর্যবেক্ষণ করুন

**WebGPU:**
- সর্বাধিক গোপনীয়তা এবং গতির জন্য WebGPU ব্যবহার করুন
- ছোট মডেলের জন্য মডেল কোয়ান্টাইজেশন বাস্তবায়ন করুন
- ব্যাকগ্রাউন্ড প্রসেসিংয়ের জন্য Web Workers ব্যবহার করুন
- ব্রাউজার স্টোরেজে কম্পাইলড মডেল ক্যাশ করুন

**ওপেন WebUI:**
- কথোপকথনের ইতিহাসের জন্য স্থায়ী ভলিউম ব্যবহার করুন
- ডকার কন্টেইনারের জন্য রিসোর্স সীমা কনফিগার করুন
- ইউজার ডেটার জন্য ব্যাকআপ কৌশল বাস্তবায়ন করুন
- SSL টার্মিনেশনের জন্য রিভার্স প্রক্সি সেট আপ করুন

### ইন্টিগ্রেশন প্যাটার্ন

**হাইব্রিড লোকাল/ক্লাউড:**
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

**মাল্টি-মডাল পাইপলাইন:**
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

## প্রোডাকশন ডিপ্লয়মেন্ট

### নিরাপত্তা বিবেচনা

- **API কী**: এনভায়রনমেন্ট ভেরিয়েবল ব্যবহার করুন, কখনোই হার্ডকোড করবেন না
- **নেটওয়ার্ক**: প্রোডাকশনে HTTPS ব্যবহার করুন, টিম অ্যাক্সেসের জন্য VPN বিবেচনা করুন
- **অ্যাক্সেস কন্ট্রোল**: ওপেন WebUI-এর জন্য প্রমাণীকরণ বাস্তবায়ন করুন
- **ডেটা গোপনীয়তা**: কোন ডেটা লোকাল থাকে এবং কোনটি ক্লাউডে যায় তা নিরীক্ষণ করুন
- **আপডেট**: Foundry Local এবং কন্টেইনার আপডেট রাখুন

### মনিটরিং এবং রক্ষণাবেক্ষণ

- **হেলথ চেক**: এন্ডপয়েন্ট মনিটরিং বাস্তবায়ন করুন
- **লগিং**: সমস্ত কম্পোনেন্ট থেকে লগ কেন্দ্রীভূত করুন
- **মেট্রিকস**: রেসপন্স টাইম, ত্রুটি হার, রিসোর্স ব্যবহার ট্র্যাক করুন
- **ব্যাকআপ**: কথোপকথনের ডেটা এবং কনফিগারেশনের নিয়মিত ব্যাকআপ

## রেফারেন্স এবং রিসোর্স

### ডকুমেন্টেশন
- [চেইনলিট ডকুমেন্টেশন](https://docs.chainlit.io/) - সম্পূর্ণ ফ্রেমওয়ার্ক গাইড
- [Foundry Local ডকুমেন্টেশন](https://learn.microsoft.com/azure/ai-foundry/foundry-local/) - মাইক্রোসফটের অফিসিয়াল ডকস
- [ONNX Runtime Web](https://onnxruntime.ai/docs/get-started/with-javascript/web.html) - WebGPU ইন্টিগ্রেশন
- [ওপেন WebUI ডকুমেন্টেশন](https://docs.openwebui.com/) - উন্নত কনফিগারেশন

### নমুনা ফাইল
- [`app.py`](../../../../../Module08/samples/04/app.py) - প্রোডাকশন চেইনলিট অ্যাপ্লিকেশন
- [`chainlit_app.ipynb`](./chainlit_app.ipynb) - শিক্ষামূলক নোটবুক
- [`webgpu-demo/`](../../../../../Module08/samples/04/webgpu-demo) - ব্রাউজার-ভিত্তিক AI ইনফারেন্স
- [`open-webui-guide.md`](./open-webui-guide.md) - সম্পূর্ণ ওপেন WebUI সেটআপ

### সম্পর্কিত নমুনা
- [সেশন ৪ ডকুমেন্টেশন](../../04.CuttingEdgeModels.md) - সম্পূর্ণ সেশন গাইড
- [Foundry Local নমুনা](https://github.com/microsoft/foundry-local/tree/main/samples) - অফিসিয়াল নমুনা

---

