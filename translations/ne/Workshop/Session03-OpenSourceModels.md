<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "d6ad6c8b4a0e3ecef3afb86a6f578e1c",
  "translation_date": "2025-10-09T09:35:49+00:00",
  "source_file": "Workshop/Session03-OpenSourceModels.md",
  "language_code": "ne"
}
-->
# सत्र ३: फाउन्ड्री लोकलमा ओपन-सोर्स मोडेलहरू

## सारांश

हगिङ फेस र अन्य ओपन-सोर्स मोडेलहरू फाउन्ड्री लोकलमा कसरी ल्याउने भन्ने कुरा पत्ता लगाउनुहोस्। चयन रणनीतिहरू, समुदाय योगदान कार्यप्रवाहहरू, प्रदर्शन तुलना पद्धति, र फाउन्ड्रीलाई कस्टम मोडेल दर्ता गरेर विस्तार गर्ने तरिका सिक्नुहोस्। यो सत्र साप्ताहिक "मोडेल मन्डे" अन्वेषण थिमहरूसँग मेल खान्छ र तपाईंलाई ओपन-सोर्स मोडेलहरू स्थानीय रूपमा मूल्याङ्कन र सञ्चालन गर्न सक्षम बनाउँछ, त्यसपछि Azure मा स्केल गर्न।

## सिक्ने उद्देश्यहरू

सत्रको अन्त्यसम्ममा तपाईं सक्षम हुनुहुनेछ:

- **खोज र मूल्याङ्कन गर्नुहोस्**: गुणस्तर बनाम स्रोत व्यापार-अफहरू प्रयोग गरेर उपयुक्त मोडेलहरू (मिस्ट्रल, जेम्मा, क्वेन, डीपसिक) पहिचान गर्नुहोस्।
- **लोड र चलाउनुहोस्**: फाउन्ड्री लोकल CLI प्रयोग गरेर समुदाय मोडेलहरू डाउनलोड, क्यास, र सुरु गर्नुहोस्।
- **बेंचमार्क गर्नुहोस्**: स्थिर विलम्बता + टोकन थ्रुपुट + गुणस्तर ह्युरिस्टिक्स लागू गर्नुहोस्।
- **विस्तार गर्नुहोस्**: SDK-संगत ढाँचाहरू अनुसरण गर्दै कस्टम मोडेल आवरण दर्ता वा अनुकूलन गर्नुहोस्।
- **तुलना गर्नुहोस्**: SLM बनाम मध्यम आकारको LLM चयन निर्णयहरूको लागि संरचित तुलना उत्पादन गर्नुहोस्।

## पूर्वापेक्षाहरू

- सत्र १ र २ पूरा गरिएको
- `foundry-local-sdk` स्थापना गरिएको पायथन वातावरण
- धेरै मोडेल क्यासहरूको लागि कम्तीमा १५GB खाली डिस्क
- वैकल्पिक: GPU/WebGPU एक्सेलेरेशन सक्षम (`foundry config list`)

### क्रस-प्ल्याटफर्म वातावरण छिटो सुरु

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

macOS बाट Windows होस्ट सेवाको विरुद्ध बेंचमार्क गर्दा सेट गर्नुहोस्:
```bash
export FOUNDRY_LOCAL_ENDPOINT=http://<windows-host>:5273/v1
```


## डेमो प्रवाह (३० मिनेट)

### १. CLI मार्फत हगिङ फेस मोडेलहरू लोड गर्नुहोस् (८ मिनेट)

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


### २. चलाउनुहोस् र छिटो जाँच गर्नुहोस् (५ मिनेट)

```powershell
foundry model run qwen2.5-0.5b
foundry model run qwen2.5-0.5b --prompt "List three benefits of local inference."

foundry model run mistral-7b
foundry model run mistral-7b --prompt "Explain retrieval augmented generation in one paragraph."
```


### ३. बेंचमार्क स्क्रिप्ट (८ मिनेट)

`samples/03-oss-models/benchmark_models.py` सिर्जना गर्नुहोस्:

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

चलाउनुहोस्:

```powershell
python samples/03-oss-models/benchmark_models.py
```


### ४. प्रदर्शन तुलना गर्नुहोस् (५ मिनेट)

व्यापार-अफहरू छलफल गर्नुहोस्: लोड समय, मेमोरी फुटप्रिन्ट (टास्क म्यानेजर / `nvidia-smi` / OS स्रोत मोनिटर अवलोकन गर्नुहोस्), आउटपुट गुणस्तर बनाम गति। GPU एक्सेलेरेशन सक्षम गरेपछि पुन: प्रयास गर्दै पायथन बेंचमार्क स्क्रिप्ट (सत्र ३) प्रयोग गरेर विलम्बता र थ्रुपुट मापन गर्नुहोस्।

### ५. स्टार्टर प्रोजेक्ट (४ मिनेट)

बेंचमार्किङ स्क्रिप्टलाई मार्कडाउन निर्यातको साथ विस्तार गरेर मोडेल तुलना रिपोर्ट जेनेरेटर सिर्जना गर्नुहोस्।

## स्टार्टर प्रोजेक्ट: `03-huggingface-models` विस्तार गर्नुहोस्

अस्तित्वमा रहेको नमूनालाई सुधार गर्नुहोस्:

1. बेंचमार्क समग्रता + CSV/Markdown आउटपुट थप्दै।
2. सरल गुणात्मक स्कोरिङ कार्यान्वयन गर्दै (प्रम्प्ट जोडी सेट + म्यानुअल एनोटेसन स्टब फाइल)।
3. प्लगयोग्य मोडेल सूची र प्रम्प्ट सेटको लागि JSON कन्फिग (`models.json`) परिचय गराउँदै।

## मान्यता जाँचसूची

```powershell
foundry cache list
foundry model run qwen2.5-0.5b
curl http://localhost:5273/v1/models
```

सबै लक्ष्य मोडेलहरू देखिनु पर्छ र प्रोब च्याट अनुरोधमा प्रतिक्रिया दिनु पर्छ।

## नमूना परिदृश्य र कार्यशाला म्यापिङ

| कार्यशाला स्क्रिप्ट | परिदृश्य | लक्ष्य | प्रम्प्ट / डेटासेट स्रोत |
|---------------------|----------|-------|--------------------------|
| `samples/session03/benchmark_oss_models.py` / `notebooks/session03_benchmark_oss_models.ipynb` | एजे प्लेटफर्म टोलीले एम्बेडेड समरीकारका लागि डिफल्ट SLM चयन गर्दै | उम्मेदवार मोडेलहरूमा विलम्बता + p95 + टोकन/सेकन्ड तुलना उत्पादन गर्नुहोस् | इनलाइन `PROMPT` var + वातावरण `BENCH_MODELS` सूची |

### परिदृश्य कथा

उत्पादन इन्जिनियरिङले अफलाइन बैठक-नोट्स सुविधाको लागि डिफल्ट हल्का समरीकरण मोडेल चयन गर्नुपर्छ। तिनीहरूले निश्चित प्रम्प्ट सेट (तलको उदाहरण हेर्नुहोस्) मा नियन्त्रित निर्धारणात्मक बेंचमार्कहरू (temperature=0) चलाउँछन् र GPU एक्सेलेरेशनको साथ र बिना विलम्बता + थ्रुपुट मेट्रिक्स सङ्कलन गर्छन्।

### उदाहरण प्रम्प्ट सेट JSON (विस्तारयोग्य)

```json
[
    "Explain the principle of retrieval augmented generation in 2 sentences.",
    "List 3 privacy benefits of local inference.",
    "Summarize why model size impacts latency on consumer hardware.",
    "Provide two scenarios where an SLM is preferable to an LLM."
]
```

प्रत्येक मोडेलमा प्रत्येक प्रम्प्ट लूप गर्नुहोस्, वितरण मेट्रिक्स प्राप्त गर्न प्रति-प्रम्प्ट विलम्बता क्याप्चर गर्नुहोस् र आउटलायरहरू पत्ता लगाउनुहोस्।

## मोडेल चयन फ्रेमवर्क

| आयाम | मेट्रिक | किन महत्त्वपूर्ण छ |
|------|--------|---------------------|
| विलम्बता | औसत / p95 | प्रयोगकर्ता अनुभव स्थिरता |
| थ्रुपुट | टोकन/सेकन्ड | ब्याच र स्ट्रिमिङ स्केलेबिलिटी |
| मेमोरी | निवासी आकार | उपकरण फिट र समवर्तीता |
| गुणस्तर | रुब्रिक प्रम्प्टहरू | कार्य उपयुक्तता |
| फुटप्रिन्ट | डिस्क क्यास | वितरण र अपडेटहरू |
| लाइसेन्स | प्रयोग अनुमति | व्यावसायिक अनुपालन |

## कस्टम मोडेलको साथ विस्तार गर्दै

उच्च-स्तरीय ढाँचा (छद्म):

```python
# pseudo_adapter.py (conceptual)
class CustomModelAdapter:
    def load(self, weights_path: str): ...
    def generate(self, prompt: str, **params) -> str: ...

# Register with local routing (future extensibility point)
```

विकसित एडाप्टर इन्टरफेसहरूको लागि आधिकारिक रिपो परामर्श गर्नुहोस्:
https://github.com/microsoft/Foundry-Local/tree/main/sdk/python

## समस्या समाधान

| समस्या | कारण | समाधान |
|-------|------|-------|
| मिस्ट्रल-७बीमा OOM | अपर्याप्त RAM/GPU | अन्य मोडेलहरू रोक्नुहोस्; सानो भेरियन्ट प्रयास गर्नुहोस् |
| पहिलो प्रतिक्रिया ढिलो | चिसो लोड | समय-समयमा हल्का प्रम्प्ट प्रयोग गरेर तातो राख्नुहोस् |
| डाउनलोड रोकियो | नेटवर्क अस्थिरता | पुन: प्रयास गर्नुहोस्; अफ-पिक समयमा प्रिफेच गर्नुहोस् |

## सन्दर्भहरू

- फाउन्ड्री लोकल SDK: https://github.com/microsoft/Foundry-Local/tree/main/sdk/python
- मोडेल मन्डे: https://aka.ms/model-mondays
- हगिङ फेस मोडेल डिस्कभरी: https://huggingface.co/models

---

**सत्र अवधि**: ३० मिनेट (+ वैकल्पिक गहिरो अध्ययन)  
**कठिनाई स्तर**: मध्यम

### वैकल्पिक सुधारहरू

| सुधार | फाइदा | कसरी |
|-------|-------|-----|
| स्ट्रिमिङ पहिलो-टोकन विलम्बता | महसुस गरिएको प्रतिक्रियाशीलता मापन गर्दछ | `BENCH_STREAM=1` प्रयोग गरेर बेंचमार्क चलाउनुहोस् (`Workshop/samples/session03` मा सुधारिएको स्क्रिप्ट) |
| निर्धारणात्मक मोड | स्थिर पुनरावृत्ति तुलना | `temperature=0`, निश्चित प्रम्प्ट सेट, संस्करण नियन्त्रण अन्तर्गत JSON आउटपुटहरू क्याप्चर गर्नुहोस् |
| गुणस्तर रुब्रिक स्कोरिङ | गुणात्मक आयाम थप्छ | अपेक्षित पक्षहरूसँग `prompts.json` कायम गर्नुहोस्; स्कोरहरू (१–५) म्यानुअल वा दोस्रो मोडेल मार्फत एनोटेट गर्नुहोस् |
| CSV / Markdown निर्यात | साझा गर्न मिल्ने रिपोर्ट | स्क्रिप्टलाई `benchmark_report.md` लेख्न विस्तार गर्नुहोस् तालिका र हाइलाइटहरू सहित |
| मोडेल क्षमता ट्यागहरू | पछि स्वचालित रुटिङमा मद्दत गर्दछ | `{alias: {capabilities:[], size_mb:..}}` सहित `models.json` कायम गर्नुहोस् |
| क्यास वार्मअप चरण | चिसो-स्टार्ट पूर्वाग्रह घटाउनुहोस् | समय लूप अघि एक वार्म राउन्ड कार्यान्वयन गर्नुहोस् (पहिले नै कार्यान्वित) |
| प्रतिशत सटीकता | बलियो टेल विलम्बता | numpy प्रतिशत प्रयोग गर्नुहोस् (पहिले नै पुन: संरचित स्क्रिप्टमा) |
| टोकन लागत अनुमान | आर्थिक तुलना | अनुमानित लागत = (टोकन/सेकन्ड * प्रति अनुरोध औसत टोकन) * ऊर्जा ह्युरिस्टिक |
| असफल मोडेलहरू स्वत: स्किप गर्दै | ब्याच रनहरूमा लचिलोपन | प्रत्येक बेंचमार्कलाई try/except मा र्याप गर्नुहोस् र स्थिति क्षेत्र चिन्ह लगाउनुहोस् |

#### न्यूनतम मार्कडाउन निर्यात स्निपेट

```python
with open("benchmark_report.md", "w") as f:
        f.write("|Model|Avg Latency|p95|TPS|\n|---|---|---|---|\n")
        for row in summary:
                f.write(f"|{row['alias']}|{row['latency_avg']:.2f}|{row['latency_p95']:.2f}|{(row.get('tokens_per_sec_avg') or 0):.1f}|\n")
```


#### निर्धारणात्मक प्रम्प्ट सेट उदाहरण

```json
[
    "Summarize retrieval augmented generation.",
    "List 3 privacy benefits of local inference.",
    "Explain when to choose an SLM over an LLM."
]
```

प्रतिबद्धताहरूमा तुलनात्मक मेट्रिक्सको लागि अनियमित प्रम्प्टहरूको सट्टा स्थिर सूची लूप गर्नुहोस्।

---

**अस्वीकरण**:  
यो दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) प्रयोग गरी अनुवाद गरिएको हो। हामी यथासम्भव सटीकता सुनिश्चित गर्न प्रयास गर्छौं, तर कृपया ध्यान दिनुहोस् कि स्वचालित अनुवादहरूमा त्रुटि वा अशुद्धता हुन सक्छ। यसको मूल भाषामा रहेको मूल दस्तावेजलाई आधिकारिक स्रोत मानिनुपर्छ। महत्वपूर्ण जानकारीका लागि, व्यावसायिक मानव अनुवाद सिफारिस गरिन्छ। यस अनुवादको प्रयोगबाट उत्पन्न हुने कुनै पनि गलतफहमी वा गलत व्याख्याको लागि हामी जिम्मेवार हुने छैनौं।