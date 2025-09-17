<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "c817161ba08864340737d623f761b9ae",
  "translation_date": "2025-09-17T19:21:19+00:00",
  "source_file": "README.md",
  "language_code": "ne"
}
-->
# EdgeAI का शुरुवातकर्ता लागि 

![कोर्स कभर छवि](../../translated_images/cover.eb18d1b9605d754b30973f4e17c6e11ea4f8473d9686ee378d6e7b44e3c70ac7.ne.png)

[![GitHub contributors](https://img.shields.io/github/contributors/microsoft/edgeai-for-beginners.svg)](https://GitHub.com/microsoft/edgeai-for-beginners/graphs/contributors)
[![GitHub issues](https://img.shields.io/github/issues/microsoft/edgeai-for-beginners.svg)](https://GitHub.com/microsoft/edgeai-for-beginners/issues)
[![GitHub pull-requests](https://img.shields.io/github/issues-pr/microsoft/edgeai-for-beginners.svg)](https://GitHub.com/microsoft/edgeai-for-beginners/pulls)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)

[![GitHub watchers](https://img.shields.io/github/watchers/microsoft/edgeai-for-beginners.svg?style=social&label=Watch)](https://GitHub.com/microsoft/edgeai-for-beginners/watchers)
[![GitHub forks](https://img.shields.io/github/forks/microsoft/edgeai-for-beginners.svg?style=social&label=Fork)](https://GitHub.com/microsoft/edgeai-for-beginners/fork)
[![GitHub stars](https://img.shields.io/github/stars/microsoft/edgeai-for-beginners?style=social&label=Star)](https://GitHub.com/microsoft/edgeai-for-beginners/stargazers)

[![Microsoft Azure AI Foundry Discord](https://dcbadge.limes.pink/api/server/ByRwuEEgH4)](https://discord.com/invite/ByRwuEEgH4)

यी स्रोतहरू प्रयोग गर्न सुरु गर्न निम्न चरणहरू अनुसरण गर्नुहोस्:

1. **रिपोजिटरीलाई Fork गर्नुहोस्**: क्लिक गर्नुहोस् [![GitHub forks](https://img.shields.io/github/forks/microsoft/edgeai-for-beginners.svg?style=social&label=Fork)](https://GitHub.com/microsoft/edgeai-for-beginners/fork)
2. **रिपोजिटरीलाई Clone गर्नुहोस्**:   `git clone https://github.com/microsoft/edgeai-for-beginners.git`
3. [**Azure AI Foundry Discord मा सामेल हुनुहोस् र विशेषज्ञहरू तथा अन्य विकासकर्ताहरूलाई भेट्नुहोस्**](https://discord.com/invite/ByRwuEEgH4)

### 🌐 बहुभाषिक समर्थन

#### GitHub Action मार्फत समर्थित (स्वचालित र सधैं अद्यावधिक)

[Arabic](../ar/README.md) | [Bengali](../bn/README.md) | [Bulgarian](../bg/README.md) | [Burmese (Myanmar)](../my/README.md) | [Chinese (Simplified)](../zh/README.md) | [Chinese (Traditional, Hong Kong)](../hk/README.md) | [Chinese (Traditional, Macau)](../mo/README.md) | [Chinese (Traditional, Taiwan)](../tw/README.md) | [Croatian](../hr/README.md) | [Czech](../cs/README.md) | [Danish](../da/README.md) | [Dutch](../nl/README.md) | [Finnish](../fi/README.md) | [French](../fr/README.md) | [German](../de/README.md) | [Greek](../el/README.md) | [Hebrew](../he/README.md) | [Hindi](../hi/README.md) | [Hungarian](../hu/README.md) | [Indonesian](../id/README.md) | [Italian](../it/README.md) | [Japanese](../ja/README.md) | [Korean](../ko/README.md) | [Malay](../ms/README.md) | [Marathi](../mr/README.md) | [Nepali](./README.md) | [Norwegian](../no/README.md) | [Persian (Farsi)](../fa/README.md) | [Polish](../pl/README.md) | [Portuguese (Brazil)](../br/README.md) | [Portuguese (Portugal)](../pt/README.md) | [Punjabi (Gurmukhi)](../pa/README.md) | [Romanian](../ro/README.md) | [Russian](../ru/README.md) | [Serbian (Cyrillic)](../sr/README.md) | [Slovak](../sk/README.md) | [Slovenian](../sl/README.md) | [Spanish](../es/README.md) | [Swahili](../sw/README.md) | [Swedish](../sv/README.md) | [Tagalog (Filipino)](../tl/README.md) | [Thai](../th/README.md) | [Turkish](../tr/README.md) | [Ukrainian](../uk/README.md) | [Urdu](../ur/README.md) | [Vietnamese](../vi/README.md)

**यदि तपाईं थप भाषाहरूको अनुवाद चाहनुहुन्छ भने, समर्थित भाषाहरू यहाँ सूचीबद्ध छन् [यहाँ](https://github.com/Azure/co-op-translator/blob/main/getting_started/supported-languages.md)**

## परिचय

**EdgeAI for Beginners** मा स्वागत छ – Edge Artificial Intelligence को परिवर्तनकारी संसारमा तपाईंको व्यापक यात्रा। यो कोर्सले शक्तिशाली AI क्षमताहरू र वास्तविक संसारमा प्रयोगको बीचको खाडललाई पूर्ति गर्दछ, जसले तपाईंलाई डेटा उत्पन्न हुने ठाउँमा र निर्णयहरू लिनुपर्ने ठाउँमा AI को क्षमता प्रयोग गर्न सक्षम बनाउँछ।

### तपाईंले के-कसरी दक्षता हासिल गर्नुहुनेछ

यो कोर्सले आधारभूत अवधारणाहरूदेखि उत्पादन-तयार कार्यान्वयनसम्मको यात्रा समेट्छ:
- **साना भाषा मोडेलहरू (SLMs)** जो Edge मा प्रयोगको लागि अनुकूलित छन्
- **हार्डवेयर-आधारित अनुकूलन** विभिन्न प्लेटफर्महरूमा
- **रियल-टाइम इनफरेन्स** गोपनीयता-संरक्षण क्षमताहरू सहित
- **उत्पादन परिनियोजन** रणनीतिहरू उद्यम अनुप्रयोगहरूको लागि

### किन EdgeAI महत्त्वपूर्ण छ

Edge AI ले आधुनिक चुनौतीहरूको समाधान गर्ने एक नयाँ दृष्टिकोण प्रस्तुत गर्दछ:
- **गोपनीयता र सुरक्षा**: संवेदनशील डेटा स्थानीय रूपमा प्रक्रिया गर्नुहोस्, क्लाउडमा नपठाई
- **रियल-टाइम प्रदर्शन**: समय-संवेदनशील अनुप्रयोगहरूको लागि नेटवर्क ढिलाइ हटाउनुहोस्
- **खर्च दक्षता**: ब्यान्डविथ र क्लाउड कम्प्युटिङ खर्च घटाउनुहोस्
- **लचिलो सञ्चालन**: नेटवर्क अवरोधको समयमा कार्यक्षमता कायम राख्नुहोस्
- **नियम अनुपालन**: डेटा सार्वभौमिकता आवश्यकताहरू पूरा गर्नुहोस्

### Edge AI

Edge AI भनेको AI एल्गोरिदम र भाषा मोडेलहरू स्थानीय हार्डवेयरमा चलाउनु हो—डेटा उत्पन्न हुने ठाउँमा—क्लाउड स्रोतहरूमा निर्भर नगरी। यसले ढिलाइ घटाउँछ, गोपनीयता सुधार गर्दछ, र वास्तविक समयमा निर्णय लिन सक्षम बनाउँछ।

### मुख्य सिद्धान्तहरू:
- **डिभाइसमा इनफरेन्स**: AI मोडेलहरू Edge उपकरणहरूमा चल्छन् (फोन, राउटर, माइक्रोकन्ट्रोलर, औद्योगिक PCs)
- **अफलाइन क्षमता**: स्थायी इन्टरनेट जडान बिना कार्य गर्दछ
- **कम ढिलाइ**: वास्तविक-समय प्रणालीहरूको लागि तत्काल प्रतिक्रिया
- **डेटा सार्वभौमिकता**: संवेदनशील डेटा स्थानीय राख्छ, सुरक्षा र अनुपालन सुधार गर्दछ

### साना भाषा मोडेलहरू (SLMs)

Phi-4, Mistral-7B, र Gemma जस्ता SLMs ठूला LLMs का अनुकूलित संस्करणहरू हुन्—प्रशिक्षित वा डिस्टिल गरिएको:
- **स्मृति खपत कम गर्नुहोस्**: सीमित Edge उपकरण स्मृतिको कुशल प्रयोग
- **कम कम्प्युट माग**: CPU र Edge GPU प्रदर्शनको लागि अनुकूलित
- **छिटो सुरु हुने समय**: प्रतिक्रियात्मक अनुप्रयोगहरूको लागि छिटो सुरुवात

यीले शक्तिशाली NLP क्षमताहरू अनलक गर्छन् जबकि निम्न सीमाहरू पूरा गर्छन्:
- **एम्बेडेड प्रणालीहरू**: IoT उपकरणहरू र औद्योगिक कन्ट्रोलरहरू
- **मोबाइल उपकरणहरू**: स्मार्टफोन र ट्याब्लेटहरू अफलाइन क्षमताहरू सहित
- **IoT उपकरणहरू**: सीमित स्रोतहरू भएका सेन्सर र स्मार्ट उपकरणहरू
- **Edge सर्भरहरू**: सीमित GPU स्रोतहरू भएका स्थानीय प्रशोधन इकाइहरू
- **व्यक्तिगत कम्प्युटरहरू**: डेस्कटप र ल्यापटप परिनियोजन परिदृश्यहरू

## कोर्स संरचना

### [मोड्युल 01: EdgeAI का आधारभूत र परिवर्तन](./Module01/README.md)
**थिम**: Edge AI परिनियोजनको परिवर्तनकारी परिवर्तन

#### अध्याय संरचना:
- [**सेक्शन 1: EdgeAI का आधारभूत**](./Module01/01.EdgeAIFundamentals.md)
  - परम्परागत क्लाउड AI बनाम Edge AI तुलना
  - Edge कम्प्युटिङ चुनौतीहरू र सीमाहरू
  - प्रमुख प्रविधिहरू: मोडेल क्वान्टाइजेशन, कम्प्रेसन अनुकूलन, साना भाषा मोडेलहरू (SLMs)
  - हार्डवेयर एक्सेलेरेशन: NPUs, GPU अनुकूलन, CPU अनुकूलन
  - फाइदाहरू: गोपनीयता सुरक्षा, कम ढिलाइ, अफलाइन क्षमता, खर्च दक्षता

- [**सेक्शन 2: वास्तविक संसारका केस अध्ययनहरू**](./Module01/02.RealWorldCaseStudies.md)
  - Microsoft Phi & Mu मोडेल इकोसिस्टम
  - Japan Airlines AI रिपोर्टिङ प्रणाली केस अध्ययन
  - बजार प्रभाव र भविष्यको दिशा
  - परिनियोजन विचारहरू र उत्कृष्ट अभ्यासहरू

- [**सेक्शन 3: व्यावहारिक कार्यान्वयन मार्गदर्शिका**](./Module01/03.PracticalImplementationGuide.md)
  - विकास वातावरण सेटअप (Python 3.10+, .NET 8+)
  - हार्डवेयर आवश्यकताहरू र सिफारिस गरिएको कन्फिगरेसनहरू
  - कोर मोडेल परिवार स्रोतहरू
  - क्वान्टाइजेशन र अनुकूलन उपकरणहरू (Llama.cpp, Microsoft Olive, Apple MLX)
  - मूल्यांकन र प्रमाणीकरण चेकलिस्ट

- [**सेक्शन 4: Edge AI परिनियोजन हार्डवेयर प्लेटफर्महरू**](./Module01/04.EdgeDeployment.md)
  - Edge AI परिनियोजन विचारहरू र आवश्यकताहरू
  - Intel Edge AI हार्डवेयर र अनुकूलन प्रविधिहरू
  - मोबाइल र एम्बेडेड प्रणालीहरूको लागि Qualcomm AI समाधानहरू
  - NVIDIA Jetson र Edge कम्प्युटिङ प्लेटफर्महरू
  - Windows AI PC प्लेटफर्महरू NPU एक्सेलेरेशन सहित
  - हार्डवेयर-विशिष्ट अनुकूलन रणनीतिहरू

---

### [मोड्युल 02: साना भाषा मोडेलका आधारभूत](./Module02/README.md)
**थिम**: SLM सैद्धान्तिक सिद्धान्तहरू, कार्यान्वयन रणनीतिहरू, र उत्पादन परिनियोजन

#### अध्याय संरचना:
- [**सेक्शन 1: Microsoft Phi मोडेल परिवारका आधारभूत**](./Module02/01.PhiFamily.md)
  - डिजाइन दर्शनको विकास (Phi-1 देखि Phi-4)
  - दक्षता-प्रथम आर्किटेक्चर डिजाइन
  - विशेष क्षमताहरू (तर्क, मल्टीमोडल, Edge परिनियोजन)

- [**सेक्शन 2: Qwen परिवारका आधारभूत**](./Module02/02.QwenFamily.md)
  - खुला स्रोत उत्कृष्टता (Qwen 1.0 देखि Qwen3) - Hugging Face मार्फत उपलब्ध
  - सोच्ने मोड क्षमताहरू सहित उन्नत तर्क आर्किटेक्चर
  - स्केलेबल परिनियोजन विकल्पहरू (0.5B-235B पैरामीटर)

- [**सेक्शन 3: Gemma परिवारका आधारभूत**](./Module02/03.GemmaFamily.md)
  - अनुसन्धान-प्रेरित नवाचार (Gemma 3 & 3n)
  - मल्टीमोडल उत्कृष्टता
  - मोबाइल-प्रथम आर्किटेक्चर

- [**सेक्शन 4: BitNET परिवारका आधारभूत**](./Module02/04.BitNETFamily.md)
  - क्रान्तिकारी क्वान्टाइजेशन प्रविधि (1.58-bit)
  - https://github.com/microsoft/BitNet बाट विशेष इनफरेन्स फ्रेमवर्क
  - अत्यधिक दक्षताका माध्यमबाट दिगो AI नेतृत्व

- [**सेक्शन 5: Microsoft Mu मोडेलका आधारभूत**](./Module02/05.mumodel.md)
  - Windows 11 मा निर्मित डिभाइस-प्रथम आर्किटेक्चर
  - Windows 11 सेटिङ्ससँग प्रणाली एकीकरण
  - गोपनीयता-संरक्षण अफलाइन सञ्चालन

- [**सेक्शन 6: Phi-Silica का आधारभूत**](./Module02/06.phisilica.md)
  - Windows 11 Copilot+ PCs मा निर्मित NPU-अनुकूलित आर्किटेक्चर
  - असाधारण दक्षता (650 टोकन/सेकेन्ड 1.5W मा)
  - Windows App SDK सँग विकासकर्ता एकीकरण

---

### [मोड्युल 03: साना भाषा मोडेल परिनियोजन](./Module03/README.md)
**थिम**: SLM जीवनचक्र परिनियोजन, सैद्धान्तिकदेखि उत्पादन वातावरणसम्म

#### अध्याय संरचना:
- [**सेक्शन 1: SLM उन्नत सिकाइ**](./Module03/01.SLMAdvancedLearning.md)
  - पैरामीटर वर्गीकरण फ्रेमवर्क (Micro SLM 100M-1.4B, Medium SLM 14B-30B)
  - उन्नत अनुकूलन प्रविधिहरू (क्वान्टाइजेशन विधिहरू, BitNET 1-bit क्वान्टाइजेशन)
  - मोडेल प्राप्ति रणनीतिहरू (Phi मोडेलहरूको लागि Azure AI Foundry, चयनित मोडेलहरूको लागि Hugging Face)

- [**सेक्शन 2: स्थानीय वातावरण परिनियोजन**](./Module03/02.DeployingSLMinLocalEnv.md)
  - Ollama सार्वभौमिक प्लेटफर्म परिनियोजन
  - Microsoft Foundry स्थानीय उद्यम-ग्रेड समाधानहरू
  - फ्रेमवर्क तुलनात्मक विश्लेषण

- [**सेक्शन 3: कन्टेनराइज्ड क्लाउड परिनियोजन**](./Module03/03.DeployingSLMinCloud.md)
  - vLLM उच्च-प्रदर्शन इनफरेन्स परिनियोजन
  - Ollama कन्टेनर व्यवस्थापन
  - ONNX Runtime Edge-अनुकूलित कार्यान्वयन

---

### [मोड्युल 04: मोडेल ढाँचा रूपान्तरण र क्वान्टाइजेशन](./Module04/README.md)
**थिम**: Edge परिनियोजनका लागि प्लेटफर्महरूमा मोडेल अनुकूलन उपकरणको पूर्ण सेट

#### अध्याय संरचना:
- [**सेक्शन 1: मोडेल ढाँचा रूपान्तरण र क्वान्टाइजेशनका आधारभूत**](./Module04/01.Introduce.md)
  - सटीकता वर्गीकरण फ्रेमवर्क (अत्यन्त कम, कम, मध्यम सटीकता)
  - GGUF र ONNX ढाँचाका फाइदाहरू र प्रयोग केसहरू
  - क्वान्टाइजेशनका फाइदाहरू सञ्चालन दक्षताका लागि
  - प्रदर्शन बेंचमार्क र स्मृति खपत तुलना
- [**Section 2: Llama.cpp कार्यान्वयन मार्गदर्शन**](./Module04/02.Llamacpp.md)
  - क्रस-प्ल्याटफर्म स्थापना (Windows, macOS, Linux)
  - GGUF ढाँचा रूपान्तरण र क्वान्टाइजेसन स्तरहरू (Q2_K देखि Q8_0)
  - हार्डवेयर एक्सेलेरेशन (CUDA, Metal, OpenCL, Vulkan)
  - Python एकीकरण र REST API परिनियोजन

- [**Section 3: Microsoft Olive Optimization Suite**](./Module04/03.MicrosoftOlive.md)
  - हार्डवेयर-आधारित मोडेल अनुकूलन ४०+ बिल्ट-इन कम्पोनेन्टहरूसँग
  - गतिशील र स्थिर क्वान्टाइजेसनद्वारा स्वतः-अनुकूलन
  - Azure ML वर्कफ्लोहरूसँग उद्यम एकीकरण
  - लोकप्रिय मोडेल समर्थन (Llama, Phi, चयनित Qwen मोडेलहरू, Gemma)

- [**Section 4: OpenVINO Toolkit Optimization Suite**](./Module04/04.openvino.md)
  - Intel को क्रस-प्ल्याटफर्म AI परिनियोजनका लागि ओपन-सोर्स टूलकिट
  - उन्नत अनुकूलनका लागि Neural Network Compression Framework (NNCF)
  - ठूलो भाषा मोडेल परिनियोजनका लागि OpenVINO GenAI
  - CPU, GPU, VPU, र AI एक्सेलेरेटरहरूमा हार्डवेयर एक्सेलेरेशन

- [**Section 5: Apple MLX Framework गहिरो अध्ययन**](./Module04/05.AppleMLX.md)
  - Apple Silicon का लागि एकीकृत मेमोरी आर्किटेक्चर
  - LLaMA, Mistral, Phi-3, चयनित Qwen मोडेलहरूको समर्थन
  - LoRA फाइन-ट्युनिङ र मोडेल अनुकूलन
  - Hugging Face एकीकरण ४-बिट/८-बिट क्वान्टाइजेसनका साथ

- [**Section 6: Edge AI विकास वर्कफ्लो संश्लेषण**](./Module04/06.workflow-synthesis.md)
  - बहु-अनुकूलन फ्रेमवर्कहरू एकीकृत गर्ने एकीकृत वर्कफ्लो आर्किटेक्चर
  - फ्रेमवर्क चयन निर्णय वृक्षहरू र प्रदर्शन व्यापार-अफ विश्लेषण
  - उत्पादन तयारी प्रमाणीकरण र व्यापक परिनियोजन रणनीतिहरू
  - उदाउँदो हार्डवेयर र मोडेल आर्किटेक्चरहरूको लागि भविष्य-प्रूफिङ रणनीतिहरू

---

### [Module 05: SLMOps - सानो भाषा मोडेल अपरेसनहरू](./Module05/README.md)
**थिम**: डिस्टिलेसनदेखि उत्पादन परिनियोजनसम्मको सम्पूर्ण SLM जीवनचक्र अपरेसनहरू

#### अध्याय संरचना:
- [**Section 1: SLMOps को परिचय**](./Module05/01.IntroduceSLMOps.md)
  - AI अपरेसनहरूमा SLMOps को परिप्रेक्ष्य परिवर्तन
  - लागत दक्षता र गोपनीयता-प्रथम आर्किटेक्चर
  - रणनीतिक व्यापार प्रभाव र प्रतिस्पर्धात्मक लाभहरू
  - वास्तविक-विश्व कार्यान्वयन चुनौतीहरू र समाधानहरू

- [**Section 2: मोडेल डिस्टिलेसन - सिद्धान्तदेखि व्यवहारसम्म**](./Module05/02.SLMOps-Distillation.md)
  - शिक्षकबाट विद्यार्थी मोडेलहरूमा ज्ञान स्थानान्तरण
  - दुई-चरणीय डिस्टिलेसन प्रक्रिया कार्यान्वयन
  - व्यावहारिक उदाहरणहरूसहित Azure ML डिस्टिलेसन वर्कफ्लोहरू
  - ८५% इन्फरेन्स समय कटौती ९२% शुद्धता कायम राख्दै

- [**Section 3: फाइन-ट्युनिङ - विशिष्ट कार्यहरूको लागि मोडेलहरू अनुकूलन**](./Module05/03.SLMOps-Finetuing.md)
  - PEFT (Parameter-Efficient Fine-Tuning) प्रविधिहरू
  - LoRA र QLoRA उन्नत विधिहरू
  - Microsoft Olive फाइन-ट्युनिङ कार्यान्वयन
  - बहु-अडाप्टर प्रशिक्षण र हाइपरप्यारामिटर अनुकूलन

- [**Section 4: परिनियोजन - उत्पादन-तयारी कार्यान्वयन**](./Module05/04.SLMOps.Deployment.md)
  - उत्पादनका लागि मोडेल रूपान्तरण र क्वान्टाइजेसन
  - Foundry Local परिनियोजन कन्फिगरेसन
  - प्रदर्शन बेंचमार्किङ र गुणस्तर प्रमाणीकरण
  - ७५% आकार कटौती उत्पादन निगरानीका साथ

---

### [Module 06: SLM Agentic Systems - AI एजेन्टहरू र फङ्सन कलिङ](./Module06/README.md)
**थिम**: SLM एजेन्टिक प्रणाली कार्यान्वयन आधारदेखि उन्नत फङ्सन कलिङ र Model Context Protocol एकीकरणसम्म

#### अध्याय संरचना:
- [**Section 1: AI एजेन्टहरू र साना भाषा मोडेलहरूको आधार**](./Module06/01.IntroduceAgent.md)
  - एजेन्ट वर्गीकरण फ्रेमवर्क (reflex, model-based, goal-based, learning agents)
  - SLM को आधारभूत तत्वहरू र अनुकूलन रणनीतिहरू (GGUF, क्वान्टाइजेसन, एज फ्रेमवर्कहरू)
  - SLM बनाम LLM व्यापार-अफ विश्लेषण (१०-३०× लागत कटौती, ७०-८०% कार्य प्रभावकारिता)
  - Ollama, VLLM, र Microsoft एज समाधानहरूसँग व्यावहारिक परिनियोजन

- [**Section 2: साना भाषा मोडेलहरूमा फङ्सन कलिङ**](./Module06/02.FunctionCalling.md)
  - प्रणालीगत वर्कफ्लो कार्यान्वयन (intent detection, JSON output, external execution)
  - प्लेटफर्म-विशिष्ट कार्यान्वयनहरू (Phi-4-mini, चयनित Qwen मोडेलहरू, Microsoft Foundry Local)
  - उन्नत उदाहरणहरू (बहु-एजेन्ट सहयोग, गतिशील उपकरण चयन)
  - उत्पादन विचारहरू (rate limiting, audit logging, security measures)

- [**Section 3: Model Context Protocol (MCP) एकीकरण**](./Module06/03.IntroduceMCP.md)
  - प्रोटोकल आर्किटेक्चर र स्तरित प्रणाली डिजाइन
  - बहु-ब्याकएन्ड समर्थन (Ollama विकासका लागि, vLLM उत्पादनका लागि)
  - कनेक्शन प्रोटोकलहरू (STDIO र SSE मोडहरू)
  - वास्तविक-विश्व अनुप्रयोगहरू (वेब स्वचालन, डेटा प्रशोधन, API एकीकरण)

---

### [Module 07: EdgeAI कार्यान्वयन नमूनाहरू](./Module07/README.md)
**थिम**: विभिन्न प्लेटफर्म र फ्रेमवर्कहरूमा व्यापक EdgeAI कार्यान्वयनहरू

#### अध्याय संरचना:
- [**Visual Studio Code का लागि AI Toolkit**](./Module07/aitoolkit.md)
  - VS Code भित्र व्यापक Edge AI विकास वातावरण
  - एज परिनियोजनका लागि मोडेल क्याटलग र खोज
  - स्थानीय परीक्षण, अनुकूलन, र एजेन्ट विकास वर्कफ्लोहरू
  - एज परिदृश्यहरूको लागि प्रदर्शन निगरानी र मूल्याङ्कन

- [**Windows EdgeAI विकास मार्गदर्शन**](./Module07/windowdeveloper.md)
  - Windows AI Foundry प्लेटफर्मको व्यापक अवलोकन
  - Phi Silica API कुशल NPU इन्फरेन्सका लागि
  - छवि प्रशोधन र OCR का लागि Computer Vision APIs
  - स्थानीय विकास र परीक्षणका लागि Foundry Local CLI

- [**NVIDIA Jetson Orin Nano मा EdgeAI**](./Module07/README.md#1-edgeai-in-nvidia-jetson-orin-nano)
  - क्रेडिट-कार्ड आकारको फार्म फ्याक्टरमा ६७ TOPS AI प्रदर्शन
  - जेनेरेटिभ AI मोडेल समर्थन (vision transformers, LLMs, vision-language models)
  - रोबोटिक्स, ड्रोन, बुद्धिमान क्यामेरा, स्वायत्त उपकरणहरूमा अनुप्रयोगहरू
  - लोकतान्त्रित AI विकासका लागि किफायती $२४९ प्लेटफर्म

- [**.NET MAUI र ONNX Runtime GenAI का साथ मोबाइल अनुप्रयोगहरूमा EdgeAI**](./Module07/README.md#2-edgeai-in-mobile-applications-with-net-maui-and-onnx-runtime-genai)
  - एकल C# कोडबेसका साथ क्रस-प्ल्याटफर्म मोबाइल AI
  - हार्डवेयर एक्सेलेरेशन समर्थन (CPU, GPU, मोबाइल AI प्रोसेसरहरू)
  - प्लेटफर्म-विशिष्ट अनुकूलनहरू (CoreML iOS का लागि, NNAPI Android का लागि)
  - पूर्ण जेनेरेटिभ AI लूप कार्यान्वयन

- [**Azure मा साना भाषा मोडेल इन्जिनका साथ EdgeAI**](./Module07/README.md#3-edgeai-in-azure-with-small-language-models-engine)
  - क्लाउड-एज हाइब्रिड परिनियोजन आर्किटेक्चर
  - Azure AI सेवाहरू ONNX Runtime का साथ एकीकरण
  - उद्यम-स्तर परिनियोजन र निरन्तर मोडेल व्यवस्थापन
  - बुद्धिमान दस्तावेज प्रशोधनका लागि हाइब्रिड AI वर्कफ्लोहरू

- [**Windows ML का साथ EdgeAI**](./Module07/README.md#4-edgeai-with-windows-ml)
  - Windows AI Foundry आधारभूत तत्वहरू प्रदर्शनात्मक उपकरण-मा इन्फरेन्सका लागि
  - सार्वभौमिक हार्डवेयर समर्थन (AMD, Intel, NVIDIA, Qualcomm सिलिकन)
  - स्वचालित हार्डवेयर अमूर्तता र अनुकूलन
  - विविध Windows हार्डवेयर इकोसिस्टमका लागि एकीकृत फ्रेमवर्क

- [**Foundry Local अनुप्रयोगहरूसँग EdgeAI**](./Module07/README.md#5-edgeai-with-foundry-local-applications)
  - गोपनीयता-केंद्रित RAG कार्यान्वयन स्थानीय स्रोतहरूसँग
  - Phi-3 भाषा मोडेल एकीकरण सेम्यान्टिक खोजका साथ (Phi मोडेलहरू मात्र)
  - स्थानीय भेक्टर डाटाबेस समर्थन (SQLite, Qdrant)
  - डेटा सम्प्रभुता र अफलाइन अपरेशन क्षमताहरू

## पाठ्यक्रम सिकाइ उद्देश्यहरू

यस व्यापक EdgeAI पाठ्यक्रम पूरा गरेर, तपाईं उत्पादन-तयारी EdgeAI समाधानहरू डिजाइन, कार्यान्वयन, र परिनियोजन गर्ने विशेषज्ञता विकास गर्नुहुनेछ। हाम्रो संरचित दृष्टिकोणले सुनिश्चित गर्दछ कि तपाईंले सैद्धान्तिक आधारहरू र व्यावहारिक कार्यान्वयन सीपहरू दुवैमा महारत हासिल गर्नुहुन्छ।
यो पाठ्यक्रमले तपाईंलाई एआई प्रविधिको प्रयोगको अग्रभागमा राख्छ, जहाँ बौद्धिक क्षमता आधुनिक जीवनलाई शक्ति दिने उपकरणहरू र प्रणालीहरूमा सहज रूपमा समाहित गरिन्छ।

## फाइल संरचना ट्री डायग्राम

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

## पाठ्यक्रमका विशेषताहरू

- **प्रगतिशील सिकाइ**: आधारभूत अवधारणाबाट उन्नत प्रयोगसम्म क्रमिक रूपमा अगाडि बढ्नुहोस्
- **सिद्धान्त र अभ्यासको समायोजन**: प्रत्येक मोड्युलमा सैद्धान्तिक आधार र व्यावहारिक कार्यहरू समावेश छन्
- **वास्तविक केस अध्ययनहरू**: माइक्रोसफ्ट, अलीबाबा, गुगल, र अन्यका वास्तविक केसहरूमा आधारित
- **ह्यान्ड्स-अन अभ्यास**: पूर्ण कन्फिगरेसन फाइलहरू, API परीक्षण प्रक्रिया, र डिप्लोयमेन्ट स्क्रिप्टहरू
- **प्रदर्शन मापदण्डहरू**: अनुमान गति, मेमोरी प्रयोग, र स्रोत आवश्यकताहरूको विस्तृत तुलना
- **उद्योग-स्तरीय विचारहरू**: सुरक्षा अभ्यासहरू, अनुपालन फ्रेमवर्कहरू, र डाटा सुरक्षा रणनीतिहरू

## सुरु गर्ने तरिका

सिफारिस गरिएको सिकाइ मार्ग:
1. **Module01** बाट सुरु गर्नुहोस् ताकि EdgeAI को आधारभूत समझ निर्माण गर्न सकियोस्
2. **Module02** मा अगाडि बढ्नुहोस् ताकि विभिन्न SLM मोडेल परिवारहरूको गहिरो समझ प्राप्त गर्न सकियोस्
3. **Module03** सिक्नुहोस् ताकि व्यावहारिक डिप्लोयमेन्ट सीपहरूमा महारत हासिल गर्न सकियोस्
4. **Module04** जारी राख्नुहोस् ताकि उन्नत मोडेल अनुकूलन, फर्म्याट रूपान्तरण, र फ्रेमवर्क संश्लेषण सिक्न सकियोस्
5. **Module05** पूरा गर्नुहोस् ताकि उत्पादन-तयार कार्यान्वयनहरूको लागि SLMOps मा महारत हासिल गर्न सकियोस्
6. **Module06** अन्वेषण गर्नुहोस् ताकि SLM एजेन्टिक प्रणालीहरू र फङ्सन कलिङ क्षमताहरू बुझ्न सकियोस्
7. **Module07** समाप्त गर्नुहोस् ताकि AI Toolkit र विविध EdgeAI कार्यान्वयन नमूनाहरूको व्यावहारिक अनुभव प्राप्त गर्न सकियोस्

प्रत्येक मोड्युल स्वतन्त्र रूपमा पूर्ण रूपमा डिजाइन गरिएको छ, तर क्रमिक सिकाइले उत्कृष्ट परिणाम प्रदान गर्नेछ।

## अध्ययन मार्गदर्शक

सिकाइ अनुभवलाई अधिकतम बनाउनको लागि एक व्यापक [अध्ययन मार्गदर्शक](STUDY_GUIDE.md) उपलब्ध छ। अध्ययन मार्गदर्शकले प्रदान गर्दछ:

- **संरचित सिकाइ मार्गहरू**: २० घण्टामा पाठ्यक्रम पूरा गर्नको लागि अनुकूलित तालिकाहरू
- **समय वितरण मार्गदर्शन**: पढाइ, अभ्यास, र परियोजनाहरूको सन्तुलनको लागि विशिष्ट सिफारिसहरू
- **मुख्य अवधारणामा ध्यान केन्द्रित**: प्रत्येक मोड्युलको प्राथमिकता दिइएको सिकाइ उद्देश्यहरू
- **आत्म-मूल्यांकन उपकरणहरू**: तपाईंको समझ परीक्षण गर्नका लागि प्रश्नहरू र अभ्यासहरू
- **मिनी-परियोजना विचारहरू**: तपाईंको सिकाइलाई सुदृढ गर्नका लागि व्यावहारिक अनुप्रयोगहरू

अध्ययन मार्गदर्शकले तीव्र सिकाइ (१ हप्ता) र अंशकालिक अध्ययन (३ हप्ता) दुवैलाई समायोजन गर्न डिजाइन गरिएको छ, र तपाईंले पाठ्यक्रममा केवल १० घण्टा समर्पित गर्न सक्ने भए पनि समय प्रभावकारी रूपमा वितरण गर्ने स्पष्ट मार्गदर्शन प्रदान गर्दछ।

---

**EdgeAI को भविष्य मोडेल आर्किटेक्चरहरू, क्वान्टाइजेसन प्रविधिहरू, र डिप्लोयमेन्ट रणनीतिहरूको निरन्तर सुधारमा निर्भर छ, जसले दक्षता र विशेषज्ञतालाई सामान्य उद्देश्य क्षमताहरूभन्दा प्राथमिकता दिन्छ। यो परिप्रेक्ष्य परिवर्तनलाई अपनाउने संगठनहरू एआईको रूपान्तरणात्मक सम्भावनालाई उपयोग गर्न सक्षम हुनेछन्, जबकि आफ्नो डाटा र सञ्चालनहरूमा नियन्त्रण कायम राख्नेछन्।**

## अन्य पाठ्यक्रमहरू

हाम्रो टोलीले अन्य पाठ्यक्रमहरू उत्पादन गर्दछ! हेर्नुहोस्:

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

**अस्वीकरण**:  
यो दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) प्रयोग गरेर अनुवाद गरिएको छ। हामी शुद्धताको लागि प्रयास गर्छौं, तर कृपया ध्यान दिनुहोस् कि स्वचालित अनुवादहरूमा त्रुटिहरू वा अशुद्धताहरू हुन सक्छ। यसको मूल भाषा मा रहेको मूल दस्तावेज़लाई आधिकारिक स्रोत मानिनुपर्छ। महत्वपूर्ण जानकारीको लागि, व्यावसायिक मानव अनुवाद सिफारिस गरिन्छ। यस अनुवादको प्रयोगबाट उत्पन्न हुने कुनै पनि गलतफहमी वा गलत व्याख्याको लागि हामी जिम्मेवार हुने छैनौं।