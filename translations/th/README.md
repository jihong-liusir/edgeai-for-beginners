<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "9a189d7d9d47816a518ca119d79dc19b",
  "translation_date": "2025-09-22T19:00:18+00:00",
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

**หากคุณต้องการให้มีการรองรับภาษาเพิ่มเติม รายการภาษาที่รองรับสามารถดูได้ [ที่นี่](https://github.com/Azure/co-op-translator/blob/main/getting_started/supported-languages.md)**

## บทนำ

ยินดีต้อนรับสู่ **EdgeAI สำหรับผู้เริ่มต้น** – การเดินทางที่ครอบคลุมสู่โลกแห่ง Edge Artificial Intelligence ที่เปลี่ยนแปลงวงการ คอร์สนี้จะช่วยให้คุณเข้าใจและนำความสามารถของ AI ไปใช้ในอุปกรณ์ edge เพื่อการตัดสินใจที่รวดเร็วและมีประสิทธิภาพในที่ที่ข้อมูลถูกสร้างขึ้น

### สิ่งที่คุณจะได้เรียนรู้

คอร์สนี้จะพาคุณตั้งแต่แนวคิดพื้นฐานไปจนถึงการใช้งานจริงในระดับผลิตภัณฑ์ โดยครอบคลุม:
- **Small Language Models (SLMs)** ที่ปรับแต่งสำหรับการใช้งานในอุปกรณ์ edge  
- **การปรับแต่งให้เหมาะกับฮาร์ดแวร์** บนแพลตฟอร์มหลากหลาย  
- **การวิเคราะห์แบบเรียลไทม์** พร้อมความสามารถในการรักษาความเป็นส่วนตัว  
- **กลยุทธ์การใช้งานในระดับผลิตภัณฑ์** สำหรับแอปพลิเคชันในองค์กร  

### ทำไม EdgeAI ถึงสำคัญ

Edge AI เป็นการเปลี่ยนแปลงที่ช่วยแก้ไขปัญหาสำคัญในยุคปัจจุบัน:
- **ความเป็นส่วนตัวและความปลอดภัย**: ประมวลผลข้อมูลสำคัญในพื้นที่โดยไม่ต้องส่งไปยังคลาวด์  
- **ประสิทธิภาพแบบเรียลไทม์**: ลดความล่าช้าจากเครือข่ายสำหรับแอปพลิเคชันที่ต้องการความรวดเร็ว  
- **ความคุ้มค่า**: ลดค่าใช้จ่ายด้านแบนด์วิดท์และการประมวลผลในคลาวด์  
- **การทำงานที่ยืดหยุ่น**: สามารถทำงานได้แม้ในกรณีที่เครือข่ายล่ม  
- **การปฏิบัติตามกฎระเบียบ**: รองรับข้อกำหนดด้านความเป็นเจ้าของข้อมูล  

### Edge AI

Edge AI หมายถึงการรันอัลกอริทึม AI และโมเดลภาษาบนฮาร์ดแวร์ในพื้นที่ใกล้กับที่ข้อมูลถูกสร้างขึ้น โดยไม่ต้องพึ่งพาทรัพยากรคลาวด์สำหรับการวิเคราะห์ ซึ่งช่วยลดความล่าช้า เพิ่มความเป็นส่วนตัว และช่วยให้ตัดสินใจได้แบบเรียลไทม์

### หลักการสำคัญ:
- **การวิเคราะห์บนอุปกรณ์**: โมเดล AI ทำงานบนอุปกรณ์ edge เช่น โทรศัพท์ เราเตอร์ ไมโครคอนโทรลเลอร์ และ PC อุตสาหกรรม  
- **ความสามารถในการทำงานแบบออฟไลน์**: ทำงานได้โดยไม่ต้องเชื่อมต่ออินเทอร์เน็ตตลอดเวลา  
- **ความล่าช้าต่ำ**: ตอบสนองทันทีเหมาะสำหรับระบบเรียลไทม์  
- **การรักษาความเป็นเจ้าของข้อมูล**: เก็บข้อมูลสำคัญไว้ในพื้นที่เพื่อเพิ่มความปลอดภัยและการปฏิบัติตามกฎระเบียบ  

### Small Language Models (SLMs)

SLMs เช่น Phi-4, Mistral-7B และ Gemma เป็นเวอร์ชันที่ปรับแต่งของ LLMs ขนาดใหญ่ โดยถูกฝึกหรือปรับแต่งเพื่อ:
- **ลดการใช้หน่วยความจำ**: ใช้หน่วยความจำในอุปกรณ์ edge อย่างมีประสิทธิภาพ  
- **ลดความต้องการในการประมวลผล**: ปรับแต่งให้เหมาะกับ CPU และ GPU ในอุปกรณ์ edge  
- **เริ่มต้นใช้งานได้เร็วขึ้น**: การเริ่มต้นที่รวดเร็วสำหรับแอปพลิเคชันที่ต้องการการตอบสนอง  

SLMs ช่วยให้สามารถใช้งาน NLP ที่ทรงพลังได้ในข้อจำกัดของ:
- **ระบบฝังตัว**: อุปกรณ์ IoT และตัวควบคุมอุตสาหกรรม  
- **อุปกรณ์มือถือ**: สมาร์ทโฟนและแท็บเล็ตที่มีความสามารถในการทำงานแบบออฟไลน์  
- **อุปกรณ์ IoT**: เซ็นเซอร์และอุปกรณ์อัจฉริยะที่มีทรัพยากรจำกัด  
- **เซิร์ฟเวอร์ edge**: หน่วยประมวลผลในพื้นที่ที่มีทรัพยากร GPU จำกัด  
- **คอมพิวเตอร์ส่วนบุคคล**: การใช้งานบนเดสก์ท็อปและแล็ปท็อป  

## โครงสร้างคอร์ส

### [Module 01: พื้นฐาน EdgeAI และการเปลี่ยนแปลง](./Module01/README.md)  
**ธีม**: การเปลี่ยนแปลงของการใช้งาน Edge AI  

#### โครงสร้างบท:
- [**Section 1: พื้นฐาน EdgeAI**](./Module01/01.EdgeAIFundamentals.md)  
  - เปรียบเทียบ AI บนคลาวด์แบบดั้งเดิมกับ Edge AI  
  - ความท้าทายและข้อจำกัดของการประมวลผล edge  
  - เทคโนโลยีสำคัญ: การลดขนาดโมเดล การปรับแต่ง และ Small Language Models (SLMs)  
  - การเร่งความเร็วด้วยฮาร์ดแวร์: NPUs, GPU optimization, CPU optimization  
  - ข้อดี: ความปลอดภัย ความล่าช้าต่ำ ความสามารถในการทำงานแบบออฟไลน์ ความคุ้มค่า  

- [**Section 2: กรณีศึกษาในโลกจริง**](./Module01/02.RealWorldCaseStudies.md)  
  - ระบบโมเดล Phi & Mu ของ Microsoft  
  - กรณีศึกษาระบบรายงาน AI ของ Japan Airlines  
  - ผลกระทบต่อตลาดและทิศทางในอนาคต  
  - ข้อควรพิจารณาและแนวทางปฏิบัติที่ดีที่สุดในการใช้งาน  

- [**Section 3: คู่มือการใช้งานจริง**](./Module01/03.PracticalImplementationGuide.md)  
  - การตั้งค่าสภาพแวดล้อมการพัฒนา (Python 3.10+, .NET 8+)  
  - ความต้องการฮาร์ดแวร์และการกำหนดค่าที่แนะนำ  
  - ทรัพยากรโมเดลหลัก  
  - เครื่องมือการลดขนาดและการปรับแต่ง (Llama.cpp, Microsoft Olive, Apple MLX)  
  - รายการตรวจสอบการประเมินผลและการตรวจสอบ  

- [**Section 4: แพลตฟอร์มฮาร์ดแวร์สำหรับการใช้งาน Edge AI**](./Module01/04.EdgeDeployment.md)  
  - ข้อควรพิจารณาและความต้องการในการใช้งาน Edge AI  
  - ฮาร์ดแวร์ Edge AI ของ Intel และเทคนิคการปรับแต่ง  
  - โซลูชัน AI ของ Qualcomm สำหรับระบบมือถือและฝังตัว  
  - NVIDIA Jetson และแพลตฟอร์มการประมวลผล edge  
  - แพลตฟอร์ม Windows AI PC พร้อมการเร่งความเร็วด้วย NPU  
  - กลยุทธ์การปรับแต่งเฉพาะฮาร์ดแวร์  

---

### [Module 02: พื้นฐาน Small Language Models](./Module02/README.md)  
**ธีม**: หลักการทฤษฎี SLMs กลยุทธ์การใช้งาน และการใช้งานในระดับผลิตภัณฑ์  

#### โครงสร้างบท:
- [**Section 1: พื้นฐานตระกูลโมเดล Microsoft Phi**](./Module02/01.PhiFamily.md)  
  - วิวัฒนาการของปรัชญาการออกแบบ (Phi-1 ถึง Phi-4)  
  - การออกแบบสถาปัตยกรรมที่เน้นประสิทธิภาพ  
  - ความสามารถเฉพาะทาง (การให้เหตุผล, มัลติโหมด, การใช้งาน edge)  

- [**Section 2: พื้นฐานตระกูล Qwen**](./Module02/02.QwenFamily.md)  
  - ความเป็นเลิศในโอเพ่นซอร์ส (Qwen 1.0 ถึง Qwen3) - มีให้ใช้งานผ่าน Hugging Face  
  - สถาปัตยกรรมการให้เหตุผลขั้นสูงพร้อมความสามารถในโหมดคิด  
  - ตัวเลือกการใช้งานที่ปรับขนาดได้ (0.5B-235B พารามิเตอร์)  

- [**Section 3: พื้นฐานตระกูล Gemma**](./Module02/03.GemmaFamily.md)  
  - นวัตกรรมที่ขับเคลื่อนด้วยการวิจัย (Gemma 3 & 3n)  
  - ความเป็นเลิศในมัลติโหมด  
  - สถาปัตยกรรมที่เน้นมือถือ  

- [**Section 4: พื้นฐานตระกูล BitNET**](./Module02/04.BitNETFamily.md)  
  - เทคโนโลยีการลดขนาดที่ปฏิวัติวงการ (1.58-bit)  
  - เฟรมเวิร์กการวิเคราะห์เฉพาะทางจาก https://github.com/microsoft/BitNet  
  - ความเป็นผู้นำด้าน AI ที่ยั่งยืนผ่านประสิทธิภาพขั้นสูง  

- [**Section 5: พื้นฐานตระกูลโมเดล Microsoft Mu**](./Module02/05.mumodel.md)  
  - สถาปัตยกรรมที่เน้นอุปกรณ์ซึ่งสร้างขึ้นใน Windows 11  
  - การผสานรวมระบบกับการตั้งค่า Windows 11  
  - การทำงานแบบออฟไลน์ที่รักษาความเป็นส่วนตัว  

- [**Section 6: พื้นฐาน Phi-Silica**](./Module02/06.phisilica.md)  
  - สถาปัตยกรรมที่ปรับแต่งสำหรับ NPU ซึ่งสร้างขึ้นใน Windows 11 Copilot+ PCs  
  - ประสิทธิภาพที่ยอดเยี่ยม (650 tokens/second ที่ 1.5W)  
  - การผสานรวมสำหรับนักพัฒนากับ Windows App SDK  

---

### [Module 03: การใช้งาน Small Language Models](./Module03/README.md)  
**ธีม**: วงจรการใช้งาน SLMs ครบวงจร ตั้งแต่ทฤษฎีจนถึงสภาพแวดล้อมการผลิต  

#### โครงสร้างบท:
- [**Section 1: การเรียนรู้ขั้นสูงของ SLMs**](./Module03/01.SLMAdvancedLearning.md)  
  - เฟรมเวิร์กการจำแนกพารามิเตอร์ (Micro SLM 100M-1.4B, Medium SLM 14B-30B)  
  - เทคนิคการปรับแต่งขั้นสูง (วิธีการลดขนาด, BitNET 1-bit quantization)  
  - กลยุทธ์การได้มาของโมเดล (Azure AI Foundry สำหรับ Phi models, Hugging Face สำหรับโมเดลที่เลือก)  

- [**Section 2: การใช้งานในสภาพแวดล้อมท้องถิ่น**](./Module03/02.DeployingSLMinLocalEnv.md)  
  - การใช้งานแพลตฟอร์ม Ollama แบบสากล  
  - โซลูชันระดับองค์กรในพื้นที่ของ Microsoft Foundry  
  - การวิเคราะห์เปรียบเทียบเฟรมเวิร์ก  

- [**Section 3: การใช้งานในคลาวด์แบบคอนเทนเนอร์**](./Module03/03.DeployingSLMinCloud.md)  
  - การใช้งานการวิเคราะห์ประสิทธิภาพสูงด้วย vLLM  
  - การจัดการคอนเทนเนอร์ Ollama  
  - การใช้งานที่ปรับแต่งสำหรับ edge ด้วย ONNX Runtime  

---

### [Module 04: การแปลงรูปแบบโมเดลและการลดขนาด](./Module04/README.md)  
**ธีม**: เครื่องมือการปรับแต่งโมเดลครบวงจรสำหรับการใช้งาน edge บนแพลตฟอร์มต่างๆ  

#### โครงสร้างบท:
- [**Section 1: พื้นฐานการแปลงรูปแบบโมเดลและการลดขนาด**](./Module04/01.Introduce.md)  
  - เฟรมเวิร์กการจำแนกความแม่นยำ (ultra-low, low, medium precision)  
  - ข้อ
- [**Section 2: คู่มือการใช้งาน Llama.cpp**](./Module04/02.Llamacpp.md)
  - การติดตั้งข้ามแพลตฟอร์ม (Windows, macOS, Linux)
  - การแปลงรูปแบบ GGUF และระดับการลดขนาด (Q2_K ถึง Q8_0)
  - การเร่งความเร็วด้วยฮาร์ดแวร์ (CUDA, Metal, OpenCL, Vulkan)
  - การผสาน Python และการใช้งาน REST API

- [**Section 3: Microsoft Olive Optimization Suite**](./Module04/03.MicrosoftOlive.md)
  - การปรับแต่งโมเดลตามฮาร์ดแวร์ด้วยส่วนประกอบในตัวกว่า 40 รายการ
  - การปรับแต่งอัตโนมัติด้วยการลดขนาดแบบไดนามิกและแบบคงที่
  - การผสานในระดับองค์กรกับเวิร์กโฟลว์ Azure ML
  - การสนับสนุนโมเดลยอดนิยม (Llama, Phi, โมเดล Qwen ที่เลือก, Gemma)

- [**Section 4: OpenVINO Toolkit Optimization Suite**](./Module04/04.openvino.md)
  - เครื่องมือโอเพ่นซอร์สของ Intel สำหรับการใช้งาน AI ข้ามแพลตฟอร์ม
  - Neural Network Compression Framework (NNCF) สำหรับการปรับแต่งขั้นสูง
  - OpenVINO GenAI สำหรับการใช้งานโมเดลภาษาขนาดใหญ่
  - การเร่งความเร็วด้วยฮาร์ดแวร์บน CPU, GPU, VPU และตัวเร่ง AI

- [**Section 5: เจาะลึก Apple MLX Framework**](./Module04/05.AppleMLX.md)
  - สถาปัตยกรรมหน่วยความจำรวมสำหรับ Apple Silicon
  - การสนับสนุน LLaMA, Mistral, Phi, โมเดล Qwen ที่เลือก
  - การปรับแต่ง LoRA และการปรับแต่งโมเดล
  - การผสานกับ Hugging Face พร้อมการลดขนาด 4-bit/8-bit

- [**Section 6: การสังเคราะห์เวิร์กโฟลว์การพัฒนา Edge AI**](./Module04/06.workflow-synthesis.md)
  - สถาปัตยกรรมเวิร์กโฟลว์แบบรวมที่ผสานกรอบการปรับแต่งหลายตัว
  - ต้นไม้การตัดสินใจเลือกกรอบการทำงานและการวิเคราะห์การแลกเปลี่ยนประสิทธิภาพ
  - การตรวจสอบความพร้อมใช้งานในระดับการผลิตและกลยุทธ์การใช้งานที่ครอบคลุม
  - กลยุทธ์การเตรียมพร้อมสำหรับฮาร์ดแวร์และสถาปัตยกรรมโมเดลที่เกิดขึ้นใหม่

---

### [Module 05: SLMOps - การดำเนินงานโมเดลภาษาขนาดเล็ก](./Module05/README.md)
**ธีม**: การดำเนินงานวงจรชีวิต SLM ตั้งแต่การกลั่นจนถึงการใช้งานในระดับการผลิต

#### โครงสร้างบท:
- [**Section 1: บทนำสู่ SLMOps**](./Module05/01.IntroduceSLMOps.md)
  - การเปลี่ยนแปลงแนวคิด SLMOps ในการดำเนินงาน AI
  - สถาปัตยกรรมที่คุ้มค่าและเน้นความเป็นส่วนตัว
  - ผลกระทบเชิงกลยุทธ์ต่อธุรกิจและข้อได้เปรียบทางการแข่งขัน
  - ความท้าทายและวิธีแก้ปัญหาในการใช้งานจริง

- [**Section 2: การกลั่นโมเดล - จากทฤษฎีสู่การปฏิบัติ**](./Module05/02.SLMOps-Distillation.md)
  - การถ่ายโอนความรู้จากโมเดลครูสู่โมเดลนักเรียน
  - การใช้งานกระบวนการกลั่นสองขั้นตอน
  - เวิร์กโฟลว์การกลั่น Azure ML พร้อมตัวอย่างการใช้งานจริง
  - ลดเวลาในการประมวลผลลง 85% พร้อมรักษาความแม่นยำไว้ 92%

- [**Section 3: การปรับแต่ง - การปรับแต่งโมเดลสำหรับงานเฉพาะ**](./Module05/03.SLMOps-Finetuing.md)
  - เทคนิคการปรับแต่งที่มีประสิทธิภาพด้านพารามิเตอร์ (PEFT)
  - วิธีการขั้นสูง LoRA และ QLoRA
  - การใช้งานการปรับแต่ง Microsoft Olive
  - การฝึกอบรมหลายตัวปรับแต่งและการปรับแต่งไฮเปอร์พารามิเตอร์

- [**Section 4: การใช้งาน - การปรับแต่งให้พร้อมสำหรับการผลิต**](./Module05/04.SLMOps.Deployment.md)
  - การแปลงโมเดลและการลดขนาดสำหรับการผลิต
  - การตั้งค่าการใช้งาน Foundry Local
  - การวัดประสิทธิภาพและการตรวจสอบคุณภาพ
  - ลดขนาดลง 75% พร้อมการตรวจสอบการใช้งานในระดับการผลิต

---

### [Module 06: SLM Agentic Systems - AI Agents และการเรียกฟังก์ชัน](./Module06/README.md)
**ธีม**: การใช้งานระบบ SLM agentic ตั้งแต่พื้นฐานจนถึงการเรียกฟังก์ชันขั้นสูงและการผสาน Model Context Protocol

#### โครงสร้างบท:
- [**Section 1: พื้นฐาน AI Agents และ Small Language Models**](./Module06/01.IntroduceAgent.md)
  - กรอบการจัดประเภทเอเจนต์ (reflex, model-based, goal-based, learning agents)
  - พื้นฐาน SLM และกลยุทธ์การปรับแต่ง (GGUF, การลดขนาด, กรอบงาน edge)
  - การวิเคราะห์การแลกเปลี่ยนระหว่าง SLM และ LLM (ลดต้นทุน 10-30×, ประสิทธิภาพงาน 70-80%)
  - การใช้งานจริงด้วย Ollama, VLLM และโซลูชัน edge ของ Microsoft

- [**Section 2: การเรียกฟังก์ชันใน Small Language Models**](./Module06/02.FunctionCalling.md)
  - การใช้งานเวิร์กโฟลว์อย่างเป็นระบบ (การตรวจจับเจตนา, JSON output, การดำเนินการภายนอก)
  - การใช้งานเฉพาะแพลตฟอร์ม (Phi-4-mini, โมเดล Qwen ที่เลือก, Microsoft Foundry Local)
  - ตัวอย่างขั้นสูง (การทำงานร่วมกันของหลายเอเจนต์, การเลือกเครื่องมือแบบไดนามิก)
  - ข้อควรพิจารณาในการผลิต (การจำกัดอัตรา, การบันทึกการตรวจสอบ, มาตรการความปลอดภัย)

- [**Section 3: การผสาน Model Context Protocol (MCP)**](./Module06/03.IntroduceMCP.md)
  - สถาปัตยกรรมโปรโตคอลและการออกแบบระบบแบบชั้น
  - การสนับสนุนหลาย backend (Ollama สำหรับการพัฒนา, vLLM สำหรับการผลิต)
  - โปรโตคอลการเชื่อมต่อ (โหมด STDIO และ SSE)
  - การใช้งานจริง (การทำงานอัตโนมัติบนเว็บ, การประมวลผลข้อมูล, การผสาน API)

---

### [Module 07: ตัวอย่างการใช้งาน EdgeAI](./Module07/README.md)
**ธีม**: การใช้งาน EdgeAI อย่างครอบคลุมในแพลตฟอร์มและกรอบงานที่หลากหลาย

#### โครงสร้างบท:
- [**AI Toolkit สำหรับ Visual Studio Code**](./Module07/aitoolkit.md)
  - สภาพแวดล้อมการพัฒนา Edge AI ที่ครอบคลุมภายใน VS Code
  - แคตตาล็อกโมเดลและการค้นพบสำหรับการใช้งาน edge
  - เวิร์กโฟลว์การทดสอบในเครื่อง, การปรับแต่ง และการพัฒนาเอเจนต์
  - การตรวจสอบประสิทธิภาพและการประเมินสำหรับสถานการณ์ edge

- [**คู่มือการพัฒนา EdgeAI บน Windows**](./Module07/windowdeveloper.md)
  - ภาพรวมแพลตฟอร์ม Windows AI Foundry อย่างครอบคลุม
  - Phi Silica API สำหรับการประมวลผล NPU ที่มีประสิทธิภาพ
  - Computer Vision APIs สำหรับการประมวลผลภาพและ OCR
  - Foundry Local CLI สำหรับการพัฒนาและทดสอบในเครื่อง

- [**EdgeAI ใน NVIDIA Jetson Orin Nano**](./Module07/README.md#1-edgeai-in-nvidia-jetson-orin-nano)
  - ประสิทธิภาพ AI 67 TOPS ในขนาดเท่าบัตรเครดิต
  - การสนับสนุนโมเดล Generative AI (vision transformers, LLMs, vision-language models)
  - การใช้งานในหุ่นยนต์, โดรน, กล้องอัจฉริยะ, อุปกรณ์อัตโนมัติ
  - แพลตฟอร์มราคาไม่แพง $249 สำหรับการพัฒนา AI ที่เข้าถึงได้

- [**EdgeAI ในแอปพลิเคชันมือถือด้วย .NET MAUI และ ONNX Runtime GenAI**](./Module07/README.md#2-edgeai-in-mobile-applications-with-net-maui-and-onnx-runtime-genai)
  - AI บนมือถือข้ามแพลตฟอร์มด้วยฐานโค้ด C# เดียว
  - การสนับสนุนการเร่งความเร็วด้วยฮาร์ดแวร์ (CPU, GPU, ตัวประมวลผล AI บนมือถือ)
  - การปรับแต่งเฉพาะแพลตฟอร์ม (CoreML สำหรับ iOS, NNAPI สำหรับ Android)
  - การใช้งานวงจร Generative AI อย่างสมบูรณ์

- [**EdgeAI ใน Azure ด้วย Small Language Models Engine**](./Module07/README.md#3-edgeai-in-azure-with-small-language-models-engine)
  - สถาปัตยกรรมการใช้งานแบบไฮบริดระหว่างคลาวด์และ edge
  - การผสานบริการ Azure AI กับ ONNX Runtime
  - การใช้งานในระดับองค์กรและการจัดการโมเดลอย่างต่อเนื่อง
  - เวิร์กโฟลว์ AI แบบไฮบริดสำหรับการประมวลผลเอกสารอัจฉริยะ

- [**EdgeAI กับ Windows ML**](./Module07/README.md#4-edgeai-with-windows-ml)
  - พื้นฐาน Windows AI Foundry สำหรับการประมวลผลในอุปกรณ์ที่มีประสิทธิภาพ
  - การสนับสนุนฮาร์ดแวร์แบบสากล (AMD, Intel, NVIDIA, Qualcomm silicon)
  - การแยกฮาร์ดแวร์และการปรับแต่งอัตโนมัติ
  - กรอบงานแบบรวมสำหรับระบบฮาร์ดแวร์ Windows ที่หลากหลาย

- [**EdgeAI กับแอปพลิเคชัน Foundry Local**](./Module07/README.md#5-edgeai-with-foundry-local-applications)
  - การใช้งาน RAG ที่เน้นความเป็นส่วนตัวด้วยทรัพยากรในเครื่อง
  - การผสานโมเดลภาษา Phi-4 กับการค้นหาเชิงความหมาย (เฉพาะโมเดล Phi)
  - การสนับสนุนฐานข้อมูลเวกเตอร์ในเครื่อง (SQLite, Qdrant)
  - ความสามารถในการดำเนินการแบบออฟไลน์และการรักษาความเป็นเจ้าของข้อมูล

### [Module 08: Microsoft Foundry Local – ชุดเครื่องมือสำหรับนักพัฒนาแบบครบวงจร](./Module08/README.md)
**ธีม**: สร้าง, ใช้งาน และผสาน AI ในเครื่องด้วย Foundry Local; ขยายและผสานกับ Azure AI Foundry

#### โครงสร้างบท:
- [**1: เริ่มต้นใช้งาน Foundry Local**](./Module08/01.FoundryLocalSetup.md)
- [**2: สร้างโซลูชัน AI ด้วย Azure AI Foundry**](./Module08/02.AzureAIFoundryIntegration.md)
- [**3: โมเดลโอเพ่นซอร์ส Foundry Local**](./Module08/03.OpenSourceModels.md)
- [**4: โมเดลล้ำสมัยและการประมวลผลในอุปกรณ์**](./Module08/04.CuttingEdgeModels.md)
- [**5: เอเจนต์ที่ขับเคลื่อนด้วย AI กับ Foundry Local**](./Module08/05.AIPoweredAgents.md)
- [**6: โมเดลในฐานะเครื่องมือ**](./Module08/06.ModelsAsTools.md)

## วัตถุประสงค์การเรียนรู้ของหลักสูตร

เมื่อจบหลักสูตร EdgeAI นี้ คุณจะมีความเชี่ยวชาญในการออกแบบ, ใช้งาน และปรับใช้โซลูชัน EdgeAI ที่พร้อมสำหรับการผลิต วิธีการที่มีโครงสร้างของเราจะช่วยให้คุณเชี่ยวชาญทั้งพื้นฐานทางทฤษฎีและทักษะการใช้งานจริง

### ความสามารถทางเทคนิค

**ความรู้พื้นฐาน**
- เข้าใจความแตกต่างพื้นฐานระหว่างสถาปัตยกรรม AI บนคลาวด์และ edge
- เชี่ยวชาญหลักการของการลดขนาดโมเดล, การบีบอัด และการปรับแต่งสำหรับสภาพแวดล้อมที่มีทรัพยากรจำกัด
- เข้าใจตัวเลือกการเร่งความเร็วด้วยฮาร์ดแวร์ (NPUs, GPUs, CPUs) และผลกระทบต่อการใช้งาน

**ทักษะการใช้งาน**
- ใช้งาน Small Language Models บนแพลตฟอร์ม edge ที่หลากหลาย (มือถือ, อุปกรณ์ฝังตัว, IoT, edge servers)
- ใช้กรอบการปรับแต่ง เช่น Llama.cpp, Microsoft Olive, ONNX Runtime และ Apple MLX
- ใช้งานระบบการประมวลผลแบบเรียลไทม์ที่มีข้อกำหนดการตอบสนองในระดับเสี้ยววินาที

**ความเชี่ยวชาญในระดับการผลิต**
- ออกแบบสถาปัตยกรรม EdgeAI ที่ปรับขยายได้สำหรับการใช้งานในองค์กร
- ใช้งานกลยุทธ์การตรวจสอบ, การบำรุงรักษา และการอัปเดตสำหรับระบบที่ปรับใช้แล้ว
- ใช้แนวปฏิบัติที่ดีที่สุดด้านความปลอดภัยสำหรับการใช้งาน EdgeAI ที่รักษาความเป็นส่วนตัว

### ความสามารถเชิงกลยุทธ์

**กรอบการตัดสินใจ**
- ประเมินโอกาส EdgeAI และระบุกรณีการใช้งานที่เหมาะสมสำหรับการใช้งานทางธุรกิจ
- ประเมินการแลกเปลี่ยนระหว่างความแม่นยำของโมเดล, ความเร็วในการประมวลผล, การใช้พลังงาน และต้นทุนฮาร์ดแวร์
- เลือกครอบครัว SLM และการกำหนดค่าที่เหมาะสมตามข้อจำกัดการใช้งานเฉพาะ

**สถาปัตยกรรมระบบ**
- ออกแบบโซลูชัน EdgeAI แบบครบวงจรที่ผสานกับโครงสร้างพื้นฐานที่มีอยู่
- วางแผนสถาปัตยกรรม edge-cloud แบบไฮบริดเพื่อประสิทธิภาพและความคุ้มค่าที่ดีที่สุด
- ใช้งานท่อส่งข้อมูลและการประมวลผลสำหรับแอปพลิเคชัน AI แบบเรียลไทม์

### การใช้งานในอุตสาหกรรม

**สถานการณ์การใช้งานจริง**
- **การผลิต**: ระบบควบคุมคุณภาพ, การบำรุงรักษาเชิงคาดการณ์ และการปรับปรุงกระบวนการ
- **การดูแลสุขภาพ**: เครื่องมือวินิจฉัยที่รักษาความเป็นส่วนตัวและระบบติดตามผู้ป่วย
- **การขนส่ง**: การตัดสินใจของยานพาหนะอัตโนมัติและการจัดการจราจร
- **เมืองอัจฉริยะ**: โครงสร้างพื้นฐานอัจฉริยะและระบบการจัดการทรัพยากร
- **อิเล็กทรอนิกส์สำหรับผู้บริโภค**: แอปพลิเคชันมือถือที่ขับเคลื่อนด้วย AI และอุปกรณ์สมาร์ทโฮม

## ภาพรวมผลลัพธ์การเรียนรู้

### ผลลัพธ์การเรียนรู้ Module 01:
- เข้าใจความแตกต่างพื้นฐานระหว่างสถาปัตยกรรม AI บนคลาวด์และ edge
- เชี่ยวชาญเทคนิคการปรับแต่งหลักสำหรับการใช้งาน edge
- รับรู้การใช้งานจริงและเรื่องราวความสำเร็จ
- ได้รับทักษะการใช้งานจริงสำหรับการใช้งาน EdgeAI

### ผลลัพธ์การเรียนรู้ Module 02:
- เข้าใจลึกซึ้งเกี่ยวกับปรัชญาการออกแบบ SLM และผลกระทบต่อการใช้งาน
- เชี่ยวชาญความสามารถในการตัดสินใจเชิงกลยุทธ์ตามข้อจำกัดด้านการคำนวณและข้อกำหนดด้านประสิทธิภาพ
- เข้าใจการแลกเปลี่ยนความยืดหยุ่นในการใช้งาน
- มีข้อมูลเชิงลึกที่พร้อมสำหรับอนาคตเกี่ยวกับสถาปัตยกรรม AI ที่มีประสิทธิภาพ

### ผลลัพธ์การเรียนรู้ Module 03:
- ความสามารถในการเลือกโมเดลเชิงกลยุทธ์
- เชี่ยวชาญเทคนิคการปรับแต่ง
- เชี่ยวชาญความยืดหยุ่นในการใช้งาน
- ความสามารถในการกำหนดค่าที่พร้อมสำหรับการผลิต

### ผลลัพธ์การเรียนรู้ Module 04:
- เข้าใจล
- **การจัดการความเสี่ยง**: ระบุและลดความเสี่ยงทางเทคนิคและการดำเนินงานในระบบ EdgeAI
- **การเพิ่มประสิทธิภาพ ROI**: แสดงให้เห็นถึงคุณค่าทางธุรกิจที่วัดผลได้จากการใช้งาน EdgeAI

### โอกาสในการพัฒนาอาชีพ

**ตำแหน่งงานมืออาชีพ**
- EdgeAI Solutions Architect
- Machine Learning Engineer (Edge Specialization)
- IoT AI Developer
- Mobile AI Application Developer
- Enterprise AI Consultant

**ภาคอุตสาหกรรม**
- การผลิตอัจฉริยะและอุตสาหกรรม 4.0
- ยานยนต์อัตโนมัติและการขนส่ง
- เทคโนโลยีด้านสุขภาพและอุปกรณ์การแพทย์
- เทคโนโลยีการเงินและความปลอดภัย
- อิเล็กทรอนิกส์สำหรับผู้บริโภคและแอปพลิเคชันมือถือ

### การรับรองและการตรวจสอบ

**การพัฒนาผลงาน**
- ทำโครงการ EdgeAI แบบครบวงจรเพื่อแสดงความสามารถในทางปฏิบัติ
- ใช้งานโซลูชันที่พร้อมสำหรับการผลิตบนแพลตฟอร์มฮาร์ดแวร์หลากหลาย
- บันทึกกลยุทธ์การเพิ่มประสิทธิภาพและการปรับปรุงประสิทธิภาพที่ทำได้

**เส้นทางการเรียนรู้ต่อเนื่อง**
- พื้นฐานสำหรับการเชี่ยวชาญ AI ขั้นสูง
- การเตรียมตัวสำหรับสถาปัตยกรรมไฮบริดระหว่างคลาวด์และเอดจ์
- ประตูสู่เทคโนโลยีและเฟรมเวิร์ก AI ที่เกิดขึ้นใหม่

หลักสูตรนี้จะช่วยให้คุณอยู่ในแนวหน้าของการใช้งานเทคโนโลยี AI ที่สามารถผสานความสามารถอัจฉริยะเข้ากับอุปกรณ์และระบบที่ขับเคลื่อนชีวิตยุคใหม่ได้อย่างไร้รอยต่อ

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
├── Module08/ (Hands on with Foundry Local)
│   ├── 01.FoundryLocalSetup.md
│   ├── 02.AzureAIFoundryIntegration.md
│   ├── 03.OpenSourceModels.md
│   ├── 04.CuttingEdgeModels.md
│   ├── 05.AIPoweredAgents.md
│   ├── 06.ModelsAsTools.md
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
- **การผสมผสานทฤษฎีและปฏิบัติ**: แต่ละโมดูลประกอบด้วยทั้งพื้นฐานทางทฤษฎีและการปฏิบัติจริง
- **กรณีศึกษาในชีวิตจริง**: อ้างอิงจากกรณีจริงของ Microsoft, Alibaba, Google และอื่น ๆ
- **การฝึกปฏิบัติจริง**: การตั้งค่าไฟล์, การทดสอบ API และสคริปต์การใช้งาน
- **เกณฑ์มาตรฐานประสิทธิภาพ**: การเปรียบเทียบความเร็วในการประมวลผล, การใช้หน่วยความจำ และความต้องการทรัพยากรอย่างละเอียด
- **ข้อพิจารณาระดับองค์กร**: แนวทางปฏิบัติด้านความปลอดภัย, กรอบการปฏิบัติตามกฎระเบียบ และกลยุทธ์การปกป้องข้อมูล

## เริ่มต้นการเรียนรู้

เส้นทางการเรียนรู้ที่แนะนำ:
1. เริ่มต้นด้วย **Module01** เพื่อสร้างความเข้าใจพื้นฐานเกี่ยวกับ EdgeAI
2. ดำเนินการต่อที่ **Module02** เพื่อเข้าใจเชิงลึกเกี่ยวกับกลุ่มโมเดล SLM ต่าง ๆ
3. เรียนรู้ **Module03** เพื่อเชี่ยวชาญทักษะการใช้งานในทางปฏิบัติ
4. ต่อด้วย **Module04** สำหรับการเพิ่มประสิทธิภาพโมเดลขั้นสูง, การแปลงรูปแบบ และการผสานเฟรมเวิร์ก
5. ทำ **Module05** เพื่อเชี่ยวชาญ SLMOps สำหรับการใช้งานที่พร้อมสำหรับการผลิต
6. สำรวจ **Module06** เพื่อเข้าใจระบบ SLM agentic และความสามารถในการเรียกฟังก์ชัน
7. จบด้วย **Module07** เพื่อรับประสบการณ์จริงกับ AI Toolkit และตัวอย่างการใช้งาน EdgeAI ที่หลากหลาย
8. สำรวจ **Module08** สำหรับชุดเครื่องมือ Foundry Local สำหรับนักพัฒนา (การพัฒนาที่เน้นในพื้นที่พร้อมการผสาน Azure แบบไฮบริด)

แต่ละโมดูลถูกออกแบบให้สมบูรณ์ในตัวเอง แต่การเรียนรู้ตามลำดับจะให้ผลลัพธ์ที่ดีที่สุด

## คู่มือการศึกษา

[คู่มือการศึกษา](STUDY_GUIDE.md) ที่ครอบคลุมมีให้เพื่อช่วยให้คุณได้รับประโยชน์สูงสุดจากการเรียนรู้ คู่มือการศึกษาประกอบด้วย:

- **เส้นทางการเรียนรู้ที่มีโครงสร้าง**: ตารางเวลาที่ปรับให้เหมาะสมสำหรับการเรียนจบหลักสูตรใน 20 ชั่วโมง
- **คำแนะนำการจัดสรรเวลา**: คำแนะนำเฉพาะสำหรับการจัดสมดุลระหว่างการอ่าน, การฝึกฝน และโครงการ
- **การเน้นแนวคิดสำคัญ**: วัตถุประสงค์การเรียนรู้ที่จัดลำดับความสำคัญสำหรับแต่ละโมดูล
- **เครื่องมือประเมินตนเอง**: คำถามและแบบฝึกหัดเพื่อทดสอบความเข้าใจของคุณ
- **ไอเดียโครงการขนาดเล็ก**: การประยุกต์ใช้ในทางปฏิบัติเพื่อเสริมสร้างการเรียนรู้ของคุณ

คู่มือการศึกษาถูกออกแบบมาเพื่อรองรับทั้งการเรียนรู้แบบเข้มข้น (1 สัปดาห์) และการเรียนแบบพาร์ทไทม์ (3 สัปดาห์) พร้อมคำแนะนำที่ชัดเจนเกี่ยวกับวิธีการจัดสรรเวลาอย่างมีประสิทธิภาพ แม้ว่าคุณจะมีเวลาเรียนเพียง 10 ชั่วโมงก็ตาม

---

**อนาคตของ EdgeAI อยู่ที่การพัฒนาอย่างต่อเนื่องของสถาปัตยกรรมโมเดล, เทคนิคการลดขนาด และกลยุทธ์การใช้งานที่ให้ความสำคัญกับประสิทธิภาพและความเชี่ยวชาญเฉพาะด้านมากกว่าความสามารถทั่วไป องค์กรที่ยอมรับการเปลี่ยนแปลงนี้จะอยู่ในตำแหน่งที่ดีในการใช้ศักยภาพการเปลี่ยนแปลงของ AI ในขณะที่ยังคงควบคุมข้อมูลและการดำเนินงานของตนได้อย่างมีประสิทธิภาพ**

## หลักสูตรอื่น ๆ

ทีมของเราผลิตหลักสูตรอื่น ๆ! ลองดู:

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

