<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "562ac0eae12d808c9f45fbb77eb5c84f",
  "translation_date": "2025-09-24T22:42:09+00:00",
  "source_file": "Module08/samples/04/README.md",
  "language_code": "th"
}
-->
# ตัวอย่าง 04: แอปพลิเคชันแชทสำหรับการใช้งานจริงด้วย Chainlit

ตัวอย่างที่ครอบคลุมแสดงวิธีการหลากหลายในการสร้างแอปพลิเคชันแชทที่พร้อมใช้งานจริงโดยใช้ Microsoft Foundry Local พร้อมด้วยอินเทอร์เฟซเว็บที่ทันสมัย การตอบสนองแบบสตรีม และเทคโนโลยีเบราว์เซอร์ล้ำสมัย

## สิ่งที่รวมอยู่ในตัวอย่าง

- **🚀 Chainlit Chat App** (`app.py`): แอปพลิเคชันแชทที่พร้อมใช้งานจริงพร้อมการสตรีม
- **🌐 WebGPU Demo** (`webgpu-demo/`): การประมวลผล AI บนเบราว์เซอร์พร้อมการเร่งความเร็วด้วยฮาร์ดแวร์
- **🎨 Open WebUI Integration** (`open-webui-guide.md`): อินเทอร์เฟซแบบมืออาชีพคล้าย ChatGPT
- **📚 Educational Notebook** (`chainlit_app.ipynb`): วัสดุการเรียนรู้แบบโต้ตอบ

## เริ่มต้นใช้งานอย่างรวดเร็ว

### 1. แอปพลิเคชันแชท Chainlit

```cmd
# Navigate to Module08 directory
cd Module08

# Start your model
foundry model run phi-4-mini

# Run Chainlit app (using port 8080 to avoid conflicts)
chainlit run samples\04\app.py -w --port 8080
```

เปิดที่: `http://localhost:8080`

### 2. การสาธิต WebGPU บนเบราว์เซอร์

```cmd
# Navigate to WebGPU demo
cd Module08\samples\04\webgpu-demo

# Serve the demo
python -m http.server 5173
```

เปิดที่: `http://localhost:5173`

### 3. การตั้งค่า Open WebUI

```cmd
# Run Open WebUI with Docker
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```

เปิดที่: `http://localhost:3000`

## รูปแบบสถาปัตยกรรม

### ตารางการตัดสินใจระหว่าง Local และ Cloud

| สถานการณ์ | คำแนะนำ | เหตุผล |
|------------|----------|--------|
| **ข้อมูลที่ต้องการความเป็นส่วนตัว** | 🏠 Local (Foundry) | ข้อมูลไม่ออกจากอุปกรณ์ |
| **การวิเคราะห์ที่ซับซ้อน** | ☁️ Cloud (Azure OpenAI) | เข้าถึงโมเดลขนาดใหญ่ |
| **แชทแบบเรียลไทม์** | 🏠 Local (Foundry) | ความหน่วงต่ำ ตอบสนองเร็ว |
| **การวิเคราะห์เอกสาร** | 🔄 Hybrid | Local สำหรับการดึงข้อมูล, Cloud สำหรับการวิเคราะห์ |
| **การสร้างโค้ด** | 🏠 Local (Foundry) | ความเป็นส่วนตัว + โมเดลเฉพาะทาง |
| **งานวิจัย** | ☁️ Cloud (Azure OpenAI) | ต้องการฐานความรู้กว้างขวาง |

### การเปรียบเทียบเทคโนโลยี

| เทคโนโลยี | กรณีการใช้งาน | ข้อดี | ข้อเสีย |
|------------|---------------|-------|----------|
| **Chainlit** | นักพัฒนา Python, การสร้างต้นแบบเร็ว | ตั้งค่าง่าย, รองรับการสตรีม | ใช้ได้เฉพาะ Python |
| **WebGPU** | ความเป็นส่วนตัวสูงสุด, สถานการณ์ออฟไลน์ | ทำงานในเบราว์เซอร์, ไม่ต้องใช้เซิร์ฟเวอร์ | ขนาดโมเดลจำกัด |
| **Open WebUI** | การใช้งานจริง, ทีมงาน | UI มืออาชีพ, การจัดการผู้ใช้ | ต้องใช้ Docker |

## ข้อกำหนดเบื้องต้น

- **Foundry Local**: ติดตั้งและทำงานอยู่ ([ดาวน์โหลด](https://aka.ms/foundry-local-installer))
- **Python**: 3.10+ พร้อม virtual environment
- **โมเดล**: โหลดอย่างน้อยหนึ่งโมเดล (`foundry model run phi-4-mini`)
- **เบราว์เซอร์**: Chrome/Edge ที่รองรับ WebGPU สำหรับการสาธิต
- **Docker**: สำหรับ Open WebUI (ไม่บังคับ)

## การติดตั้งและการตั้งค่า

### 1. การตั้งค่า Python Environment

```cmd
# Navigate to Module08 directory
cd Module08

# Create and activate virtual environment
py -m venv .venv
.venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### 2. การตั้งค่า Foundry Local

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

## แอปพลิเคชันตัวอย่าง

### แอปพลิเคชันแชท Chainlit

**คุณสมบัติ:**
- 🚀 **การสตรีมแบบเรียลไทม์**: โทเค็นปรากฏขึ้นเมื่อถูกสร้าง
- 🛡️ **การจัดการข้อผิดพลาดที่แข็งแกร่ง**: การลดผลกระทบและการกู้คืนอย่างราบรื่น
- 🎨 **UI ทันสมัย**: อินเทอร์เฟซแชทมืออาชีพพร้อมใช้งาน
- 🔧 **การตั้งค่าที่ยืดหยุ่น**: ตัวแปรสภาพแวดล้อมและการตรวจจับอัตโนมัติ
- 📱 **การออกแบบที่ตอบสนอง**: ใช้งานได้ทั้งบนเดสก์ท็อปและมือถือ

**เริ่มต้นใช้งานอย่างรวดเร็ว:**
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

### การสาธิต WebGPU บนเบราว์เซอร์

**คุณสมบัติ:**
- 🌐 **AI บนเบราว์เซอร์**: ไม่ต้องใช้เซิร์ฟเวอร์ ทำงานทั้งหมดในเบราว์เซอร์
- ⚡ **การเร่งความเร็วด้วย WebGPU**: ใช้ฮาร์ดแวร์เมื่อมี
- 🔒 **ความเป็นส่วนตัวสูงสุด**: ข้อมูลไม่ออกจากอุปกรณ์ของคุณ
- 🎯 **ไม่ต้องติดตั้ง**: ใช้งานได้ในเบราว์เซอร์ที่รองรับ
- 🔄 **การสำรองข้อมูลที่ราบรื่น**: เปลี่ยนไปใช้ CPU หาก WebGPU ไม่พร้อมใช้งาน

**การใช้งาน:**
```cmd
cd samples\04\webgpu-demo
python -m http.server 5173
# Open http://localhost:5173
```

### การรวม Open WebUI

**คุณสมบัติ:**
- 🎨 **อินเทอร์เฟซคล้าย ChatGPT**: UI มืออาชีพและคุ้นเคย
- 👥 **รองรับผู้ใช้หลายคน**: บัญชีผู้ใช้และประวัติการสนทนา
- 📁 **การประมวลผลไฟล์**: อัปโหลดและวิเคราะห์เอกสาร
- 🔄 **การสลับโมเดล**: สลับระหว่างโมเดลต่าง ๆ ได้ง่าย
- 🐳 **การใช้งานด้วย Docker**: การตั้งค่าที่พร้อมใช้งานจริงแบบคอนเทนเนอร์

**การตั้งค่าอย่างรวดเร็ว:**
```cmd
docker run -d --name open-webui -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```

## การอ้างอิงการตั้งค่า

### ตัวแปรสภาพแวดล้อม

| ตัวแปร | คำอธิบาย | ค่าเริ่มต้น | ตัวอย่าง |
|--------|-----------|-------------|----------|
| `MODEL` | ชื่อโมเดลที่จะใช้ | `phi-4-mini` | `qwen2.5-7b-instruct` |
| `BASE_URL` | จุดเชื่อมต่อ Foundry Local | ตรวจจับอัตโนมัติ | `http://localhost:51211` |
| `API_KEY` | คีย์ API (ไม่บังคับสำหรับ Local) | `""` | `your-api-key` |

## การแก้ไขปัญหา

### ปัญหาทั่วไป

**แอปพลิเคชัน Chainlit:**

1. **บริการไม่พร้อมใช้งาน:**
   ```cmd
   # Check Foundry Local status
   foundry service status
   foundry service ps
   
   # Validate API endpoint (note: port 51211)
   curl http://localhost:51211/v1/models
   ```

2. **ปัญหาการชนกันของพอร์ต:**
   ```cmd
   # Check what's using port 8080
   netstat -ano | findstr :8080
   
   # Use different port if needed
   chainlit run samples\04\app.py -w --port 3000
   ```

3. **ปัญหาสภาพแวดล้อม Python:**
   ```cmd
   # Verify correct interpreter in VS Code
   # Ctrl+Shift+P → Python: Select Interpreter
   # Choose: Module08/.venv/Scripts/python.exe
   
   # Reinstall dependencies
   pip install -r requirements.txt
   ```

**การสาธิต WebGPU:**

1. **WebGPU ไม่รองรับ:**
   - อัปเดตเป็น Chrome/Edge 113+
   - เปิดใช้งาน WebGPU: `chrome://flags/#enable-unsafe-webgpu`
   - ตรวจสอบสถานะ GPU: `chrome://gpu`
   - การสาธิตจะเปลี่ยนไปใช้ CPU โดยอัตโนมัติ

2. **ข้อผิดพลาดในการโหลดโมเดล:**
   - ตรวจสอบการเชื่อมต่ออินเทอร์เน็ตสำหรับการดาวน์โหลดโมเดล
   - ตรวจสอบคอนโซลเบราว์เซอร์สำหรับข้อผิดพลาด CORS
   - ตรวจสอบว่าคุณกำลังให้บริการผ่าน HTTP (ไม่ใช่ file://)

**Open WebUI:**

1. **การเชื่อมต่อถูกปฏิเสธ:**
   ```cmd
   # Check Docker is running
   docker --version
   
   # Check container status
   docker ps | findstr open-webui
   
   # View container logs
   docker logs open-webui
   ```

2. **โมเดลไม่ปรากฏ:**
   ```cmd
   # Verify Foundry Local endpoint
   curl http://localhost:51211/v1/models
   
   # Restart Open WebUI
   docker restart open-webui
   ```

### รายการตรวจสอบการตรวจสอบ

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

## การใช้งานขั้นสูง

### การปรับปรุงประสิทธิภาพ

**Chainlit:**
- ใช้การสตรีมเพื่อประสิทธิภาพที่รับรู้ได้ดีขึ้น
- ใช้การเชื่อมต่อแบบ pooling สำหรับการใช้งานพร้อมกันสูง
- แคชการตอบสนองของโมเดลสำหรับคำถามที่ซ้ำกัน
- ตรวจสอบการใช้งานหน่วยความจำเมื่อมีประวัติการสนทนาขนาดใหญ่

**WebGPU:**
- ใช้ WebGPU เพื่อความเป็นส่วนตัวและความเร็วสูงสุด
- ใช้การลดขนาดโมเดลเพื่อโมเดลที่เล็กลง
- ใช้ Web Workers สำหรับการประมวลผลเบื้องหลัง
- แคชโมเดลที่คอมไพล์ในพื้นที่จัดเก็บของเบราว์เซอร์

**Open WebUI:**
- ใช้พื้นที่จัดเก็บถาวรสำหรับประวัติการสนทนา
- กำหนดขีดจำกัดทรัพยากรสำหรับคอนเทนเนอร์ Docker
- ใช้กลยุทธ์การสำรองข้อมูลสำหรับข้อมูลผู้ใช้
- ตั้งค่าพร็อกซีย้อนกลับสำหรับการยกเลิก SSL

### รูปแบบการรวม

**Hybrid Local/Cloud:**
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

**Multi-Modal Pipeline:**
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

## การใช้งานจริง

### ข้อควรพิจารณาด้านความปลอดภัย

- **คีย์ API**: ใช้ตัวแปรสภาพแวดล้อม ห้ามเขียนคีย์ในโค้ด
- **เครือข่าย**: ใช้ HTTPS ในการใช้งานจริง พิจารณา VPN สำหรับการเข้าถึงทีม
- **การควบคุมการเข้าถึง**: ใช้การตรวจสอบสิทธิ์สำหรับ Open WebUI
- **ความเป็นส่วนตัวของข้อมูล**: ตรวจสอบว่าข้อมูลใดอยู่ใน Local และข้อมูลใดไปยัง Cloud
- **การอัปเดต**: อัปเดต Foundry Local และคอนเทนเนอร์ให้ทันสมัย

### การตรวจสอบและการบำรุงรักษา

- **การตรวจสอบสถานะ**: ใช้การตรวจสอบจุดเชื่อมต่อ
- **การบันทึก**: รวมบันทึกจากทุกองค์ประกอบ
- **เมตริก**: ติดตามเวลาตอบสนอง อัตราข้อผิดพลาด การใช้งานทรัพยากร
- **การสำรองข้อมูล**: สำรองข้อมูลการสนทนาและการตั้งค่าเป็นประจำ

## เอกสารอ้างอิงและทรัพยากร

### เอกสาร

- [Chainlit Documentation](https://docs.chainlit.io/) - คู่มือเฟรมเวิร์กครบถ้วน
- [Foundry Local Documentation](https://learn.microsoft.com/azure/ai-foundry/foundry-local/) - เอกสาร Microsoft อย่างเป็นทางการ
- [ONNX Runtime Web](https://onnxruntime.ai/docs/get-started/with-javascript/web.html) - การรวม WebGPU
- [Open WebUI Documentation](https://docs.openwebui.com/) - การตั้งค่าขั้นสูง

### ไฟล์ตัวอย่าง
- [`app.py`](../../../../../Module08/samples/04/app.py) - แอปพลิเคชัน Chainlit สำหรับการใช้งานจริง
- [`chainlit_app.ipynb`](./chainlit_app.ipynb) - โน้ตบุ๊กเพื่อการศึกษา
- [`webgpu-demo/`](../../../../../Module08/samples/04/webgpu-demo) - การประมวลผล AI บนเบราว์เซอร์
- [`open-webui-guide.md`](./open-webui-guide.md) - การตั้งค่า Open WebUI ครบถ้วน

### ตัวอย่างที่เกี่ยวข้อง
- [Session 4 Documentation](../../04.CuttingEdgeModels.md) - คู่มือเซสชันครบถ้วน
- [Foundry Local Samples](https://github.com/microsoft/foundry-local/tree/main/samples) - ตัวอย่างอย่างเป็นทางการ

---

