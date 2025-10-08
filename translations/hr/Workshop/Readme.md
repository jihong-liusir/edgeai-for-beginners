<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "48d0fb38be925084a6ebd957d4b045e5",
  "translation_date": "2025-10-08T14:12:56+00:00",
  "source_file": "Workshop/Readme.md",
  "language_code": "hr"
}
-->
# EdgeAI za početnike - Radionica

> **Praktični vodič za izgradnju produkcijski spremnih Edge AI aplikacija**
>
> Savladajte lokalno AI implementiranje uz Microsoft Foundry Local, od prve chat interakcije do orkestracije više agenata u 6 progresivnih sesija.

---

## 🎯 Uvod

Dobrodošli na **EdgeAI za početnike radionicu** - vaš praktični vodič za izgradnju inteligentnih aplikacija koje se u potpunosti izvode na lokalnom hardveru. Ova radionica pretvara teorijske koncepte Edge AI-a u stvarne vještine kroz progresivno izazovne vježbe koristeći Microsoft Foundry Local i male jezične modele (SLM).

### Zašto ova radionica?

**Revolucija Edge AI-a je ovdje**

Organizacije diljem svijeta prelaze s AI-a ovisnog o oblaku na edge računalstvo iz tri ključna razloga:

1. **Privatnost i usklađenost** - Obrada osjetljivih podataka lokalno bez prijenosa u oblak (HIPAA, GDPR, financijski propisi)
2. **Performanse** - Eliminacija mrežne latencije (50-500ms lokalno naspram 500-2000ms povratnog puta u oblaku)
3. **Kontrola troškova** - Uklanjanje troškova po tokenu API-ja i skaliranje bez troškova oblaka

**Ali Edge AI je drugačiji**

Pokretanje AI-a na lokalnim uređajima zahtijeva nove vještine:
- Odabir i optimizacija modela za ograničene resurse
- Upravljanje lokalnim uslugama i hardverska akceleracija
- Inženjering upita za manje modele
- Obrasci implementacije za edge uređaje

**Ova radionica pruža te vještine**

U 6 fokusiranih sesija (~3 sata ukupno), napredovat ćete od "Hello World" do implementacije produkcijski spremnih sustava s više agenata - sve lokalno na vašem računalu.

---

## 📚 Ciljevi učenja

Završetkom ove radionice moći ćete:

### Osnovne kompetencije
1. **Implementirati i upravljati lokalnim AI uslugama**
   - Instalirati i konfigurirati Microsoft Foundry Local
   - Odabrati odgovarajuće modele za edge implementaciju
   - Upravljati životnim ciklusom modela (preuzimanje, učitavanje, predmemoriranje)
   - Pratiti korištenje resursa i optimizirati performanse

2. **Izgraditi aplikacije pokretane AI-em**
   - Implementirati OpenAI-kompatibilne chat interakcije lokalno
   - Dizajnirati učinkovite upite za male jezične modele
   - Upravljati streaming odgovorima za bolji korisnički doživljaj
   - Integrirati lokalne modele u postojeće aplikacije

3. **Kreirati RAG (Retrieval Augmented Generation) sustave**
   - Izgraditi semantičko pretraživanje pomoću ugrađenih podataka
   - Temeljiti odgovore LLM-a na specifičnom znanju iz domene
   - Procijeniti kvalitetu RAG-a koristeći industrijske standarde
   - Skalirati od prototipa do produkcije

4. **Optimizirati performanse modela**
   - Provoditi benchmark testove za više modela
   - Mjeriti latenciju, propusnost i vrijeme prvog tokena
   - Odabrati optimalne modele na temelju kompromisa brzine/kvalitete
   - Usporediti SLM i LLM u stvarnim scenarijima

5. **Orkestrirati sustave s više agenata**
   - Dizajnirati specijalizirane agente za različite zadatke
   - Implementirati memoriju i upravljanje kontekstom agenata
   - Koordinirati agente u složenim radnim procesima
   - Pametno usmjeravati zahtjeve između više modela

6. **Implementirati produkcijski spremna rješenja**
   - Implementirati rukovanje greškama i logiku ponovnog pokušaja
   - Pratiti korištenje tokena i sistemske resurse
   - Izgraditi skalabilne arhitekture koristeći obrasce modela kao alata
   - Planirati migracijske putove od edge-a do hibridnih rješenja (edge + oblak)

---

## 🎓 Ishodi učenja

### Što ćete izgraditi

Do kraja ove radionice, izradit ćete:

| Sesija | Rezultat | Demonstrirane vještine |
|--------|----------|-------------------------|
| **1** | Chat aplikaciju sa streamingom | Postavljanje usluge, osnovne interakcije, streaming UX |
| **2** | RAG sustav s evaluacijom | Ugrađeni podaci, semantičko pretraživanje, metričke procjene kvalitete |
| **3** | Suite za benchmark testiranje više modela | Mjerenje performansi, usporedba modela |
| **4** | Usporednik SLM-a i LLM-a | Analiza kompromisa, strategije optimizacije |
| **5** | Orkestrator s više agenata | Dizajn agenata, upravljanje memorijom, koordinacija |
| **6** | Sustav za inteligentno usmjeravanje | Detekcija namjere, odabir modela, skalabilnost |

### Matrica kompetencija

| Razina vještine | Sesija 1-2 | Sesija 3-4 | Sesija 5-6 |
|-----------------|-----------|------------|------------|
| **Početnik** | ✅ Postavljanje i osnove | ⚠️ Izazovno | ❌ Previše napredno |
| **Srednji** | ✅ Brzi pregled | ✅ Ključne lekcije | ⚠️ Ciljevi za napredak |
| **Napredni** | ✅ Lako prolazi | ✅ Usavršavanje | ✅ Obrasci za produkciju |

### Vještine spremne za karijeru

**Nakon ove radionice, bit ćete spremni:**

✅ **Izgraditi aplikacije usmjerene na privatnost**
- Zdravstvene aplikacije koje lokalno obrađuju PHI/PII
- Financijske usluge s zahtjevima za usklađenost
- Vladine sustave s potrebama za suverenitetom podataka

✅ **Optimizirati za edge okruženja**
- IoT uređaje s ograničenim resursima
- Mobilne aplikacije koje rade offline
- Sustave u stvarnom vremenu s niskom latencijom

✅ **Dizajnirati inteligentne arhitekture**
- Sustave s više agenata za složene radne procese
- Hibridne edge-cloud implementacije
- AI infrastrukturu optimiziranu za troškove

✅ **Voditi Edge AI inicijative**
- Procijeniti izvedivost Edge AI-a za projekte
- Odabrati odgovarajuće modele i okvire
- Dizajnirati skalabilna lokalna AI rješenja

---

## 🗺️ Struktura radionice

### Pregled sesija (6 sesija × 30 minuta = 3 sata)

| Sesija | Tema | Fokus | Trajanje |
|--------|------|-------|----------|
| **1** | Početak s Foundry Local | Instalacija, validacija, prve interakcije | 30 min |
| **2** | Izgradnja AI rješenja s RAG-om | Inženjering upita, ugrađeni podaci, evaluacija | 30 min |
| **3** | Open Source modeli | Otkrivanje modela, benchmark testiranje, odabir | 30 min |
| **4** | Najnoviji modeli | SLM vs LLM, optimizacija, okviri | 30 min |
| **5** | Agenti pokretani AI-em | Dizajn agenata, orkestracija, memorija | 30 min |
| **6** | Modeli kao alati | Usmjeravanje, povezivanje, strategije skaliranja | 30 min |

---

## 🚀 Brzi početak

### Preduvjeti

**Sistemski zahtjevi:**
- **OS**: Windows 10/11, macOS 11+ ili Linux (Ubuntu 20.04+)
- **RAM**: Minimalno 8GB, preporučeno 16GB+
- **Prostor**: 10GB+ slobodnog prostora za modele
- **CPU**: Moderni procesor s podrškom za AVX2
- **GPU** (opcionalno): CUDA-kompatibilan ili Qualcomm NPU za ubrzanje

**Softverski zahtjevi:**
- **Python 3.8+** ([Preuzmi](https://www.python.org/downloads/))
- **Microsoft Foundry Local** ([Vodič za instalaciju](../../../Workshop))
- **Git** ([Preuzmi](https://git-scm.com/downloads))
- **Visual Studio Code** (preporučeno) ([Preuzmi](https://code.visualstudio.com/))

### Postavljanje u 3 koraka

#### 1. Instalirajte Foundry Local

**Windows:**
```powershell
winget install Microsoft.FoundryLocal
```

**macOS:**
```bash
brew tap microsoft/foundrylocal
brew install foundrylocal
```

**Provjera instalacije:**
```bash
foundry --version
foundry service status
```

#### 2. Klonirajte repozitorij i instalirajte ovisnosti

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

#### 3. Pokrenite svoj prvi primjer

```bash
# Start Foundry Local and load a model
foundry model run phi-4-mini

# Run the chat bootstrap sample
cd samples/session01
python chat_bootstrap.py "What is edge AI?"
```

**✅ Uspješno!** Trebali biste vidjeti streaming odgovor o Edge AI-u.

---

## 📦 Resursi radionice

### Python primjeri

Progresivni praktični primjeri koji demonstriraju svaki koncept:

| Sesija | Primjer | Opis | Vrijeme izvođenja |
|--------|---------|------|-------------------|
| 1 | [`chat_bootstrap.py`](../../../Workshop/samples/session01/chat_bootstrap.py) | Osnovni i streaming chat | ~30s |
| 2 | [`rag_pipeline.py`](../../../Workshop/samples/session02/rag_pipeline.py) | RAG s ugrađenim podacima | ~45s |
| 2 | [`rag_eval_ragas.py`](../../../Workshop/samples/session02/rag_eval_ragas.py) | Evaluacija kvalitete RAG-a | ~60s |
| 3 | [`benchmark_oss_models.py`](../../../Workshop/samples/session03/benchmark_oss_models.py) | Benchmark testiranje više modela | ~2-3m |
| 4 | [`model_compare.py`](../../../Workshop/samples/session04/model_compare.py) | Usporedba SLM-a i LLM-a | ~45s |
| 5 | [`agents_orchestrator.py`](../../../Workshop/samples/session05/agents_orchestrator.py) | Sustav s više agenata | ~60s |
| 6 | [`models_router.py`](../../../Workshop/samples/session06/models_router.py) | Usmjeravanje temeljeno na namjeri | ~45s |
| 6 | [`models_pipeline.py`](../../../Workshop/samples/session06/models_pipeline.py) | Višekorakna pipeline | ~60s |

### Jupyter bilježnice

Interaktivno istraživanje s objašnjenjima i vizualizacijama:

| Sesija | Bilježnica | Opis | Težina |
|--------|------------|------|--------|
| 1 | [`session01_chat_bootstrap.ipynb`](./notebooks/session01_chat_bootstrap.ipynb) | Osnove chata i streaming | ⭐ Početnik |
| 2 | [`session02_rag_pipeline.ipynb`](./notebooks/session02_rag_pipeline.ipynb) | Izgradnja RAG sustava | ⭐⭐ Srednji |
| 2 | [`session02_rag_eval_ragas.ipynb`](./notebooks/session02_rag_eval_ragas.ipynb) | Evaluacija kvalitete RAG-a | ⭐⭐ Srednji |
| 3 | [`session03_benchmark_oss_models.ipynb`](./notebooks/session03_benchmark_oss_models.ipynb) | Benchmark testiranje modela | ⭐⭐ Srednji |
| 4 | [`session04_model_compare.ipynb`](./notebooks/session04_model_compare.ipynb) | Usporedba modela | ⭐⭐ Srednji |
| 5 | [`session05_agents_orchestrator.ipynb`](./notebooks/session05_agents_orchestrator.ipynb) | Orkestracija agenata | ⭐⭐⭐ Napredni |
| 6 | [`session06_models_router.ipynb`](./notebooks/session06_models_router.ipynb) | Usmjeravanje temeljeno na namjeri | ⭐⭐⭐ Napredni |
| 6 | [`session06_models_pipeline.ipynb`](./notebooks/session06_models_pipeline.ipynb) | Orkestracija pipeline-a | ⭐⭐⭐ Napredni |

### Dokumentacija

Sveobuhvatni vodiči i reference:

| Dokument | Opis | Koristite kada |
|----------|------|----------------|
| [QUICK_START.md](./QUICK_START.md) | Vodič za brzo postavljanje | Početak od nule |
| [QUICK_REFERENCE.md](./QUICK_REFERENCE.md) | Brzi pregled naredbi i API-ja | Trebate brze odgovore |
| [FOUNDRY_SDK_QUICKREF.md](./FOUNDRY_SDK_QUICKREF.md) | Obrasci i primjeri SDK-a | Pisanje koda |
| [ENV_CONFIGURATION.md](./ENV_CONFIGURATION.md) | Vodič za konfiguraciju varijabli okruženja | Konfiguriranje primjera |
| [SAMPLES_UPDATE_SUMMARY.md](./SAMPLES_UPDATE_SUMMARY.md) | Najnovija poboljšanja primjera | Razumijevanje promjena |
| [SDK_MIGRATION_NOTES.md](./SDK_MIGRATION_NOTES.md) | Vodič za migraciju | Nadogradnja koda |
| [notebooks/TROUBLESHOOTING.md](./notebooks/TROUBLESHOOTING.md) | Uobičajeni problemi i rješenja | Rješavanje problema |

---

## 🎓 Preporuke za put učenja

### Za početnike (3-4 sata)
1. ✅ Sesija 1: Početak (fokus na postavljanje i osnovni chat)
2. ✅ Sesija 2: Osnove RAG-a (preskočite evaluaciju za početak)
3. ✅ Sesija 3: Jednostavno benchmark testiranje (samo 2 modela)
4. ⏭️ Preskočite sesije 4-6 za sada
5. 🔄 Vratite se na sesije 4-6 nakon izrade prve aplikacije

### Za srednje razvijene programere (3 sata)
1. ⚡ Sesija 1: Brza validacija postavljanja
2. ✅ Sesija 2: Kompletan RAG pipeline s evaluacijom
3. ✅ Sesija 3: Kompletan suite za benchmark testiranje
4. ✅ Sesija 4: Optimizacija modela
5. ✅ Sesije 5-6: Fokus na obrasce arhitekture

### Za napredne praktičare (2-3 sata)
1. ⚡ Sesije 1-3: Brzi pregled i validacija
2. ✅ Sesija 4: Dubinska analiza optimizacije
3. ✅ Sesija 5: Arhitektura s više agenata
4. ✅ Sesija 6: Obrasci za produkciju i skaliranje
5. 🚀 Proširenje: Izgradnja prilagođene logike usmjeravanja i hibridnih implementacija

---

## Paket sesija radionice (Fokusirane laboratorijske vježbe od 30 minuta)

Ako slijedite skraćeni format radionice od 6 sesija, koristite ove posvećene vodiče (svaki se povezuje i nadopunjuje šire module dokumentacije iznad):

| Sesija radionice | Vodič | Glavni fokus |
|------------------|-------|-------------|
| 1 | [Session01-GettingStartedFoundryLocal](./Session01-GettingStartedFoundryLocal.md) | Instalacija, validacija, pokretanje phi & GPT-OSS-20B, ubrzanje |
| 2 | [Session02-BuildAISolutionsRAG](./Session02-BuildAISolutionsRAG.md) | Inženjering upita, RAG obrasci, CSV i dokumentacija, migracija |
| 3 | [Session03-OpenSourceModels](./Session03-OpenSourceModels.md) | Integracija Hugging Face-a, benchmark testiranje, odabir modela |
| 4 | [Session04-CuttingEdgeModels](./Session04-CuttingEdgeModels.md) | SLM vs LLM, WebGPU, Chainlit RAG, ONNX ubrzanje |
| 5 | [Session05-AIPoweredAgents](./Session05-AIPoweredAgents.md) | Uloge agenata, memorija, alati, orkestracija |
| 6 | [Session06-ModelsAsTools](./Session06-ModelsAsTools.md) | Usmjeravanje, povezivanje, skaliranje prema Azure-u |
Svaka datoteka sesije uključuje: sažetak, ciljeve učenja, tijek demonstracije od 30 minuta, početni projekt, kontrolni popis za validaciju, rješavanje problema i reference na službeni Foundry Local Python SDK.

### Primjeri skripti

Instalacija ovisnosti za radionicu (Windows):

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

Ako pokrećete Foundry Local uslugu na drugom (Windows) računalu ili virtualnom stroju s macOS-a, izvezite krajnju točku:

```bash
export FOUNDRY_LOCAL_ENDPOINT=http://<windows-host>:5273/v1
```

| Sesija | Skripta(e) | Opis |
|--------|------------|------|
| 1 | `samples/session01/chat_bootstrap.py` | Pokretanje usluge i streaming razgovora |
| 2 | `samples/session02/rag_pipeline.py` | Minimalni RAG (memorijski ugrađeni podaci) |
|   | `samples/session02/rag_eval_ragas.py` | Evaluacija RAG-a s metrikama ragas |
| 3 | `samples/session03/benchmark_oss_models.py` | Benchmarking latencije i propusnosti za više modela |
| 4 | `samples/session04/model_compare.py` | Usporedba SLM-a i LLM-a (latencija i uzorci izlaza) |
| 5 | `samples/session05/agents_orchestrator.py` | Istraživački → urednički proces s dva agenta |
| 6 | `samples/session06/models_router.py` | Demo usmjeravanja temeljenog na namjeri |
|   | `samples/session06/models_pipeline.py` | Višekorak: planiranje, izvršenje, poboljšanje |

### Varijable okruženja (zajedničke za sve primjere)

| Varijabla | Namjena | Primjer |
|-----------|---------|---------|
| `FOUNDRY_LOCAL_ALIAS` | Zadani alias za osnovne primjere s jednim modelom | `phi-4-mini` |
| `SLM_ALIAS` / `LLM_ALIAS` | Eksplicitni SLM naspram većeg modela za usporedbu | `phi-4-mini` / `gpt-oss-20b` |
| `BENCH_MODELS` | Popis aliasa za benchmarking, odvojen zarezima | `qwen2.5-0.5b,gemma-2-2b,mistral-7b` |
| `BENCH_ROUNDS` | Broj ponavljanja benchmarka po modelu | `3` |
| `BENCH_PROMPT` | Upit korišten u benchmarkingu | `Objasnite ukratko generaciju obogaćenu pretraživanjem.` |
| `EMBED_MODEL` | Model za ugrađivanje rečenica | `sentence-transformers/all-MiniLM-L6-v2` |
| `RAG_QUESTION` | Zamjena testnog upita za RAG pipeline | `Zašto koristiti RAG s lokalnom inferencijom?` |
| `AGENT_QUESTION` | Zamjena upita za pipeline agenata | `Objasnite zašto je edge AI važan za usklađenost.` |
| `AGENT_MODEL_PRIMARY` | Alias modela za istraživačkog agenta | `phi-4-mini` |
| `AGENT_MODEL_EDITOR` | Alias modela za uredničkog agenta (može se razlikovati) | `gpt-oss-20b` |
| `SHOW_USAGE` | Kada je `1`, ispisuje korištenje tokena po završetku | `1` |
| `RETRY_ON_FAIL` | Kada je `1`, ponovno pokušava na prolaznim greškama u razgovoru | `1` |
| `RETRY_BACKOFF` | Sekunde čekanja prije ponovnog pokušaja | `1.0` |

Ako varijabla nije postavljena, skripte se oslanjaju na razumne zadane vrijednosti. Za demonstracije s jednim modelom obično je potrebna samo `FOUNDRY_LOCAL_ALIAS`.

### Pomoćni modul

Svi primjeri sada dijele pomoćnu skriptu `samples/workshop_utils.py` koja omogućuje:

* Stvaranje predmemoriranog `FoundryLocalManager` + OpenAI klijenta
* Pomoćnu funkciju `chat_once()` s opcionalnim ponovnim pokušajem + ispisom korištenja
* Jednostavno izvješćivanje o korištenju tokena (omogućeno putem `SHOW_USAGE=1`)

Ovo smanjuje dupliciranje i ističe najbolje prakse za učinkovitu lokalnu orkestraciju modela.

## Opcionalna poboljšanja (među sesijama)

| Tema | Poboljšanje | Sesije | Okruženje / Prekidač |
|------|-------------|--------|----------------------|
| Determinizam | Fiksna temperatura + stabilni setovi upita | 1–6 | Postavite `temperature=0`, `top_p=1` |
| Vidljivost korištenja tokena | Dosljedno podučavanje o troškovima/učinkovitosti | 1–6 | `SHOW_USAGE=1` |
| Streaming prvog tokena | Metrika percipirane latencije | 1,3,4,6 | `BENCH_STREAM=1` (benchmark) |
| Otpornost na greške | Rješava prolazne greške pri hladnom pokretanju | Sve | `RETRY_ON_FAIL=1` + `RETRY_BACKOFF` |
| Više-modelski agenti | Specijalizacija uloga | 5 | `AGENT_MODEL_PRIMARY`, `AGENT_MODEL_EDITOR` |
| Adaptivno usmjeravanje | Namjera + heuristika troškova | 6 | Proširite usmjerivač s logikom eskalacije |
| Vektorska memorija | Dugoročno semantičko pamćenje | 2,5,6 | Integrirajte FAISS/Chroma indeks ugrađivanja |
| Izvoz tragova | Revizija i evaluacija | 2,5,6 | Dodajte JSON linije po koraku |
| Kvalitativne metrike | Praćenje kvalitete | 3–6 | Sekundarni upiti za ocjenjivanje |
| Brzi testovi | Brza validacija prije radionice | Sve | `python Workshop/tests/smoke.py` |

### Deterministički brzi početak

```powershell
set FOUNDRY_LOCAL_ALIAS=phi-4-mini
set SHOW_USAGE=1
python Workshop\tests\smoke.py
```

Očekujte stabilan broj tokena za ponovljene identične ulaze.

### Evaluacija RAG-a (Sesija 2)

Koristite `rag_eval_ragas.py` za izračun relevantnosti odgovora, vjerodostojnosti i preciznosti konteksta na malom sintetičkom skupu podataka:

```powershell
python samples/session02/rag_eval_ragas.py
```

Proširite dodavanjem većeg JSONL-a s pitanjima, kontekstima i istinitim podacima, zatim konvertirajte u Hugging Face `Dataset`.

## Dodatak za točnost CLI naredbi

Radionica namjerno koristi samo trenutno dokumentirane/stabilne Foundry Local CLI naredbe.

### Referencirane stabilne naredbe

| Kategorija | Naredba | Namjena |
|------------|---------|---------|
| Osnovno | `foundry --version` | Prikazuje instaliranu verziju |
| Osnovno | `foundry init` | Inicijalizira konfiguraciju |
| Usluga | `foundry service start` | Pokreće lokalnu uslugu (ako nije automatski) |
| Usluga | `foundry status` | Prikazuje status usluge |
| Modeli | `foundry model list` | Popis kataloga/dostupnih modela |
| Modeli | `foundry model download <alias>` | Preuzima težine modela u predmemoriju |
| Modeli | `foundry model run <alias>` | Pokreće (učitava) model lokalno; kombinirajte s `--prompt` za jednokratni upit |
| Modeli | `foundry model unload <alias>` / `foundry model stop <alias>` | Uklanja model iz memorije (ako je podržano) |
| Predmemorija | `foundry cache list` | Popis predmemoriranih (preuzetih) modela |
| Sustav | `foundry system info` | Snimka hardverskih i akceleracijskih mogućnosti |
| Sustav | `foundry system gpu-info` | Dijagnostičke informacije o GPU-u |
| Konfiguracija | `foundry config list` | Prikazuje trenutne vrijednosti konfiguracije |
| Konfiguracija | `foundry config set <key> <value>` | Ažurira konfiguraciju |

### Jednokratni uzorak upita

Umjesto zastarjele naredbe `model chat`, koristite:

```powershell
foundry model run <alias> --prompt "Your question here"
```

Ovo izvršava jedan ciklus upita/odgovora, zatim izlazi.

### Uklonjeni/izbjegnuti uzorci

| Zastarjelo/Nedokumentirano | Zamjena/Preporuka |
|----------------------------|-------------------|
| `foundry model chat <model> "..."` | `foundry model run <model> --prompt "..."` |
| `foundry model list --running` | Koristite obični `foundry model list` + nedavne aktivnosti/logove |
| `foundry model list --cached` | `foundry cache list` |
| `foundry model stats <model>` | Koristite Python skriptu za benchmarking + OS alate (Task Manager / `nvidia-smi`) |
| `foundry model benchmark ...` | `samples/session03/benchmark_oss_models.py` |

### Benchmarking i telemetrija

- Latencija, p95, tokeni/sekunda: `samples/session03/benchmark_oss_models.py`
- Latencija prvog tokena (streaming): postavite `BENCH_STREAM=1`
- Korištenje resursa: OS monitori (Task Manager, Activity Monitor, `nvidia-smi`) + `foundry system info`.

Kako nove CLI telemetrijske naredbe postanu stabilne, mogu se integrirati uz minimalne izmjene u sesijskim datotekama.

### Automatska provjera sintakse

Automatski linter sprječava ponovno uvođenje zastarjelih CLI uzoraka unutar blokova koda u markdown datotekama:

Skripta: `Workshop/scripts/lint_markdown_cli.py`

Zastarjeli uzorci blokirani su unutar blokova koda.

Preporučene zamjene:
| Zastarjelo | Zamjena |
|-----------|---------|
| `foundry model chat <a> "..."` | `foundry model run <a> --prompt "..."` |
| `model list --running` | `model list` |
| `model list --cached` | `cache list` |
| `model stats` | Skripta za benchmarking + alati sustava |
| `model benchmark` | `samples/session03/benchmark_oss_models.py` |
| `model list --available` | `model list` |

Pokrenite lokalno:
```powershell
python Workshop\scripts\lint_markdown_cli.py --verbose
```

GitHub Action: `.github/workflows/markdown-cli-lint.yml` pokreće se na svakom pushu i PR-u.

Opcionalni pre-commit hook:
```bash
echo "python Workshop/scripts/lint_markdown_cli.py" > .git/hooks/pre-commit
chmod +x .git/hooks/pre-commit
```

## Brza tablica migracije CLI → SDK

| Zadatak | CLI Jednolinijska naredba | SDK (Python) ekvivalent | Napomene |
|---------|---------------------------|-------------------------|----------|
| Pokreni model jednom (upit) | `foundry model run phi-4-mini --prompt "Hello"` | `manager=FoundryLocalManager("phi-4-mini"); client=OpenAI(base_url=manager.endpoint, api_key=manager.api_key or "not-needed"); client.chat.completions.create(model=manager.get_model_info("phi-4-mini").id, messages=[{"role":"user","content":"Hello"}])` | SDK automatski pokreće uslugu i predmemoriju |
| Preuzmi (predmemoriraj) model | `foundry model download qwen2.5-0.5b` | `FoundryLocalManager("qwen2.5-0.5b")  # pokreće preuzimanje/učitavanje` | Manager odabire najbolju varijantu ako alias mapira na više verzija |
| Popis kataloga | `foundry model list` | `# koristite manager za svaki alias ili održavajte poznati popis` | CLI agregira; SDK trenutno po aliasu |
| Popis predmemoriranih modela | `foundry cache list` | `manager.list_cached_models()` | Nakon inicijalizacije managera (bilo koji alias) |
| Omogući GPU akceleraciju | `foundry config set compute.onnx.enable_gpu true` | `# CLI akcija; SDK pretpostavlja da je konfiguracija već primijenjena` | Konfiguracija je vanjski učinak |
| Dohvati URL krajnje točke | (implicitno) | `manager.endpoint` | Koristi se za stvaranje OpenAI-kompatibilnog klijenta |
| Zagrij model | `foundry model run <alias>` zatim prvi upit | `chat_once(alias, messages=[...])` (pomoćna funkcija) | Pomoćne funkcije rješavaju početnu latenciju hladnog pokretanja |
| Mjeri latenciju | `python benchmark_oss_models.py` | `import benchmark_oss_models` (ili nova skripta za izvoz) | Preferirajte skriptu za dosljedne metrike |
| Zaustavi/ukloni model | `foundry model unload <alias>` | (Nije izloženo – ponovno pokrenite uslugu/proces) | Obično nije potrebno za tijek radionice |
| Dohvati korištenje tokena | (pogledajte izlaz) | `resp.usage.total_tokens` | Dostupno ako backend vraća objekt korištenja |

## Izvoz benchmarka u Markdown

Koristite skriptu `Workshop/scripts/export_benchmark_markdown.py` za pokretanje svježeg benchmarka (ista logika kao `samples/session03/benchmark_oss_models.py`) i generiranje GitHub-prijateljske Markdown tablice plus sirovog JSON-a.

### Primjer

```powershell
python Workshop\scripts\export_benchmark_markdown.py --models "qwen2.5-0.5b,gemma-2-2b,mistral-7b" --prompt "Explain retrieval augmented generation briefly." --rounds 3 --output benchmark_report.md
```

Generirane datoteke:
| Datoteka | Sadržaj |
|----------|---------|
| `benchmark_report.md` | Markdown tablica + interpretacijski savjeti |
| `benchmark_report.json` | Sirovi niz metrika (za usporedbu/trend praćenje) |

Postavite `BENCH_STREAM=1` u okruženju za uključivanje latencije prvog tokena ako je podržano.

---

**Izjava o odricanju odgovornosti**:  
Ovaj dokument je preveden pomoću AI usluge za prevođenje [Co-op Translator](https://github.com/Azure/co-op-translator). Iako nastojimo osigurati točnost, imajte na umu da automatski prijevodi mogu sadržavati pogreške ili netočnosti. Izvorni dokument na izvornom jeziku treba smatrati autoritativnim izvorom. Za ključne informacije preporučuje se profesionalni prijevod od strane čovjeka. Ne preuzimamo odgovornost za nesporazume ili pogrešna tumačenja koja mogu proizaći iz korištenja ovog prijevoda.