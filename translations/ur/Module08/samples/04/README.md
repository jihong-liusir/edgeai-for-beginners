<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "562ac0eae12d808c9f45fbb77eb5c84f",
  "translation_date": "2025-09-24T13:40:35+00:00",
  "source_file": "Module08/samples/04/README.md",
  "language_code": "ur"
}
-->
# نمونہ 04: چینلٹ کے ساتھ پروڈکشن چیٹ ایپلیکیشنز

یہ ایک جامع نمونہ ہے جو مائیکروسافٹ فاؤنڈری لوکل کا استعمال کرتے ہوئے پروڈکشن کے لیے تیار چیٹ ایپلیکیشنز بنانے کے مختلف طریقے دکھاتا ہے، جس میں جدید ویب انٹرفیس، اسٹریمنگ جوابات، اور جدید براؤزر ٹیکنالوجیز شامل ہیں۔

## کیا شامل ہے؟

- **🚀 چینلٹ چیٹ ایپ** (`app.py`): اسٹریمنگ کے ساتھ پروڈکشن کے لیے تیار چیٹ ایپلیکیشن
- **🌐 ویب جی پی یو ڈیمو** (`webgpu-demo/`): ہارڈویئر ایکسیلیریشن کے ساتھ براؤزر پر مبنی AI انفرنس
- **🎨 اوپن ویب UI انٹیگریشن** (`open-webui-guide.md`): پروفیشنل ChatGPT جیسا انٹرفیس
- **📚 تعلیمی نوٹ بک** (`chainlit_app.ipynb`): انٹرایکٹو لرننگ مواد

## فوری آغاز

### 1. چینلٹ چیٹ ایپلیکیشن

```cmd
# Navigate to Module08 directory
cd Module08

# Start your model
foundry model run phi-4-mini

# Run Chainlit app (using port 8080 to avoid conflicts)
chainlit run samples\04\app.py -w --port 8080
```

کھلتا ہے: `http://localhost:8080`

### 2. ویب جی پی یو براؤزر ڈیمو

```cmd
# Navigate to WebGPU demo
cd Module08\samples\04\webgpu-demo

# Serve the demo
python -m http.server 5173
```

کھلتا ہے: `http://localhost:5173`

### 3. اوپن ویب UI سیٹ اپ

```cmd
# Run Open WebUI with Docker
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```

کھلتا ہے: `http://localhost:3000`

## آرکیٹیکچر پیٹرنز

### لوکل بمقابلہ کلاؤڈ فیصلہ میٹرکس

| منظرنامہ | سفارش | وجہ |
|----------|----------------|--------|
| **پرائیویسی حساس ڈیٹا** | 🏠 لوکل (فاؤنڈری) | ڈیٹا کبھی بھی ڈیوائس سے باہر نہیں جاتا |
| **پیچیدہ استدلال** | ☁️ کلاؤڈ (Azure OpenAI) | بڑے ماڈلز تک رسائی |
| **ریئل ٹائم چیٹ** | 🏠 لوکل (فاؤنڈری) | کم لیٹنسی، تیز جوابات |
| **دستاویز تجزیہ** | 🔄 ہائبرڈ | لوکل نکالنے کے لیے، کلاؤڈ تجزیہ کے لیے |
| **کوڈ جنریشن** | 🏠 لوکل (فاؤنڈری) | پرائیویسی + خصوصی ماڈلز |
| **ریسرچ ٹاسکس** | ☁️ کلاؤڈ (Azure OpenAI) | وسیع علم کی بنیاد کی ضرورت |

### ٹیکنالوجی کا موازنہ

| ٹیکنالوجی | استعمال کا کیس | فوائد | نقصانات |
|------------|----------|------|------|
| **چینلٹ** | پائتھون ڈویلپرز، تیز پروٹوٹائپنگ | آسان سیٹ اپ، اسٹریمنگ سپورٹ | صرف پائتھون |
| **ویب جی پی یو** | زیادہ سے زیادہ پرائیویسی، آف لائن منظرنامے | براؤزر نیٹو، سرور کی ضرورت نہیں | محدود ماڈل سائز |
| **اوپن ویب UI** | پروڈکشن ڈپلائمنٹ، ٹیمز | پروفیشنل UI، یوزر مینجمنٹ | ڈوکر کی ضرورت |

## ضروریات

- **فاؤنڈری لوکل**: انسٹال اور چل رہا ([ڈاؤنلوڈ کریں](https://aka.ms/foundry-local-installer))
- **پائتھون**: 3.10+ کے ساتھ ورچوئل ماحول
- **ماڈل**: کم از کم ایک لوڈ کیا ہوا (`foundry model run phi-4-mini`)
- **براؤزر**: کروم/ایج کے ساتھ ویب جی پی یو سپورٹ کے لیے ڈیمو
- **ڈوکر**: اوپن ویب UI کے لیے (اختیاری)

## انسٹالیشن اور سیٹ اپ

### 1. پائتھون ماحول سیٹ اپ

```cmd
# Navigate to Module08 directory
cd Module08

# Create and activate virtual environment
py -m venv .venv
.venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### 2. فاؤنڈری لوکل سیٹ اپ

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

## نمونہ ایپلیکیشنز

### چینلٹ چیٹ ایپلیکیشن

**خصوصیات:**
- 🚀 **ریئل ٹائم اسٹریمنگ**: ٹوکنز جیسے ہی جنریٹ ہوتے ہیں ظاہر ہوتے ہیں
- 🛡️ **مضبوط ایرر ہینڈلنگ**: گریسفل ڈیگریڈیشن اور ریکوری
- 🎨 **جدید UI**: پروفیشنل چیٹ انٹرفیس آؤٹ آف دی باکس
- 🔧 **لچکدار کنفیگریشن**: ماحول کے متغیرات اور خودکار ڈیٹیکشن
- 📱 **ریسپانسیو ڈیزائن**: ڈیسک ٹاپ اور موبائل ڈیوائسز پر کام کرتا ہے

**فوری آغاز:**
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

### ویب جی پی یو براؤزر ڈیمو

**خصوصیات:**
- 🌐 **براؤزر نیٹو AI**: کوئی سرور کی ضرورت نہیں، مکمل طور پر براؤزر میں چلتا ہے
- ⚡ **ویب جی پی یو ایکسیلیریشن**: ہارڈویئر ایکسیلیریشن جب دستیاب ہو
- 🔒 **زیادہ سے زیادہ پرائیویسی**: ڈیٹا کبھی بھی آپ کے ڈیوائس سے باہر نہیں جاتا
- 🎯 **زیرو انسٹال**: کسی بھی مطابقت پذیر براؤزر میں کام کرتا ہے
- 🔄 **گریسفل فال بیک**: اگر ویب جی پی یو دستیاب نہ ہو تو CPU پر واپس آتا ہے

**چلانا:**
```cmd
cd samples\04\webgpu-demo
python -m http.server 5173
# Open http://localhost:5173
```

### اوپن ویب UI انٹیگریشن

**خصوصیات:**
- 🎨 **ChatGPT جیسا انٹرفیس**: پروفیشنل، مانوس UI
- 👥 **ملٹی یوزر سپورٹ**: یوزر اکاؤنٹس اور گفتگو کی تاریخ
- 📁 **فائل پروسیسنگ**: دستاویزات اپلوڈ اور تجزیہ کریں
- 🔄 **ماڈل سوئچنگ**: مختلف ماڈلز کے درمیان آسان سوئچنگ
- 🐳 **ڈوکر ڈپلائمنٹ**: پروڈکشن کے لیے تیار کنٹینرائزڈ سیٹ اپ

**فوری سیٹ اپ:**
```cmd
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```

## کنفیگریشن ریفرنس

### ماحول کے متغیرات

| متغیر | وضاحت | ڈیفالٹ | مثال |
|----------|-------------|---------|----------|
| `MODEL` | استعمال کرنے کے لیے ماڈل کا عرف | `phi-4-mini` | `qwen2.5-7b-instruct` |
| `BASE_URL` | فاؤنڈری لوکل اینڈ پوائنٹ | خودکار ڈیٹیکٹڈ | `http://localhost:51211` |
| `API_KEY` | API کی (لوکل کے لیے اختیاری) | `""` | `your-api-key` |

## مسائل کا حل

### عام مسائل

**چینلٹ ایپلیکیشن:**

1. **سروس دستیاب نہیں:**
   ```cmd
   # Check Foundry Local status
   foundry service status
   foundry service ps
   
   # Validate API endpoint (note: port 51211)
   curl http://localhost:51211/v1/models
   ```

2. **پورٹ تنازعات:**
   ```cmd
   # Check what's using port 8080
   netstat -ano | findstr :8080
   
   # Use different port if needed
   chainlit run samples\04\app.py -w --port 3000
   ```

3. **پائتھون ماحول کے مسائل:**
   ```cmd
   # Verify correct interpreter in VS Code
   # Ctrl+Shift+P → Python: Select Interpreter
   # Choose: Module08/.venv/Scripts/python.exe
   
   # Reinstall dependencies
   pip install -r requirements.txt
   ```

**ویب جی پی یو ڈیمو:**

1. **ویب جی پی یو سپورٹ نہیں:**
   - کروم/ایج 113+ پر اپڈیٹ کریں
   - ویب جی پی یو کو فعال کریں: `chrome://flags/#enable-unsafe-webgpu`
   - GPU اسٹیٹس چیک کریں: `chrome://gpu`
   - ڈیمو خودکار طور پر CPU پر واپس آ جائے گا

2. **ماڈل لوڈنگ ایررز:**
   - ماڈل ڈاؤنلوڈ کے لیے انٹرنیٹ کنکشن یقینی بنائیں
   - براؤزر کنسول میں CORS ایررز چیک کریں
   - تصدیق کریں کہ آپ HTTP کے ذریعے سرور کر رہے ہیں (file:// نہیں)

**اوپن ویب UI:**

1. **کنکشن ریفیوزڈ:**
   ```cmd
   # Check Docker is running
   docker --version
   
   # Check container status
   docker ps | findstr open-webui
   
   # View container logs
   docker logs open-webui
   ```

2. **ماڈلز ظاہر نہیں ہو رہے:**
   ```cmd
   # Verify Foundry Local endpoint
   curl http://localhost:51211/v1/models
   
   # Restart Open WebUI
   docker restart open-webui
   ```

### توثیق چیک لسٹ

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

## ایڈوانسڈ استعمال

### کارکردگی کی اصلاح

**چینلٹ:**
- بہتر محسوس شدہ کارکردگی کے لیے اسٹریمنگ استعمال کریں
- زیادہ ہم وقتی کے لیے کنکشن پولنگ نافذ کریں
- بار بار سوالات کے لیے ماڈل جوابات کی کیشنگ کریں
- بڑی گفتگو کی تاریخ کے ساتھ میموری استعمال کی نگرانی کریں

**ویب جی پی یو:**
- زیادہ سے زیادہ پرائیویسی اور رفتار کے لیے ویب جی پی یو استعمال کریں
- چھوٹے ماڈلز کے لیے ماڈل کوانٹائزیشن نافذ کریں
- بیک گراؤنڈ پروسیسنگ کے لیے ویب ورکرز استعمال کریں
- براؤزر اسٹوریج میں کمپائل شدہ ماڈلز کی کیشنگ کریں

**اوپن ویب UI:**
- گفتگو کی تاریخ کے لیے مستقل والیومز استعمال کریں
- ڈوکر کنٹینر کے لیے وسائل کی حدیں کنفیگر کریں
- یوزر ڈیٹا کے لیے بیک اپ حکمت عملی نافذ کریں
- SSL ٹرمینیشن کے لیے ریورس پراکسی سیٹ اپ کریں

### انٹیگریشن پیٹرنز

**ہائبرڈ لوکل/کلاؤڈ:**
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

**ملٹی موڈل پائپ لائن:**
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

## پروڈکشن ڈپلائمنٹ

### سیکیورٹی کے تحفظات

- **API کیز**: ماحول کے متغیرات استعمال کریں، کبھی بھی ہارڈ کوڈ نہ کریں
- **نیٹ ورک**: پروڈکشن میں HTTPS استعمال کریں، ٹیم تک رسائی کے لیے VPN پر غور کریں
- **رسائی کنٹرول**: اوپن ویب UI کے لیے تصدیق نافذ کریں
- **ڈیٹا پرائیویسی**: آڈٹ کریں کہ کون سا ڈیٹا لوکل رہتا ہے اور کون سا کلاؤڈ پر جاتا ہے
- **اپڈیٹس**: فاؤنڈری لوکل اور کنٹینرز کو اپڈیٹ رکھیں

### مانیٹرنگ اور دیکھ بھال

- **ہیلتھ چیکس**: اینڈ پوائنٹ مانیٹرنگ نافذ کریں
- **لاگنگ**: تمام اجزاء سے لاگز کو مرکزی بنائیں
- **میٹرکس**: جواب کے اوقات، ایرر ریٹس، وسائل کے استعمال کو ٹریک کریں
- **بیک اپ**: گفتگو کے ڈیٹا اور کنفیگریشنز کا باقاعدہ بیک اپ

## حوالہ جات اور وسائل

### دستاویزات
- [چینلٹ دستاویزات](https://docs.chainlit.io/) - مکمل فریم ورک گائیڈ
- [فاؤنڈری لوکل دستاویزات](https://learn.microsoft.com/azure/ai-foundry/foundry-local/) - مائیکروسافٹ کی آفیشل دستاویزات
- [ONNX رن ٹائم ویب](https://onnxruntime.ai/docs/get-started/with-javascript/web.html) - ویب جی پی یو انٹیگریشن
- [اوپن ویب UI دستاویزات](https://docs.openwebui.com/) - ایڈوانسڈ کنفیگریشن

### نمونہ فائلز
- [`app.py`](../../../../../Module08/samples/04/app.py) - پروڈکشن چینلٹ ایپلیکیشن
- [`chainlit_app.ipynb`](./chainlit_app.ipynb) - تعلیمی نوٹ بک
- [`webgpu-demo/`](../../../../../Module08/samples/04/webgpu-demo) - براؤزر پر مبنی AI انفرنس
- [`open-webui-guide.md`](./open-webui-guide.md) - مکمل اوپن ویب UI سیٹ اپ

### متعلقہ نمونے
- [سیشن 4 دستاویزات](../../04.CuttingEdgeModels.md) - مکمل سیشن گائیڈ
- [فاؤنڈری لوکل نمونے](https://github.com/microsoft/foundry-local/tree/main/samples) - آفیشل نمونے

---

