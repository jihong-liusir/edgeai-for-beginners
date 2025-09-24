<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "13cb0371a2aea01d721186ced4a25e1a",
  "translation_date": "2025-09-24T22:51:22+00:00",
  "source_file": "Module08/samples/08/README.md",
  "language_code": "th"
}
-->
# ตัวอย่างแชท Windows 11 - Foundry Local

แอปพลิเคชันแชทสมัยใหม่สำหรับ Windows 11 ที่ผสานรวม Microsoft Foundry Local เข้ากับอินเทอร์เฟซที่สวยงามและเป็นธรรมชาติ สร้างขึ้นด้วย Electron และปฏิบัติตามรูปแบบ Foundry Local อย่างเป็นทางการของ Microsoft

## ภาพรวม

ตัวอย่างนี้แสดงให้เห็นถึงวิธีการสร้างแอปพลิเคชันแชทที่พร้อมใช้งานจริง โดยใช้โมเดล AI ในเครื่องผ่าน Foundry Local เพื่อมอบประสบการณ์การสนทนา AI ที่เน้นความเป็นส่วนตัวโดยไม่ต้องพึ่งพาคลาวด์

## คุณสมบัติ

### 🎨 **การออกแบบเนทีฟของ Windows 11**
- การผสานรวม Fluent Design System
- เอฟเฟกต์วัสดุ Mica และความโปร่งใส
- รองรับธีมเนทีฟของ Windows 11
- เลย์เอาต์ที่ตอบสนองต่อทุกขนาดหน้าจอ
- การสลับโหมดมืด/สว่างอัตโนมัติ

### 🤖 **การผสานรวมโมเดล AI**
- การผสานบริการ Foundry Local
- รองรับโมเดลหลายตัวพร้อมการสลับแบบเรียลไทม์
- การตอบสนองแบบสตรีมมิ่งเรียลไทม์
- การสลับระหว่างโมเดลในเครื่องและคลาวด์
- การตรวจสอบและสถานะของโมเดล

### 💬 **ประสบการณ์แชท**
- ตัวบ่งชี้การพิมพ์แบบเรียลไทม์
- การบันทึกประวัติข้อความ
- การส่งออกบทสนทนา
- การตั้งค่าระบบข้อความที่กำหนดเอง
- การจัดการและแยกสาขาบทสนทนา

### ⚡ **คุณสมบัติด้านประสิทธิภาพ**
- การโหลดแบบ Lazy และการจำลองเสมือน
- การเรนเดอร์ที่เหมาะสมสำหรับบทสนทนายาวๆ
- การโหลดโมเดลล่วงหน้าในพื้นหลัง
- การจัดการหน่วยความจำอย่างมีประสิทธิภาพ
- แอนิเมชันและการเปลี่ยนภาพที่ราบรื่น

## สถาปัตยกรรม

```
┌─────────────────────────────────────────────────────────────┐
│                    Windows 11 Chat App                     │
├─────────────────┬─────────────────┬─────────────────────────┤
│   Electron UI   │   IPC Bridge    │    Foundry Manager      │
│                 │                 │                         │
│ • Fluent Design │ • Secure Comms  │ • Model Loading         │
│ • Chat Interface│ • Event Routing │ • Health Monitoring     │
│ • Settings      │ • State Sync    │ • Performance Tracking │
│ • Themes        │ • Error Handler │ • Resource Management   │
└─────────────────┴─────────────────┴─────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│               Microsoft Foundry Local Service               │
│                                                             │
│ • Local Model Hosting    • OpenAI API Compatibility        │
│ • Real-time Inference    • Model Catalog Management        │
│ • Streaming Responses    • Health & Status Monitoring      │
└─────────────────────────────────────────────────────────────┘
```

## ข้อกำหนดเบื้องต้น

### ความต้องการของระบบ
- **OS**: Windows 11 (แนะนำ 22H2 หรือใหม่กว่า)
- **RAM**: ขั้นต่ำ 8GB, แนะนำ 16GB+ สำหรับโมเดลขนาดใหญ่
- **Storage**: พื้นที่ว่าง 10GB+ สำหรับโมเดล
- **GPU**: ไม่จำเป็น แต่แนะนำสำหรับการประมวลผลที่เร็วขึ้น

### ซอฟต์แวร์ที่ต้องการ
- **Node.js**: v18.0.0 หรือใหม่กว่า
- **Foundry Local**: เวอร์ชันล่าสุดจาก Microsoft
- **Git**: สำหรับการโคลนและพัฒนา

## การติดตั้ง

### 1. ติดตั้ง Foundry Local
```powershell
# Download from GitHub releases and install
winget install Microsoft.FoundryLocal

# Verify installation
foundry --version
```

### 2. โคลนและตั้งค่า
```bash
# Navigate to sample directory
cd Module08/samples/08

# Install dependencies
npm install

# Install Electron if not global
npm install -g electron
```

### 3. กำหนดค่าระบบ
```powershell
# Optional: Set cloud model credentials for hybrid mode
$env:AZURE_OPENAI_KEY="your-api-key"
$env:AZURE_OPENAI_ENDPOINT="your-endpoint"
$env:AZURE_OPENAI_MODEL="gpt-4"
```

### 4. รันแอปพลิเคชัน
```bash
# Development mode
npm start

# Production build
npm run build
npm run dist
```

## โครงสร้างโปรเจกต์

```
08/
├── README.md                 # This documentation
├── package.json             # Project dependencies and scripts
├── electron.js              # Main Electron process
├── preload.js              # Secure preload script
├── src/
│   ├── index.html          # Main application UI
│   ├── styles/
│   │   ├── fluent.css      # Windows 11 Fluent Design
│   │   ├── chat.css        # Chat interface styles
│   │   └── themes.css      # Light/Dark theme support
│   ├── scripts/
│   │   ├── app.js          # Main application logic
│   │   ├── chat.js         # Chat functionality
│   │   ├── models.js       # Model management
│   │   ├── settings.js     # Settings and preferences
│   │   └── utils.js        # Utility functions
│   └── assets/
│       ├── icons/          # Application icons
│       ├── sounds/         # Notification sounds
│       └── images/         # UI images and illustrations
├── foundry/
│   ├── manager.js          # Foundry Local integration
│   └── health.js           # Health monitoring
└── build/
    ├── icon.ico            # Windows application icon
    └── installer.nsi       # NSIS installer script
```

## การเจาะลึกคุณสมบัติสำคัญ

### การผสานรวม Windows 11

**Fluent Design System**
- วัสดุพื้นหลัง Mica
- เอฟเฟกต์โปร่งใสแบบ Acrylic
- มุมโค้งมนและการจัดวางที่ทันสมัย
- พาเลตสีเนทีฟของ Windows 11
- โทนสีเชิงความหมายเพื่อการเข้าถึง

**คุณสมบัติเนทีฟของ Windows**
- การผสาน Jump List สำหรับแชทล่าสุด
- การแจ้งเตือน Windows สำหรับข้อความใหม่
- ความคืบหน้าใน Taskbar สำหรับการทำงานของโมเดล
- การผสาน System Tray พร้อมการดำเนินการด่วน
- รองรับการยืนยันตัวตนด้วย Windows Hello

### การจัดการโมเดล AI

**โมเดลในเครื่อง**
```javascript
// Automatic model discovery and loading
const models = await foundryManager.discoverModels();
await foundryManager.loadModel('phi-4-mini');

// Model health monitoring
const health = await foundryManager.checkHealth();
console.log(`Model Status: ${health.status}`);
console.log(`Memory Usage: ${health.memoryUsage}MB`);
```

**การรองรับแบบไฮบริด (คลาวด์/ในเครื่อง)**
```javascript
// Seamless switching between local and cloud models
if (useCloudModel) {
    await chatManager.switchToCloud('gpt-4');
} else {
    await chatManager.switchToLocal('phi-4-mini');
}
```

### คุณสมบัติอินเทอร์เฟซแชท

**การสตรีมแบบเรียลไทม์**
- การแสดงผลตอบสนองทีละโทเค็น
- แอนิเมชันการพิมพ์ที่ราบรื่น
- การยกเลิกคำขอ
- ตัวบ่งชี้การพิมพ์และสถานะ

**การจัดการบทสนทนา**
- ประวัติแชทที่คงอยู่
- การส่งออก/นำเข้าบทสนทนา
- การค้นหาและกรองข้อความ
- การแยกสาขาบทสนทนา
- การตั้งค่าระบบข้อความที่กำหนดเองต่อบทสนทนา

**การเข้าถึง**
- การนำทางด้วยคีย์บอร์ดเต็มรูปแบบ
- ความเข้ากันได้กับโปรแกรมอ่านหน้าจอ
- รองรับโหมดคอนทราสต์สูง
- การปรับขนาดฟอนต์ที่กำหนดเอง
- การผสานการป้อนข้อมูลด้วยเสียง

## ตัวอย่างการใช้งาน

### การผสานแชทพื้นฐาน
```javascript
// Initialize the chat system
const chat = new ChatManager({
    foundryEndpoint: 'http://localhost:5273',
    defaultModel: 'phi-4-mini',
    streaming: true
});

// Send a message
const response = await chat.sendMessage({
    content: 'Explain quantum computing',
    model: 'phi-4-mini',
    systemPrompt: 'You are a helpful physics teacher.'
});

// Handle streaming responses
chat.on('chunk', (chunk) => {
    appendMessageChunk(chunk.content);
});
```

### การจัดการโมเดล
```javascript
// Load a new model
await modelManager.loadModel('qwen2.5-coder-0.5b', {
    showProgress: true,
    autoStart: true
});

// Monitor model performance
modelManager.on('performance', (metrics) => {
    updatePerformanceUI(metrics);
});

// Switch models mid-conversation
await chat.switchModel('phi-4-mini', {
    preserveContext: true
});
```

### การตั้งค่าและการปรับแต่ง
```javascript
// Configure chat behavior
const settings = {
    theme: 'system', // auto, light, dark
    model: 'phi-4-mini',
    streaming: true,
    maxTokens: 1000,
    temperature: 0.7,
    systemPrompt: 'You are a helpful assistant.'
};

await settingsManager.updateSettings(settings);
```

## ตัวเลือกการกำหนดค่า

### การตั้งค่าแอปพลิเคชัน
- **ธีม**: โหมดอัตโนมัติ, โหมดสว่าง, โหมดมืด
- **โมเดล**: การเลือกโมเดลเริ่มต้น
- **ประสิทธิภาพ**: การตั้งค่าการประมวลผล
- **ความเป็นส่วนตัว**: นโยบายการเก็บข้อมูล
- **การแจ้งเตือน**: การแจ้งเตือนข้อความ
- **ทางลัด**: คีย์ลัด

### การตั้งค่าแชท
- **การสตรีม**: เปิด/ปิดการตอบสนองแบบเรียลไทม์
- **ความยาวบริบท**: หน่วยความจำบทสนทนา
- **อุณหภูมิ**: ความคิดสร้างสรรค์ของการตอบสนอง
- **โทเค็นสูงสุด**: ขีดจำกัดความยาวของการตอบสนอง
- **ระบบข้อความ**: พฤติกรรมผู้ช่วยเริ่มต้น

### การตั้งค่าโมเดล
- **การดาวน์โหลดอัตโนมัติ**: การอัปเดตโมเดลอัตโนมัติ
- **ขนาดแคช**: ขีดจำกัดการจัดเก็บโมเดลในเครื่อง
- **โหมดประสิทธิภาพ**: การตั้งค่า CPU หรือ GPU
- **การตรวจสอบสุขภาพ**: ช่วงเวลาการตรวจสอบ

## การพัฒนา

### การสร้างจากซอร์ส
```bash
# Install development dependencies
npm install

# Run in development mode
npm run dev

# Build for production
npm run build

# Create installer
npm run dist
```

### การดีบัก
```bash
# Enable debug mode
set DEBUG=foundry-chat:*
npm start

# View developer tools
# Press F12 in the application
```

### การทดสอบ
```bash
# Run unit tests
npm test

# Run integration tests
npm run test:integration

# Run end-to-end tests
npm run test:e2e
```

## การเพิ่มประสิทธิภาพ

### การจัดการหน่วยความจำ
- การจำลองข้อความอย่างมีประสิทธิภาพ
- การเก็บขยะอัตโนมัติ
- การตรวจสอบหน่วยความจำของโมเดล
- การล้างทรัพยากรเมื่อออกจากโปรแกรม

### การเพิ่มประสิทธิภาพการเรนเดอร์
- การเลื่อนแบบเสมือนสำหรับบทสนทนายาวๆ
- การโหลดประวัติข้อความแบบ Lazy
- การอัปเดต React/DOM ที่เหมาะสม
- แอนิเมชันที่เร่งด้วย GPU

### การเพิ่มประสิทธิภาพเครือข่าย
- การรวมการเชื่อมต่อ
- การจัดกลุ่มคำขอ
- การลองใหม่อัตโนมัติ
- รองรับโหมดออฟไลน์

## การพิจารณาด้านความปลอดภัย

### ความเป็นส่วนตัวของข้อมูล
- สถาปัตยกรรมที่เน้นในเครื่อง
- ไม่มีการส่งข้อมูลไปยังคลาวด์ (โหมดในเครื่อง)
- การจัดเก็บบทสนทนาแบบเข้ารหัส
- การจัดการข้อมูลรับรองที่ปลอดภัย

### ความปลอดภัยของแอปพลิเคชัน
- กระบวนการเรนเดอร์ที่ถูกจำกัด
- นโยบายความปลอดภัยของเนื้อหา (CSP)
- ไม่มีการรันโค้ดระยะไกล
- การสื่อสาร IPC ที่ปลอดภัย

## การแก้ไขปัญหา

### ปัญหาทั่วไป

**Foundry Local ไม่เริ่มทำงาน**
```powershell
# Check service status
foundry status

# Restart service
foundry restart

# Check logs
foundry logs
```

**การโหลดโมเดลล้มเหลว**
- ตรวจสอบพื้นที่ดิสก์ที่เพียงพอ
- ตรวจสอบการเชื่อมต่ออินเทอร์เน็ตสำหรับการดาวน์โหลด
- อัปเดตไดรเวอร์ GPU
- ลองใช้ตัวแปรโมเดลอื่น

**ปัญหาด้านประสิทธิภาพ**
- ตรวจสอบทรัพยากรระบบ
- ปรับการตั้งค่าโมเดล
- เปิดใช้งานการเร่งฮาร์ดแวร์
- ปิดแอปพลิเคชันที่ใช้ทรัพยากรมาก

### โหมดดีบัก
เปิดใช้งานการบันทึกดีบักโดยตั้งค่าตัวแปรสภาพแวดล้อม:
```powershell
$env:DEBUG="foundry:*"
$env:FOUNDRY_LOG_LEVEL="debug"
```

## การมีส่วนร่วม

### การตั้งค่าการพัฒนา
1. Fork รีโพซิทอรี
2. สร้างฟีเจอร์สาขา
3. ติดตั้งการพึ่งพา: `npm install`
4. ทำการเปลี่ยนแปลงและทดสอบ
5. ส่งคำขอ Pull Request

### รูปแบบโค้ด
- มีการกำหนดค่า ESLint
- ใช้ Prettier สำหรับการจัดรูปแบบโค้ด
- ใช้ TypeScript เพื่อความปลอดภัยของประเภท
- ใช้ JSDoc สำหรับการเขียนเอกสาร

## ผลลัพธ์การเรียนรู้

หลังจากทำตัวอย่างนี้เสร็จ คุณจะเข้าใจ:

1. **การพัฒนาบน Windows 11**
   - การใช้งาน Fluent Design System
   - การผสานรวม Windows เนทีฟ
   - แนวทางปฏิบัติที่ดีที่สุดด้านความปลอดภัยของ Electron

2. **การผสานรวมโมเดล AI**
   - สถาปัตยกรรมบริการ Foundry Local
   - การจัดการวงจรชีวิตของโมเดล
   - การตรวจสอบและเพิ่มประสิทธิภาพ

3. **ระบบแชทแบบเรียลไทม์**
   - การจัดการการตอบสนองแบบสตรีมมิ่ง
   - การจัดการสถานะบทสนทนา
   - รูปแบบประสบการณ์ผู้ใช้

4. **การพัฒนาแอปพลิเคชันสำหรับการใช้งานจริง**
   - การจัดการข้อผิดพลาดและการกู้คืน
   - การเพิ่มประสิทธิภาพ
   - การพิจารณาด้านความปลอดภัย
   - กลยุทธ์การทดสอบ

## ขั้นตอนถัดไป

- **ตัวอย่าง 09**: ระบบการจัดการหลายตัวแทน
- **ตัวอย่าง 10**: การผสาน Foundry Local เป็นเครื่องมือ
- **หัวข้อขั้นสูง**: การปรับแต่งโมเดลเฉพาะ
- **การปรับใช้**: รูปแบบการปรับใช้ในองค์กร

## ใบอนุญาต

ตัวอย่างนี้ปฏิบัติตามใบอนุญาตเดียวกันกับโครงการ Microsoft Foundry Local

---

