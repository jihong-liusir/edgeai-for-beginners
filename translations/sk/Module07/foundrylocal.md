<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "070a706937c5ac9feb45693b8c572d25",
  "translation_date": "2025-09-23T01:22:25+00:00",
  "source_file": "Module07/foundrylocal.md",
  "language_code": "sk"
}
-->
# Foundry Local na Windows (Overené)

Tento návod vám pomôže nainštalovať, spustiť a integrovať Microsoft Foundry Local na Windows. Všetky kroky a príkazy sú overené podľa dokumentácie Microsoft Learn.

- Začíname: https://learn.microsoft.com/azure/ai-foundry/foundry-local/get-started
- Architektúra: https://learn.microsoft.com/azure/ai-foundry/foundry-local/concepts/foundry-local-architecture
- Referencia CLI: https://learn.microsoft.com/azure/ai-foundry/foundry-local/reference/reference-cli
- Integrácia SDK: https://learn.microsoft.com/azure/ai-foundry/foundry-local/how-to/how-to-integrate-with-inference-sdks
- Kompilácia HF modelov (BYOM): https://learn.microsoft.com/azure/ai-foundry/foundry-local/how-to/how-to-compile-hugging-face-models
- Windows AI: Lokálne vs Cloud: https://learn.microsoft.com/windows/ai/cloud-ai#key-decision-factors-for-app-developers

## 1) Inštalácia / Aktualizácia na Windows

- Inštalácia:
```cmd
winget install Microsoft.FoundryLocal
```
- Aktualizácia:
```cmd
winget upgrade --id Microsoft.FoundryLocal
```
- Kontrola verzie:
```cmd
foundry --version
```

## 2) Základy CLI (Tri kategórie)

- Model:
```cmd
foundry model --help
foundry model list
foundry model run gpt-oss-20b
```
- Služba:
```cmd
foundry service --help
foundry service status
foundry service ps
```
- Cache:
```cmd
foundry cache --help
foundry cache list
```

Poznámky:
- Služba poskytuje REST API kompatibilné s OpenAI. Port pre endpoint je dynamicky pridelený; použite `foundry service status` na jeho zistenie.
- Používajte SDK pre pohodlie; automaticky spracujú zistenie endpointu tam, kde je to podporované.

## 3) Zistenie lokálneho endpointu (Dynamický port)

Foundry Local priraďuje dynamický port pri každom spustení služby:
```cmd
foundry service status
```
Použite nahlásený `http://localhost:<PORT>` ako váš `base_url` s cestami kompatibilnými s OpenAI (napríklad `/v1/chat/completions`).

## 4) Rýchly test cez OpenAI Python SDK

```cmd
set BASE_URL=http://localhost:PORT
python - <<PY
from openai import OpenAI
client = OpenAI(base_url="%BASE_URL%/v1", api_key="")
resp = client.chat.completions.create(
    model="gpt-oss-20b",
    messages=[{"role":"user","content":"Say hello from Foundry Local."}],
    max_tokens=64,
)
print(resp.choices[0].message.content)
PY
```
Referencie:
- Integrácia SDK: https://learn.microsoft.com/azure/ai-foundry/foundry-local/how-to/how-to-integrate-with-inference-sdks

## 5) Vlastný model (Kompilácia pomocou Olive)

Ak potrebujete model, ktorý nie je v katalógu, skompilujte ho do ONNX pre Foundry Local pomocou Olive.

Vysoká úroveň procesu (pozrite dokumentáciu pre kroky):
```cmd
foundry cache cd models
foundry cache list
foundry model run llama-3.2 --verbose
```
Dokumentácia:
- Kompilácia BYOM: https://learn.microsoft.com/azure/ai-foundry/foundry-local/how-to/how-to-compile-hugging-face-models

## 6) Riešenie problémov

- Skontrolujte stav služby a logy:
```cmd
foundry service status
foundry service diag
```
- Vymažte alebo presuňte cache:
```cmd
foundry cache list
foundry cache remove <model>
foundry cache cd <path>
```
- Aktualizujte na najnovšiu preview verziu:
```cmd
winget upgrade --id Microsoft.FoundryLocal
```

## 7) Súvisiace skúsenosti vývojárov na Windows

- Možnosti lokálnej vs cloudovej AI na Windows, vrátane Foundry Local a Windows ML:
  https://learn.microsoft.com/windows/ai/cloud-ai#key-decision-factors-for-app-developers
- VS Code AI Toolkit s Foundry Local (použite `foundry service status` na získanie URL endpointu pre chat):
  https://learn.microsoft.com/azure/ai-foundry/foundry-local/concepts/foundry-local-architecture#key-components

---

