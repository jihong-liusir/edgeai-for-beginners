<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "ddaad917d0c16fc3d498a6b4eabc8088",
  "translation_date": "2025-10-09T13:21:06+00:00",
  "source_file": "Workshop/notebooks/quickstart.md",
  "language_code": "th"
}
-->
# คู่มือเริ่มต้นใช้งาน Workshop Notebooks

## สารบัญ

- [ข้อกำหนดเบื้องต้น](../../../../Workshop/notebooks)
- [การตั้งค่าเริ่มต้น](../../../../Workshop/notebooks)
- [เซสชัน 04: การเปรียบเทียบโมเดล](../../../../Workshop/notebooks)
- [เซสชัน 05: การจัดการหลายเอเจนต์](../../../../Workshop/notebooks)
- [เซสชัน 06: การจัดเส้นทางโมเดลตามเจตนา](../../../../Workshop/notebooks)
- [ตัวแปรสภาพแวดล้อม](../../../../Workshop/notebooks)
- [คำสั่งทั่วไป](../../../../Workshop/notebooks)

---

## ข้อกำหนดเบื้องต้น

### 1. ติดตั้ง Foundry Local

**Windows:**
```bash
winget install Microsoft.FoundryLocal
```

**macOS:**
```bash
brew tap microsoft/foundrylocal
brew install foundrylocal
```

**ตรวจสอบการติดตั้ง:**
```bash
foundry --version
```

### 2. ติดตั้งไลบรารี Python

```bash
cd Workshop
pip install -r requirements.txt
```

หรือเลือกติดตั้งทีละตัว:
```bash
pip install foundry-local-sdk openai numpy requests
```

---

## การตั้งค่าเริ่มต้น

### เริ่มบริการ Foundry Local

**จำเป็นต้องทำก่อนใช้งานโน้ตบุ๊กใดๆ:**

```bash
# Start the service
foundry service start

# Verify it's running
foundry service status
```

ผลลัพธ์ที่คาดหวัง:
```
✅ Service started successfully
Endpoint: http://localhost:59959
```

### ดาวน์โหลดและโหลดโมเดล

โน้ตบุ๊กจะใช้โมเดลเหล่านี้เป็นค่าเริ่มต้น:

```bash
# Download models (first time only - may take several minutes)
foundry model download phi-4-mini
foundry model download qwen2.5-3b
foundry model download phi-3.5-mini
foundry model download qwen2.5-0.5b

# Load models into memory
foundry model run phi-4-mini
foundry model run qwen2.5-3b
foundry model run phi-3.5-mini
```

### ตรวจสอบการตั้งค่า

```bash
# List loaded models
foundry model ls

# Check service health
curl http://localhost:59959/v1/models
```

---

## เซสชัน 04: การเปรียบเทียบโมเดล

### วัตถุประสงค์
เปรียบเทียบประสิทธิภาพระหว่าง Small Language Models (SLM) และ Large Language Models (LLM)

### การตั้งค่าอย่างรวดเร็ว

```bash
# Start service (if not already running)
foundry service start

# Load required models
foundry model run phi-4-mini
foundry model run qwen2.5-3b
```

### การใช้งานโน้ตบุ๊ก

1. **เปิด** `session04_model_compare.ipynb` ใน VS Code หรือ Jupyter
2. **รีสตาร์ทเคอร์เนล** (Kernel → Restart Kernel)
3. **รันทุกเซลล์** ตามลำดับ

### การตั้งค่าหลัก

**โมเดลเริ่มต้น:**
- **SLM:** `phi-4-mini` (~4GB RAM, เร็วกว่า)
- **LLM:** `qwen2.5-3b` (~3GB RAM, ใช้หน่วยความจำอย่างมีประสิทธิภาพ)

**ตัวแปรสภาพแวดล้อม (ไม่บังคับ):**
```python
import os
os.environ['SLM_ALIAS'] = 'phi-4-mini'
os.environ['LLM_ALIAS'] = 'qwen2.5-3b'
os.environ['FOUNDRY_LOCAL_ENDPOINT'] = 'http://localhost:59959/v1'
```

### ผลลัพธ์ที่คาดหวัง

```
================================================================================
COMPARISON SUMMARY
================================================================================
Alias                Latency(s)      Tokens     Route               
--------------------------------------------------------------------------------
phi-4-mini           1.234           150        chat.completions    
qwen2.5-3b           2.456           180        chat.completions    
================================================================================

💡 SLM is 1.99x faster than LLM for this prompt
```

### การปรับแต่ง

**ใช้โมเดลอื่น:**
```python
os.environ['SLM_ALIAS'] = 'phi-3.5-mini'
os.environ['LLM_ALIAS'] = 'qwen2.5-1.5b'
```

**ปรับแต่งคำสั่ง:**
```python
os.environ['COMPARE_PROMPT'] = 'Explain quantum computing in simple terms'
```

### เช็คลิสต์การตรวจสอบ

- [ ] เซลล์ 12 แสดงโมเดลที่ถูกต้อง (phi-4-mini, qwen2.5-3b)
- [ ] เซลล์ 12 แสดงเอ็นด์พอยต์ที่ถูกต้อง (พอร์ต 59959)
- [ ] เซลล์ 16 การวินิจฉัยผ่าน (✅ บริการกำลังทำงาน)
- [ ] เซลล์ 20 การตรวจสอบเบื้องต้นผ่าน (ทั้งสองโมเดลโอเค)
- [ ] เซลล์ 22 การเปรียบเทียบเสร็จสมบูรณ์พร้อมค่าความหน่วง
- [ ] เซลล์ 24 การตรวจสอบแสดง 🎉 ALL CHECKS PASSED!

### ระยะเวลาที่คาดการณ์
- **ครั้งแรก:** 5-10 นาที (รวมการดาวน์โหลดโมเดล)
- **ครั้งถัดไป:** 1-2 นาที

---

## เซสชัน 05: การจัดการหลายเอเจนต์

### วัตถุประสงค์
แสดงการทำงานร่วมกันของหลายเอเจนต์โดยใช้ Foundry Local SDK - เอเจนต์ทำงานร่วมกันเพื่อสร้างผลลัพธ์ที่ปรับปรุงแล้ว

### การตั้งค่าอย่างรวดเร็ว

```bash
# Start service
foundry service start

# Load models
foundry model run phi-4-mini  # Primary model
foundry model run qwen2.5-7b  # Optional: higher quality editor
```

### การใช้งานโน้ตบุ๊ก

1. **เปิด** `session05_agents_orchestrator.ipynb`
2. **รีสตาร์ทเคอร์เนล**
3. **รันทุกเซลล์** ตามลำดับ

### การตั้งค่าหลัก

**การตั้งค่าเริ่มต้น (ใช้โมเดลเดียวกันสำหรับทั้งสองเอเจนต์):**
```python
PRIMARY_ALIAS = 'phi-4-mini'
EDITOR_ALIAS = 'phi-4-mini'  # Uses same model
```

**การตั้งค่าขั้นสูง (ใช้โมเดลต่างกัน):**
```python
import os
os.environ['AGENT_MODEL_PRIMARY'] = 'phi-4-mini'     # Fast for research
os.environ['AGENT_MODEL_EDITOR'] = 'qwen2.5-7b'      # High quality for editing
```

### สถาปัตยกรรม

```
User Question
    ↓
Researcher Agent (phi-4-mini)
  → Gathers bullet points
    ↓
Editor Agent (phi-4-mini or qwen2.5-7b)
  → Refines into executive summary
    ↓
Final Output
```

### ผลลัพธ์ที่คาดหวัง

```
================================================================================
[Pipeline] Question: Explain why edge AI matters for compliance.
================================================================================

[Stage 1: Research]
Output: • Edge AI processes data locally, reducing transmission...

[Stage 2: Editorial Refinement]
Output: Executive Summary: Edge AI enhances compliance by keeping data...

[FINAL OUTPUT]
Executive Summary: Edge AI enhances compliance by keeping sensitive data 
on-premises and reduces latency through local processing.

[METADATA]
Models used: {'researcher': 'phi-4-mini', 'editor': 'phi-4-mini'}
```

### การขยาย

**เพิ่มเอเจนต์เพิ่มเติม:**
```python
critic = Agent(
    name='Critic',
    system='Review content for accuracy',
    client=client,
    model_id=model_id
)
```

**การทดสอบแบบแบตช์:**
```python
test_questions = [
    "What are benefits of local AI?",
    "How does RAG improve accuracy?",
]

for q in test_questions:
    result = pipeline(q, verbose=False)
    print(result['final'])
```

### ระยะเวลาที่คาดการณ์
- **ครั้งแรก:** 3-5 นาที
- **ครั้งถัดไป:** 1-2 นาทีต่อคำถาม

---

## เซสชัน 06: การจัดเส้นทางโมเดลตามเจตนา

### วัตถุประสงค์
จัดเส้นทางคำสั่งไปยังโมเดลเฉพาะทางอย่างชาญฉลาดตามเจตนาที่ตรวจพบ

### การตั้งค่าอย่างรวดเร็ว

```bash
# Start service
foundry service start

# Load all routing models (CPU variants recommended)
foundry model run phi-4-mini-cpu
foundry model run qwen2.5-0.5b-cpu
foundry model run phi-3.5-mini-cpu
```

**หมายเหตุ:** เซสชัน 06 ใช้โมเดล CPU เป็นค่าเริ่มต้นเพื่อความเข้ากันได้สูงสุด

### การใช้งานโน้ตบุ๊ก

1. **เปิด** `session06_models_router.ipynb`
2. **รีสตาร์ทเคอร์เนล**
3. **รันทุกเซลล์** ตามลำดับ

### การตั้งค่าหลัก

**แคตตาล็อกเริ่มต้น (โมเดล CPU):**
```python
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```

**ทางเลือก (โมเดล GPU):**
```python
# Uncomment GPU catalog in Cell #6 if you have sufficient VRAM (8GB+)
CATALOG = {
    'phi-4-mini': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini': {'capabilities':['code','refactor'],'priority':3},
}
```

### การตรวจจับเจตนา

Router ใช้รูปแบบ regex ในการตรวจจับเจตนา:

| เจตนา | ตัวอย่างรูปแบบ | เส้นทางที่จัด |
|-------|-----------------|---------------|
| `code` | "refactor", "implement function" | phi-3.5-mini-cpu |
| `classification` | "categorize", "classify this" | qwen2.5-0.5b-cpu |
| `summarize` | "summarize", "tl;dr" | phi-4-mini-cpu |
| `general` | อื่นๆ ทั้งหมด | phi-4-mini-cpu |

### ผลลัพธ์ที่คาดหวัง

```
✓ Using CPU-optimized models (default configuration)
  Models: phi-4-mini-cpu, qwen2.5-0.5b-cpu, phi-3.5-mini-cpu

Routing prompts to specialized models...
============================================================

Prompt: Refactor this Python function for readability
  Intent: code           | Model: phi-3.5-mini-cpu
  Output: Here's a refactored version...
  Tokens: 156

Prompt: Categorize this email as urgent or normal
  Intent: classification | Model: qwen2.5-0.5b-cpu
  Output: Category: Normal
  Tokens: 45

✓ Success! All prompts routed correctly.
```

### การปรับแต่ง

**เพิ่มเจตนาใหม่:**
```python
import re

# Add to RULES
RULES.append((re.compile('translate|翻译', re.I), 'translation'))

# Add capability to catalog
CATALOG['phi-4-mini-cpu']['capabilities'].append('translation')
```

**เปิดใช้งานการติดตามโทเค็น:**
```python
import os
os.environ['SHOW_USAGE'] = '1'
```

### การเปลี่ยนไปใช้โมเดล GPU

หากคุณมี VRAM 8GB ขึ้นไป:

1. ใน **เซลล์ #6** ให้คอมเมนต์แคตตาล็อก CPU
2. ยกเลิกคอมเมนต์แคตตาล็อก GPU
3. โหลดโมเดล GPU:
   ```bash
   foundry model run phi-4-mini
   foundry model run qwen2.5-0.5b
   foundry model run phi-3.5-mini
   ```
4. รีสตาร์ทเคอร์เนลและรันโน้ตบุ๊กใหม่

### ระยะเวลาที่คาดการณ์
- **ครั้งแรก:** 5-10 นาที (โหลดโมเดล)
- **ครั้งถัดไป:** 30-60 วินาทีต่อการทดสอบ

---

## ตัวแปรสภาพแวดล้อม

### การตั้งค่าทั่วไป

ตั้งค่าก่อนเริ่ม Jupyter/VS Code:

**Windows (Command Prompt):**
```cmd
set FOUNDRY_LOCAL_ENDPOINT=http://localhost:59959/v1
set SHOW_USAGE=1
set RETRY_ON_FAIL=1
```

**Windows (PowerShell):**
```powershell
$env:FOUNDRY_LOCAL_ENDPOINT="http://localhost:59959/v1"
$env:SHOW_USAGE="1"
$env:RETRY_ON_FAIL="1"
```

**macOS/Linux:**
```bash
export FOUNDRY_LOCAL_ENDPOINT=http://localhost:59959/v1
export SHOW_USAGE=1
export RETRY_ON_FAIL=1
```

### การตั้งค่าในโน้ตบุ๊ก

ตั้งค่าในตอนเริ่มต้นของโน้ตบุ๊กใดๆ:

```python
import os

# Foundry Local configuration
os.environ['FOUNDRY_LOCAL_ENDPOINT'] = 'http://localhost:59959/v1'

# Model selection
os.environ['SLM_ALIAS'] = 'phi-4-mini'
os.environ['LLM_ALIAS'] = 'qwen2.5-3b'

# Agent models
os.environ['AGENT_MODEL_PRIMARY'] = 'phi-4-mini'
os.environ['AGENT_MODEL_EDITOR'] = 'qwen2.5-7b'

# Debugging
os.environ['SHOW_USAGE'] = '1'       # Show token usage
os.environ['RETRY_ON_FAIL'] = '1'    # Enable retries
os.environ['RETRY_BACKOFF'] = '2.0'  # Retry delay
```

---

## คำสั่งทั่วไป

### การจัดการบริการ

```bash
# Start service
foundry service start

# Check status
foundry service status

# Stop service
foundry service stop

# View logs
foundry service logs
```

### การจัดการโมเดล

```bash
# List all available models in catalog
foundry model catalog

# List loaded models
foundry model ls

# Download a model
foundry model download phi-4-mini

# Load a model
foundry model run phi-4-mini

# Unload a model
foundry model unload phi-4-mini

# Remove a model
foundry model remove phi-4-mini

# Get model info
foundry model info phi-4-mini
```

### การทดสอบเอ็นด์พอยต์

```bash
# Check service health
curl http://localhost:59959/health

# List available models via API
curl http://localhost:59959/v1/models

# Test model completion
curl http://localhost:59959/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "phi-4-mini",
    "messages": [{"role":"user","content":"Hello"}],
    "max_tokens": 50
  }'
```

### คำสั่งวินิจฉัย

```bash
# Check everything
foundry --version
foundry service status
foundry model ls
foundry device info

# GPU status (NVIDIA)
nvidia-smi

# NPU status (Qualcomm)
foundry device info
```

---

## แนวทางปฏิบัติที่ดีที่สุด

### ก่อนเริ่มโน้ตบุ๊กใดๆ

1. **ตรวจสอบว่าบริการกำลังทำงาน:**
   ```bash
   foundry service status
   ```

2. **ตรวจสอบว่าโมเดลถูกโหลดแล้ว:**
   ```bash
   foundry model ls
   ```

3. **รีสตาร์ทเคอร์เนล** หากรันใหม่

4. **ล้างผลลัพธ์ทั้งหมด** เพื่อการรันที่สะอาด

### การจัดการทรัพยากร

1. **ใช้โมเดล CPU เป็นค่าเริ่มต้น** เพื่อความเข้ากันได้
2. **เปลี่ยนไปใช้โมเดล GPU** เฉพาะเมื่อคุณมี VRAM 8GB ขึ้นไป
3. **ปิดแอปพลิเคชัน GPU อื่นๆ** ก่อนใช้งาน
4. **รักษาบริการให้ทำงาน** ระหว่างเซสชันโน้ตบุ๊ก
5. **ตรวจสอบการใช้งานทรัพยากร** ด้วย Task Manager / nvidia-smi

### การแก้ไขปัญหา

1. **ตรวจสอบบริการก่อนเสมอ** ก่อนแก้ไขโค้ด
2. **รีสตาร์ทเคอร์เนล** หากเห็นการตั้งค่าที่ค้าง
3. **รันเซลล์วินิจฉัยใหม่** หลังจากมีการเปลี่ยนแปลง
4. **ตรวจสอบชื่อโมเดล** ให้ตรงกับที่โหลด
5. **ตรวจสอบพอร์ตเอ็นด์พอยต์** ให้ตรงกับสถานะบริการ

---

## อ้างอิงด่วน: ชื่อย่อโมเดล

### โมเดลทั่วไป

| ชื่อย่อ | ขนาด | เหมาะสำหรับ | RAM/VRAM | ตัวแปร |
|---------|------|-------------|----------|--------|
| `phi-4-mini` | ~4B | แชททั่วไป, สรุป | 4-6GB | `-cpu`, `-cuda-gpu`, `-npu` |
| `phi-3.5-mini` | ~3.5B | การสร้างโค้ด, การปรับปรุงโค้ด | 3-5GB | `-cpu`, `-cuda-gpu`, `-npu` |
| `qwen2.5-3b` | ~3B | งานทั่วไป, มีประสิทธิภาพ | 3-4GB | `-cpu`, `-cuda-gpu` |
| `qwen2.5-1.5b` | ~1.5B | เร็ว, ใช้ทรัพยากรต่ำ | 2-3GB | `-cpu`, `-cuda-gpu` |
| `qwen2.5-0.5b` | ~0.5B | การจัดประเภท, ใช้ทรัพยากรน้อยที่สุด | 1-2GB | `-cpu`, `-cuda-gpu` |

### การตั้งชื่อตัวแปร

- **ชื่อฐาน** (เช่น `phi-4-mini`): เลือกตัวแปรที่ดีที่สุดสำหรับฮาร์ดแวร์ของคุณโดยอัตโนมัติ
- **`-cpu`**: ปรับแต่งสำหรับ CPU, ใช้งานได้ทุกที่
- **`-cuda-gpu`**: ปรับแต่งสำหรับ NVIDIA GPU, ต้องการ VRAM 8GB ขึ้นไป
- **`-npu`**: ปรับแต่งสำหรับ Qualcomm NPU, ต้องการไดรเวอร์ NPU

**คำแนะนำ:** ใช้ชื่อฐาน (ไม่มีคำต่อท้าย) และให้ Foundry Local เลือกตัวแปรที่ดีที่สุดโดยอัตโนมัติ

---

## ตัวชี้วัดความสำเร็จ

คุณพร้อมเมื่อเห็น:

✅ `foundry service status` แสดง "running"  
✅ `foundry model ls` แสดงโมเดลที่คุณต้องการ  
✅ บริการเข้าถึงได้ที่เอ็นด์พอยต์ที่ถูกต้อง  
✅ การตรวจสอบสุขภาพคืนค่า 200 OK  
✅ เซลล์วินิจฉัยในโน้ตบุ๊กผ่าน  
✅ ไม่มีข้อผิดพลาดการเชื่อมต่อในผลลัพธ์  

---

## การขอความช่วยเหลือ

### เอกสาร
- **ที่เก็บหลัก**: https://github.com/microsoft/Foundry-Local  
- **Python SDK**: https://github.com/microsoft/Foundry-Local/tree/main/sdk/python  
- **CLI Reference**: https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-cli.md  
- **การแก้ไขปัญหา**: ดู `troubleshooting.md` ในไดเรกทอรีนี้  

### ปัญหาใน GitHub
- https://github.com/microsoft/Foundry-Local/issues  
- https://github.com/microsoft/edgeai-for-beginners/issues  

---

**อัปเดตล่าสุด:** 8 ตุลาคม 2025  
**เวอร์ชัน:** Workshop Notebooks 2.0  

---

**ข้อจำกัดความรับผิดชอบ**:  
เอกสารนี้ได้รับการแปลโดยใช้บริการแปลภาษา AI [Co-op Translator](https://github.com/Azure/co-op-translator) แม้ว่าเราจะพยายามให้การแปลมีความถูกต้อง แต่โปรดทราบว่าการแปลโดยอัตโนมัติอาจมีข้อผิดพลาดหรือความไม่ถูกต้อง เอกสารต้นฉบับในภาษาดั้งเดิมควรถือเป็นแหล่งข้อมูลที่เชื่อถือได้ สำหรับข้อมูลที่สำคัญ ขอแนะนำให้ใช้บริการแปลภาษามืออาชีพ เราไม่รับผิดชอบต่อความเข้าใจผิดหรือการตีความผิดที่เกิดจากการใช้การแปลนี้