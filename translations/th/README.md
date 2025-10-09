<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "8bcf70fe61c9007c880f9753cc9c3e01",
  "translation_date": "2025-10-09T12:39:39+00:00",
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
3. [**เข้าร่วม Azure AI Foundry Discord และพบกับผู้เชี่ยวชาญและนักพัฒนาคนอื่นๆ**](https://discord.com/invite/ByRwuEEgH4)  

### 🌐 รองรับหลายภาษา

#### รองรับผ่าน GitHub Action (อัตโนมัติและอัปเดตเสมอ)

[Arabic](../ar/README.md) | [Bengali](../bn/README.md) | [Bulgarian](../bg/README.md) | [Burmese (Myanmar)](../my/README.md) | [Chinese (Simplified)](../zh/README.md) | [Chinese (Traditional, Hong Kong)](../hk/README.md) | [Chinese (Traditional, Macau)](../mo/README.md) | [Chinese (Traditional, Taiwan)](../tw/README.md) | [Croatian](../hr/README.md) | [Czech](../cs/README.md) | [Danish](../da/README.md) | [Dutch](../nl/README.md) | [Finnish](../fi/README.md) | [French](../fr/README.md) | [German](../de/README.md) | [Greek](../el/README.md) | [Hebrew](../he/README.md) | [Hindi](../hi/README.md) | [Hungarian](../hu/README.md) | [Indonesian](../id/README.md) | [Italian](../it/README.md) | [Japanese](../ja/README.md) | [Korean](../ko/README.md) | [Malay](../ms/README.md) | [Marathi](../mr/README.md) | [Nepali](../ne/README.md) | [Norwegian](../no/README.md) | [Persian (Farsi)](../fa/README.md) | [Polish](../pl/README.md) | [Portuguese (Brazil)](../br/README.md) | [Portuguese (Portugal)](../pt/README.md) | [Punjabi (Gurmukhi)](../pa/README.md) | [Romanian](../ro/README.md) | [Russian](../ru/README.md) | [Serbian (Cyrillic)](../sr/README.md) | [Slovak](../sk/README.md) | [Slovenian](../sl/README.md) | [Spanish](../es/README.md) | [Swahili](../sw/README.md) | [Swedish](../sv/README.md) | [Tagalog (Filipino)](../tl/README.md) | [Thai](./README.md) | [Turkish](../tr/README.md) | [Ukrainian](../uk/README.md) | [Urdu](../ur/README.md) | [Vietnamese](../vi/README.md)

**หากคุณต้องการให้มีการสนับสนุนภาษาเพิ่มเติม สามารถดูรายการภาษาที่รองรับได้ [ที่นี่](https://github.com/Azure/co-op-translator/blob/main/getting_started/supported-languages.md)**

## บทนำ

ยินดีต้อนรับสู่ **EdgeAI สำหรับผู้เริ่มต้น** – การเดินทางที่ครอบคลุมสู่โลกแห่งปัญญาประดิษฐ์ที่เปลี่ยนแปลงโลกของ Edge AI คอร์สนี้จะช่วยเชื่อมโยงความสามารถอันทรงพลังของ AI เข้ากับการใช้งานจริงในโลกแห่งความเป็นจริงบนอุปกรณ์ Edge เพื่อให้คุณสามารถใช้ศักยภาพของ AI ได้โดยตรงในที่ที่ข้อมูลถูกสร้างขึ้นและการตัดสินใจต้องเกิดขึ้น

### สิ่งที่คุณจะได้เรียนรู้

คอร์สนี้จะพาคุณจากพื้นฐานไปจนถึงการใช้งานจริงในระดับการผลิต ครอบคลุม:
- **Small Language Models (SLMs)** ที่ปรับแต่งสำหรับการใช้งานบนอุปกรณ์ Edge  
- **การปรับแต่งให้เหมาะสมกับฮาร์ดแวร์** บนแพลตฟอร์มที่หลากหลาย  
- **การวิเคราะห์แบบเรียลไทม์** พร้อมความสามารถในการรักษาความเป็นส่วนตัว  
- **กลยุทธ์การใช้งานในระดับการผลิต** สำหรับแอปพลิเคชันในองค์กร  

### ทำไม EdgeAI ถึงสำคัญ

Edge AI เป็นการเปลี่ยนแปลงที่สำคัญซึ่งช่วยแก้ปัญหาท้าทายของยุคสมัยใหม่:
- **ความเป็นส่วนตัวและความปลอดภัย**: ประมวลผลข้อมูลที่สำคัญในพื้นที่โดยไม่ต้องส่งไปยังคลาวด์  
- **ประสิทธิภาพแบบเรียลไทม์**: ลดความล่าช้าของเครือข่ายสำหรับแอปพลิเคชันที่ต้องการความรวดเร็ว  
- **ประหยัดค่าใช้จ่าย**: ลดค่าใช้จ่ายในการใช้แบนด์วิดท์และการประมวลผลบนคลาวด์  
- **การทำงานที่ยืดหยุ่น**: สามารถทำงานได้แม้ในขณะที่เครือข่ายล่ม  
- **การปฏิบัติตามกฎระเบียบ**: ปฏิบัติตามข้อกำหนดด้านอธิปไตยของข้อมูล  

### Edge AI

Edge AI หมายถึงการรันอัลกอริทึม AI และโมเดลภาษาบนฮาร์ดแวร์ในพื้นที่ใกล้กับที่ข้อมูลถูกสร้างขึ้น โดยไม่ต้องพึ่งพาทรัพยากรคลาวด์สำหรับการวิเคราะห์ ซึ่งช่วยลดความล่าช้า เพิ่มความเป็นส่วนตัว และช่วยให้สามารถตัดสินใจได้แบบเรียลไทม์

### หลักการสำคัญ:
- **การวิเคราะห์บนอุปกรณ์**: โมเดล AI รันบนอุปกรณ์ Edge (โทรศัพท์, เราเตอร์, ไมโครคอนโทรลเลอร์, คอมพิวเตอร์อุตสาหกรรม)  
- **ความสามารถในการทำงานแบบออฟไลน์**: ทำงานได้โดยไม่ต้องเชื่อมต่ออินเทอร์เน็ตตลอดเวลา  
- **ความล่าช้าต่ำ**: ตอบสนองทันทีเหมาะสำหรับระบบเรียลไทม์  
- **อธิปไตยของข้อมูล**: เก็บข้อมูลที่สำคัญในพื้นที่ เพิ่มความปลอดภัยและการปฏิบัติตามกฎระเบียบ  

### Small Language Models (SLMs)

SLMs เช่น Phi-4, Mistral-7B และ Gemma เป็นเวอร์ชันที่ปรับแต่งของ LLMs ขนาดใหญ่ ซึ่งได้รับการฝึกฝนหรือปรับแต่งเพื่อ:
- **ลดการใช้หน่วยความจำ**: ใช้หน่วยความจำของอุปกรณ์ Edge อย่างมีประสิทธิภาพ  
- **ลดความต้องการในการประมวลผล**: ปรับให้เหมาะสมกับการทำงานของ CPU และ GPU บนอุปกรณ์ Edge  
- **เริ่มต้นได้เร็วขึ้น**: การเริ่มต้นที่รวดเร็วสำหรับแอปพลิเคชันที่ต้องการการตอบสนอง  

พวกมันช่วยปลดล็อกความสามารถ NLP ที่ทรงพลังในขณะที่ตอบสนองข้อจำกัดของ:
- **ระบบฝังตัว**: อุปกรณ์ IoT และตัวควบคุมอุตสาหกรรม  
- **อุปกรณ์พกพา**: สมาร์ทโฟนและแท็บเล็ตที่มีความสามารถออฟไลน์  
- **อุปกรณ์ IoT**: เซ็นเซอร์และอุปกรณ์อัจฉริยะที่มีทรัพยากรจำกัด  
- **เซิร์ฟเวอร์ Edge**: หน่วยประมวลผลในพื้นที่ที่มีทรัพยากร GPU จำกัด  
- **คอมพิวเตอร์ส่วนบุคคล**: สถานการณ์การใช้งานบนเดสก์ท็อปและแล็ปท็อป  

## โมดูลคอร์ส & การนำทาง

| โมดูล | หัวข้อ | พื้นที่โฟกัส | เนื้อหาสำคัญ | ระดับ | ระยะเวลา |
|-------|--------|---------------|---------------|-------|-----------|
| [📖 00 ](./introduction.md) | [แนะนำ EdgeAI](./introduction.md) | พื้นฐาน & บริบท | ภาพรวม EdgeAI • การใช้งานในอุตสาหกรรม • แนะนำ SLM • วัตถุประสงค์การเรียนรู้ | ผู้เริ่มต้น | 1-2 ชม. |
| [📚 01](../../Module01) | [พื้นฐาน EdgeAI](./Module01/README.md) | การเปรียบเทียบ Cloud กับ Edge AI | พื้นฐาน EdgeAI • กรณีศึกษาในโลกจริง • คู่มือการใช้งาน • การปรับใช้ Edge | ผู้เริ่มต้น | 3-4 ชม. |
| [🧠 02](../../Module02) | [พื้นฐานโมเดล SLM](./Module02/README.md) | ครอบครัวโมเดล & สถาปัตยกรรม | ครอบครัว Phi • ครอบครัว Qwen • ครอบครัว Gemma • BitNET • μModel • Phi-Silica | ผู้เริ่มต้น | 4-5 ชม. |
| [🚀 03](../../Module03) | [การปฏิบัติการปรับใช้ SLM](./Module03/README.md) | การปรับใช้ในพื้นที่ & คลาวด์ | การเรียนรู้ขั้นสูง • สภาพแวดล้อมในพื้นที่ • การปรับใช้ในคลาวด์ | ระดับกลาง | 4-5 ชม. |
| [⚙️ 04](../../Module04) | [เครื่องมือปรับแต่งโมเดล](./Module04/README.md) | การปรับแต่งข้ามแพลตฟอร์ม | บทนำ • Llama.cpp • Microsoft Olive • OpenVINO • Apple MLX • การสังเคราะห์เวิร์กโฟลว์ | ระดับกลาง | 5-6 ชม. |
| [🔧 05](../../Module05) | [SLMOps การผลิต](./Module05/README.md) | การดำเนินงานในระดับการผลิต | บทนำ SLMOps • การกลั่นโมเดล • การปรับแต่ง • การปรับใช้ในระดับการผลิต | ระดับสูง | 5-6 ชม. |
| [🤖 06](../../Module06) | [AI Agents & การเรียกฟังก์ชัน](./Module06/README.md) | เฟรมเวิร์กเอเจนต์ & MCP | บทนำเอเจนต์ • การเรียกฟังก์ชัน • โปรโตคอลบริบทโมเดล | ระดับสูง | 4-5 ชม. |
| [💻 07](../../Module07) | [การใช้งานแพลตฟอร์ม](./Module07/README.md) | ตัวอย่างข้ามแพลตฟอร์ม | เครื่องมือ AI • Foundry Local • การพัฒนาบน Windows | ระดับสูง | 3-4 ชม. |
| [🏭 08](../../Module08) | [เครื่องมือ Foundry Local](./Module08/README.md) | ตัวอย่างพร้อมใช้งานในระดับการผลิต | แอปพลิเคชันตัวอย่าง (ดูรายละเอียดด้านล่าง) | ผู้เชี่ยวชาญ | 8-10 ชม. |

### 🏭 **โมดูล 08: แอปพลิเคชันตัวอย่าง**

- [01: เริ่มต้นใช้งาน REST Chat](./Module08/samples/01/README.md)  
- [02: การผสานรวม OpenAI SDK](./Module08/samples/02/README.md)  
- [03: การค้นหาและเปรียบเทียบโมเดล](./Module08/samples/03/README.md)  
- [04: แอปพลิเคชัน Chainlit RAG](./Module08/samples/04/README.md)  
- [05: การจัดการหลายเอเจนต์](./Module08/samples/05/README.md)  
- [06: ตัวจัดการโมเดลเป็นเครื่องมือ](./Module08/samples/06/README.md)  
- [07: ไคลเอนต์ API โดยตรง](./Module08/samples/07/README.md)  
- [08: แอปแชท Windows 11](./Module08/samples/08/README.md)  
- [09: ระบบหลายเอเจนต์ขั้นสูง](./Module08/samples/09/README.md)  
- [10: เฟรมเวิร์กเครื่องมือ Foundry](./Module08/samples/10/README.md)  

### 🎓 **เวิร์กชอป: เส้นทางการเรียนรู้แบบลงมือปฏิบัติ**

วัสดุการเรียนรู้แบบลงมือปฏิบัติที่ครอบคลุมพร้อมการใช้งานที่พร้อมสำหรับการผลิต:

- **[คู่มือเวิร์กชอป](./Workshop/Readme.md)** - วัตถุประสงค์การเรียนรู้ที่สมบูรณ์ ผลลัพธ์ และการนำทางทรัพยากร  
- **ตัวอย่าง Python** (6 เซสชัน) - อัปเดตด้วยแนวปฏิบัติที่ดีที่สุด การจัดการข้อผิดพลาด และเอกสารประกอบที่ครอบคลุม  
- **Jupyter Notebooks** (8 แบบโต้ตอบ) - บทเรียนทีละขั้นตอนพร้อมการเปรียบเทียบและการตรวจสอบประสิทธิภาพ  
- **คู่มือเซสชัน** - คู่มือ Markdown ที่ละเอียดสำหรับแต่ละเซสชันของเวิร์กชอป  
- **เครื่องมือตรวจสอบ** - สคริปต์สำหรับตรวจสอบคุณภาพโค้ดและการทดสอบเบื้องต้น  

**สิ่งที่คุณจะได้สร้าง:**
- แอปพลิเคชันแชท AI ในพื้นที่พร้อมการสนับสนุนการสตรีม  
- ท่อส่ง RAG พร้อมการประเมินคุณภาพ (RAGAS)  
- เครื่องมือเปรียบเทียบและวัดประสิทธิภาพหลายโมเดล  
- ระบบการจัดการหลายเอเจนต์  
- การจัดการโมเดลอัจฉริยะด้วยการเลือกตามงาน  

### 📊 **สรุปเส้นทางการเรียนรู้**
- **ระยะเวลารวม**: 36-45 ชั่วโมง  
- **เส้นทางผู้เริ่มต้น**: โมดูล 01-02 (7-9 ชั่วโมง)  
- **เส้นทางระดับกลาง**: โมดูล 03-04 (9-11 ชั่วโมง)  
- **เส้นทางระดับสูง**: โมดูล 05-07 (12-15 ชั่วโมง)  
- **เส้นทางผู้เชี่ยวชาญ**: โมดูล 08 (8-10 ชั่วโมง)  

## สิ่งที่คุณจะได้สร้าง

### 🎯 ทักษะหลัก
- **สถาปัตยกรรม Edge AI**: ออกแบบระบบ AI ที่เน้นการทำงานในพื้นที่ร่วมกับการผสานคลาวด์  
- **การปรับแต่งโมเดล**: ลดขนาดและเพิ่มความเร็วของโมเดลสำหรับการใช้งานบน Edge (เพิ่มความเร็ว 85%, ลดขนาด 75%)  
- **การปรับใช้ข้ามแพลตฟอร์ม**: Windows, อุปกรณ์พกพา, ระบบฝังตัว และระบบไฮบริดคลาวด์-Edge  
- **การดำเนินงานในระดับการผลิต**: การตรวจสอบ, การขยายขนาด, และการบำรุงรักษา Edge AI ในการผลิต  

### 🏗️ โครงการปฏิบัติ
- **แอปแชท Foundry Local**: แอปพลิเคชัน Windows 11
- **เราเตอร์โมเดล**: การเลือกโมเดลอย่างชาญฉลาดตามการวิเคราะห์งาน  
- **เฟรมเวิร์ก API**: ลูกค้าพร้อมใช้งานสำหรับการสตรีมและการตรวจสอบสุขภาพ  
- **เครื่องมือข้ามแพลตฟอร์ม**: รูปแบบการผสานรวม LangChain/Semantic Kernel  

### 🏢 การใช้งานในอุตสาหกรรม  
**การผลิต** • **การดูแลสุขภาพ** • **ยานยนต์อัตโนมัติ** • **เมืองอัจฉริยะ** • **แอปพลิเคชันมือถือ**  

## เริ่มต้นอย่างรวดเร็ว  

**เส้นทางการเรียนรู้ที่แนะนำ** (รวม 20-30 ชั่วโมง):  

0. **📖 บทนำ** ([Introduction.md](./introduction.md)): พื้นฐาน EdgeAI + บริบทอุตสาหกรรม + กรอบการเรียนรู้  
1. **📚 พื้นฐาน** (โมดูล 01-02): แนวคิด EdgeAI + กลุ่มโมเดล SLM  
2. **⚙️ การปรับแต่ง** (โมดูล 03-04): การปรับใช้ + เฟรมเวิร์กการลดขนาด  
3. **🚀 การผลิต** (โมดูล 05-06): SLMOps + เอเจนต์ AI + การเรียกฟังก์ชัน  
4. **💻 การใช้งาน** (โมดูล 07-08): ตัวอย่างแพลตฟอร์ม + เครื่องมือ Foundry Local  

แต่ละโมดูลประกอบด้วยทฤษฎี การฝึกปฏิบัติ และตัวอย่างโค้ดที่พร้อมใช้งานในงานจริง  

## ผลกระทบต่ออาชีพ  

**บทบาททางเทคนิค**: สถาปนิกโซลูชัน EdgeAI • วิศวกร ML (Edge) • นักพัฒนา IoT AI • นักพัฒนา AI บนมือถือ  

**ภาคอุตสาหกรรม**: การผลิต 4.0 • เทคโนโลยีการดูแลสุขภาพ • ระบบอัตโนมัติ • FinTech • อิเล็กทรอนิกส์สำหรับผู้บริโภค  

**โครงการพอร์ตโฟลิโอ**: ระบบหลายเอเจนต์ • แอป RAG สำหรับการผลิต • การปรับใช้ข้ามแพลตฟอร์ม • การปรับปรุงประสิทธิภาพ  

## โครงสร้างของ Repository  

```
edgeai-for-beginners/
├── 📖 introduction.md  # Foundation: EdgeAI Overview & Learning Framework
├── 📚 Module01-04/     # Fundamentals → SLMs → Deployment → Optimization  
├── 🔧 Module05-06/     # SLMOps → AI Agents → Function Calling
├── 💻 Module07/        # Platform Samples (VS Code, Windows, Jetson, Mobile)
├── 🏭 Module08/        # Foundry Local Toolkit + 10 Comprehensive Samples
│   ├── samples/01-06/  # Foundation: REST, SDK, RAG, Agents, Routing
│   └── samples/07-10/  # Advanced: API Client, Windows App, Enterprise Agents, Tools
├── 🌐 translations/    # Multi-language support (8+ languages)
└── 📋 STUDY_GUIDE.md   # Structured learning paths & time allocation
```
  

## ไฮไลต์ของคอร์ส  

✅ **การเรียนรู้แบบก้าวหน้า**: ทฤษฎี → การปฏิบัติ → การปรับใช้ในงานจริง  
✅ **กรณีศึกษาในงานจริง**: Microsoft, Japan Airlines, การใช้งานในองค์กร  
✅ **ตัวอย่างการฝึกปฏิบัติ**: ตัวอย่างมากกว่า 50 รายการ, เดโม Foundry Local ครบถ้วน 10 รายการ  
✅ **เน้นประสิทธิภาพ**: ปรับปรุงความเร็ว 85%, ลดขนาด 75%  
✅ **หลายแพลตฟอร์ม**: Windows, มือถือ, อุปกรณ์ฝังตัว, ไฮบริดคลาวด์-เอดจ์  
✅ **พร้อมใช้งานในงานจริง**: เฟรมเวิร์กการตรวจสอบ, การขยาย, ความปลอดภัย, การปฏิบัติตามข้อกำหนด  

📖 **[คู่มือการศึกษา](STUDY_GUIDE.md)**: เส้นทางการเรียนรู้ 20 ชั่วโมงที่มีคำแนะนำการจัดสรรเวลาและเครื่องมือประเมินตนเอง  

---

**EdgeAI คืออนาคตของการปรับใช้ AI**: เน้นการใช้งานในพื้นที่, รักษาความเป็นส่วนตัว, และมีประสิทธิภาพ เรียนรู้ทักษะเหล่านี้เพื่อสร้างแอปพลิเคชันอัจฉริยะรุ่นต่อไป  

## คอร์สอื่น ๆ  

ทีมของเราผลิตคอร์สอื่น ๆ ด้วย! ลองดูที่:  

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

## ขอความช่วยเหลือ  

หากคุณติดขัดหรือมีคำถามเกี่ยวกับการสร้างแอป AI เข้าร่วมที่นี่:  

[![Azure AI Foundry Discord](https://img.shields.io/badge/Discord-Azure_AI_Foundry_Community_Discord-blue?style=for-the-badge&logo=discord&color=5865f2&logoColor=fff)](https://aka.ms/foundry/discord)  

หากคุณมีข้อเสนอแนะเกี่ยวกับผลิตภัณฑ์หรือพบข้อผิดพลาดขณะสร้าง โปรดเยี่ยมชม:  

[![Azure AI Foundry Developer Forum](https://img.shields.io/badge/GitHub-Azure_AI_Foundry_Developer_Forum-blue?style=for-the-badge&logo=github&color=000000&logoColor=fff)](https://aka.ms/foundry/forum)  

---

**ข้อจำกัดความรับผิดชอบ**:  
เอกสารนี้ได้รับการแปลโดยใช้บริการแปลภาษา AI [Co-op Translator](https://github.com/Azure/co-op-translator) แม้ว่าเราจะพยายามให้การแปลมีความถูกต้อง แต่โปรดทราบว่าการแปลอัตโนมัติอาจมีข้อผิดพลาดหรือความไม่ถูกต้อง เอกสารต้นฉบับในภาษาดั้งเดิมควรถือเป็นแหล่งข้อมูลที่เชื่อถือได้ สำหรับข้อมูลที่สำคัญ ขอแนะนำให้ใช้บริการแปลภาษามนุษย์ที่มีความเชี่ยวชาญ เราไม่รับผิดชอบต่อความเข้าใจผิดหรือการตีความผิดที่เกิดจากการใช้การแปลนี้