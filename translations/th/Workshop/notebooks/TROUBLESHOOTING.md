<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "e88a16101de37838f7cf256a9cd0f199",
  "translation_date": "2025-10-09T13:22:45+00:00",
  "source_file": "Workshop/notebooks/TROUBLESHOOTING.md",
  "language_code": "th"
}
-->
# สมุดงานเวิร์กช็อป - คู่มือแก้ปัญหา

## สารบัญ

- [ปัญหาทั่วไปและวิธีแก้ไข](../../../../Workshop/notebooks)
- [ปัญหาเฉพาะในเซสชัน 04](../../../../Workshop/notebooks)
- [ปัญหาเฉพาะในเซสชัน 05](../../../../Workshop/notebooks)
- [ปัญหาเฉพาะในเซสชัน 06](../../../../Workshop/notebooks)
- [ปัญหาเฉพาะฮาร์ดแวร์](../../../../Workshop/notebooks)
- [คำสั่งวินิจฉัย](../../../../Workshop/notebooks)
- [การขอความช่วยเหลือ](../../../../Workshop/notebooks)

---

## ปัญหาทั่วไปและวิธีแก้ไข

### 🔴 CUDA Out of Memory

**ข้อความแสดงข้อผิดพลาด:**
```
CUDA failure 2: out of memory
```

**สาเหตุ:** GPU ไม่มี VRAM เพียงพอสำหรับโหลดโมเดล

**วิธีแก้ไข:**

#### ตัวเลือกที่ 1: ใช้เวอร์ชัน CPU (แนะนำ)
```python
# In your notebook, update the CATALOG to use CPU variants
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```

#### ตัวเลือกที่ 2: ใช้โมเดลขนาดเล็กบน GPU
```python
# Use only the smallest model
CATALOG = {
    'qwen2.5-0.5b': {'capabilities':['general','code','summarize','classification'],'priority':1},
}
```

#### ตัวเลือกที่ 3: ล้างหน่วยความจำ GPU
```bash
# Close other GPU-intensive applications
# Check GPU memory usage
nvidia-smi

# Restart Foundry Local service
foundry service stop
foundry service start
```

#### ตัวเลือกที่ 4: เพิ่มหน่วยความจำ GPU (ถ้าเป็นไปได้)
- ปิดแท็บเบราว์เซอร์, โปรแกรมตัดต่อวิดีโอ หรือแอปอื่นๆ ที่ใช้ GPU
- ลดเอฟเฟกต์ภาพใน Windows
- ใช้ GPU เฉพาะถ้าคุณมีทั้ง GPU แบบรวมและแบบเฉพาะ

---

### 🔴 APIConnectionError: Connection Error

**ข้อความแสดงข้อผิดพลาด:**
```
APIConnectionError: Connection error
[Retry 1/2] Setup failed for 'phi-4-mini': APIConnectionError: Connection error.
```

**สาเหตุ:** บริการ Foundry Local ไม่ได้ทำงานหรือไม่สามารถเข้าถึงได้

**วิธีแก้ไข:**

#### ขั้นตอนที่ 1: ตรวจสอบสถานะบริการ
```bash
foundry service status
```

#### ขั้นตอนที่ 2: เริ่มบริการหากหยุดทำงาน
```bash
foundry service start
```

#### ขั้นตอนที่ 3: ตรวจสอบ Endpoint
```bash
# Check what port the service is using
foundry service status

# Test with curl (adjust port if different)
curl http://localhost:59959/health
curl http://localhost:55769/health
```

#### ขั้นตอนที่ 4: โหลดโมเดลที่จำเป็น
```bash
foundry model run phi-4-mini
foundry model run qwen2.5-3b
foundry model run phi-3.5-mini
```

#### ขั้นตอนที่ 5: รีสตาร์ท Kernel ของสมุดงาน
หลังจากเริ่มบริการและโหลดโมเดลแล้ว ให้รีสตาร์ท Kernel ของสมุดงานและรันเซลล์ทั้งหมดอีกครั้ง

---

### 🔴 Model Not Found in Catalog

**ข้อความแสดงข้อผิดพลาด:**
```
ValueError: Model phi-3.5-mini-cpu not found in the catalog.
[ERROR] Model 'phi-4-mini' not found in the catalog
```

**สาเหตุ:** โมเดลยังไม่ได้ดาวน์โหลดหรือโหลดใน Foundry Local

**วิธีแก้ไข:**

#### ตัวเลือกที่ 1: ดาวน์โหลดและโหลดโมเดล
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

#### ตัวเลือกที่ 2: ใช้โหมดเลือกอัตโนมัติ
อัปเดต CATALOG ของคุณให้ใช้ชื่อโมเดลพื้นฐาน (โดยไม่มีคำต่อท้าย `-cpu`):

```python
CATALOG = {
    'phi-4-mini': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini': {'capabilities':['code','refactor'],'priority':3},
}
```

Foundry Local SDK จะเลือกเวอร์ชันที่เหมาะสมที่สุด (CPU, GPU หรือ NPU) สำหรับฮาร์ดแวร์ของคุณโดยอัตโนมัติ

---

### 🔴 HttpResponseError: 500 - Failed Loading Model

**ข้อความแสดงข้อผิดพลาด:**
```
HttpResponseError: 500 - Failed loading model
```

**สาเหตุ:** ไฟล์โมเดลเสียหายหรือไม่เข้ากันกับฮาร์ดแวร์

**วิธีแก้ไข:**

#### ดาวน์โหลดโมเดลใหม่
```bash
# Remove corrupted model
foundry model remove phi-3.5-mini

# Download fresh copy
foundry model download phi-3.5-mini
```

#### ใช้เวอร์ชันอื่น
```bash
# Try CPU variant instead
foundry model download phi-3.5-mini-cpu
```

---

### 🔴 ImportError: No Module Found

**ข้อความแสดงข้อผิดพลาด:**
```
ModuleNotFoundError: No module named 'foundry_local'
```

**สาเหตุ:** แพ็กเกจ foundry-local-sdk ยังไม่ได้ติดตั้ง

**วิธีแก้ไข:**

```bash
# Install SDK
pip install foundry-local-sdk

# Verify installation
pip show foundry-local-sdk
python -c "from foundry_local import FoundryLocalManager; print('SDK OK')"
```

---

### � การร้องขอครั้งแรกช้า

**อาการ:** การทำงานครั้งแรกใช้เวลา 30+ วินาที แต่การร้องขอครั้งถัดไปเร็ว

**สาเหตุ:** เป็นพฤติกรรมปกติ - บริการกำลังโหลดโมเดลเข้าสู่หน่วยความจำในครั้งแรก

**วิธีแก้ไข:**

#### โหลดโมเดลล่วงหน้า
```bash
# Download and load all models you'll use before running notebooks
foundry model download phi-4-mini
foundry model download qwen2.5-3b
foundry model download phi-3.5-mini

foundry model run phi-4-mini
foundry model run qwen2.5-3b
```

#### ให้บริการทำงานต่อเนื่อง
```bash
# Start service manually and leave it running
foundry service start
```

---

## ปัญหาเฉพาะในเซสชัน 04

### การตั้งค่าพอร์ตผิด

**ปัญหา:** สมุดงานเชื่อมต่อกับพอร์ตผิด (55769 vs 59959 vs 57127)

**วิธีแก้ไข:**

1. ตรวจสอบว่าพอร์ตใดที่ Foundry Local ใช้งาน:
```bash
foundry service status
# Note the port number displayed
```

2. อัปเดตเซลล์ 10 ในสมุดงาน:
```python
ENDPOINT = os.getenv('FOUNDRY_LOCAL_ENDPOINT', 'http://localhost:59959/v1')
# Replace 59959 with your actual port
```

3. รีสตาร์ท Kernel และรันเซลล์ 6, 8, 10, 12, 16, 20, 22 ใหม่

---

### การเลือกโมเดลผิด

**ปัญหา:** สมุดงานแสดง gpt-oss-20b หรือ qwen2.5-7b แทน qwen2.5-3b

**วิธีแก้ไข:**

1. รีสตาร์ท Kernel ของสมุดงาน (ล้างสถานะตัวแปรเก่า)
2. รันเซลล์ 10 ใหม่ (ตั้งค่า Model Aliases)
3. รันเซลล์ 12 ใหม่ (แสดงการตั้งค่า)
4. **ตรวจสอบ:** เซลล์ 12 ควรแสดง `LLM Model: qwen2.5-3b`

---

### เซลล์วินิจฉัยล้มเหลว

**ปัญหา:** เซลล์ 16 แสดง "❌ Foundry Local service not found!"

**วิธีแก้ไข:**

1. ตรวจสอบว่าบริการกำลังทำงาน:
```bash
foundry service status
```

2. ทดสอบ Endpoint ด้วยตนเอง:
```bash
curl http://localhost:59959/v1/models
```

3. หาก curl ใช้งานได้แต่สมุดงานไม่ทำงาน:
   - รีสตาร์ท Kernel ของสมุดงาน
   - รันเซลล์ตามลำดับ: 6, 8, 10, 12, 14, 16

4. หาก curl ใช้งานไม่ได้:
   - เริ่มบริการ: `foundry service start`
   - โหลดโมเดล: `foundry model run phi-4-mini` และ `foundry model run qwen2.5-3b`

---

### การตรวจสอบเบื้องต้นล้มเหลว

**ปัญหา:** เซลล์ 20 แสดงข้อผิดพลาดการเชื่อมต่อแม้ว่าการวินิจฉัยจะผ่านแล้ว

**วิธีแก้ไข:**

1. ตรวจสอบว่าโมเดลถูกโหลดแล้ว:
```bash
foundry model ls
# Should show phi-4-mini and qwen2.5-3b
```

2. หากโมเดลหายไป:
```bash
foundry model run phi-4-mini
foundry model run qwen2.5-3b
```

3. รันเซลล์ 20 ใหม่หลังจากโหลดโมเดลแล้ว

---

### การเปรียบเทียบล้มเหลวด้วยค่า None

**ปัญหา:** เซลล์ 22 ทำงานเสร็จแต่แสดงเวลาแฝงเป็น None

**วิธีแก้ไข:**

1. ตรวจสอบว่าการตรวจสอบเบื้องต้นผ่านแล้ว (เซลล์ 20)
2. รันเซลล์ 22 ใหม่ - โมเดลอาจต้องการเวลาในการโหลดในคำขอแรก
3. ตรวจสอบว่าโมเดลทั้งสองถูกโหลด: `foundry model ls`

---

## ปัญหาเฉพาะในเซสชัน 05

### เอเจนต์ใช้โมเดลผิด

**ปัญหา:** เอเจนต์ไม่ได้ใช้โมเดลที่คาดหวัง

**วิธีแก้ไข:**

ตรวจสอบการตั้งค่า:
```python
# Check which models are assigned
print(f"Researcher: {researcher.model_id}")
print(f"Editor: {editor.model_id}")
```

รีสตาร์ท Kernel หากโมเดลไม่ถูกต้อง

---

### Memory Context Overflow

**ปัญหา:** การตอบกลับของเอเจนต์ลดคุณภาพลงเมื่อเวลาผ่านไป

**วิธีแก้ไข:** ได้รับการจัดการโดยอัตโนมัติแล้ว - เอเจนต์จะเก็บข้อความล่าสุดเพียง 6 ข้อความในหน่วยความจำ

---

## ปัญหาเฉพาะในเซสชัน 06

### ความสับสนระหว่างโมเดล CPU และ GPU

**ปัญหา:** เกิดข้อผิดพลาด CUDA เมื่อใช้การตั้งค่าเริ่มต้น

**วิธีแก้ไข:** การตั้งค่าเริ่มต้นตอนนี้ใช้โมเดล CPU หากคุณพบข้อผิดพลาด CUDA:

1. ตรวจสอบว่าคุณกำลังใช้ CATALOG CPU เริ่มต้น:
```python
# Cell should show CPU variants
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```

2. รีสตาร์ท Kernel และรันเซลล์ทั้งหมดใหม่

---

### การตรวจจับเจตนาไม่ทำงาน

**ปัญหา:** Prompt ถูกส่งไปยังโมเดลผิด

**วิธีแก้ไข:**

ทดสอบการตรวจจับเจตนา:
```python
# Run the intent detection test cell
for prompt in test_prompts:
    intent = detect_intent(prompt)
    print(f"{prompt[:50]}... → {intent}")
```

อัปเดต RULES หากรูปแบบต้องการการปรับเปลี่ยน

---

## ปัญหาเฉพาะฮาร์ดแวร์

### NVIDIA GPU

**ตรวจสอบสถานะ GPU:**
```bash
nvidia-smi
```

**ปัญหาทั่วไป:**
- **ไดรเวอร์ล้าสมัย**: อัปเดตไดรเวอร์ NVIDIA
- **CUDA เวอร์ชันไม่ตรงกัน**: ติดตั้ง Foundry Local ใหม่
- **หน่วยความจำ GPU กระจัดกระจาย**: รีสตาร์ทระบบ

### Qualcomm NPU

**ตรวจสอบสถานะ NPU:**
```bash
foundry device info
```

**ปัญหาทั่วไป:**
- **ไม่ได้ติดตั้งไดรเวอร์ NPU**: ติดตั้งไดรเวอร์ Qualcomm NPU
- **ไม่มีเวอร์ชัน NPU**: ใช้เวอร์ชัน CPU
- **Windows เวอร์ชันเก่าเกินไป**: อัปเดตเป็น Windows 11 เวอร์ชันล่าสุด

### ระบบที่ใช้เฉพาะ CPU

**โมเดลที่แนะนำ:**
```python
CATALOG = {
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','general'],'priority':2},
}
```

**เคล็ดลับการเพิ่มประสิทธิภาพ:**
- ใช้โมเดลที่เล็กที่สุด
- ลด max_tokens
- อดทนกับการร้องขอครั้งแรก

---

## คำสั่งวินิจฉัย

### ตรวจสอบทุกอย่าง
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

### ใน Python
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

## การขอความช่วยเหลือ

### 1. ตรวจสอบบันทึก
```bash
# Windows
foundry service logs

# Or check Windows Event Viewer
# Application Logs -> Microsoft-FoundryLocal
```

### 2. ปัญหาใน GitHub
- ค้นหาปัญหาที่มีอยู่: https://github.com/microsoft/Foundry-Local/issues
- สร้างปัญหาใหม่พร้อม:
  - ข้อความแสดงข้อผิดพลาด (ข้อความเต็ม)
  - ผลลัพธ์ของ `foundry service status`
  - ผลลัพธ์ของ `foundry --version`
  - ข้อมูล GPU/NPU (nvidia-smi ฯลฯ)
  - ขั้นตอนการทำซ้ำปัญหา

### 3. เอกสาร
- **ที่เก็บหลัก**: https://github.com/microsoft/Foundry-Local
- **Python SDK**: https://github.com/microsoft/Foundry-Local/tree/main/sdk/python
- **CLI Reference**: https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-cli.md
- **การแก้ปัญหา**: https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-troubleshooting.md

---

## เช็คลิสต์การแก้ไขด่วน

เมื่อเกิดปัญหา ลองทำตามลำดับนี้:

- [ ] ตรวจสอบว่าบริการกำลังทำงาน: `foundry service status`
- [ ] รีสตาร์ทบริการ: `foundry service stop && foundry service start`
- [ ] ตรวจสอบว่าโมเดลมีอยู่: `foundry model ls | grep phi-4-mini`
- [ ] โหลดโมเดลที่จำเป็น: `foundry model run phi-4-mini`
- [ ] ตรวจสอบหน่วยความจำ GPU: `nvidia-smi` (ถ้าใช้ NVIDIA)
- [ ] ลองใช้เวอร์ชัน CPU: ใช้ `phi-4-mini-cpu` แทน `phi-4-mini`
- [ ] รีสตาร์ท Kernel ของสมุดงาน
- [ ] ล้างผลลัพธ์ของสมุดงานและรันเซลล์ทั้งหมดใหม่
- [ ] ติดตั้ง SDK ใหม่: `pip install --upgrade --force-reinstall foundry-local-sdk`
- [ ] รีบูตระบบ (เป็นทางเลือกสุดท้าย)

---

## เคล็ดลับป้องกันปัญหา

### แนวทางปฏิบัติที่ดีที่สุด

1. **ตรวจสอบบริการเสมอ:**
   ```bash
   foundry service status
   ```

2. **ใช้เวอร์ชัน CPU เป็นค่าเริ่มต้น:**
   ```python
   CATALOG = {
       'phi-4-mini-cpu': {...},
       'qwen2.5-0.5b-cpu': {...},
   }
   ```

3. **โหลดโมเดลล่วงหน้าก่อนรันสมุดงาน:**
   ```bash
   foundry model run phi-4-mini
   foundry model run qwen2.5-3b
   ```

4. **ให้บริการทำงานต่อเนื่อง:**
   - อย่าหยุด/เริ่มบริการโดยไม่จำเป็น
   - ให้บริการทำงานในพื้นหลังระหว่างเซสชัน

5. **ตรวจสอบทรัพยากร:**
   - ตรวจสอบหน่วยความจำ GPU ก่อนรัน
   - ปิดแอปพลิเคชัน GPU ที่ไม่จำเป็น
   - ใช้ Task Manager / nvidia-smi

6. **อัปเดตเป็นประจำ:**
   ```bash
   winget upgrade Microsoft.FoundryLocal
   pip install --upgrade foundry-local-sdk
   ```

---

**อัปเดตล่าสุด:** 8 ตุลาคม 2025

---

**ข้อจำกัดความรับผิดชอบ**:  
เอกสารนี้ได้รับการแปลโดยใช้บริการแปลภาษา AI [Co-op Translator](https://github.com/Azure/co-op-translator) แม้ว่าเราจะพยายามให้การแปลมีความถูกต้อง แต่โปรดทราบว่าการแปลอัตโนมัติอาจมีข้อผิดพลาดหรือความไม่ถูกต้อง เอกสารต้นฉบับในภาษาต้นทางควรถือเป็นแหล่งข้อมูลที่เชื่อถือได้ สำหรับข้อมูลที่สำคัญ แนะนำให้ใช้บริการแปลภาษามนุษย์ที่เป็นมืออาชีพ เราไม่รับผิดชอบต่อความเข้าใจผิดหรือการตีความผิดพลาดที่เกิดจากการใช้การแปลนี้