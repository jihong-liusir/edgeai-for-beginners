<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "dbe223abcd2955df69a08033ff16d389",
  "translation_date": "2025-10-03T08:14:25+00:00",
  "source_file": "README.md",
  "language_code": "sr"
}
-->
# EdgeAI за почетнике

![Слика курса](../../translated_images/cover.eb18d1b9605d754b30973f4e17c6e11ea4f8473d9686ee378d6e7b44e3c70ac7.sr.png)

[![GitHub доприносиоци](https://img.shields.io/github/contributors/microsoft/edgeai-for-beginners.svg)](https://GitHub.com/microsoft/edgeai-for-beginners/graphs/contributors)  
[![GitHub проблеми](https://img.shields.io/github/issues/microsoft/edgeai-for-beginners.svg)](https://GitHub.com/microsoft/edgeai-for-beginners/issues)  
[![GitHub захтеви за промене](https://img.shields.io/github/issues-pr/microsoft/edgeai-for-beginners.svg)](https://GitHub.com/microsoft/edgeai-for-beginners/pulls)  
[![Добродошли захтеви за промене](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)  

[![GitHub пратиоци](https://img.shields.io/github/watchers/microsoft/edgeai-for-beginners.svg?style=social&label=Watch)](https://GitHub.com/microsoft/edgeai-for-beginners/watchers)  
[![GitHub форкови](https://img.shields.io/github/forks/microsoft/edgeai-for-beginners.svg?style=social&label=Fork)](https://GitHub.com/microsoft/edgeai-for-beginners/fork)  
[![GitHub звездице](https://img.shields.io/github/stars/microsoft/edgeai-for-beginners?style=social&label=Star)](https://GitHub.com/microsoft/edgeai-for-beginners/stargazers)  

[![Microsoft Azure AI Foundry Discord](https://dcbadge.limes.pink/api/server/ByRwuEEgH4)](https://discord.com/invite/ByRwuEEgH4)

Пратите ове кораке да бисте започели коришћење ових ресурса:

1. **Форкујте репозиторијум**: Кликните [![GitHub форкови](https://img.shields.io/github/forks/microsoft/edgeai-for-beginners.svg?style=social&label=Fork)](https://GitHub.com/microsoft/edgeai-for-beginners/fork)  
2. **Клонирајте репозиторијум**: `git clone https://github.com/microsoft/edgeai-for-beginners.git`  
3. [**Придружите се Azure AI Foundry Discord серверу и упознајте стручњаке и друге програмере**](https://discord.com/invite/ByRwuEEgH4)  

### 🌐 Подршка за више језика

#### Подржано преко GitHub Action (аутоматски и увек ажурирано)

[Арапски](../ar/README.md) | [Бенгалски](../bn/README.md) | [Бугарски](../bg/README.md) | [Бирмански (Мјанмар)](../my/README.md) | [Кинески (поједностављени)](../zh/README.md) | [Кинески (традиционални, Хонг Конг)](../hk/README.md) | [Кинески (традиционални, Макао)](../mo/README.md) | [Кинески (традиционални, Тајван)](../tw/README.md) | [Хрватски](../hr/README.md) | [Чешки](../cs/README.md) | [Дански](../da/README.md) | [Холандски](../nl/README.md) | [Фински](../fi/README.md) | [Француски](../fr/README.md) | [Немачки](../de/README.md) | [Грчки](../el/README.md) | [Хебрејски](../he/README.md) | [Хинди](../hi/README.md) | [Мађарски](../hu/README.md) | [Индонежански](../id/README.md) | [Италијански](../it/README.md) | [Јапански](../ja/README.md) | [Корејски](../ko/README.md) | [Малајски](../ms/README.md) | [Марати](../mr/README.md) | [Непалски](../ne/README.md) | [Норвешки](../no/README.md) | [Персијски (фарси)](../fa/README.md) | [Пољски](../pl/README.md) | [Португалски (Бразил)](../br/README.md) | [Португалски (Португал)](../pt/README.md) | [Пунџаби (Гурмуки)](../pa/README.md) | [Румунски](../ro/README.md) | [Руски](../ru/README.md) | [Српски (ћирилица)](./README.md) | [Словачки](../sk/README.md) | [Словеначки](../sl/README.md) | [Шпански](../es/README.md) | [Свахили](../sw/README.md) | [Шведски](../sv/README.md) | [Тагалог (Филипински)](../tl/README.md) | [Тајландски](../th/README.md) | [Турски](../tr/README.md) | [Украјински](../uk/README.md) | [Урду](../ur/README.md) | [Вијетнамски](../vi/README.md)

**Ако желите да се подрже додатни језици, листа је доступна [овде](https://github.com/Azure/co-op-translator/blob/main/getting_started/supported-languages.md)**

## Увод

Добродошли у **EdgeAI за почетнике** – ваш свеобухватни водич кроз трансформативни свет Edge вештачке интелигенције. Овај курс повезује моћне могућности вештачке интелигенције са практичном применом у стварном свету на уређајима на ивици, омогућавајући вам да искористите потенцијал вештачке интелигенције директно тамо где се подаци генеришу и где је потребно доносити одлуке.

### Шта ћете савладати

Овај курс вас води од основних концепата до имплементација спремних за производњу, обухватајући:
- **Мали језички модели (SLM)** оптимизовани за примену на ивици
- **Оптимизација у складу са хардвером** на различитим платформама
- **Инференција у реалном времену** уз очување приватности
- **Стратегије примене у производњи** за пословне апликације

### Зашто је EdgeAI важан

EdgeAI представља промену парадигме која решава кључне савремене изазове:
- **Приватност и безбедност**: Обрада осетљивих података локално, без излагања облаку
- **Перформансе у реалном времену**: Елиминисање кашњења у мрежи за апликације критичне за време
- **Ефикасност трошкова**: Смањење трошкова пропусног опсега и рачунарства у облаку
- **Отпорност у раду**: Одржавање функционалности током прекида мреже
- **Усклађеност са прописима**: Испуњавање захтева за суверенитетом података

### Edge AI

Edge AI подразумева покретање алгоритама вештачке интелигенције и језичких модела локално на хардверу, близу места где се подаци генеришу, без ослањања на ресурсе облака за инференцију. Смањује кашњење, побољшава приватност и омогућава доношење одлука у реалном времену.

### Основни принципи:
- **Инференција на уређају**: Модели вештачке интелигенције се покрећу на уређајима на ивици (телефони, рутери, микроконтролери, индустријски рачунари)
- **Офлајн способност**: Функционише без сталне интернет конекције
- **Ниско кашњење**: Одговори у реалном времену погодни за системе у реалном времену
- **Суверенитет података**: Чува осетљиве податке локално, побољшавајући безбедност и усклађеност

### Мали језички модели (SLM)

SLM-ови као што су Phi-4, Mistral-7B и Gemma су оптимизоване верзије већих LLM-ова – обучени или дестиловани за:
- **Смањен меморијски отисак**: Ефикасно коришћење ограничене меморије уређаја на ивици
- **Мање захтеве за рачунарском снагом**: Оптимизовани за перформансе CPU-а и GPU-а на ивици
- **Брже време покретања**: Брза иницијализација за одзивне апликације

Они омогућавају моћне NLP могућности уз испуњавање ограничења:
- **Уграђени системи**: IoT уређаји и индустријски контролери
- **Мобилни уређаји**: Смартфони и таблети са офлајн способностима
- **IoT уређаји**: Сензори и паметни уређаји са ограниченим ресурсима
- **Сервери на ивици**: Локалне јединице за обраду са ограниченим GPU ресурсима
- **Персонални рачунари**: Сценарији примене на десктоп и лаптоп рачунарима

## Модули курса и навигација

| Модул | Тема | Фокус | Кључни садржај | Ниво | Трајање |
|-------|------|-------|----------------|------|---------|
| [📖 00 ](./introduction.md) | [Увод у EdgeAI](./introduction.md) | Основе и контекст | Преглед EdgeAI • Примене у индустрији • Увод у SLM • Циљеви учења | Почетник | 1-2 сата |
| [📚 01](../../Module01) | [Основе EdgeAI](./Module01/README.md) | Поређење облака и Edge AI | Основе EdgeAI • Студије случаја из стварног света • Водич за имплементацију • Примена на ивици | Почетник | 3-4 сата |
| [🧠 02](../../Module02) | [Основе SLM модела](./Module02/README.md) | Породице модела и архитектура | Породица Phi • Породица Qwen • Породица Gemma • BitNET • μModel • Phi-Silica | Почетник | 4-5 сати |
| [🚀 03](../../Module03) | [Практична примена SLM](./Module03/README.md) | Локална и облачна примена | Напредно учење • Локално окружење • Примена у облаку | Средњи | 4-5 сати |
| [⚙️ 04](../../Module04) | [Алат за оптимизацију модела](./Module04/README.md) | Оптимизација на више платформи | Увод • Llama.cpp • Microsoft Olive • OpenVINO • Apple MLX • Синтеза радног процеса | Средњи | 5-6 сати |
| [🔧 05](../../Module05) | [SLMOps у производњи](./Module05/README.md) | Операције у производњи | Увод у SLMOps • Дестилација модела • Фино подешавање • Примена у производњи | Напредни | 5-6 сати |
| [🤖 06](../../Module06) | [AI агенти и позивање функција](./Module06/README.md) | Оквири агената и MCP | Увод у агенте • Позивање функција • Протокол контекста модела | Напредни | 4-5 сати |
| [💻 07](../../Module07) | [Примена на платформи](./Module07/README.md) | Примери на више платформи | AI алатке • Foundry Local • Развој за Windows | Напредни | 3-4 сата |
| [🏭 08](../../Module08) | [Foundry Local алатке](./Module08/README.md) | Примери спремни за производњу | Пример апликација (погледајте детаље испод) | Експерт | 8-10 сати |

### 🏭 **Модул 08: Пример апликација**

- [01: Брзи почетак REST чета](./Module08/samples/01/README.md)  
- [02: Интеграција OpenAI SDK-а](./Module08/samples/02/README.md)  
- [03: Откривање модела и бенчмаркинг](./Module08/samples/03/README.md)  
- [04: Chainlit RAG апликација](./Module08/samples/04/README.md)  
- [05: Оркестрација више агената](./Module08/samples/05/README.md)  
- [06: Рутер за моделе као алатке](./Module08/samples/06/README.md)  
- [07: Клијент директног API-а](./Module08/samples/07/README.md)  
- [08: Windows 11 апликација за чет](./Module08/samples/08/README.md)  
- [09: Напредни систем више агената](./Module08/samples/09/README.md)  
- [10: Оквир алатки Foundry](./Module08/samples/10/README.md)  

### 📊 **Резиме пута учења**
- **Укупно трајање**: 36-45 сати  
- **Пут за почетнике**: Модули 01-02 (7-9 сати)  
- **Средњи пут**: Модули 03-04 (9-11 сати)  
- **Напредни пут**: Модули 05-07 (12-15 сати)  
- **Експертски пут**: Модул 08 (8-10 сати)  

## Шта ћете изградити

### 🎯 Основне компетенције
- **Архитектура Edge AI**: Дизајнирање система вештачке интелигенције са локалним приступом и интеграцијом облака  
- **Оптимизација модела**: Квантизација и компресија модела за примену на ивици (85% убрзање, 75% смањење величине)  
- **Примена на више платформи**: Windows, мобилни уређаји, уграђени системи и хибридни системи облак-ивица  
- **Операције у производњи**: Праћење, скалирање и одржавање Edge AI у производњи  

### 🏗️ Практични пројекти
- **Foundry Local апликације за чет**: Windows 11 апликација са могућношћу промене модела  
- **Системи више агената**: Координатор са специјализованим агентима за сложене радне процесе  
- **RAG апликације**: Локална обрада докумената са претрагом вектора  
- **Рутери модела**: Интелигентан избор између модела на основу анализе задатка  
- **API оквири**: Клијенти спремни за производњу са стримингом и праћењем здравља  
- **Алатке за више платформи**: Шаблони интеграције LangChain/Semantic Kernel  

### 🏢 Примене у индустрији
**Производња** • **Здравство** • **Аутономна возила** • **Паметни градови** • **Мобилне апликације**

## Брзи почетак

**Препоручени пут учења** (укупно 20-30 сати):

0. **📖 Увод** ([Introduction.md](./introduction.md)): Основе EdgeAI + контекст индустрије + оквир за учење  
1. **📚 Основе** (Модули 01-02): Концепти EdgeAI + породице SLM модела  
2. **⚙️ Оптимизација** (Модули 03-04): Примена + окв
3. **🚀 Производња** (Модули 05-06): SLMOps + AI агенти + позивање функција  
4. **💻 Имплементација** (Модули 07-08): Примери платформе + Foundry Local алат

Сваки модул укључује теорију, практичне вежбе и узорке кода спремне за производњу.

## Утицај на каријеру

**Техничке улоге**: EdgeAI архитекта решења • ML инжењер (Edge) • IoT AI програмер • Мобилни AI програмер  

**Индустријски сектори**: Производња 4.0 • Здравствена технологија • Аутономни системи • ФинТек • Потрошачка електроника  

**Пројекти за портфолио**: Системи са више агената • RAG апликације за производњу • Мултиплатформска имплементација • Оптимизација перформанси  

## Структура репозиторијума

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
  

## Истакнути делови курса

✅ **Прогресивно учење**: Теорија → Практична примена → Имплементација у производњи  
✅ **Студије случаја из стварног света**: Microsoft, Japan Airlines, корпоративне имплементације  
✅ **Практични примери**: 50+ примера, 10 свеобухватних Foundry Local демонстрација  
✅ **Фокус на перформансе**: 85% побољшања брзине, 75% смањења величине  
✅ **Мултиплатформска подршка**: Windows, мобилни уређаји, уграђени системи, хибридни cloud-edge  
✅ **Спремно за производњу**: Надзор, скалабилност, безбедност, оквири за усклађеност  

📖 **[Доступан водич за учење](STUDY_GUIDE.md)**: Структурисан план учења од 20 сати са смерницама за расподелу времена и алатима за самопроцену.

---

**EdgeAI представља будућност имплементације AI-а**: локално оријентисан, са очувањем приватности и ефикасношћу. Савладајте ове вештине да бисте изградили следећу генерацију интелигентних апликација.

## Остали курсеви

Наш тим производи и друге курсеве! Погледајте:

- [MCP за почетнике](https://github.com/microsoft/mcp-for-beginners)  
- [AI агенти за почетнике](https://github.com/microsoft/ai-agents-for-beginners?WT.mc_id=academic-105485-koreyst)  
- [Генеративни AI за почетнике користећи .NET](https://github.com/microsoft/Generative-AI-for-beginners-dotnet?WT.mc_id=academic-105485-koreyst)  
- [Генеративни AI за почетнике користећи JavaScript](https://github.com/microsoft/generative-ai-with-javascript?WT.mc_id=academic-105485-koreyst)  
- [Генеративни AI за почетнике](https://github.com/microsoft/generative-ai-for-beginners?WT.mc_id=academic-105485-koreyst)  
- [ML за почетнике](https://aka.ms/ml-beginners?WT.mc_id=academic-105485-koreyst)  
- [Наука о подацима за почетнике](https://aka.ms/datascience-beginners?WT.mc_id=academic-105485-koreyst)  
- [AI за почетнике](https://aka.ms/ai-beginners?WT.mc_id=academic-105485-koreyst)  
- [Сајбер безбедност за почетнике](https://github.com/microsoft/Security-101??WT.mc_id=academic-96948-sayoung)  
- [Веб развој за почетнике](https://aka.ms/webdev-beginners?WT.mc_id=academic-105485-koreyst)  
- [IoT за почетнике](https://aka.ms/iot-beginners?WT.mc_id=academic-105485-koreyst)  
- [XR развој за почетнике](https://github.com/microsoft/xr-development-for-beginners?WT.mc_id=academic-105485-koreyst)  
- [Savladavanje GitHub Copilot-а за AI парно програмирање](https://aka.ms/GitHubCopilotAI?WT.mc_id=academic-105485-koreyst)  
- [Savladavanje GitHub Copilot-а за C#/.NET програмере](https://github.com/microsoft/mastering-github-copilot-for-dotnet-csharp-developers?WT.mc_id=academic-105485-koreyst)  
- [Изаберите своју Copilot авантуру](https://github.com/microsoft/CopilotAdventures?WT.mc_id=academic-105485-koreyst)  

## Добијање помоћи

Ако се заглавите или имате питања о изградњи AI апликација, придружите се:

[![Azure AI Foundry Discord](https://img.shields.io/badge/Discord-Azure_AI_Foundry_Community_Discord-blue?style=for-the-badge&logo=discord&color=5865f2&logoColor=fff)](https://aka.ms/foundry/discord)

Ако имате повратне информације о производу или наиђете на грешке током изградње, посетите:

[![Azure AI Foundry Developer Forum](https://img.shields.io/badge/GitHub-Azure_AI_Foundry_Developer_Forum-blue?style=for-the-badge&logo=github&color=000000&logoColor=fff)](https://aka.ms/foundry/forum)

---

**Одрицање од одговорности**:  
Овај документ је преведен помоћу услуге за превођење уз помоћ вештачке интелигенције [Co-op Translator](https://github.com/Azure/co-op-translator). Иако се трудимо да обезбедимо тачност, молимо вас да имате у виду да аутоматски преводи могу садржати грешке или нетачности. Оригинални документ на изворном језику треба сматрати меродавним извором. За критичне информације препоручује се професионални превод од стране људи. Не сносимо одговорност за било каква погрешна тумачења или неспоразуме који могу настати услед коришћења овог превода.