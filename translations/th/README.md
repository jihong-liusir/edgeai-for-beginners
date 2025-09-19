<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "c817161ba08864340737d623f761b9ae",
  "translation_date": "2025-09-18T06:15:36+00:00",
  "source_file": "README.md",
  "language_code": "th"
}
-->
# EdgeAI สำหรับผู้เริ่มต้น

![ภาพหน้าปกคอร์ส](../../translated_images/cover.eb18d1b9605d754b30973f4e17c6e11ea4f8473d9686ee378d6e7b44e3c70ac7.th.png)

[![GitHub contributors](https://img.shields.io/github/contributors/microsoft/edgeai-for-beginners.svg)](https://GitHub.com/microsoft/edgeai-for-beginners/graphs/contributors)
[![GitHub issues](https://img.shields.io/github/issues/microsoft/edgeai-for-beginners.svg)](https://GitHub.com/microsoft/edgeai-for-beginners/issues)
[![GitHub pull-requests](https://img.shields.io/github/issues-pr/microsoft/edgeai-for-beginners.svg)](https://GitHub.com/microsoft/edgeai-for-beginners/pulls)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)

[![GitHub watchers](https://img.shields.io/github/watchers/microsoft/edgeai-for-beginners.svg?style=social&label=Watch)](https://GitHub.com/microsoft/edgeai-for-beginners/watchers)
[![GitHub forks](https://img.shields.io/github/forks/microsoft/edgeai-for-beginners.svg?style=social&label=Fork)](https://GitHub.com/microsoft/edgeai-for-beginners/fork)
[![GitHub stars](https://img.shields.io/github/stars/microsoft/edgeai-for-beginners?style=social&label=Star)](https://GitHub.com/microsoft/edgeai-for-beginners/stargazers)

[![Microsoft Azure AI Foundry Discord](https://dcbadge.limes.pink/api/server/ByRwuEEgH4)](https://discord.com/invite/ByRwuEEgH4)

ทำตามขั้นตอนเหล่านี้เพื่อเริ่มต้นใช้งานทรัพยากรเหล่านี้:

1. **Fork Repository**: คลิก [![GitHub forks](https://img.shields.io/github/forks/microsoft/edgeai-for-beginners.svg?style=social&label=Fork)](https://GitHub.com/microsoft/edgeai-for-beginners/fork)
2. **Clone Repository**: `git clone https://github.com/microsoft/edgeai-for-beginners.git`
3. [**เข้าร่วม Azure AI Foundry Discord เพื่อพบปะผู้เชี่ยวชาญและนักพัฒนาคนอื่นๆ**](https://discord.com/invite/ByRwuEEgH4)

### 🌐 รองรับหลายภาษา

#### รองรับผ่าน GitHub Action (อัตโนมัติและอัปเดตเสมอ)

[Arabic](../ar/README.md) | [Bengali](../bn/README.md) | [Bulgarian](../bg/README.md) | [Burmese (Myanmar)](../my/README.md) | [Chinese (Simplified)](../zh/README.md) | [Chinese (Traditional, Hong Kong)](../hk/README.md) | [Chinese (Traditional, Macau)](../mo/README.md) | [Chinese (Traditional, Taiwan)](../tw/README.md) | [Croatian](../hr/README.md) | [Czech](../cs/README.md) | [Danish](../da/README.md) | [Dutch](../nl/README.md) | [Finnish](../fi/README.md) | [French](../fr/README.md) | [German](../de/README.md) | [Greek](../el/README.md) | [Hebrew](../he/README.md) | [Hindi](../hi/README.md) | [Hungarian](../hu/README.md) | [Indonesian](../id/README.md) | [Italian](../it/README.md) | [Japanese](../ja/README.md) | [Korean](../ko/README.md) | [Malay](../ms/README.md) | [Marathi](../mr/README.md) | [Nepali](../ne/README.md) | [Norwegian](../no/README.md) | [Persian (Farsi)](../fa/README.md) | [Polish](../pl/README.md) | [Portuguese (Brazil)](../br/README.md) | [Portuguese (Portugal)](../pt/README.md) | [Punjabi (Gurmukhi)](../pa/README.md) | [Romanian](../ro/README.md) | [Russian](../ru/README.md) | [Serbian (Cyrillic)](../sr/README.md) | [Slovak](../sk/README.md) | [Slovenian](../sl/README.md) | [Spanish](../es/README.md) | [Swahili](../sw/README.md) | [Swedish](../sv/README.md) | [Tagalog (Filipino)](../tl/README.md) | [Thai](./README.md) | [Turkish](../tr/README.md) | [Ukrainian](../uk/README.md) | [Urdu](../ur/README.md) | [Vietnamese](../vi/README.md)

**หากคุณต้องการให้มีการรองรับภาษาเพิ่มเติม รายการภาษาที่รองรับอยู่ [ที่นี่](https://github.com/Azure/co-op-translator/blob/main/getting_started/supported-languages.md)**

## บทนำ

ยินดีต้อนรับสู่ **EdgeAI สำหรับผู้เริ่มต้น** – การเดินทางที่ครอบคลุมสู่โลกแห่งการเปลี่ยนแปลงของปัญญาประดิษฐ์บนอุปกรณ์ปลายทาง คอร์สนี้เชื่อมโยงความสามารถ AI อันทรงพลังเข้ากับการใช้งานจริงในโลกแห่งความเป็นจริงบนอุปกรณ์ปลายทาง ช่วยให้คุณสามารถใช้ศักยภาพของ AI ได้โดยตรงในที่ที่ข้อมูลถูกสร้างขึ้นและการตัดสินใจต้องเกิดขึ้น

### สิ่งที่คุณจะได้เรียนรู้

คอร์สนี้จะพาคุณจากแนวคิดพื้นฐานไปจนถึงการใช้งานที่พร้อมสำหรับการผลิต ครอบคลุม:
- **Small Language Models (SLMs)** ที่ปรับแต่งสำหรับการใช้งานบนอุปกรณ์ปลายทาง
- **การปรับแต่งที่คำนึงถึงฮาร์ดแวร์** บนแพลตฟอร์มที่หลากหลาย
- **การวิเคราะห์แบบเรียลไทม์** พร้อมความสามารถในการรักษาความเป็นส่วนตัว
- **กลยุทธ์การใช้งานในระดับองค์กร** สำหรับการใช้งานจริง

### ทำไม EdgeAI ถึงสำคัญ

Edge AI เป็นการเปลี่ยนแปลงที่ตอบสนองความท้าทายสำคัญในยุคปัจจุบัน:
- **ความเป็นส่วนตัวและความปลอดภัย**: ประมวลผลข้อมูลที่ละเอียดอ่อนในพื้นที่โดยไม่ต้องส่งไปยังคลาวด์
- **ประสิทธิภาพแบบเรียลไทม์**: ลดความล่าช้าของเครือข่ายสำหรับแอปพลิเคชันที่ต้องการความรวดเร็ว
- **ความคุ้มค่า**: ลดค่าใช้จ่ายด้านแบนด์วิดท์และการประมวลผลบนคลาวด์
- **การทำงานที่ยืดหยุ่น**: รักษาการทำงานในช่วงที่เครือข่ายขัดข้อง
- **การปฏิบัติตามกฎระเบียบ**: ตอบสนองความต้องการด้านอธิปไตยของข้อมูล

### Edge AI

Edge AI หมายถึงการรันอัลกอริทึม AI และโมเดลภาษาบนฮาร์ดแวร์ในพื้นที่—ใกล้กับที่ข้อมูลถูกสร้างขึ้น—โดยไม่ต้องพึ่งพาทรัพยากรคลาวด์สำหรับการวิเคราะห์ ช่วยลดความล่าช้า เพิ่มความเป็นส่วนตัว และช่วยให้การตัดสินใจแบบเรียลไทม์เป็นไปได้

### หลักการสำคัญ:
- **การวิเคราะห์บนอุปกรณ์**: โมเดล AI ทำงานบนอุปกรณ์ปลายทาง (โทรศัพท์ เราเตอร์ ไมโครคอนโทรลเลอร์ คอมพิวเตอร์อุตสาหกรรม)
- **ความสามารถแบบออฟไลน์**: ทำงานได้โดยไม่ต้องเชื่อมต่ออินเทอร์เน็ตอย่างต่อเนื่อง
- **ความล่าช้าต่ำ**: ตอบสนองทันทีเหมาะสำหรับระบบเรียลไทม์
- **อธิปไตยของข้อมูล**: เก็บข้อมูลที่ละเอียดอ่อนในพื้นที่ เพิ่มความปลอดภัยและการปฏิบัติตามกฎระเบียบ

### Small Language Models (SLMs)

SLMs เช่น Phi-4, Mistral-7B และ Gemma เป็นเวอร์ชันที่ปรับแต่งของ LLMs ขนาดใหญ่—ผ่านการฝึกอบรมหรือการลดขนาดเพื่อ:
- **ลดการใช้หน่วยความจำ**: ใช้หน่วยความจำของอุปกรณ์ปลายทางอย่างมีประสิทธิภาพ
- **ลดความต้องการในการประมวลผล**: ปรับแต่งสำหรับประสิทธิภาพ CPU และ GPU บนอุปกรณ์ปลายทาง
- **เริ่มต้นได้เร็วขึ้น**: การเริ่มต้นที่รวดเร็วสำหรับแอปพลิเคชันที่ตอบสนองทันที

SLMs ช่วยให้เกิดความสามารถ NLP ที่ทรงพลังในขณะที่ตอบสนองข้อจำกัดของ:
- **ระบบฝังตัว**: อุปกรณ์ IoT และตัวควบคุมอุตสาหกรรม
- **อุปกรณ์มือถือ**: สมาร์ทโฟนและแท็บเล็ตที่มีความสามารถแบบออฟไลน์
- **อุปกรณ์ IoT**: เซ็นเซอร์และอุปกรณ์อัจฉริยะที่มีทรัพยากรจำกัด
- **เซิร์ฟเวอร์ปลายทาง**: หน่วยประมวลผลในพื้นที่ที่มีทรัพยากร GPU จำกัด
- **คอมพิวเตอร์ส่วนบุคคล**: การใช้งานบนเดสก์ท็อปและแล็ปท็อป

## โครงสร้างคอร์ส

### [Module 01: พื้นฐานและการเปลี่ยนแปลงของ EdgeAI](./Module01/README.md)
**ธีม**: การเปลี่ยนแปลงของการใช้งาน Edge AI

#### โครงสร้างบท:
- [**Section 1: พื้นฐานของ EdgeAI**](./Module01/01.EdgeAIFundamentals.md)
  - เปรียบเทียบ AI บนคลาวด์แบบดั้งเดิมกับ Edge AI
  - ความท้าทายและข้อจำกัดของการประมวลผลปลายทาง
  - เทคโนโลยีสำคัญ: การลดขนาดโมเดล การปรับแต่งการบีบอัด Small Language Models (SLMs)
  - การเร่งความเร็วด้วยฮาร์ดแวร์: NPUs, การปรับแต่ง GPU, การปรับแต่ง CPU
  - ข้อดี: ความปลอดภัย ความล่าช้าต่ำ ความสามารถแบบออฟไลน์ ความคุ้มค่า

- [**Section 2: กรณีศึกษาในโลกแห่งความเป็นจริง**](./Module01/02.RealWorldCaseStudies.md)
  - ระบบนิเวศของโมเดล Microsoft Phi & Mu
  - กรณีศึกษาระบบรายงาน AI ของ Japan Airlines
  - ผลกระทบต่อตลาดและทิศทางในอนาคต
  - ข้อควรพิจารณาและแนวทางปฏิบัติที่ดีที่สุดในการใช้งาน

- [**Section 3: คู่มือการใช้งานจริง**](./Module01/03.PracticalImplementationGuide.md)
  - การตั้งค่าสภาพแวดล้อมการพัฒนา (Python 3.10+, .NET 8+)
  - ข้อกำหนดฮาร์ดแวร์และการกำหนดค่าที่แนะนำ
  - ทรัพยากรของครอบครัวโมเดลหลัก
  - เครื่องมือการลดขนาดและการปรับแต่ง (Llama.cpp, Microsoft Olive, Apple MLX)
  - รายการตรวจสอบการประเมินและการตรวจสอบ

- [**Section 4: แพลตฟอร์มฮาร์ดแวร์สำหรับการใช้งาน Edge AI**](./Module01/04.EdgeDeployment.md)
  - ข้อควรพิจารณาและข้อกำหนดสำหรับการใช้งาน Edge AI
  - ฮาร์ดแวร์ Edge AI ของ Intel และเทคนิคการปรับแต่ง
  - โซลูชัน AI ของ Qualcomm สำหรับระบบมือถือและฝังตัว
  - NVIDIA Jetson และแพลตฟอร์มการประมวลผลปลายทาง
  - แพลตฟอร์ม Windows AI PC พร้อมการเร่งความเร็ว NPU
  - กลยุทธ์การปรับแต่งเฉพาะฮาร์ดแวร์

---

### [Module 02: พื้นฐานของ Small Language Models](./Module02/README.md)
**ธีม**: หลักการทฤษฎี SLM การใช้งาน และการใช้งานในระดับการผลิต

#### โครงสร้างบท:
- [**Section 1: พื้นฐานของครอบครัวโมเดล Microsoft Phi**](./Module02/01.PhiFamily.md)
  - วิวัฒนาการของปรัชญาการออกแบบ (Phi-1 ถึง Phi-4)
  - การออกแบบสถาปัตยกรรมที่เน้นประสิทธิภาพ
  - ความสามารถเฉพาะทาง (การให้เหตุผล, มัลติโหมด, การใช้งานปลายทาง)

- [**Section 2: พื้นฐานของครอบครัวโมเดล Qwen**](./Module02/02.QwenFamily.md)
  - ความเป็นเลิศในโอเพ่นซอร์ส (Qwen 1.0 ถึง Qwen3) - มีให้ใช้งานผ่าน Hugging Face
  - สถาปัตยกรรมการให้เหตุผลขั้นสูงพร้อมความสามารถในโหมดคิด
  - ตัวเลือกการใช้งานที่ปรับขนาดได้ (0.5B-235B พารามิเตอร์)

- [**Section 3: พื้นฐานของครอบครัวโมเดล Gemma**](./Module02/03.GemmaFamily.md)
  - นวัตกรรมที่ขับเคลื่อนด้วยการวิจัย (Gemma 3 & 3n)
  - ความเป็นเลิศในมัลติโหมด
  - สถาปัตยกรรมที่เน้นมือถือ

- [**Section 4: พื้นฐานของครอบครัวโมเดล BitNET**](./Module02/04.BitNETFamily.md)
  - เทคโนโลยีการลดขนาดที่ปฏิวัติวงการ (1.58-bit)
  - เฟรมเวิร์กการวิเคราะห์เฉพาะทางจาก https://github.com/microsoft/BitNet
  - ความเป็นผู้นำ AI ที่ยั่งยืนผ่านประสิทธิภาพขั้นสูงสุด

- [**Section 5: พื้นฐานของโมเดล Microsoft Mu**](./Module02/05.mumodel.md)
  - สถาปัตยกรรมที่เน้นอุปกรณ์ใน Windows 11
  - การผสานรวมระบบกับการตั้งค่า Windows 11
  - การทำงานแบบออฟไลน์ที่รักษาความเป็นส่วนตัว

- [**Section 6: พื้นฐานของ Phi-Silica**](./Module02/06.phisilica.md)
  - สถาปัตยกรรมที่ปรับแต่ง NPU ใน Windows 11 Copilot+ PCs
  - ประสิทธิภาพที่ยอดเยี่ยม (650 โทเค็น/วินาทีที่ 1.5W)
  - การผสานรวมสำหรับนักพัฒนากับ Windows App SDK

---

### [Module 03: การใช้งาน Small Language Models](./Module03/README.md)
**ธีม**: วงจรการใช้งาน SLM ครบวงจร ตั้งแต่ทฤษฎีจนถึงสภาพแวดล้อมการผลิต

#### โครงสร้างบท:
- [**Section 1: การเรียนรู้ขั้นสูงของ SLM**](./Module03/01.SLMAdvancedLearning.md)
  - เฟรมเวิร์กการจำแนกพารามิเตอร์ (Micro SLM 100M-1.4B, Medium SLM 14B-30B)
  - เทคนิคการปรับแต่งขั้นสูง (วิธีการลดขนาด, BitNET 1-bit quantization)
  - กลยุทธ์การได้มาของโมเดล (Azure AI Foundry สำหรับโมเดล Phi, Hugging Face สำหรับโมเดลที่เลือก)

- [**Section 2: การใช้งานในสภาพแวดล้อมท้องถิ่น**](./Module03/02.DeployingSLMinLocalEnv.md)
  - การใช้งานแพลตฟอร์ม Ollama แบบสากล
  - โซลูชันระดับองค์กรในพื้นที่ของ Microsoft Foundry
  - การวิเคราะห์เปรียบเทียบเฟรมเวิร์ก

- [**Section 3: การใช้งานแบบคอนเทนเนอร์ในคลาวด์**](./Module03/03.DeployingSLMinCloud.md)
  - การใช้งานการวิเคราะห์ประสิทธิภาพสูง vLLM
  - การจัดการคอนเทนเนอร์ Ollama
  - การใช้งานที่ปรับแต่งสำหรับปลายทางด้วย ONNX Runtime

---

### [Module 04: การแปลงรูปแบบโมเดลและการลดขนาด](./Module04/README.md)
**ธีม**: ชุดเครื่องมือการปรับแต่งโมเดลที่สมบูรณ์สำหรับการใช้งานปลายทางบนแพลตฟอร์มต่างๆ

#### โครงสร้างบท:
- [**Section 1: พื้นฐานการแปลงรูปแบบโมเดลและการลดขนาด**](./Module04/01.Int
- [**Section 2: คู่มือการใช้งาน Llama.cpp**](./Module04/02.Llamacpp.md)
  - การติดตั้งข้ามแพลตฟอร์ม (Windows, macOS, Linux)
  - การแปลงรูปแบบ GGUF และระดับการลดขนาด (Q2_K ถึง Q8_0)
  - การเร่งความเร็วฮาร์ดแวร์ (CUDA, Metal, OpenCL, Vulkan)
  - การผสาน Python และการปรับใช้ REST API

- [**Section 3: Microsoft Olive Optimization Suite**](./Module04/03.MicrosoftOlive.md)
  - การปรับแต่งโมเดลที่คำนึงถึงฮาร์ดแวร์ด้วยส่วนประกอบในตัวกว่า 40 รายการ
  - การปรับแต่งอัตโนมัติด้วยการลดขนาดแบบไดนามิกและแบบคงที่
  - การผสานกับเวิร์กโฟลว์ Azure ML สำหรับองค์กร
  - การสนับสนุนโมเดลยอดนิยม (Llama, Phi, โมเดล Qwen ที่เลือก, Gemma)

- [**Section 4: OpenVINO Toolkit Optimization Suite**](./Module04/04.openvino.md)
  - เครื่องมือโอเพ่นซอร์สของ Intel สำหรับการปรับใช้ AI ข้ามแพลตฟอร์ม
  - Neural Network Compression Framework (NNCF) สำหรับการปรับแต่งขั้นสูง
  - OpenVINO GenAI สำหรับการปรับใช้โมเดลภาษาขนาดใหญ่
  - การเร่งความเร็วฮาร์ดแวร์บน CPU, GPU, VPU และตัวเร่ง AI

- [**Section 5: เจาะลึก Apple MLX Framework**](./Module04/05.AppleMLX.md)
  - สถาปัตยกรรมหน่วยความจำรวมสำหรับ Apple Silicon
  - การสนับสนุน LLaMA, Mistral, Phi-3, โมเดล Qwen ที่เลือก
  - การปรับแต่ง LoRA และการปรับแต่งโมเดล
  - การผสานกับ Hugging Face พร้อมการลดขนาด 4-bit/8-bit

- [**Section 6: การสังเคราะห์เวิร์กโฟลว์การพัฒนา Edge AI**](./Module04/06.workflow-synthesis.md)
  - สถาปัตยกรรมเวิร์กโฟลว์แบบรวมที่ผสานกรอบการปรับแต่งหลายตัว
  - ต้นไม้การตัดสินใจเลือกกรอบการทำงานและการวิเคราะห์การแลกเปลี่ยนประสิทธิภาพ
  - การตรวจสอบความพร้อมสำหรับการผลิตและกลยุทธ์การปรับใช้ที่ครอบคลุม
  - กลยุทธ์การเตรียมพร้อมสำหรับฮาร์ดแวร์และสถาปัตยกรรมโมเดลที่เกิดขึ้นใหม่

---

### [Module 05: SLMOps - การดำเนินงานโมเดลภาษาขนาดเล็ก](./Module05/README.md)
**ธีม**: การดำเนินงานวงจรชีวิต SLM ตั้งแต่การกลั่นจนถึงการปรับใช้ในผลิตภัณฑ์

#### โครงสร้างบท:
- [**Section 1: แนะนำ SLMOps**](./Module05/01.IntroduceSLMOps.md)
  - การเปลี่ยนแปลงกระบวนทัศน์ SLMOps ในการดำเนินงาน AI
  - สถาปัตยกรรมที่คุ้มค่าและเน้นความเป็นส่วนตัว
  - ผลกระทบเชิงกลยุทธ์ต่อธุรกิจและข้อได้เปรียบทางการแข่งขัน
  - ความท้าทายและวิธีแก้ปัญหาในการใช้งานจริง

- [**Section 2: การกลั่นโมเดล - จากทฤษฎีสู่การปฏิบัติ**](./Module05/02.SLMOps-Distillation.md)
  - การถ่ายโอนความรู้จากโมเดลครูสู่โมเดลนักเรียน
  - การดำเนินการกระบวนการกลั่นสองขั้นตอน
  - เวิร์กโฟลว์การกลั่น Azure ML พร้อมตัวอย่างการใช้งานจริง
  - ลดเวลาในการอนุมานลง 85% พร้อมรักษาความแม่นยำ 92%

- [**Section 3: การปรับแต่ง - การปรับแต่งโมเดลสำหรับงานเฉพาะ**](./Module05/03.SLMOps-Finetuing.md)
  - เทคนิคการปรับแต่งที่มีประสิทธิภาพด้านพารามิเตอร์ (PEFT)
  - วิธีขั้นสูง LoRA และ QLoRA
  - การปรับแต่งด้วย Microsoft Olive
  - การฝึกอบรมหลายตัวปรับแต่งและการปรับแต่งไฮเปอร์พารามิเตอร์

- [**Section 4: การปรับใช้ - การดำเนินการพร้อมใช้งานในผลิตภัณฑ์**](./Module05/04.SLMOps.Deployment.md)
  - การแปลงโมเดลและการลดขนาดสำหรับการผลิต
  - การกำหนดค่าการปรับใช้ Foundry Local
  - การเปรียบเทียบประสิทธิภาพและการตรวจสอบคุณภาพ
  - ลดขนาดลง 75% พร้อมการตรวจสอบการผลิต

---

### [Module 06: ระบบตัวแทน SLM - ตัวแทน AI และการเรียกฟังก์ชัน](./Module06/README.md)
**ธีม**: การใช้งานระบบตัวแทน SLM ตั้งแต่พื้นฐานจนถึงการเรียกฟังก์ชันขั้นสูงและการผสาน Model Context Protocol

#### โครงสร้างบท:
- [**Section 1: ตัวแทน AI และพื้นฐานโมเดลภาษาขนาดเล็ก**](./Module06/01.IntroduceAgent.md)
  - กรอบการจำแนกประเภทตัวแทน (ตัวแทนสะท้อน, ตัวแทนตามโมเดล, ตัวแทนตามเป้าหมาย, ตัวแทนเรียนรู้)
  - พื้นฐาน SLM และกลยุทธ์การปรับแต่ง (GGUF, การลดขนาด, กรอบงาน Edge)
  - การวิเคราะห์การแลกเปลี่ยนระหว่าง SLM และ LLM (ลดต้นทุน 10-30×, ประสิทธิภาพงาน 70-80%)
  - การปรับใช้จริงด้วย Ollama, VLLM และโซลูชัน Edge ของ Microsoft

- [**Section 2: การเรียกฟังก์ชันในโมเดลภาษาขนาดเล็ก**](./Module06/02.FunctionCalling.md)
  - การดำเนินการเวิร์กโฟลว์อย่างเป็นระบบ (การตรวจจับเจตนา, เอาต์พุต JSON, การดำเนินการภายนอก)
  - การใช้งานเฉพาะแพลตฟอร์ม (Phi-4-mini, โมเดล Qwen ที่เลือก, Microsoft Foundry Local)
  - ตัวอย่างขั้นสูง (การทำงานร่วมกันของตัวแทนหลายตัว, การเลือกเครื่องมือแบบไดนามิก)
  - ข้อควรพิจารณาในการผลิต (การจำกัดอัตรา, การบันทึกการตรวจสอบ, มาตรการรักษาความปลอดภัย)

- [**Section 3: การผสาน Model Context Protocol (MCP)**](./Module06/03.IntroduceMCP.md)
  - สถาปัตยกรรมโปรโตคอลและการออกแบบระบบแบบชั้น
  - การสนับสนุนหลายแบ็กเอนด์ (Ollama สำหรับการพัฒนา, vLLM สำหรับการผลิต)
  - โปรโตคอลการเชื่อมต่อ (โหมด STDIO และ SSE)
  - การใช้งานจริง (การทำงานอัตโนมัติบนเว็บ, การประมวลผลข้อมูล, การผสาน API)

---

### [Module 07: ตัวอย่างการใช้งาน EdgeAI](./Module07/README.md)
**ธีม**: การใช้งาน EdgeAI อย่างครอบคลุมในแพลตฟอร์มและกรอบงานที่หลากหลาย

#### โครงสร้างบท:
- [**เครื่องมือ AI สำหรับ Visual Studio Code**](./Module07/aitoolkit.md)
  - สภาพแวดล้อมการพัฒนา Edge AI ที่ครอบคลุมภายใน VS Code
  - แคตตาล็อกโมเดลและการค้นพบสำหรับการปรับใช้ Edge
  - เวิร์กโฟลว์การทดสอบในพื้นที่, การปรับแต่ง และการพัฒนาตัวแทน
  - การตรวจสอบประสิทธิภาพและการประเมินสำหรับสถานการณ์ Edge

- [**คู่มือการพัฒนา EdgeAI บน Windows**](./Module07/windowdeveloper.md)
  - ภาพรวมแพลตฟอร์ม Windows AI Foundry อย่างครอบคลุม
  - Phi Silica API สำหรับการอนุมาน NPU ที่มีประสิทธิภาพ
  - Computer Vision APIs สำหรับการประมวลผลภาพและ OCR
  - Foundry Local CLI สำหรับการพัฒนาและทดสอบในพื้นที่

- [**EdgeAI ใน NVIDIA Jetson Orin Nano**](./Module07/README.md#1-edgeai-in-nvidia-jetson-orin-nano)
  - ประสิทธิภาพ AI 67 TOPS ในรูปแบบขนาดเท่าบัตรเครดิต
  - การสนับสนุนโมเดล Generative AI (vision transformers, LLMs, vision-language models)
  - การใช้งานในหุ่นยนต์, โดรน, กล้องอัจฉริยะ, อุปกรณ์อัตโนมัติ
  - แพลตฟอร์มราคาไม่แพง $249 สำหรับการพัฒนา AI ที่เข้าถึงได้

- [**EdgeAI ในแอปพลิเคชันมือถือด้วย .NET MAUI และ ONNX Runtime GenAI**](./Module07/README.md#2-edgeai-in-mobile-applications-with-net-maui-and-onnx-runtime-genai)
  - AI บนมือถือข้ามแพลตฟอร์มด้วยฐานโค้ด C# เดียว
  - การสนับสนุนการเร่งความเร็วฮาร์ดแวร์ (CPU, GPU, ตัวประมวลผล AI บนมือถือ)
  - การปรับแต่งเฉพาะแพลตฟอร์ม (CoreML สำหรับ iOS, NNAPI สำหรับ Android)
  - การดำเนินการวงจร Generative AI อย่างสมบูรณ์

- [**EdgeAI ใน Azure ด้วย Small Language Models Engine**](./Module07/README.md#3-edgeai-in-azure-with-small-language-models-engine)
  - สถาปัตยกรรมการปรับใช้แบบไฮบริดระหว่างคลาวด์และ Edge
  - การผสานบริการ Azure AI กับ ONNX Runtime
  - การปรับใช้ระดับองค์กรและการจัดการโมเดลอย่างต่อเนื่อง
  - เวิร์กโฟลว์ AI แบบไฮบริดสำหรับการประมวลผลเอกสารอัจฉริยะ

- [**EdgeAI กับ Windows ML**](./Module07/README.md#4-edgeai-with-windows-ml)
  - พื้นฐาน Windows AI Foundry สำหรับการอนุมานบนอุปกรณ์ที่มีประสิทธิภาพ
  - การสนับสนุนฮาร์ดแวร์สากล (AMD, Intel, NVIDIA, Qualcomm silicon)
  - การแยกนามธรรมฮาร์ดแวร์และการปรับแต่งอัตโนมัติ
  - กรอบงานแบบรวมสำหรับระบบฮาร์ดแวร์ Windows ที่หลากหลาย

- [**EdgeAI กับแอปพลิเคชัน Foundry Local**](./Module07/README.md#5-edgeai-with-foundry-local-applications)
  - การดำเนินการ RAG ที่เน้นความเป็นส่วนตัวด้วยทรัพยากรในพื้นที่
  - การผสานโมเดลภาษา Phi-3 กับการค้นหาเชิงความหมาย (เฉพาะโมเดล Phi)
  - การสนับสนุนฐานข้อมูลเวกเตอร์ในพื้นที่ (SQLite, Qdrant)
  - ความสามารถในการดำเนินการแบบออฟไลน์และอธิปไตยข้อมูล

## วัตถุประสงค์การเรียนรู้ของหลักสูตร

เมื่อจบหลักสูตร EdgeAI ที่ครอบคลุมนี้ คุณจะพัฒนาความเชี่ยวชาญในการออกแบบ ใช้งาน และปรับใช้โซลูชัน EdgeAI ที่พร้อมสำหรับการผลิต วิธีการที่มีโครงสร้างของเราช่วยให้คุณเชี่ยวชาญทั้งพื้นฐานทางทฤษฎีและทักษะการใช้งานจริง
หลักสูตรนี้จะนำคุณไปสู่แนวหน้าของการใช้งานเทคโนโลยี AI โดยที่ความสามารถอัจฉริยะถูกผสานเข้ากับอุปกรณ์และระบบที่ขับเคลื่อนชีวิตยุคใหม่อย่างไร้รอยต่อ

## แผนผังโครงสร้างไฟล์

```
edgeai-for-beginners/
├── imgs/
│   └── cover.png
├── Module01/ (EdgeAI Fundamentals and Transformation)
│   ├── 01.EdgeAIFundamentals.md
│   ├── 02.RealWorldCaseStudies.md
│   ├── 03.PracticalImplementationGuide.md
│   ├── 04.EdgeDeployment.md
│   └── README.md
├── Module02/ (Small Language Model Foundations)
│   ├── 01.PhiFamily.md
│   ├── 02.QwenFamily.md
│   ├── 03.GemmaFamily.md
│   ├── 04.BitNETFamily.md
│   ├── 05.mumodel.md
│   ├── 06.phisilica.md
│   └── README.md
├── Module03/ (SLM Deployment Practice)
│   ├── 01.SLMAdvancedLearning.md
│   ├── 02.DeployingSLMinLocalEnv.md
│   ├── 03.DeployingSLMinCloud.md
│   └── README.md
├── Module04/ (Model Format Conversion and Quantization)
│   ├── 01.Introduce.md
│   ├── 02.Llamacpp.md
│   ├── 03.MicrosoftOlive.md
│   ├── 04.openvino.md
│   ├── 05.AppleMLX.md
│   ├── 06.workflow-synthesis.md
│   └── README.md
├── Module05/ (SLMOps - Small Language Model Operations)
│   ├── 01.IntroduceSLMOps.md
│   ├── 02.SLMOps-Distillation.md
│   ├── 03.SLMOps-Finetuing.md
│   ├── 04.SLMOps.Deployment.md
│   └── README.md
├── Module06/ (SLM Agentic Systems)
│   ├── 01.IntroduceAgent.md
│   ├── 02.FunctionCalling.md
│   ├── 03.IntroduceMCP.md
│   └── README.md
├── Module07/ (EdgeAI Implementation Samples)
│   ├── aitoolkit.md
│   ├── windowdeveloper.md
│   └── README.md
├── CODE_OF_CONDUCT.md
├── LICENSE
├── README.md (This file)
├── SECURITY.md
├── STUDY_GUIDE.md
└── SUPPORT.md
```

## คุณสมบัติของหลักสูตร

- **การเรียนรู้แบบก้าวหน้า**: เรียนรู้จากแนวคิดพื้นฐานไปจนถึงการใช้งานขั้นสูง
- **การผสานทฤษฎีและปฏิบัติ**: แต่ละโมดูลประกอบด้วยพื้นฐานทางทฤษฎีและการปฏิบัติจริง
- **กรณีศึกษาจริง**: อ้างอิงจากกรณีศึกษาจริงของ Microsoft, Alibaba, Google และอื่นๆ
- **การฝึกปฏิบัติจริง**: การตั้งค่าไฟล์, ขั้นตอนการทดสอบ API และสคริปต์การใช้งาน
- **การเปรียบเทียบประสิทธิภาพ**: การวิเคราะห์ความเร็วในการประมวลผล, การใช้หน่วยความจำ และความต้องการทรัพยากร
- **การพิจารณาระดับองค์กร**: แนวทางปฏิบัติด้านความปลอดภัย, กรอบการปฏิบัติตามข้อกำหนด และกลยุทธ์การปกป้องข้อมูล

## เริ่มต้นการเรียนรู้

เส้นทางการเรียนรู้ที่แนะนำ:
1. เริ่มต้นด้วย **Module01** เพื่อสร้างความเข้าใจพื้นฐานเกี่ยวกับ EdgeAI
2. ดำเนินการต่อด้วย **Module02** เพื่อเข้าใจเชิงลึกเกี่ยวกับกลุ่มโมเดล SLM ต่างๆ
3. เรียนรู้ **Module03** เพื่อเชี่ยวชาญทักษะการใช้งานจริง
4. ต่อด้วย **Module04** สำหรับการปรับแต่งโมเดลขั้นสูง, การแปลงรูปแบบ และการผสานกรอบการทำงาน
5. จบ **Module05** เพื่อเชี่ยวชาญ SLMOps สำหรับการใช้งานที่พร้อมสำหรับการผลิต
6. สำรวจ **Module06** เพื่อเข้าใจระบบ SLM แบบตัวแทนและความสามารถในการเรียกใช้งานฟังก์ชัน
7. ปิดท้ายด้วย **Module07** เพื่อรับประสบการณ์จริงกับ AI Toolkit และตัวอย่างการใช้งาน EdgeAI ที่หลากหลาย

แต่ละโมดูลถูกออกแบบให้สมบูรณ์ในตัวเอง แต่การเรียนรู้ตามลำดับจะให้ผลลัพธ์ที่ดีที่สุด

## คู่มือการศึกษา

[คู่มือการศึกษา](STUDY_GUIDE.md) ที่ครอบคลุมมีให้เพื่อช่วยให้คุณเพิ่มประสิทธิภาพการเรียนรู้ของคุณ คู่มือการศึกษานี้ประกอบด้วย:

- **เส้นทางการเรียนรู้ที่มีโครงสร้าง**: ตารางเวลาที่ปรับให้เหมาะสมสำหรับการเรียนจบหลักสูตรใน 20 ชั่วโมง
- **คำแนะนำการจัดสรรเวลา**: คำแนะนำเฉพาะสำหรับการสมดุลระหว่างการอ่าน, การฝึกฝน และโครงการ
- **การเน้นแนวคิดสำคัญ**: วัตถุประสงค์การเรียนรู้ที่จัดลำดับความสำคัญสำหรับแต่ละโมดูล
- **เครื่องมือประเมินตนเอง**: คำถามและแบบฝึกหัดเพื่อทดสอบความเข้าใจของคุณ
- **ไอเดียโครงการขนาดเล็ก**: การประยุกต์ใช้งานจริงเพื่อเสริมสร้างการเรียนรู้ของคุณ

คู่มือการศึกษานี้ถูกออกแบบมาให้เหมาะสมทั้งการเรียนรู้แบบเข้มข้น (1 สัปดาห์) และการเรียนรู้แบบพาร์ทไทม์ (3 สัปดาห์) พร้อมคำแนะนำที่ชัดเจนเกี่ยวกับวิธีการจัดสรรเวลาอย่างมีประสิทธิภาพ แม้ว่าคุณจะมีเวลาเรียนเพียง 10 ชั่วโมงก็ตาม

---

**อนาคตของ EdgeAI อยู่ที่การพัฒนาอย่างต่อเนื่องของสถาปัตยกรรมโมเดล, เทคนิคการลดขนาด และกลยุทธ์การใช้งานที่ให้ความสำคัญกับประสิทธิภาพและความเชี่ยวชาญเฉพาะด้านมากกว่าความสามารถทั่วไป องค์กรที่ยอมรับการเปลี่ยนแปลงนี้จะอยู่ในตำแหน่งที่ดีในการใช้ศักยภาพการเปลี่ยนแปลงของ AI ในขณะที่ยังคงควบคุมข้อมูลและการดำเนินงานของตนได้**

## หลักสูตรอื่นๆ

ทีมของเราผลิตหลักสูตรอื่นๆ! ลองดู:

- [MCP for Beginners](https://github.com/microsoft/mcp-for-beginners)
- [AI Agents For Beginners](https://github.com/microsoft/ai-agents-for-beginners?WT.mc_id=academic-105485-koreyst)
- [Generative AI for Beginners using .NET](https://github.com/microsoft/Generative-AI-for-beginners-dotnet?WT.mc_id=academic-105485-koreyst)
- [Generative AI for Beginners using JavaScript](https://github.com/microsoft/generative-ai-with-javascript?WT.mc_id=academic-105485-koreyst)
- [Generative AI for Beginners](https://github.com/microsoft/generative-ai-for-beginners?WT.mc_id=academic-105485-koreyst)
- [ML for Beginners](https://aka.ms/ml-beginners?WT.mc_id=academic-105485-koreyst)
- [Data Science for Beginners](https://aka.ms/datascience-beginners?WT.mc_id=academic-105485-koreyst)
- [AI for Beginners](https://aka.ms/ai-beginners?WT.mc_id=academic-105485-koreyst)
- [Cybersecurity for Beginners](https://github.com/microsoft/Security-101??WT.mc_id=academic-96948-sayoung)
- [Web Dev for Beginners](https://aka.ms/webdev-beginners?WT.mc_id=academic-105485-koreyst)
- [IoT for Beginners](https://aka.ms/iot-beginners?WT.mc_id=academic-105485-koreyst)
- [XR Development for Beginners](https://github.com/microsoft/xr-development-for-beginners?WT.mc_id=academic-105485-koreyst)
- [Mastering GitHub Copilot for AI Paired Programming](https://aka.ms/GitHubCopilotAI?WT.mc_id=academic-105485-koreyst)
- [Mastering GitHub Copilot for C#/.NET Developers](https://github.com/microsoft/mastering-github-copilot-for-dotnet-csharp-developers?WT.mc_id=academic-105485-koreyst)
- [Choose Your Own Copilot Adventure](https://github.com/microsoft/CopilotAdventures?WT.mc_id=academic-105485-koreyst)

---

**ข้อจำกัดความรับผิดชอบ**:  
เอกสารนี้ได้รับการแปลโดยใช้บริการแปลภาษา AI [Co-op Translator](https://github.com/Azure/co-op-translator) แม้ว่าเราจะพยายามให้การแปลมีความถูกต้องมากที่สุด แต่โปรดทราบว่าการแปลอัตโนมัติอาจมีข้อผิดพลาดหรือความไม่ถูกต้อง เอกสารต้นฉบับในภาษาดั้งเดิมควรถือเป็นแหล่งข้อมูลที่เชื่อถือได้ สำหรับข้อมูลที่สำคัญ ขอแนะนำให้ใช้บริการแปลภาษามืออาชีพ เราไม่รับผิดชอบต่อความเข้าใจผิดหรือการตีความผิดที่เกิดจากการใช้การแปลนี้