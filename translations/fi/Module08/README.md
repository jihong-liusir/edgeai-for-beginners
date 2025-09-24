<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "50d80c321803b5170d9a9cd9bbfb37a3",
  "translation_date": "2025-09-24T23:28:57+00:00",
  "source_file": "Module08/README.md",
  "language_code": "fi"
}
-->
# Moduuli 08: Käytännön harjoituksia Microsoft Foundry Local - Täydellinen kehittäjätyökalupakki

## Yleiskatsaus

Microsoft Foundry Local edustaa seuraavan sukupolven reunalaskennan AI-kehitystä, tarjoten kehittäjille tehokkaat työkalut AI-sovellusten rakentamiseen, käyttöönottoon ja skaalaamiseen paikallisesti samalla, kun säilytetään saumaton integraatio Azure AI Foundryn kanssa. Tämä moduuli kattaa Foundry Localin perusteellisesti asennuksesta edistyneeseen agenttikehitykseen.

**Keskeiset teknologiat:**
- Microsoft Foundry Local CLI ja SDK
- Azure AI Foundry -integraatio
- Mallien paikallinen inferenssi
- Mallien paikallinen välimuisti ja optimointi
- Agenttipohjaiset arkkitehtuurit

## Oppimistavoitteet

Tämän moduulin suorittamalla opit:

- **Hallitsemaan Foundry Localia**: Asenna, konfiguroi ja optimoi Windows 11 -kehitystä varten
- **Ottamaan käyttöön erilaisia malleja**: Suorita phi-, qwen-, deepseek- ja GPT-malleja paikallisesti CLI-komentojen avulla
- **Rakentamaan tuotantoratkaisuja**: Luo AI-sovelluksia edistyneellä prompt-engineeringillä ja dataintegraatiolla
- **Hyödyntämään avoimen lähdekoodin ekosysteemiä**: Integroi Hugging Face -malleja ja yhteisön kontribuutioita
- **Kehittämään AI-agentteja**: Rakenna älykkäitä agentteja perustamis- ja orkestrointikyvyillä
- **Toteuttamaan yrityskäytön malleja**: Luo modulaarisia, skaalautuvia AI-ratkaisuja tuotantokäyttöön

## Istunnon rakenne

### [1: Aloittaminen Foundry Localilla](./01.FoundryLocalSetup.md)
**Painopiste**: Asennus, CLI-asetukset, mallien käyttöönotto ja laitteiston optimointi

**Keskeiset aiheet**: Täydellinen asennus • CLI-komennot • Mallien välimuisti • Laitteiston kiihdytys • Monimallien käyttöönotto

**Esimerkki**: [REST Chat Quickstart](./samples/01/README.md) • [OpenAI SDK Integration](./samples/02/README.md) • [Model Discovery & Benchmarking](./samples/03/README.md)

**Kesto**: 2-3 tuntia | **Taso**: Aloittelija

---

### [2: Rakenna AI-ratkaisuja Azure AI Foundrylla](./02.AzureAIFoundryIntegration.md)
**Painopiste**: Edistynyt prompt-engineering, dataintegraatio ja pilviyhteydet

**Keskeiset aiheet**: Prompt-engineering • Dataintegraatio • Azure-työnkulut • Suorituskyvyn optimointi • Seuranta

**Esimerkki**: [Chainlit RAG Application](./samples/04/README.md)

**Kesto**: 2-3 tuntia | **Taso**: Keskitaso

---

### [3: Avoimen lähdekoodin mallit Foundry Localilla](./03.OpenSourceModels.md)
**Painopiste**: Hugging Face -integraatio, BYOM-strategiat ja yhteisön mallit

**Keskeiset aiheet**: Hugging Face -integraatio • Bring-your-own-model • Model Mondays -oivallukset • Yhteisön kontribuutiot • Mallien valinta

**Esimerkki**: [Multi-Agent Orchestration](./samples/05/README.md)

**Kesto**: 2-3 tuntia | **Taso**: Keskitaso

---

### [4: Tutustu huippumalleihin](./04.CuttingEdgeModels.md)
**Painopiste**: LLM:t vs SLM:t, EdgeAI-toteutus ja edistyneet demot

**Keskeiset aiheet**: Mallien vertailu • Reuna- vs pilvi-inferenssi • Phi + ONNX Runtime • Chainlit RAG -sovellus • WebGPU-optimointi

**Esimerkki**: [Models-as-Tools Router](./samples/06/README.md)

**Kesto**: 3-4 tuntia | **Taso**: Edistynyt

---

### [5: Rakenna AI-pohjaisia agentteja nopeasti](./05.AIPoweredAgents.md)
**Painopiste**: Agenttiarkkitehtuurit, järjestelmäpromptit, perustaminen ja orkestrointi

**Keskeiset aiheet**: Agenttisuunnittelumallit • Järjestelmäpromptien suunnittelu • Perustamistekniikat • Moniagenttijärjestelmät • Tuotantokäyttöön ottaminen

**Esimerkki**: [Multi-Agent Orchestration](./samples/05/README.md) • [Advanced Multi-Agent System](./samples/09/README.md)

**Kesto**: 3-4 tuntia | **Taso**: Edistynyt

---

### [6: Foundry Local - Mallit työkaluina](./06.ModelsAsTools.md)
**Painopiste**: Modulaariset AI-ratkaisut, yritysskaalaus ja tuotantokäytön mallit

**Keskeiset aiheet**: Mallit työkaluina • Paikallinen käyttöönotto • SDK/API-integraatio • Yritysarkkitehtuurit • Skaalausstrategiat

**Esimerkki**: [Models-as-Tools Router](./samples/06/README.md) • [Foundry Tools Framework](./samples/10/README.md)

**Kesto**: 3-4 tuntia | **Taso**: Ekspertti

---

### [7: Suorat API-integraatiomallit](./samples/07/README.md)
**Painopiste**: REST API -integraatio ilman SDK-riippuvuuksia maksimaalisen hallinnan saavuttamiseksi

**Keskeiset aiheet**: HTTP-asiakasohjelman toteutus • Mukautettu autentikointi • Mallien terveyden seuranta • Vastausten suoratoisto • Tuotannon virheenkäsittely

**Esimerkki**: [Direct API Client](./samples/07/README.md)

**Kesto**: 2-3 tuntia | **Taso**: Keskitaso

---

### [8: Windows 11 -natiivi chat-sovellus](./samples/08/README.md)
**Painopiste**: Modernien natiivien chat-sovellusten rakentaminen Foundry Local -integraatiolla

**Keskeiset aiheet**: Electron-kehitys • Fluent Design System • Natiivi Windows-integraatio • Reaaliaikainen suoratoisto • Chat-käyttöliittymän suunnittelu

**Esimerkki**: [Windows 11 Chat Application](./samples/08/README.md)

**Kesto**: 3-4 tuntia | **Taso**: Edistynyt

---

### [9: Edistynyt moniagenttien orkestrointi](./samples/09/README.md)
**Painopiste**: Monimutkainen agenttien koordinointi, erikoistuneet tehtävien delegoinnit ja yhteistyöhön perustuvat AI-työnkulut

**Keskeiset aiheet**: Älykäs agenttien koordinointi • Funktiokutsumallit • Agenttien välinen viestintä • Työnkulun orkestrointi • Laadunvarmistusmekanismit

**Esimerkki**: [Advanced Multi-Agent System](./samples/09/README.md)

**Kesto**: 4-5 tuntia | **Taso**: Ekspertti

---

### [10: Foundry Local työkalukehyksenä](./samples/10/README.md)
**Painopiste**: Työkalu-ensimmäinen arkkitehtuuri Foundry Localin integroimiseksi olemassa oleviin sovelluksiin ja kehyksiin

**Keskeiset aiheet**: LangChain-integraatio • Semanttiset Kernel-funktiot • REST API -kehykset • CLI-työkalut • Jupyter-integraatio • Tuotantokäytön mallit

**Esimerkki**: [Foundry Tools Framework](./samples/10/README.md)

**Kesto**: 4-5 tuntia | **Taso**: Ekspertti

## Esivaatimukset

### Järjestelmävaatimukset
- **Käyttöjärjestelmä**: Windows 11 (22H2 tai uudempi)
- **Muisti**: 16GB RAM (32GB suositeltu suuremmille malleille)
- **Tallennustila**: 50GB vapaata tilaa mallien välimuistille
- **Laitteisto**: NPU-tuettu laite suositeltu (Copilot+ PC), GPU valinnainen
- **Verkko**: Nopea internetyhteys mallien alkuperäistä latausta varten

### Kehitysympäristö
- Visual Studio Code AI Toolkit -laajennuksella
- Python 3.10+ ja pip
- Git versionhallintaan
- PowerShell tai komentokehote
- Azure CLI (valinnainen pilvi-integraatiota varten)

### Tietovaatimukset
- Perustiedot AI/ML-konsepteista
- Komentorivin peruskäyttö
- Python-ohjelmoinnin perusteet
- REST API -konseptit
- Perustiedot promptien ja mallien inferenssistä

## Moduulin aikataulu

**Arvioitu kokonaisaika**: 30-38 tuntia

| Istunto | Painopistealue | Esimerkit | Aika | Monimutkaisuus |
|---------|----------------|-----------|------|----------------|
|  1 | Asennus & perusteet | 01, 02, 03 | 2-3 tuntia | Aloittelija |
|  2 | AI-ratkaisut | 04 | 2-3 tuntia | Keskitaso |
|  3 | Avoin lähdekoodi | 05 | 2-3 tuntia | Keskitaso |
|  4 | Edistyneet mallit | 06 | 3-4 tuntia | Edistynyt |
|  5 | AI-agentit | 05, 09 | 3-4 tuntia | Edistynyt |
|  6 | Yritystyökalut | 06, 10 | 3-4 tuntia | Ekspertti |
|  7 | Suora API-integraatio | 07 | 2-3 tuntia | Keskitaso |
|  8 | Windows 11 -chat-sovellus | 08 | 3-4 tuntia | Edistynyt |
|  9 | Edistynyt moniagentti | 09 | 4-5 tuntia | Ekspertti |
| 10 | Työkalukehys | 10 | 4-5 tuntia | Ekspertti |

## Keskeiset resurssit

**Virallinen dokumentaatio:**
- [Microsoft Foundry Local GitHub](https://github.com/microsoft/Foundry-Local) - Lähdekoodi ja viralliset esimerkit
- [Azure AI Foundry Dokumentaatio](https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/) - Täydellinen asennus- ja käyttöopas
- [Model Mondays -sarja](https://aka.ms/model-mondays) - Viikoittaiset malliesittelyt ja tutoriaalit

**Yhteisö & tuki:**
- [Foundry Local Keskustelut](https://github.com/microsoft/Foundry-Local/discussions) - Yhteisön kysymykset ja ominaisuuspyynnöt
- [Microsoft AI Developer Community](https://techcommunity.microsoft.com/category/artificialintelligence) - Uusimmat uutiset ja parhaat käytännöt

## Oppimistulokset

Moduulin suorittamisen jälkeen sinulla on valmiudet:

### Tekninen osaaminen
- **Käyttöönotto ja hallinta**: Foundry Local -asennukset kehitys- ja tuotantoympäristöissä
- **Mallien integrointi**: Työskentele saumattomasti erilaisten malliperheiden kanssa Microsoftilta, Hugging Facelta ja yhteisöltä
- **Sovellusten rakentaminen**: Luo tuotantovalmiita AI-sovelluksia edistyneillä ominaisuuksilla ja optimoinneilla
- **Agenttien kehittäminen**: Toteuta kehittyneitä AI-agentteja perustamis-, päättely- ja työkaluintegraatiolla

### Strateginen ymmärrys
- **Arkkitehtuuripäätökset**: Tee tietoisia valintoja paikallisen ja pilvikäytön välillä
- **Suorituskyvyn optimointi**: Optimoi inferenssin suorituskyky eri laitteistokokoonpanoissa
- **Yritysskaalaus**: Suunnittele sovelluksia, jotka skaalautuvat paikallisista prototyypeistä yrityskäyttöön
- **Tietosuoja ja turvallisuus**: Toteuta tietosuojaa säilyttäviä AI-ratkaisuja paikallisella inferenssillä

### Innovointikyvyt
- **Nopea prototyyppaus**: Rakenna ja testaa AI-sovelluskonsepteja nopeasti kaikkien 10 esimerkkimallin avulla
- **Yhteisöintegraatio**: Hyödynnä avoimen lähdekoodin malleja ja osallistu ekosysteemiin
- **Edistyneet mallit**: Toteuta huippuluokan AI-malleja, kuten RAG, agentit ja työkaluintegraatio
- **Kehyksen hallinta**: Eksperttitason integraatio LangChainin, Semantic Kernelin, Chainlitin ja Electronin kanssa
- **Tuotantokäyttöön ottaminen**: Ota käyttöön skaalautuvia AI-ratkaisuja paikallisista prototyypeistä yritysjärjestelmiin
- **Tulevaisuuden kehitys**: Rakenna sovelluksia, jotka ovat valmiita tuleviin AI-teknologioihin ja malleihin

## Aloittaminen

1. **Ympäristön asennus**: Varmista Windows 11 ja suositeltu laitteisto (katso esivaatimukset)
2. **Asenna Foundry Local**: Seuraa istuntoa 1 täydelliseen asennukseen ja konfigurointiin
3. **Suorita esimerkki 01**: Aloita perus REST API -integraatiolla varmistaaksesi asennuksen
4. **Etene esimerkkien läpi**: Suorita esimerkit 01-10 kattavan osaamisen saavuttamiseksi

## Menestysmittarit

Seuraa edistymistäsi kaikkien 10 kattavan esimerkin läpi:

### Perustaso (Esimerkit 01-03)
- [ ] Asenna ja konfiguroi Foundry Local onnistuneesti
- [ ] Suorita REST API -integraatio (Esimerkki 01)
- [ ] Toteuta OpenAI SDK -yhteensopivuus (Esimerkki 02)
- [ ] Suorita mallien etsintä ja vertailu (Esimerkki 03)

### Sovellustaso (Esimerkit 04-06)
- [ ] Ota käyttöön ja suorita vähintään 4 eri malliperhettä
- [ ] Rakenna toimiva RAG-chat-sovellus (Esimerkki 04)
- [ ] Luo moniagenttien orkestrointijärjestelmä (Esimerkki 05)
- [ ] Toteuta älykäs mallien reititys (Esimerkki 06)

### Edistynyt integraatiotaso (Esimerkit 07-10)
- [ ] Rakenna tuotantovalmiita API-asiakasohjelmia (Esimerkki 07)
- [ ] Kehitä Windows 11 -natiivi chat-sovellus (Esimerkki 08)
- [ ] Toteuta edistynyt moniagenttijärjestelmä (Esimerkki 09)
- [ ] Luo kattava työkalukehys (Esimerkki 10)

### Hallinnan indikaattorit
- [ ] Suorita kaikki 10 esimerkkiä ilman virheitä
- [ ] Mukauta vähintään 3 esimerkkiä tiettyihin käyttötapauksiin
- [ ] Ota käyttöön 2+ esimerkkiä tuotantokaltaisissa ympäristöissä
- [ ] Osallistu parannuksiin tai laajennuksiin esimerkkikoodissa
- [ ] Integroi Foundry Local -mallit henkilökohtaisiin/ammatillisiin projekteihin

## Pikaopas - Kaikki 10 esimerkkiä

### Ympäristön asennus (Vaaditaan kaikille esimerkeille)

```powershell
# 1. Clone and navigate to Module08
cd Module08

# 2. Create Python virtual environment
py -m venv .venv
.\.venv\Scripts\activate

# 3. Install base dependencies
pip install -r requirements.txt

# 4. Install Foundry Local (if not already installed)
winget install Microsoft.FoundryLocal

# 5. Verify Foundry Local installation
foundry --version
foundry model list
```

### Perustason esimerkit (01-06)

**Esimerkki 01: REST Chat Quickstart**
```powershell
# Start Foundry Local service
foundry model run phi-4-mini

# Run REST chat demo
python samples/01/chat_quickstart.py
```

**Esimerkki 02: OpenAI SDK Integration**
```powershell
# Ensure model is running
foundry status

# Run SDK demo
python samples/02/sdk_quickstart.py
```

**Esimerkki 03: Model Discovery & Benchmarking**
```powershell
# Run comprehensive model testing
samples/03/list_and_bench.cmd

# Or run individual components
foundry model list --available
foundry model download qwen2.5-0.5b
foundry model benchmark phi-4-mini
```

**Esimerkki 04: Chainlit RAG Application**
```powershell
# Install Chainlit dependencies
pip install chainlit langchain chromadb

# Start RAG chat application
chainlit run samples/04/app.py -w
# Opens browser at http://localhost:8000
```

**Esimerkki 05: Multi-Agent Orchestration**
```powershell
# Run agent coordinator demo
python -m samples.05.agents.coordinator

# Run specific agent examples
python samples/05/examples/specialists_demo.py
```

**Esimerkki 06: Models-as-Tools Router**
```powershell
# Configure environment
set BASE_URL=http://localhost:8000
set GENERAL_MODEL=phi-4-mini
set CODE_MODEL=qwen2.5-7b-instruct

# Run intelligent router
python samples/06/router.py "Analyze this Python code for performance issues"
```

### Edistyneet integraatioesimerkit (07-10)

**Esimerkki 07: Direct API Client**
```powershell
# Navigate to sample directory
cd samples/07

# Install additional dependencies
pip install -r requirements.txt

# Run basic API examples
python examples/basic_usage.py

# Try streaming responses
python examples/streaming.py

# Test production patterns
python examples/production.py
```

**Esimerkki 08: Windows 11 Chat Application**
```powershell
# Navigate to sample directory
cd samples/08

# Install Node.js dependencies
npm install

# Start Electron application
npm start

# Or build for production
npm run build
```

**Esimerkki 09: Advanced Multi-Agent System**
```powershell
# Navigate to sample directory
cd samples/09

# Install agent system dependencies
pip install -r requirements.txt

# Run basic coordination example
python examples/basic_coordination.py

# Try complex workflow
python examples/complex_workflow.py

# Interactive agent demo
python examples/interactive_demo.py
```

**Esimerkki 10: Foundry Tools Framework**
```powershell
# Navigate to sample directory
cd samples/10

# Install framework dependencies
pip install -r requirements.txt

# Run basic tools demo
python examples/basic_tools.py

# Start REST API server
python examples/rest_api_server.py
# API available at http://localhost:8080

# Try CLI application
python examples/cli_application.py --help

# Launch Jupyter notebook
jupyter notebook examples/jupyter_notebook.ipynb

# Test LangChain integration
python examples/langchain_demo.py
```


Tämä moduuli edustaa huippua edge AI -kehityksessä, yhdistäen Microsoftin yritystason työkalut avoimen lähdekoodin ekosysteemin joustavuuteen ja innovaatioon. Hallitsemalla Foundry Localin kaikki 10 kattavaa esimerkkiä, sijoitut AI-sovelluskehityksen eturintamaan.

**Täydellinen oppimispolku:**
- **Perusta** (Esimerkit 01-03): API-integraatio ja mallien hallinta
- **Sovellukset** (Esimerkit 04-06): RAG, agentit ja älykäs reititys
- **Edistynyt** (Esimerkit 07-10): Tuotantokehykset ja yritysintegraatio

Azure OpenAI -integraatiota varten (Istunto 2), katso yksittäisten esimerkkien README-tiedostot tarvittavista ympäristömuuttujista ja API-versioasetuksista.

---

