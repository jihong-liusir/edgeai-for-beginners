<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "48d0fb38be925084a6ebd957d4b045e5",
  "translation_date": "2025-10-09T13:01:42+00:00",
  "source_file": "Workshop/Readme.md",
  "language_code": "th"
}
-->
# EdgeAI สำหรับผู้เริ่มต้น - Workshop

> **เส้นทางการเรียนรู้แบบลงมือทำเพื่อสร้างแอปพลิเคชัน Edge AI ที่พร้อมใช้งานจริง**
>
> เรียนรู้การใช้งาน AI ในพื้นที่ด้วย Microsoft Foundry Local ตั้งแต่การสร้างแชทครั้งแรกไปจนถึงการจัดการหลายเอเจนต์ใน 6 เซสชันที่พัฒนาขึ้นอย่างต่อเนื่อง

---

## 🎯 บทนำ

ยินดีต้อนรับสู่ **EdgeAI สำหรับผู้เริ่มต้น Workshop** - คู่มือการเรียนรู้แบบลงมือทำเพื่อสร้างแอปพลิเคชันอัจฉริยะที่ทำงานบนฮาร์ดแวร์ในพื้นที่ทั้งหมด Workshop นี้จะเปลี่ยนแนวคิด Edge AI เชิงทฤษฎีให้กลายเป็นทักษะในโลกจริงผ่านการฝึกฝนที่ท้าทายมากขึ้นเรื่อย ๆ โดยใช้ Microsoft Foundry Local และ Small Language Models (SLMs)

### ทำไมต้อง Workshop นี้?

**การปฏิวัติ Edge AI มาถึงแล้ว**

องค์กรทั่วโลกกำลังเปลี่ยนจาก AI ที่พึ่งพา Cloud ไปสู่ Edge Computing ด้วยเหตุผลสำคัญสามประการ:

1. **ความเป็นส่วนตัวและการปฏิบัติตามกฎระเบียบ** - ประมวลผลข้อมูลที่ละเอียดอ่อนในพื้นที่โดยไม่ต้องส่งผ่าน Cloud (HIPAA, GDPR, กฎระเบียบทางการเงิน)
2. **ประสิทธิภาพ** - ขจัดความล่าช้าของเครือข่าย (50-500ms ในพื้นที่เทียบกับ 500-2000ms รอบการส่งข้อมูลผ่าน Cloud)
3. **การควบคุมต้นทุน** - ลดค่าใช้จ่าย API ต่อ Token และขยายขนาดโดยไม่ต้องเสียค่าใช้จ่าย Cloud

**แต่ Edge AI นั้นแตกต่าง**

การใช้งาน AI ในพื้นที่ต้องการทักษะใหม่:
- การเลือกและปรับแต่งโมเดลให้เหมาะสมกับข้อจำกัดของทรัพยากร
- การจัดการบริการในพื้นที่และการเร่งความเร็วฮาร์ดแวร์
- การออกแบบ Prompt สำหรับโมเดลขนาดเล็ก
- รูปแบบการใช้งานจริงสำหรับอุปกรณ์ Edge

**Workshop นี้มอบทักษะเหล่านั้นให้คุณ**

ใน 6 เซสชันที่มุ่งเน้น (~3 ชั่วโมงทั้งหมด) คุณจะก้าวจาก "Hello World" ไปสู่การใช้งานระบบหลายเอเจนต์ที่พร้อมใช้งานจริง - ทั้งหมดทำงานในพื้นที่บนเครื่องของคุณ

---

## 📚 วัตถุประสงค์การเรียนรู้

เมื่อจบ Workshop นี้ คุณจะสามารถ:

### ทักษะหลัก
1. **ใช้งานและจัดการบริการ AI ในพื้นที่**
   - ติดตั้งและกำหนดค่า Microsoft Foundry Local
   - เลือกโมเดลที่เหมาะสมสำหรับการใช้งานในพื้นที่
   - จัดการวงจรชีวิตของโมเดล (ดาวน์โหลด, โหลด, แคช)
   - ตรวจสอบการใช้งานทรัพยากรและปรับปรุงประสิทธิภาพ

2. **สร้างแอปพลิเคชันที่ขับเคลื่อนด้วย AI**
   - ใช้งานแชทที่เข้ากันได้กับ OpenAI ในพื้นที่
   - ออกแบบ Prompt ที่มีประสิทธิภาพสำหรับ Small Language Models
   - จัดการการตอบสนองแบบ Streaming เพื่อ UX ที่ดียิ่งขึ้น
   - ผสานโมเดลในพื้นที่เข้ากับแอปพลิเคชันที่มีอยู่

3. **สร้างระบบ RAG (Retrieval Augmented Generation)**
   - สร้างการค้นหาเชิงความหมายด้วย Embeddings
   - เชื่อมโยงการตอบสนองของ LLM กับความรู้เฉพาะด้าน
   - ประเมินคุณภาพ RAG ด้วยเมตริกมาตรฐานอุตสาหกรรม
   - ขยายจากต้นแบบไปสู่การใช้งานจริง

4. **ปรับปรุงประสิทธิภาพของโมเดล**
   - ทดสอบโมเดลหลายตัวสำหรับกรณีการใช้งานของคุณ
   - วัดความล่าช้า, ความเร็วในการประมวลผล, และเวลาตอบสนองแรก
   - เลือกโมเดลที่เหมาะสมที่สุดตามการแลกเปลี่ยนระหว่างความเร็วและคุณภาพ
   - เปรียบเทียบข้อดีข้อเสียระหว่าง SLM และ LLM ในสถานการณ์จริง

5. **จัดการระบบหลายเอเจนต์**
   - ออกแบบเอเจนต์เฉพาะสำหรับงานต่าง ๆ
   - ใช้งานหน่วยความจำและการจัดการบริบทของเอเจนต์
   - ประสานงานเอเจนต์ในกระบวนการที่ซับซ้อน
   - จัดการคำขออย่างชาญฉลาดระหว่างโมเดลหลายตัว

6. **ใช้งานโซลูชันที่พร้อมใช้งานจริง**
   - ใช้งานการจัดการข้อผิดพลาดและตรรกะการลองใหม่
   - ตรวจสอบการใช้งาน Token และทรัพยากรระบบ
   - สร้างสถาปัตยกรรมที่สามารถขยายได้ด้วยรูปแบบ Model-as-Tools
   - วางแผนเส้นทางการย้ายจาก Edge ไปสู่ Hybrid (Edge + Cloud)

---

## 🎓 ผลลัพธ์การเรียนรู้

### สิ่งที่คุณจะสร้าง

เมื่อจบ Workshop นี้ คุณจะได้สร้าง:

| เซสชัน | ผลงาน | ทักษะที่แสดง |
|--------|-------|--------------|
| **1** | แอปพลิเคชันแชทพร้อมการตอบสนองแบบ Streaming | การตั้งค่าบริการ, การตอบสนองพื้นฐาน, UX แบบ Streaming |
| **2** | ระบบ RAG พร้อมการประเมินผล | Embeddings, การค้นหาเชิงความหมาย, เมตริกคุณภาพ |
| **3** | ชุดทดสอบเปรียบเทียบโมเดลหลายตัว | การวัดประสิทธิภาพ, การเปรียบเทียบโมเดล |
| **4** | ตัวเปรียบเทียบ SLM กับ LLM | การวิเคราะห์ข้อแลกเปลี่ยน, กลยุทธ์การปรับปรุง |
| **5** | ระบบจัดการหลายเอเจนต์ | การออกแบบเอเจนต์, การจัดการหน่วยความจำ, การประสานงาน |
| **6** | ระบบการจัดการคำขออัจฉริยะ | การตรวจจับเจตนา, การเลือกโมเดล, การขยายขนาด |

### ตารางทักษะ

| ระดับทักษะ | เซสชัน 1-2 | เซสชัน 3-4 | เซสชัน 5-6 |
|-------------|------------|------------|------------|
| **ผู้เริ่มต้น** | ✅ การตั้งค่าและพื้นฐาน | ⚠️ ท้าทาย | ❌ ขั้นสูงเกินไป |
| **ระดับกลาง** | ✅ ทบทวนเร็ว | ✅ การเรียนรู้หลัก | ⚠️ เป้าหมายที่ยืดหยุ่น |
| **ขั้นสูง** | ✅ ผ่านได้ง่าย | ✅ การปรับปรุง | ✅ รูปแบบการใช้งานจริง |

### ทักษะพร้อมใช้งานในอาชีพ

**หลังจาก Workshop นี้ คุณจะพร้อมที่จะ:**

✅ **สร้างแอปพลิเคชันที่เน้นความเป็นส่วนตัว**
- แอปด้านสุขภาพที่จัดการ PHI/PII ในพื้นที่
- บริการทางการเงินที่ปฏิบัติตามข้อกำหนด
- ระบบรัฐบาลที่ต้องการความเป็นเจ้าของข้อมูล

✅ **ปรับให้เหมาะสมกับสภาพแวดล้อม Edge**
- อุปกรณ์ IoT ที่มีทรัพยากรจำกัด
- แอปพลิเคชันมือถือที่เน้นการทำงานแบบ Offline
- ระบบเรียลไทม์ที่มีความล่าช้าต่ำ

✅ **ออกแบบสถาปัตยกรรมอัจฉริยะ**
- ระบบหลายเอเจนต์สำหรับกระบวนการที่ซับซ้อน
- การใช้งานแบบ Hybrid Edge-Cloud
- โครงสร้างพื้นฐาน AI ที่ปรับต้นทุนได้

✅ **นำโครงการ Edge AI**
- ประเมินความเป็นไปได้ของ Edge AI สำหรับโครงการ
- เลือกโมเดลและเฟรมเวิร์กที่เหมาะสม
- ออกแบบโซลูชัน AI ในพื้นที่ที่สามารถขยายได้

---

## 🗺️ โครงสร้าง Workshop

### ภาพรวมเซสชัน (6 เซสชัน × 30 นาที = 3 ชั่วโมง)

| เซสชัน | หัวข้อ | จุดเน้น | ระยะเวลา |
|--------|-------|---------|----------|
| **1** | เริ่มต้นใช้งาน Foundry Local | ติดตั้ง, ตรวจสอบ, การตอบสนองครั้งแรก | 30 นาที |
| **2** | สร้างโซลูชัน AI ด้วย RAG | การออกแบบ Prompt, Embeddings, การประเมินผล | 30 นาที |
| **3** | โมเดลโอเพ่นซอร์ส | การค้นหาโมเดล, การทดสอบ, การเลือก | 30 นาที |
| **4** | โมเดลล้ำสมัย | SLM กับ LLM, การปรับปรุง, เฟรมเวิร์ก | 30 นาที |
| **5** | เอเจนต์ที่ขับเคลื่อนด้วย AI | การออกแบบเอเจนต์, การประสานงาน, หน่วยความจำ | 30 นาที |
| **6** | โมเดลในฐานะเครื่องมือ | การจัดการคำขอ, การเชื่อมโยง, กลยุทธ์การขยาย | 30 นาที |

---

## 🚀 เริ่มต้นอย่างรวดเร็ว

### ข้อกำหนดเบื้องต้น

**ข้อกำหนดระบบ:**
- **OS**: Windows 10/11, macOS 11+, หรือ Linux (Ubuntu 20.04+)
- **RAM**: ขั้นต่ำ 8GB, แนะนำ 16GB+
- **พื้นที่จัดเก็บ**: พื้นที่ว่าง 10GB+ สำหรับโมเดล
- **CPU**: โปรเซสเซอร์รุ่นใหม่ที่รองรับ AVX2
- **GPU** (ตัวเลือก): CUDA-compatible หรือ Qualcomm NPU สำหรับการเร่งความเร็ว

**ข้อกำหนดซอฟต์แวร์:**
- **Python 3.8+** ([ดาวน์โหลด](https://www.python.org/downloads/))
- **Microsoft Foundry Local** ([คู่มือการติดตั้ง](../../../Workshop))
- **Git** ([ดาวน์โหลด](https://git-scm.com/downloads))
- **Visual Studio Code** (แนะนำ) ([ดาวน์โหลด](https://code.visualstudio.com/))

### การตั้งค่าใน 3 ขั้นตอน

#### 1. ติดตั้ง Foundry Local

**Windows:**
```powershell
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
foundry service status
```

#### 2. โคลน Repository และติดตั้ง Dependencies

```bash
# Clone repository
git clone https://github.com/microsoft/edgeai-for-beginners.git
cd edgeai-for-beginners/Workshop

# Create virtual environment
python -m venv .venv

# Activate virtual environment
# Windows:
.\.venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

#### 3. รันตัวอย่างแรกของคุณ

```bash
# Start Foundry Local and load a model
foundry model run phi-4-mini

# Run the chat bootstrap sample
cd samples/session01
python chat_bootstrap.py "What is edge AI?"
```

**✅ สำเร็จ!** คุณควรเห็นการตอบสนองแบบ Streaming เกี่ยวกับ Edge AI

---

## 📦 ทรัพยากร Workshop

### ตัวอย่าง Python

ตัวอย่างแบบลงมือทำที่แสดงแนวคิดแต่ละอย่าง:

| เซสชัน | ตัวอย่าง | คำอธิบาย | เวลารัน |
|--------|----------|----------|---------|
| 1 | [`chat_bootstrap.py`](../../../Workshop/samples/session01/chat_bootstrap.py) | แชทพื้นฐานและแบบ Streaming | ~30 วินาที |
| 2 | [`rag_pipeline.py`](../../../Workshop/samples/session02/rag_pipeline.py) | RAG พร้อม Embeddings | ~45 วินาที |
| 2 | [`rag_eval_ragas.py`](../../../Workshop/samples/session02/rag_eval_ragas.py) | การประเมินคุณภาพ RAG | ~60 วินาที |
| 3 | [`benchmark_oss_models.py`](../../../Workshop/samples/session03/benchmark_oss_models.py) | การทดสอบเปรียบเทียบโมเดลหลายตัว | ~2-3 นาที |
| 4 | [`model_compare.py`](../../../Workshop/samples/session04/model_compare.py) | การเปรียบเทียบ SLM กับ LLM | ~45 วินาที |
| 5 | [`agents_orchestrator.py`](../../../Workshop/samples/session05/agents_orchestrator.py) | ระบบหลายเอเจนต์ | ~60 วินาที |
| 6 | [`models_router.py`](../../../Workshop/samples/session06/models_router.py) | การจัดการคำขอแบบเจตนา | ~45 วินาที |
| 6 | [`models_pipeline.py`](../../../Workshop/samples/session06/models_pipeline.py) | การเชื่อมโยงหลายขั้นตอน | ~60 วินาที |

### Jupyter Notebooks

การสำรวจแบบโต้ตอบพร้อมคำอธิบายและภาพประกอบ:

| เซสชัน | Notebook | คำอธิบาย | ระดับความยาก |
|--------|----------|----------|---------------|
| 1 | [`session01_chat_bootstrap.ipynb`](./notebooks/session01_chat_bootstrap.ipynb) | พื้นฐานแชทและ Streaming | ⭐ ผู้เริ่มต้น |
| 2 | [`session02_rag_pipeline.ipynb`](./notebooks/session02_rag_pipeline.ipynb) | สร้างระบบ RAG | ⭐⭐ ระดับกลาง |
| 2 | [`session02_rag_eval_ragas.ipynb`](./notebooks/session02_rag_eval_ragas.ipynb) | ประเมินคุณภาพ RAG | ⭐⭐ ระดับกลาง |
| 3 | [`session03_benchmark_oss_models.ipynb`](./notebooks/session03_benchmark_oss_models.ipynb) | การทดสอบโมเดล | ⭐⭐ ระดับกลาง |
| 4 | [`session04_model_compare.ipynb`](./notebooks/session04_model_compare.ipynb) | การเปรียบเทียบโมเดล | ⭐⭐ ระดับกลาง |
| 5 | [`session05_agents_orchestrator.ipynb`](./notebooks/session05_agents_orchestrator.ipynb) | การประสานงานเอเจนต์ | ⭐⭐⭐ ขั้นสูง |
| 6 | [`session06_models_router.ipynb`](./notebooks/session06_models_router.ipynb) | การจัดการคำขอแบบเจตนา | ⭐⭐⭐ ขั้นสูง |
| 6 | [`session06_models_pipeline.ipynb`](./notebooks/session06_models_pipeline.ipynb) | การประสานงานแบบ Pipeline | ⭐⭐⭐ ขั้นสูง |

### เอกสาร

คู่มือและข้อมูลอ้างอิงที่ครอบคลุม:

| เอกสาร | คำอธิบาย | ใช้เมื่อ |
|--------|----------|----------|
| [QUICK_START.md](./QUICK_START.md) | คู่มือการตั้งค่าแบบรวดเร็ว | เริ่มต้นจากศูนย์ |
| [QUICK_REFERENCE.md](./QUICK_REFERENCE.md) | แผ่นโกงคำสั่งและ API | ต้องการคำตอบด่วน |
| [FOUNDRY_SDK_QUICKREF.md](./FOUNDRY_SDK_QUICKREF.md) | รูปแบบ SDK และตัวอย่าง | เขียนโค้ด |
| [ENV_CONFIGURATION.md](./ENV_CONFIGURATION.md) | คู่มือการตั้งค่าตัวแปรสภาพแวดล้อม | กำหนดค่าตัวอย่าง |
| [SAMPLES_UPDATE_SUMMARY.md](./SAMPLES_UPDATE_SUMMARY.md) | การปรับปรุงตัวอย่างล่าสุด | ทำความเข้าใจการเปลี่ยนแปลง |
| [SDK_MIGRATION_NOTES.md](./SDK_MIGRATION_NOTES.md) | คู่มือการย้าย | อัปเกรดโค้ด |
| [notebooks/TROUBLESHOOTING.md](./notebooks/TROUBLESHOOTING.md) | ปัญหาทั่วไปและการแก้ไข | แก้ไขปัญหา |

---

## 🎓 คำแนะนำเส้นทางการเรียนรู้

### สำหรับผู้เริ่มต้น (3-4 ชั่วโมง)
1. ✅ เซสชัน 1: เริ่มต้นใช้งาน (เน้นการตั้งค่าและแชทพื้นฐาน)
2. ✅ เซสชัน 2: พื้นฐาน RAG (ข้ามการประเมินผลในตอนแรก)
3. ✅ เซสชัน 3: การทดสอบง่าย ๆ (โมเดล 2 ตัวเท่านั้น)
4. ⏭️ ข้ามเซสชัน 4-6 ไปก่อน
5. 🔄 กลับมาเซสชัน 4-6 หลังจากสร้างแอปพลิเคชันแรก

### สำหรับนักพัฒนาระดับกลาง (3 ชั่วโมง)
1. ⚡ เซสชัน 1: ตรวจสอบการตั้งค่าอย่างรวดเร็ว
2. ✅ เซสชัน 2: ระบบ RAG ที่สมบูรณ์พร้อมการประเมินผล
3. ✅ เซสชัน 3: ชุดทดสอบเปรียบเทียบเต็มรูปแบบ
4. ✅ เซสชัน 4: การปรับปรุงโมเดล
5. ✅ เซสชัน 5-6: เน้นรูปแบบสถาปัตยกรรม

### สำหรับผู้เชี่ยวชาญ (2-3 ชั่วโมง)
1. ⚡ เซสชัน 1-3: ทบทวนและตรวจสอบอย่างรวดเร็ว
2. ✅ เซสชัน 4: การปรับปรุงเชิงลึก
3. ✅ เซสชัน 5: สถาปัตยกรรมหลายเอเจนต์
4. ✅ เซสชัน 6: รูปแบบการใช้งานจริงและการขยายขนาด
5. 🚀 ขยาย: สร้างตรรกะการจัดการคำขอแบบกำหนดเองและการใช้งานแบบ Hybrid

---

## ชุดเซสชัน Workshop (Labs แบบเน้น 30 นาที)

หากคุณกำลังติดตามรูปแบบ Workshop แบบย่อ 6 เซสชัน ให้ใช้คู่มือเฉพาะเหล่านี้ (แต่ละคู่มือจะเชื่อมโยงและเสริมเอกสารโมดูลที่กว้างขึ้นด้านบน):

| เซสชัน Workshop | คู่มือ | จุดเน้นหลัก |
|------------------|-------|--------------|

ไฟล์เซสชันแต่ละไฟล์ประกอบด้วย: บทคัดย่อ, วัตถุประสงค์การเรียนรู้, ลำดับการสาธิต 30 นาที, โปรเจกต์เริ่มต้น, เช็คลิสต์การตรวจสอบ, การแก้ไขปัญหา และการอ้างอิงไปยัง Foundry Local Python SDK อย่างเป็นทางการ

### สคริปต์ตัวอย่าง

ติดตั้ง dependencies สำหรับเวิร์กช็อป (Windows):

```powershell
cd Workshop
py -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt
```

macOS / Linux:

```bash
cd Workshop
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

หากรัน Foundry Local service บนเครื่องหรือ VM (Windows) ที่ต่างจาก macOS ให้ส่งออก endpoint:

```bash
export FOUNDRY_LOCAL_ENDPOINT=http://<windows-host>:5273/v1
```

| เซสชัน | สคริปต์ | คำอธิบาย |
|--------|----------|-----------|
| 1 | `samples/session01/chat_bootstrap.py` | Bootstrap service & streaming chat |
| 2 | `samples/session02/rag_pipeline.py` | RAG ขั้นต่ำ (in-memory embeddings) |
|   | `samples/session02/rag_eval_ragas.py` | การประเมิน RAG ด้วยเมตริก ragas |
| 3 | `samples/session03/benchmark_oss_models.py` | การวัด latency & throughput ของหลายโมเดล |
| 4 | `samples/session04/model_compare.py` | การเปรียบเทียบ SLM กับ LLM (latency & ตัวอย่าง output) |
| 5 | `samples/session05/agents_orchestrator.py` | การวิจัยด้วยสองเอเจนต์ → กระบวนการแก้ไข |
| 6 | `samples/session06/models_router.py` | การสาธิตการกำหนดเส้นทางตามเจตนา |
|   | `samples/session06/models_pipeline.py` | แผน/ดำเนินการ/ปรับปรุงแบบหลายขั้นตอน |

### ตัวแปรสภาพแวดล้อม (ใช้ร่วมกันในตัวอย่าง)

| ตัวแปร | วัตถุประสงค์ | ตัวอย่าง |
|--------|---------------|----------|
| `FOUNDRY_LOCAL_ALIAS` | Alias โมเดลเดี่ยวเริ่มต้นสำหรับตัวอย่างพื้นฐาน | `phi-4-mini` |
| `SLM_ALIAS` / `LLM_ALIAS` | โมเดล SLM กับโมเดลขนาดใหญ่สำหรับการเปรียบเทียบ | `phi-4-mini` / `gpt-oss-20b` |
| `BENCH_MODELS` | รายการ alias โมเดลที่ต้องการวัดผล | `qwen2.5-0.5b,gemma-2-2b,mistral-7b` |
| `BENCH_ROUNDS` | จำนวนรอบการวัดผลต่อโมเดล | `3` |
| `BENCH_PROMPT` | Prompt ที่ใช้ในการวัดผล | `Explain retrieval augmented generation briefly.` |
| `EMBED_MODEL` | โมเดล embedding ของ sentence-transformers | `sentence-transformers/all-MiniLM-L6-v2` |
| `RAG_QUESTION` | การตั้งค่าคำถามทดสอบสำหรับ RAG pipeline | `Why use RAG with local inference?` |
| `AGENT_QUESTION` | การตั้งค่าคำถามสำหรับ agents pipeline | `Explain why edge AI matters for compliance.` |
| `AGENT_MODEL_PRIMARY` | Alias โมเดลสำหรับ research agent | `phi-4-mini` |
| `AGENT_MODEL_EDITOR` | Alias โมเดลสำหรับ editor agent (สามารถต่างกันได้) | `gpt-oss-20b` |
| `SHOW_USAGE` | เมื่อ `1` จะแสดงการใช้ token ต่อการทำงาน | `1` |
| `RETRY_ON_FAIL` | เมื่อ `1` จะลองใหม่อีกครั้งเมื่อเกิดข้อผิดพลาดชั่วคราว | `1` |
| `RETRY_BACKOFF` | วินาทีที่รอระหว่างการลองใหม่ | `1.0` |

หากตัวแปรไม่ได้ถูกตั้งค่า สคริปต์จะใช้ค่าดีฟอลต์ที่เหมาะสม สำหรับการสาธิตโมเดลเดี่ยว คุณมักจะต้องการเพียง `FOUNDRY_LOCAL_ALIAS`

### โมดูลยูทิลิตี้

ตัวอย่างทั้งหมดตอนนี้ใช้ `samples/workshop_utils.py` ซึ่งเป็นตัวช่วยที่มี:

* การสร้าง `FoundryLocalManager` + OpenAI client แบบแคช
* ตัวช่วย `chat_once()` พร้อมการลองใหม่ + การแสดงการใช้ token
* การรายงานการใช้ token แบบง่าย (เปิดใช้งานผ่าน `SHOW_USAGE=1`)

สิ่งนี้ช่วยลดการทำซ้ำและเน้นแนวทางปฏิบัติที่ดีที่สุดสำหรับการจัดการโมเดลในพื้นที่อย่างมีประสิทธิภาพ

## การปรับปรุงเพิ่มเติม (ข้ามเซสชัน)

| ธีม | การปรับปรุง | เซสชัน | Env / Toggle |
|-----|-------------|--------|--------------|
| Determinism | อุณหภูมิที่คงที่ + ชุด prompt ที่เสถียร | 1–6 | ตั้งค่า `temperature=0`, `top_p=1` |
| Token Usage Visibility | การสอนเรื่องต้นทุน/ประสิทธิภาพอย่างสม่ำเสมอ | 1–6 | `SHOW_USAGE=1` |
| Streaming First Token | เมตริก latency ที่รับรู้ได้ | 1,3,4,6 | `BENCH_STREAM=1` (benchmark) |
| Retry Resilience | จัดการ cold-start ชั่วคราว | ทั้งหมด | `RETRY_ON_FAIL=1` + `RETRY_BACKOFF` |
| Multi-Model Agents | การเชี่ยวชาญบทบาทที่หลากหลาย | 5 | `AGENT_MODEL_PRIMARY`, `AGENT_MODEL_EDITOR` |
| Adaptive Routing | เจตนา + ฮิวริสติกต้นทุน | 6 | ขยาย router ด้วย logic การยกระดับ |
| Vector Memory | การเรียกคืนเชิงความหมายระยะยาว | 2,5,6 | รวม FAISS/Chroma embedding index |
| Trace Export | การตรวจสอบและการประเมินผล | 2,5,6 | เพิ่ม JSON lines ต่อขั้นตอน |
| Quality Rubrics | การติดตามเชิงคุณภาพ | 3–6 | prompt การให้คะแนนรอง |
| Smoke Tests | การตรวจสอบก่อนเวิร์กช็อปอย่างรวดเร็ว | ทั้งหมด | `python Workshop/tests/smoke.py` |

### การเริ่มต้นแบบ Deterministic

```powershell
set FOUNDRY_LOCAL_ALIAS=phi-4-mini
set SHOW_USAGE=1
python Workshop\tests\smoke.py
```

คาดหวังจำนวน token ที่เสถียรใน input ที่เหมือนกันซ้ำๆ

### การประเมิน RAG (เซสชัน 2)

ใช้ `rag_eval_ragas.py` เพื่อคำนวณความเกี่ยวข้องของคำตอบ ความถูกต้อง และความแม่นยำของบริบทในชุดข้อมูลสังเคราะห์ขนาดเล็ก:

```powershell
python samples/session02/rag_eval_ragas.py
```

ขยายโดยการจัดเตรียม JSONL ขนาดใหญ่ที่มีคำถาม บริบท และความจริงพื้นฐาน จากนั้นแปลงเป็น Hugging Face `Dataset`

## ภาคผนวกความถูกต้องของคำสั่ง CLI

เวิร์กช็อปใช้เฉพาะคำสั่ง CLI ของ Foundry Local ที่มีการบันทึกไว้ในปัจจุบัน / มีเสถียรภาพเท่านั้น

### คำสั่งที่มีเสถียรภาพที่อ้างถึง

| หมวดหมู่ | คำสั่ง | วัตถุประสงค์ |
|----------|---------|--------------|
| Core | `foundry --version` | แสดงเวอร์ชันที่ติดตั้ง |
| Core | `foundry init` | เริ่มต้นการตั้งค่า |
| Service | `foundry service start` | เริ่ม local service (หากไม่ได้เริ่มอัตโนมัติ) |
| Service | `foundry status` | แสดงสถานะ service |
| Models | `foundry model list` | แสดงรายการโมเดลที่มีใน catalog |
| Models | `foundry model download <alias>` | ดาวน์โหลดน้ำหนักโมเดลลงใน cache |
| Models | `foundry model run <alias>` | รัน (โหลด) โมเดลในพื้นที่; ใช้ร่วมกับ `--prompt` สำหรับ one-shot |
| Models | `foundry model unload <alias>` / `foundry model stop <alias>` | ยกเลิกการโหลดโมเดลจากหน่วยความจำ (หากรองรับ) |
| Cache | `foundry cache list` | แสดงรายการโมเดลที่แคชไว้ |
| System | `foundry system info` | สแนปช็อตความสามารถของฮาร์ดแวร์ & การเร่งความเร็ว |
| System | `foundry system gpu-info` | ข้อมูลการวินิจฉัย GPU |
| Config | `foundry config list` | แสดงค่าการตั้งค่าปัจจุบัน |
| Config | `foundry config set <key> <value>` | อัปเดตการตั้งค่า |

### รูปแบบ Prompt แบบ One-Shot

แทนคำสั่งย่อย `model chat` ที่เลิกใช้แล้ว ให้ใช้:

```powershell
foundry model run <alias> --prompt "Your question here"
```

คำสั่งนี้จะดำเนินการ prompt/response รอบเดียวแล้วออก

### รูปแบบที่ถูกลบ / หลีกเลี่ยง

| เลิกใช้ / ไม่มีการบันทึก | คำแนะนำ / ทดแทน |
|--------------------------|-----------------|
| `foundry model chat <model> "..."` | `foundry model run <model> --prompt "..."` |
| `foundry model list --running` | ใช้ `foundry model list` ธรรมดา + กิจกรรมล่าสุด / logs |
| `foundry model list --cached` | `foundry cache list` |
| `foundry model stats <model>` | ใช้สคริปต์ benchmark Python + เครื่องมือ OS (Task Manager / `nvidia-smi`) |
| `foundry model benchmark ...` | `samples/session03/benchmark_oss_models.py` |

### การวัดผลและ Telemetry

- Latency, p95, tokens/sec: `samples/session03/benchmark_oss_models.py`
- Latency ของ token แรก (streaming): ตั้งค่า `BENCH_STREAM=1`
- การใช้ทรัพยากร: ตัวตรวจสอบ OS (Task Manager, Activity Monitor, `nvidia-smi`) + `foundry system info`

เมื่อคำสั่ง telemetry CLI ใหม่มีเสถียรภาพ upstream สามารถรวมเข้ากับ markdown เซสชันได้โดยแก้ไขเพียงเล็กน้อย

### Automated Lint Guard

ตัวตรวจสอบอัตโนมัติป้องกันการนำรูปแบบ CLI ที่เลิกใช้แล้วกลับมาใน code block ของไฟล์ markdown:

สคริปต์: `Workshop/scripts/lint_markdown_cli.py`

รูปแบบที่เลิกใช้จะถูกบล็อกใน code fences

คำแนะนำการทดแทน:
| เลิกใช้ | ทดแทน |
|---------|-------|
| `foundry model chat <a> "..."` | `foundry model run <a> --prompt "..."` |
| `model list --running` | `model list` |
| `model list --cached` | `cache list` |
| `model stats` | สคริปต์ benchmark + เครื่องมือระบบ |
| `model benchmark` | `samples/session03/benchmark_oss_models.py` |
| `model list --available` | `model list` |

รันในเครื่อง:
```powershell
python Workshop\scripts\lint_markdown_cli.py --verbose
```

GitHub Action: `.github/workflows/markdown-cli-lint.yml` รันทุกครั้งที่ push & PR

Optional pre-commit hook:
```bash
echo "python Workshop/scripts/lint_markdown_cli.py" > .git/hooks/pre-commit
chmod +x .git/hooks/pre-commit
```

## ตารางการย้าย CLI → SDK อย่างรวดเร็ว

| งาน | CLI One-Liner | SDK (Python) Equivalent | หมายเหตุ |
|-----|---------------|-------------------------|----------|
| รันโมเดลครั้งเดียว (prompt) | `foundry model run phi-4-mini --prompt "Hello"` | `manager=FoundryLocalManager("phi-4-mini"); client=OpenAI(base_url=manager.endpoint, api_key=manager.api_key or "not-needed"); client.chat.completions.create(model=manager.get_model_info("phi-4-mini").id, messages=[{"role":"user","content":"Hello"}])` | SDK เริ่มต้น service & caching โดยอัตโนมัติ |
| ดาวน์โหลด (cache) โมเดล | `foundry model download qwen2.5-0.5b` | `FoundryLocalManager("qwen2.5-0.5b")  # triggers download/load` | Manager เลือก variant ที่ดีที่สุดหาก alias มีหลาย build |
| แสดงรายการ catalog | `foundry model list` | `# use manager for each alias or maintain known list` | CLI รวมข้อมูล; SDK ปัจจุบันใช้การสร้างต่อ alias |
| แสดงรายการโมเดลที่แคชไว้ | `foundry cache list` | `manager.list_cached_models()` | หลังจาก manager init (alias ใดก็ได้) |
| เปิดใช้งาน GPU acceleration | `foundry config set compute.onnx.enable_gpu true` | `# CLI action; SDK assumes config already applied` | การตั้งค่าเป็นผลกระทบภายนอก |
| รับ URL endpoint | (โดยนัย) | `manager.endpoint` | ใช้เพื่อสร้าง OpenAI-compatible client |
| อุ่นโมเดล | `foundry model run <alias>` แล้ว prompt แรก | `chat_once(alias, messages=[...])` (utility) | Utilities จัดการ latency cold-start เริ่มต้น |
| วัด latency | `python benchmark_oss_models.py` | `import benchmark_oss_models` (หรือสคริปต์ exporter ใหม่) | ใช้สคริปต์เพื่อเมตริกที่สม่ำเสมอ |
| หยุด / ยกเลิกการโหลดโมเดล | `foundry model unload <alias>` | (ไม่เปิดเผย – รีสตาร์ท service / process) | โดยทั่วไปไม่จำเป็นสำหรับ flow เวิร์กช็อป |
| ดึงการใช้ token | (ดู output) | `resp.usage.total_tokens` | ให้เมื่อ backend ส่งคืนวัตถุการใช้งาน |

## การส่งออก Benchmark Markdown

ใช้สคริปต์ `Workshop/scripts/export_benchmark_markdown.py` เพื่อรัน benchmark ใหม่ (ตรรกะเดียวกับ `samples/session03/benchmark_oss_models.py`) และส่งออกตาราง Markdown ที่เหมาะกับ GitHub พร้อม JSON ดิบ

### ตัวอย่าง

```powershell
python Workshop\scripts\export_benchmark_markdown.py --models "qwen2.5-0.5b,gemma-2-2b,mistral-7b" --prompt "Explain retrieval augmented generation briefly." --rounds 3 --output benchmark_report.md
```

ไฟล์ที่สร้าง:
| ไฟล์ | เนื้อหา |
|------|---------|
| `benchmark_report.md` | ตาราง Markdown + คำแนะนำการตีความ |
| `benchmark_report.json` | อาร์เรย์เมตริกดิบ (สำหรับ diffing / การติดตามแนวโน้ม) |

ตั้งค่า `BENCH_STREAM=1` ใน environment เพื่อรวม latency ของ token แรกหากรองรับ

---

**ข้อจำกัดความรับผิดชอบ**:  
เอกสารนี้ได้รับการแปลโดยใช้บริการแปลภาษา AI [Co-op Translator](https://github.com/Azure/co-op-translator) แม้ว่าเราจะพยายามให้การแปลมีความถูกต้อง แต่โปรดทราบว่าการแปลอัตโนมัติอาจมีข้อผิดพลาดหรือความไม่ถูกต้อง เอกสารต้นฉบับในภาษาดั้งเดิมควรถือเป็นแหล่งข้อมูลที่เชื่อถือได้ สำหรับข้อมูลที่สำคัญ ขอแนะนำให้ใช้บริการแปลภาษามนุษย์ที่มีความเชี่ยวชาญ เราจะไม่รับผิดชอบต่อความเข้าใจผิดหรือการตีความผิดที่เกิดจากการใช้การแปลนี้