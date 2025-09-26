<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "02b037f55de779607eb12edcc7a7fcf2",
  "translation_date": "2025-09-26T19:03:35+00:00",
  "source_file": "Module07/foundrylocal.md",
  "language_code": "my"
}
-->
# Foundry Local ကို Windows နှင့် Mac တွင် အသုံးပြုခြင်း

ဤလမ်းညွှန်သည် Microsoft Foundry Local ကို Windows နှင့် Mac တွင် ထည့်သွင်းခြင်း၊ အလုပ်လုပ်ခြင်းနှင့် ပေါင်းစပ်အသုံးပြုခြင်းအတွက် အကူအညီပေးပါသည်။ အဆင့်ဆင့်လုပ်ဆောင်မှုများနှင့် command များကို Microsoft Learn စာရွက်စာတမ်းများနှင့်အညီ စစ်ဆေးပြီးဖြစ်သည်။

- စတင်အသုံးပြုရန်: https://learn.microsoft.com/azure/ai-foundry/foundry-local/get-started
- Architecture: https://learn.microsoft.com/azure/ai-foundry/foundry-local/concepts/foundry-local-architecture
- CLI Reference: https://learn.microsoft.com/azure/ai-foundry/foundry-local/reference/reference-cli
- SDKs ပေါင်းစပ်အသုံးပြုခြင်း: https://learn.microsoft.com/azure/ai-foundry/foundry-local/how-to/how-to-integrate-with-inference-sdks
- HF Models (BYOM) ကို Compile လုပ်ခြင်း: https://learn.microsoft.com/azure/ai-foundry/foundry-local/how-to/how-to-compile-hugging-face-models
- Windows AI: Local နှင့် Cloud အကြား: https://learn.microsoft.com/windows/ai/cloud-ai#key-decision-factors-for-app-developers

## 1) Windows တွင် Install / Upgrade လုပ်ခြင်း

- Install:
```cmd
winget install Microsoft.FoundryLocal
```
- Upgrade:
```cmd
winget upgrade --id Microsoft.FoundryLocal
```
- Version check:
```cmd
foundry --version
```
     
**Mac တွင် Install**

**MacOS**: 
Terminal ကိုဖွင့်ပြီး အောက်ပါ command ကို run လုပ်ပါ:
```bash
   brew tap microsoft/foundrylocal
   brew install foundrylocal
```

## 2) CLI အခြေခံ (အမျိုးအစား ၃ မျိုး)

- Model:
```cmd
foundry model --help
foundry model list
foundry model run gpt-oss-20b
```
- Service:
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

မှတ်ချက်များ:
- Service သည် OpenAI-compatible REST API ကို expose လုပ်ပါသည်။ Endpoint port ကို dynamic အနေနဲ့ allocate လုပ်ပါသည်။ `foundry service status` ကို အသုံးပြု၍ port ကို ရှာဖွေပါ။
- SDKs ကို အသုံးပြုပါက အဆင်ပြေပါသည်။ SDKs တွင် endpoint discovery ကို automatic အနေနဲ့ handle လုပ်ပေးပါသည်။

## 3) Local Endpoint ကို ရှာဖွေခြင်း (Dynamic Port)

Foundry Local သည် service စတင်တိုင်း dynamic port ကို assign လုပ်ပါသည်:
```cmd
foundry service status
```
Report လုပ်ထားသော `http://localhost:<PORT>` ကို OpenAI-compatible paths (ဥပမာ၊ `/v1/chat/completions`) နှင့်အတူ `base_url` အဖြစ် အသုံးပြုပါ။

## 4) OpenAI Python SDK ဖြင့် အမြန်စမ်းသပ်ခြင်း

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
References:
- SDK Integration: https://learn.microsoft.com/azure/ai-foundry/foundry-local/how-to/how-to-integrate-with-inference-sdks

## 5) ကိုယ်ပိုင် Model (Olive ဖြင့် Compile လုပ်ပါ)

Catalog တွင် မပါဝင်သော model ကို Foundry Local အတွက် ONNX အဖြစ် Olive ဖြင့် compile လုပ်ပါ။

အဆင့်မြင့် flow (လမ်းညွှန်စာတမ်းများတွင် အဆင့်များကို ကြည့်ပါ):
```cmd
foundry cache cd models
foundry cache list
foundry model run llama-3.2 --verbose
```
Docs:
- BYOM compile: https://learn.microsoft.com/azure/ai-foundry/foundry-local/how-to/how-to-compile-hugging-face-models

## 6) ပြဿနာများကို ဖြေရှင်းခြင်း

- Service status နှင့် logs ကို စစ်ဆေးပါ:
```cmd
foundry service status
foundry service diag
```
- Cache ကို ရှင်းလင်းခြင်း သို့မဟုတ် ရွှေ့ခြင်း:
```cmd
foundry cache list
foundry cache remove <model>
foundry cache cd <path>
```
- Preview version ကို နောက်ဆုံးပေါ်အဖြစ် update လုပ်ပါ:
```cmd
winget upgrade --id Microsoft.FoundryLocal
```

## 7) Windows Developer အတွေ့အကြုံနှင့် ဆက်စပ်မှု

- Windows local နှင့် cloud AI ရွေးချယ်မှုများ၊ Foundry Local နှင့် Windows ML အပါအဝင်:
  https://learn.microsoft.com/windows/ai/cloud-ai#key-decision-factors-for-app-developers
- VS Code AI Toolkit ကို Foundry Local နှင့်အတူ အသုံးပြုခြင်း (chat endpoint URL ကို ရှာဖွေရန် `foundry service status` ကို အသုံးပြုပါ):
  https://learn.microsoft.com/azure/ai-foundry/foundry-local/concepts/foundry-local-architecture#key-components

---

