<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "cb6eadc312d5658a0cd71c0085b43742",
  "translation_date": "2025-09-23T00:41:46+00:00",
  "source_file": "Module07/README.md",
  "language_code": "lt"
}
-->
# 7 skyrius: EdgeAI pavyzdžiai

Edge AI – tai dirbtinio intelekto ir kraštinio skaičiavimo susiliejimas, leidžiantis vykdyti išmanųjį apdorojimą tiesiogiai įrenginiuose, nereikalaujant ryšio su debesimi. Šiame skyriuje nagrinėjami penki skirtingi EdgeAI įgyvendinimo būdai įvairiose platformose ir sistemose, parodantys AI modelių veikimo krašte universalumą ir galią.

## 1. EdgeAI NVIDIA Jetson Orin Nano platformoje

NVIDIA Jetson Orin Nano – tai proveržis prieinamo kraštinio AI skaičiavimo srityje, suteikiantis iki 67 TOPS AI našumo kompaktiškoje, kreditinės kortelės dydžio formoje. Ši galinga Edge AI platforma demokratizuoja generatyvinio AI kūrimą tiek mėgėjams, tiek studentams, tiek profesionaliems kūrėjams.

### Pagrindinės savybės
- Suteikia iki 67 TOPS AI našumo – 1,7 karto daugiau nei ankstesnė versija
- 1024 CUDA branduoliai ir iki 32 Tensor branduolių AI apdorojimui
- 6 branduolių Arm Cortex-A78AE v8.2 64-bit CPU, maksimalus dažnis – 1,5 GHz
- Kaina tik $249, suteikiant kūrėjams, studentams ir entuziastams prieinamą platformą

### Pritaikymo sritys
Jetson Orin Nano puikiai tinka modernių generatyvinių AI modelių, tokių kaip vizijos transformatoriai, dideli kalbos modeliai ir vizijos-kalbos modeliai, vykdymui. Jis specialiai sukurtas GenAI atvejams, leidžiant vykdyti kelis LLM modelius delno dydžio įrenginyje. Populiarios pritaikymo sritys apima AI valdomą robotiką, išmaniuosius dronus, išmaniąsias kameras ir autonominius kraštinius įrenginius.

**Sužinokite daugiau**: [NVIDIA Jetson Orin Nano SuperComputer: The Next Big Thing in EdgeAI](https://medium.com/data-science-in-your-pocket/nvidias-jetson-orin-nano-supercomputer-the-next-big-thing-in-edgeai-e9eff687ae62)

## 2. EdgeAI mobiliose aplikacijose su .NET MAUI ir ONNX Runtime GenAI

Šis sprendimas parodo, kaip integruoti generatyvinį AI ir didelius kalbos modelius (LLMs) į daugiaplatformines mobilias aplikacijas naudojant .NET MAUI (Multi-platform App UI) ir ONNX Runtime GenAI. Šis metodas leidžia .NET kūrėjams kurti pažangias AI valdomas mobilias aplikacijas, kurios veikia natyviai Android ir iOS įrenginiuose.

### Pagrindinės savybės
- Sukurta ant .NET MAUI sistemos, suteikiant vieną kodų bazę tiek Android, tiek iOS aplikacijoms
- ONNX Runtime GenAI integracija leidžia vykdyti generatyvinius AI modelius tiesiogiai mobiliuose įrenginiuose
- Palaiko įvairius aparatūros akceleratorius, pritaikytus mobiliesiems įrenginiams, įskaitant CPU, GPU ir specializuotus AI procesorius
- Platformai specifinės optimizacijos, tokios kaip CoreML iOS ir NNAPI Android per ONNX Runtime
- Įgyvendina visą generatyvinio AI ciklą, įskaitant išankstinį ir po apdorojimą, inferenciją, logitų apdorojimą, paiešką ir atranką, bei KV talpyklos valdymą

### Kūrimo privalumai
.NET MAUI metodas leidžia kūrėjams pasinaudoti jau turimais C# ir .NET įgūdžiais kuriant daugiaplatformines AI aplikacijas. ONNX Runtime GenAI sistema palaiko įvairias modelių architektūras, tokias kaip Llama, Mistral, Phi, Gemma ir daugelį kitų. Optimizuoti ARM64 branduoliai pagreitina INT4 kvantizuotą matricų daugybą, užtikrinant efektyvų veikimą mobilioje aparatūroje, išlaikant pažįstamą .NET kūrimo patirtį.

### Pritaikymo sritys
Šis sprendimas idealiai tinka kūrėjams, norintiems kurti AI valdomas mobilias aplikacijas naudojant .NET technologijas, įskaitant išmaniuosius pokalbių robotus, vaizdų atpažinimo aplikacijas, kalbos vertimo įrankius ir personalizuotas rekomendacijų sistemas, kurios veikia visiškai įrenginyje, užtikrinant privatumą ir galimybę dirbti neprisijungus.

**Sužinokite daugiau**: [.NET MAUI ONNX Runtime GenAI Example](https://github.com/microsoft/onnxruntime-genai/tree/jialli/genny-maui/examples/csharp/GennyMaui)

## 3. EdgeAI Azure platformoje su mažų kalbos modelių varikliu

Microsoft Azure pagrįstas EdgeAI sprendimas orientuojasi į efektyvų mažų kalbos modelių (SLMs) diegimą debesies-krašto hibridinėse aplinkose. Šis metodas sujungia debesies masto AI paslaugas su krašto diegimo poreikiais.

### Architektūros privalumai
- Sklandi integracija su Azure AI paslaugomis
- SLMs/LLMs ir daugiarūšių modelių vykdymas įrenginyje ir debesyje naudojant ONNX Runtime
- Optimizuota įmonės masto diegimui
- Palaikymas nuolatiniam modelių atnaujinimui ir valdymui

### Pritaikymo sritys
Azure EdgeAI įgyvendinimas puikiai tinka scenarijams, kuriems reikalingas įmonės lygio AI diegimas su debesies valdymo galimybėmis. Tai apima išmanų dokumentų apdorojimą, realaus laiko analizę ir hibridinius AI darbo procesus, kurie pasinaudoja tiek debesies, tiek krašto skaičiavimo ištekliais.

**Sužinokite daugiau**: [Azure EdgeAI SLM Engine](https://github.com/microsoft/onnxruntime-genai/tree/main/examples/slm_engine)

## 4. EdgeAI su Windows ML

Windows ML – tai Microsoft pažangus vykdymo laikas, optimizuotas efektyviam modelių vykdymui įrenginyje ir supaprastintam diegimui, kuris yra Windows AI Foundry pagrindas. Ši platforma leidžia kūrėjams kurti AI valdomas Windows aplikacijas, pasinaudojant visais PC aparatūros privalumais.

### Platformos galimybės
- Veikia visuose Windows 11 kompiuteriuose, kurių versija 24H2 (build 26100) ar naujesnė
- Veikia visuose x64 ir ARM64 PC įrenginiuose, net ir tuose, kurie neturi NPU ar GPU
- Leidžia kūrėjams naudoti savo modelius ir efektyviai juos diegti visoje silicio partnerių ekosistemoje, įskaitant AMD, Intel, NVIDIA ir Qualcomm, apimančius CPU, GPU, NPU
- Naudojant infrastruktūros API, kūrėjams nebereikia kurti kelių aplikacijos versijų, kad būtų galima taikyti skirtingą silicio

### Kūrėjų privalumai
Windows ML abstrahuoja aparatūrą ir vykdymo tiekėjus, todėl galite susitelkti į savo kodo rašymą. Be to, Windows ML automatiškai atnaujinama, kad palaikytų naujausius NPU, GPU ir CPU, kai jie išleidžiami. Platforma suteikia vieningą sistemą AI kūrimui visoje įvairioje Windows aparatūros ekosistemoje.

**Sužinokite daugiau**: 
- [Windows ML apžvalga](https://learn.microsoft.com/en-us/windows/ai/new-windows-ml/overview)
- [Windows EdgeAI kūrimo vadovas](../windowdeveloper.md) – išsamus Windows Edge AI kūrimo vadovas

## 5. EdgeAI su Foundry Local aplikacijomis

Foundry Local leidžia kūrėjams kurti Retrieval Augmented Generation (RAG) aplikacijas naudojant vietinius išteklius .NET aplinkoje, derinant vietinius kalbos modelius su semantinės paieškos galimybėmis. Šis metodas suteikia privatumo orientuotus AI sprendimus, veikiančius visiškai vietinėje infrastruktūroje.

### Techninė architektūra
- Derina Phi kalbos modelį, vietinius įterpimus ir semantinį branduolį, kad sukurtų RAG scenarijų
- Naudoja įterpimus kaip vektorius (masyvus) slankiojo kablelio reikšmių, kurios atspindi turinį ir jo semantinę prasmę
- Semantinis branduolys veikia kaip pagrindinis organizatorius, integruojantis Phi ir išmaniuosius komponentus, kad sukurtų sklandų RAG procesą
- Palaikymas vietinėms vektorinėms duomenų bazėms, įskaitant SQLite ir Qdrant

### Įgyvendinimo privalumai
RAG, arba Retrieval Augmented Generation, paprastai reiškia „ieškoti informacijos ir įtraukti ją į užklausą“. Šis vietinis įgyvendinimas užtikrina duomenų privatumą, tuo pačiu teikiant išmanius atsakymus, pagrįstus individualizuotomis žinių bazėmis. Šis metodas ypač vertingas įmonių scenarijams, kuriems reikalingas duomenų suverenitetas ir galimybė veikti neprisijungus.

**Sužinokite daugiau**: [Foundry Local RAG pavyzdžiai](https://github.com/microsoft/Foundry-Local/tree/main/samples/dotNET/rag)

### Windows Foundry Local

Microsoft Foundry Local suteikia OpenAI suderinamą REST serverį, valdomą ONNX Runtime, skirtą modelių vykdymui vietoje Windows aplinkoje. Žemiau pateikiama greita, patvirtinta santrauka; oficialiuose dokumentuose rasite visą informaciją.

- Pradėkite: https://learn.microsoft.com/azure/ai-foundry/foundry-local/get-started
- Architektūra: https://learn.microsoft.com/azure/ai-foundry/foundry-local/concepts/foundry-local-architecture
- CLI nuoroda: https://learn.microsoft.com/azure/ai-foundry/foundry-local/reference/reference-cli
- Pilnas Windows vadovas šiame repozitoriume: [foundrylocal.md](./foundrylocal.md)

Įdiegimas arba atnaujinimas Windows (cmd.exe):
```cmd
winget install Microsoft.FoundryLocal
winget upgrade --id Microsoft.FoundryLocal
foundry --version
```

Naršykite CLI kategorijas:
```cmd
foundry model --help
foundry service --help
foundry cache --help
```

Vykdykite modelį ir atraskite dinaminį galinį tašką:
```cmd
foundry model run gpt-oss-20b
foundry service status
```

Greitas REST patikrinimas norint išvardyti modelius (pakeiskite PORT iš statuso):
```cmd
curl -s http://localhost:PORT/v1/models
```

Patarimai:
- SDK integracija: https://learn.microsoft.com/azure/ai-foundry/foundry-local/how-to/how-to-integrate-with-inference-sdks
- Naudokite savo modelį (kompiliavimas): https://learn.microsoft.com/azure/ai-foundry/foundry-local/how-to/how-to-compile-hugging-face-models

## Windows EdgeAI kūrimo ištekliai

Kūrėjams, kurie orientuojasi į Windows platformą, sukūrėme išsamų vadovą, apimantį visą Windows EdgeAI ekosistemą. Šis šaltinis pateikia detalią informaciją apie Windows AI Foundry, įskaitant API, įrankius ir geriausią praktiką EdgeAI kūrimui Windows aplinkoje.

### Windows AI Foundry platforma
Windows AI Foundry platforma suteikia išsamų įrankių ir API rinkinį, specialiai sukurtą Edge AI kūrimui Windows įrenginiuose. Tai apima specializuotą palaikymą NPU-akseleruotai aparatūrai, Windows ML integraciją ir platformai specifines optimizavimo technikas.

**Išsamus vadovas**: [Windows EdgeAI kūrimo vadovas](../windowdeveloper.md)

Šis vadovas apima:
- Windows AI Foundry platformos apžvalgą ir komponentus
- Phi Silica API efektyviam inferencijai NPU aparatūroje
- Kompiuterinės vizijos API vaizdų apdorojimui ir OCR
- Windows ML vykdymo laiko integraciją ir optimizaciją
- Foundry Local CLI vietiniam kūrimui ir testavimui
- Aparatūros optimizavimo strategijas Windows įrenginiams
- Praktinius įgyvendinimo pavyzdžius ir geriausią praktiką

### AI įrankių rinkinys Edge AI kūrimui
Kūrėjams, naudojantiems Visual Studio Code, AI įrankių rinkinio plėtinys suteikia išsamų kūrimo aplinką, specialiai sukurtą Edge AI aplikacijų kūrimui, testavimui ir diegimui. Šis įrankių rinkinys supaprastina visą Edge AI kūrimo procesą VS Code aplinkoje.

**Kūrimo vadovas**: [AI įrankių rinkinys Edge AI kūrimui](../aitoolkit.md)

AI įrankių rinkinio vadovas apima:
- Modelių atradimą ir pasirinkimą krašto diegimui
- Vietinio testavimo ir optimizavimo darbo procesus
- ONNX ir Ollama integraciją krašto modeliams
- Modelių konvertavimo ir kvantizavimo technikas
- Agentų kūrimą krašto scenarijams
- Našumo vertinimą ir stebėjimą
- Diegimo paruošimą ir geriausią praktiką

## Išvada

Šie penki EdgeAI įgyvendinimai parodo Edge AI sprendimų brandą ir įvairovę, prieinamą šiandien. Nuo aparatūros-akseleruotų kraštinių įrenginių, tokių kaip Jetson Orin Nano, iki programinės įrangos sistemų, tokių kaip ONNX Runtime GenAI ir Windows ML, kūrėjai turi precedento neturinčias galimybes diegti išmaniąsias aplikacijas krašte.

Bendras visų šių platformų bruožas – AI galimybių demokratizavimas, leidžiantis sudėtingą mašininį mokymąsi pasiekti kūrėjams, turintiems skirtingus įgūdžių lygius ir pritaikymo sritis. Nesvarbu, ar kuriate mobilias aplikacijas, darbalaukio programinę įrangą, ar įterptines sistemas, šie EdgeAI sprendimai suteikia pagrindą naujos kartos išmaniosioms aplikacijoms, kurios veikia efektyviai ir privačiai krašte.

Kiekviena platforma siūlo unikalius privalumus: Jetson Orin Nano aparatūros-akseleruotam kraštiniam skaičiavimui, ONNX Runtime GenAI daugiaplatforminiam mobiliųjų aplikacijų kūrimui, Azure EdgeAI įmonės debesies-krašto integracijai, Windows ML Windows-natyvioms aplikacijoms ir Foundry Local privatumo orientuotoms RAG įgyvendinimams. Kartu jos sudaro išsamų EdgeAI kūrimo ekosistemą.

---

