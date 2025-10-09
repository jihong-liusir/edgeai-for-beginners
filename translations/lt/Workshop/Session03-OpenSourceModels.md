<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "d6ad6c8b4a0e3ecef3afb86a6f578e1c",
  "translation_date": "2025-10-09T21:32:01+00:00",
  "source_file": "Workshop/Session03-OpenSourceModels.md",
  "language_code": "lt"
}
-->
# Sesija 3: Atvirojo kodo modeliai Foundry Local

## Santrauka

Sužinokite, kaip integruoti Hugging Face ir kitus atvirojo kodo modelius į Foundry Local. Išmokite modelių atrankos strategijas, bendruomenės indėlio darbo eigas, našumo palyginimo metodiką ir kaip praplėsti Foundry naudojant pasirinktinius modelių registravimus. Ši sesija atitinka savaitinius „Modelių pirmadienio“ tyrinėjimo temas ir suteikia galimybę įvertinti bei pritaikyti atvirojo kodo modelius vietoje prieš juos mastelį perkeliant į Azure.

## Mokymosi tikslai

Sesijos pabaigoje galėsite:

- **Atrasti ir įvertinti**: Identifikuoti kandidatus modelius (mistral, gemma, qwen, deepseek) naudojant kokybės ir resursų kompromisus.
- **Įkelti ir paleisti**: Naudoti Foundry Local CLI atsisiųsti, talpinti ir paleisti bendruomenės modelius.
- **Testuoti našumą**: Taikyti nuoseklius vėlinimo + žetonų pralaidumo + kokybės vertinimo kriterijus.
- **Praplėsti**: Registruoti arba pritaikyti pasirinktą modelio apvalkalą, laikantis SDK suderinamų šablonų.
- **Palyginti**: Sukurti struktūrizuotus palyginimus SLM ir vidutinio dydžio LLM atrankos sprendimams.

## Reikalavimai

- Užbaigtos 1 ir 2 sesijos
- Python aplinka su įdiegtu `foundry-local-sdk`
- Bent 15 GB laisvos vietos diske keliems modelių talpykloms
- Pasirinktinai: Įjungtas GPU/WebGPU pagreitinimas (`foundry config list`)

### Greitas startas įvairiose platformose

Windows PowerShell:
```powershell
py -m venv .venv
 .\.venv\Scripts\Activate.ps1
pip install --upgrade pip
pip install foundry-local-sdk openai numpy
```

macOS / Linux:
```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install foundry-local-sdk openai numpy
```

Kai testuojate našumą iš macOS prieš Windows host paslaugą, nustatykite:
```bash
export FOUNDRY_LOCAL_ENDPOINT=http://<windows-host>:5273/v1
```


## Demonstracijos eiga (30 min)

### 1. Įkelkite Hugging Face modelius per CLI (8 min)

```powershell
# List catalog entries (filter manually if needed)
foundry model list

# Download a set of comparison targets
foundry model download mistral-7b
foundry model download gemma-2-2b
foundry model download qwen2.5-0.5b

# Verify cache
foundry cache list
```


### 2. Paleiskite ir greitai patikrinkite (5 min)

```powershell
foundry model run qwen2.5-0.5b
foundry model run qwen2.5-0.5b --prompt "List three benefits of local inference."

foundry model run mistral-7b
foundry model run mistral-7b --prompt "Explain retrieval augmented generation in one paragraph."
```


### 3. Testavimo scenarijus (8 min)

Sukurkite `samples/03-oss-models/benchmark_models.py`:

```python
#!/usr/bin/env python3
"""Lightweight benchmarking for open-source models in Foundry Local.
Metrics: first token latency, total latency, tokens/sec (approx via usage), model size indicator.
Reference SDK: https://github.com/microsoft/Foundry-Local/tree/main/sdk/python
"""

import time, statistics, json
from openai import OpenAI

MODELS = [
    "qwen2.5-0.5b",
    "gemma-2-2b",
    "mistral-7b",
]

PROMPT = "Explain the principle of retrieval augmented generation in 2 sentences."
ROUNDS = 3

client = OpenAI(base_url="http://localhost:5273/v1", api_key="not-needed")

def run_round(model: str):
    start = time.time()
    resp = client.chat.completions.create(
        model=model,
        messages=[{"role": "user", "content": PROMPT}],
        max_tokens=150,
        temperature=0.2,
        stream=False
    )
    end = time.time()
    usage = getattr(resp, "usage", None)
    total_tokens = usage.total_tokens if usage else None
    return {
        "latency_sec": end - start,
        "total_tokens": total_tokens,
        "tokens_per_sec": (total_tokens / (end - start)) if (total_tokens and (end-start) > 0) else None,
        "sample_response": resp.choices[0].message.content[:160].replace("\n", " ")
    }

def benchmark_model(model: str):
    results = [run_round(model) for _ in range(ROUNDS)]
    latencies = [r["latency_sec"] for r in results]
    tps = [r["tokens_per_sec"] for r in results if r["tokens_per_sec"]]
    return {
        "model": model,
        "rounds": ROUNDS,
        "latency_avg": statistics.mean(latencies),
        "latency_p95": statistics.quantiles(latencies, n=20)[-1] if len(latencies) > 1 else latencies[0],
        "tokens_per_sec_avg": statistics.mean(tps) if tps else None,
        "sample": results[-1]["sample_response"]
    }

def main():
    summary = [benchmark_model(m) for m in MODELS]
    print(json.dumps(summary, indent=2))
    print("\nInterpretation Tips:\n- latency_avg: lower better\n- tokens_per_sec_avg: higher better\n- Compare quality manually on sample outputs.")

if __name__ == "__main__":
    main()
```

Paleiskite:

```powershell
python samples/03-oss-models/benchmark_models.py
```


### 4. Palyginkite našumą (5 min)

Diskutuokite apie kompromisus: įkėlimo laiką, atminties naudojimą (stebėkite Task Manager / `nvidia-smi` / OS resursų monitorių), išvesties kokybę ir greitį. Naudokite Python testavimo scenarijų (3 sesija) vėlinimo ir pralaidumo matavimui; pakartokite įjungus GPU pagreitinimą.

### 5. Pradinis projektas (4 min)

Sukurkite modelių palyginimo ataskaitų generatorių (praplėskite testavimo scenarijų su markdown eksportu).

## Pradinis projektas: Praplėskite `03-huggingface-models`

Patobulinkite esamą pavyzdį:

1. Pridėkite testavimo rezultatų agregavimą + CSV/Markdown išvestį.
2. Įgyvendinkite paprastą kokybinį vertinimą (pateikčių porų rinkinys + rankinio anotavimo failo šablonas).
3. Įtraukite JSON konfigūraciją (`models.json`) modelių sąrašo ir pateikčių rinkinio prijungimui.

## Patikrinimo sąrašas

```powershell
foundry cache list
foundry model run qwen2.5-0.5b
curl http://localhost:5273/v1/models
```

Visi tiksliniai modeliai turėtų pasirodyti ir atsakyti į testinį pokalbio užklausą.

## Pavyzdinė situacija ir dirbtuvių susiejimas

| Dirbtuvių scenarijus | Situacija | Tikslas | Pateikčių / duomenų šaltinis |
|----------------------|-----------|---------|-----------------------------|
| `samples/session03/benchmark_oss_models.py` / `notebooks/session03_benchmark_oss_models.ipynb` | Edge platformos komanda, renkantis numatytąjį SLM įterptam santraukų generatoriui | Sukurti vėlinimo + p95 + žetonų per sekundę palyginimą tarp kandidatų modelių | Vidinis `PROMPT` kintamasis + aplinkos `BENCH_MODELS` sąrašas |

### Situacijos pasakojimas

Produktų inžinerijos komanda turi pasirinkti numatytąjį lengvą santraukų modelį neprisijungus veikiančiai susitikimų užrašų funkcijai. Jie vykdo kontroliuojamus deterministinius testus (temperature=0) pagal fiksuotą pateikčių rinkinį (žr. pavyzdį žemiau) ir renka vėlinimo + pralaidumo metrikas su GPU pagreitinimu ir be jo.

### Pavyzdinis pateikčių rinkinys JSON (plečiamas)

```json
[
    "Explain the principle of retrieval augmented generation in 2 sentences.",
    "List 3 privacy benefits of local inference.",
    "Summarize why model size impacts latency on consumer hardware.",
    "Provide two scenarios where an SLM is preferable to an LLM."
]
```

Kartokite kiekvieną pateiktį kiekvienam modeliui, fiksuokite vėlinimą kiekvienai pateikčiai, kad gautumėte pasiskirstymo metrikas ir aptiktumėte anomalijas.

## Modelių atrankos struktūra

| Dimensija | Metrika | Kodėl tai svarbu |
|-----------|---------|------------------|
| Vėlinimas | vidurkis / p95 | Vartotojo patirties nuoseklumas |
| Pralaidumas | žetonai per sekundę | Grupės ir srautinio mastelio galimybės |
| Atmintis | rezidentinis dydis | Įrenginio tinkamumas ir konkurencija |
| Kokybė | pateikčių rubrika | Užduoties tinkamumas |
| Pėdsakas | disko talpykla | Platinimas ir atnaujinimai |
| Licencija | naudojimo leidimas | Komercinis suderinamumas |

## Praplėtimas su pasirinktiniu modeliu

Aukšto lygio šablonas (pseudo):

```python
# pseudo_adapter.py (conceptual)
class CustomModelAdapter:
    def load(self, weights_path: str): ...
    def generate(self, prompt: str, **params) -> str: ...

# Register with local routing (future extensibility point)
```

Konsultuokitės su oficialiu repozitoriumi dėl besikeičiančių adapterio sąsajų:
https://github.com/microsoft/Foundry-Local/tree/main/sdk/python

## Trikčių šalinimas

| Problema | Priežastis | Sprendimas |
|----------|------------|------------|
| OOM su mistral-7b | Nepakankama RAM/GPU | Sustabdykite kitus modelius; bandykite mažesnį variantą |
| Lėtas pirmasis atsakas | Šaltas įkrovimas | Palaikykite aktyvumą su periodine lengva pateiktimi |
| Atsisiuntimas stringa | Tinklo nestabilumas | Bandykite iš naujo; iš anksto atsisiųskite ne piko metu |

## Nuorodos

- Foundry Local SDK: https://github.com/microsoft/Foundry-Local/tree/main/sdk/python
- Modelių pirmadieniai: https://aka.ms/model-mondays
- Hugging Face modelių atranka: https://huggingface.co/models

---

**Sesijos trukmė**: 30 min (+ pasirinktinis giluminis tyrimas)  
**Sudėtingumas**: Vidutinis

### Pasirinktiniai patobulinimai

| Patobulinimas | Privalumas | Kaip |
|---------------|------------|------|
| Srautinio pirmojo žetono vėlinimas | Matuoja suvokiamą atsakymo greitį | Paleiskite testą su `BENCH_STREAM=1` (patobulintas scenarijus `Workshop/samples/session03`) |
| Deterministinis režimas | Stabilūs regresijos palyginimai | `temperature=0`, fiksuotas pateikčių rinkinys, fiksuokite JSON išvestis pagal versijų kontrolę |
| Kokybės rubrikos vertinimas | Prideda kokybinį matmenį | Palaikykite `prompts.json` su numatomais aspektais; rankiniu būdu arba per antrinį modelį pažymėkite balus (1–5) |
| CSV / Markdown eksportas | Dalijimosi ataskaita | Praplėskite scenarijų, kad rašytų `benchmark_report.md` su lentele ir akcentais |
| Modelio galimybių žymės | Padeda automatizuotam maršrutizavimui vėliau | Palaikykite `models.json` su `{alias: {capabilities:[], size_mb:..}}` |
| Talpyklos šildymo fazė | Sumažina šalto starto šališkumą | Atlikite vieną šildymo etapą prieš laiko matavimo ciklą (jau įgyvendinta) |
| Procentinė tikslumo analizė | Patikimas vėlinimo uodegos matavimas | Naudokite numpy procentilę (jau refaktorizuotame scenarijuje) |
| Žetono kainos apskaičiavimas | Ekonominis palyginimas | Apytikslė kaina = (žetonai per sekundę * vidutinis žetonų skaičius per užklausą) * energijos heuristika |
| Automatinis nepavykusių modelių praleidimas | Atsparumas grupės paleidimuose | Apgaubkite kiekvieną testą try/except ir pažymėkite būsenos lauką |

#### Minimalus Markdown eksporto fragmentas

```python
with open("benchmark_report.md", "w") as f:
        f.write("|Model|Avg Latency|p95|TPS|\n|---|---|---|---|\n")
        for row in summary:
                f.write(f"|{row['alias']}|{row['latency_avg']:.2f}|{row['latency_p95']:.2f}|{(row.get('tokens_per_sec_avg') or 0):.1f}|\n")
```


#### Deterministinio pateikčių rinkinio pavyzdys

```json
[
    "Summarize retrieval augmented generation.",
    "List 3 privacy benefits of local inference.",
    "Explain when to choose an SLM over an LLM."
]
```

Kartokite statinį sąrašą vietoj atsitiktinių pateikčių, kad gautumėte palyginamus metrikos duomenis tarp įsipareigojimų.

---

**Atsakomybės apribojimas**:  
Šis dokumentas buvo išverstas naudojant dirbtinio intelekto vertimo paslaugą [Co-op Translator](https://github.com/Azure/co-op-translator). Nors siekiame tikslumo, atkreipkite dėmesį, kad automatiniai vertimai gali turėti klaidų ar netikslumų. Originalus dokumentas jo gimtąja kalba turėtų būti laikomas autoritetingu šaltiniu. Dėl svarbios informacijos rekomenduojama profesionali žmogaus vertimo paslauga. Mes neprisiimame atsakomybės už nesusipratimus ar klaidingus aiškinimus, kylančius dėl šio vertimo naudojimo.