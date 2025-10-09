<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "e88a16101de37838f7cf256a9cd0f199",
  "translation_date": "2025-10-09T09:53:05+00:00",
  "source_file": "Workshop/notebooks/TROUBLESHOOTING.md",
  "language_code": "bn"
}
-->
# ওয়ার্কশপ নোটবুক - সমস্যা সমাধানের গাইড

## বিষয়সূচি

- [সাধারণ সমস্যা এবং সমাধান](../../../../Workshop/notebooks)
- [সেশন ০৪ নির্দিষ্ট সমস্যা](../../../../Workshop/notebooks)
- [সেশন ০৫ নির্দিষ্ট সমস্যা](../../../../Workshop/notebooks)
- [সেশন ০৬ নির্দিষ্ট সমস্যা](../../../../Workshop/notebooks)
- [হার্ডওয়্যার-নির্দিষ্ট সমস্যা](../../../../Workshop/notebooks)
- [ডায়াগনস্টিক কমান্ড](../../../../Workshop/notebooks)
- [সহায়তা পাওয়া](../../../../Workshop/notebooks)

---

## সাধারণ সমস্যা এবং সমাধান

### 🔴 CUDA মেমোরি শেষ হয়ে গেছে

**ত্রুটির বার্তা:**
```
CUDA failure 2: out of memory
```

**মূল কারণ:** GPU-তে মডেল লোড করার জন্য পর্যাপ্ত VRAM নেই।

**সমাধানসমূহ:**

#### অপশন ১: CPU ভ্যারিয়েন্ট ব্যবহার করুন (প্রস্তাবিত)
```python
# In your notebook, update the CATALOG to use CPU variants
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```

#### অপশন ২: GPU-তে ছোট মডেল ব্যবহার করুন
```python
# Use only the smallest model
CATALOG = {
    'qwen2.5-0.5b': {'capabilities':['general','code','summarize','classification'],'priority':1},
}
```

#### অপশন ৩: GPU মেমোরি পরিষ্কার করুন
```bash
# Close other GPU-intensive applications
# Check GPU memory usage
nvidia-smi

# Restart Foundry Local service
foundry service stop
foundry service start
```

#### অপশন ৪: GPU মেমোরি বাড়ান (যদি সম্ভব হয়)
- ব্রাউজার ট্যাব, ভিডিও এডিটর বা অন্যান্য GPU অ্যাপ বন্ধ করুন
- উইন্ডোজ ভিজ্যুয়াল ইফেক্ট কমান
- ইন্টিগ্রেটেড + ডেডিকেটেড GPU থাকলে ডেডিকেটেড GPU ব্যবহার করুন

---

### 🔴 APIConnectionError: সংযোগ ত্রুটি

**ত্রুটির বার্তা:**
```
APIConnectionError: Connection error
[Retry 1/2] Setup failed for 'phi-4-mini': APIConnectionError: Connection error.
```

**মূল কারণ:** Foundry Local সার্ভিস চালু নেই বা অ্যাক্সেসযোগ্য নয়।

**সমাধানসমূহ:**

#### ধাপ ১: সার্ভিস স্ট্যাটাস পরীক্ষা করুন
```bash
foundry service status
```

#### ধাপ ২: সার্ভিস বন্ধ থাকলে চালু করুন
```bash
foundry service start
```

#### ধাপ ৩: এন্ডপয়েন্ট যাচাই করুন
```bash
# Check what port the service is using
foundry service status

# Test with curl (adjust port if different)
curl http://localhost:59959/health
curl http://localhost:55769/health
```

#### ধাপ ৪: প্রয়োজনীয় মডেল লোড করুন
```bash
foundry model run phi-4-mini
foundry model run qwen2.5-3b
foundry model run phi-3.5-mini
```

#### ধাপ ৫: নোটবুক কার্নেল পুনরায় চালু করুন
সার্ভিস চালু করার এবং মডেল লোড করার পরে, নোটবুক কার্নেল পুনরায় চালু করুন এবং সব সেল পুনরায় চালান।

---

### 🔴 ক্যাটালগে মডেল পাওয়া যায়নি

**ত্রুটির বার্তা:**
```
ValueError: Model phi-3.5-mini-cpu not found in the catalog.
[ERROR] Model 'phi-4-mini' not found in the catalog
```

**মূল কারণ:** মডেল ডাউনলোড করা হয়নি বা Foundry Local-এ লোড করা হয়নি।

**সমাধানসমূহ:**

#### অপশন ১: মডেল ডাউনলোড এবং লোড করুন
```bash
# List available models
foundry model ls

# Download the model if not present
foundry model download phi-4-mini
foundry model download qwen2.5-3b
foundry model download phi-3.5-mini

# Load the model into memory
foundry model run phi-4-mini
foundry model run qwen2.5-3b
foundry model run phi-3.5-mini
```

#### অপশন ২: অটো-সিলেকশন মোড ব্যবহার করুন
আপনার CATALOG আপডেট করুন যাতে বেস মডেল নাম (যেমন `-cpu` সাফিক্স ছাড়া) ব্যবহার করা হয়:

```python
CATALOG = {
    'phi-4-mini': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini': {'capabilities':['code','refactor'],'priority':3},
}
```

Foundry Local SDK স্বয়ংক্রিয়ভাবে আপনার হার্ডওয়্যারের জন্য সেরা ভ্যারিয়েন্ট (CPU, GPU, বা NPU) নির্বাচন করবে।

---

### 🔴 HttpResponseError: 500 - মডেল লোডিং ব্যর্থ

**ত্রুটির বার্তা:**
```
HttpResponseError: 500 - Failed loading model
```

**মূল কারণ:** মডেল ফাইল ক্ষতিগ্রস্ত বা হার্ডওয়্যারের সাথে অসঙ্গতিপূর্ণ।

**সমাধানসমূহ:**

#### মডেল পুনরায় ডাউনলোড করুন
```bash
# Remove corrupted model
foundry model remove phi-3.5-mini

# Download fresh copy
foundry model download phi-3.5-mini
```

#### ভিন্ন ভ্যারিয়েন্ট ব্যবহার করুন
```bash
# Try CPU variant instead
foundry model download phi-3.5-mini-cpu
```

---

### 🔴 ImportError: কোনো মডিউল পাওয়া যায়নি

**ত্রুটির বার্তা:**
```
ModuleNotFoundError: No module named 'foundry_local'
```

**মূল কারণ:** foundry-local-sdk প্যাকেজ ইনস্টল করা হয়নি।

**সমাধানসমূহ:**

```bash
# Install SDK
pip install foundry-local-sdk

# Verify installation
pip show foundry-local-sdk
python -c "from foundry_local import FoundryLocalManager; print('SDK OK')"
```

---

### � প্রথম অনুরোধ ধীর

**লক্ষণ:** প্রথম কমপ্লিশন ৩০+ সেকেন্ড সময় নেয়, পরবর্তী অনুরোধ দ্রুত হয়।

**মূল কারণ:** এটি স্বাভাবিক আচরণ - সার্ভিস প্রথম অনুরোধে মডেল মেমোরিতে লোড করছে।

**সমাধানসমূহ:**

#### মডেল প্রি-লোড করুন
```bash
# Download and load all models you'll use before running notebooks
foundry model download phi-4-mini
foundry model download qwen2.5-3b
foundry model download phi-3.5-mini

foundry model run phi-4-mini
foundry model run qwen2.5-3b
```

#### সার্ভিস চালু রাখুন
```bash
# Start service manually and leave it running
foundry service start
```

---

## সেশন ০৪ নির্দিষ্ট সমস্যা

### ভুল পোর্ট কনফিগারেশন

**সমস্যা:** নোটবুক ভুল পোর্টে সংযোগ করছে (৫৫৭৬৯ বনাম ৫৯৯৫৯ বনাম ৫৭১২৭)

**সমাধান:**

1. Foundry Local কোন পোর্ট ব্যবহার করছে তা পরীক্ষা করুন:
```bash
foundry service status
# Note the port number displayed
```

2. নোটবুকের সেল ১০ আপডেট করুন:
```python
ENDPOINT = os.getenv('FOUNDRY_LOCAL_ENDPOINT', 'http://localhost:59959/v1')
# Replace 59959 with your actual port
```

3. কার্নেল পুনরায় চালু করুন এবং সেল ৬, ৮, ১০, ১২, ১৬, ২০, ২২ পুনরায় চালান

---

### ভুল মডেল নির্বাচন

**সমস্যা:** নোটবুক gpt-oss-20b বা qwen2.5-7b দেখাচ্ছে qwen2.5-3b এর পরিবর্তে

**সমাধান:**

1. নোটবুক কার্নেল পুনরায় চালু করুন (পুরানো ভ্যারিয়েবল স্টেট মুছে ফেলে)
2. সেল ১০ পুনরায় চালান (মডেল এলিয়াস সেট করুন)
3. সেল ১২ পুনরায় চালান (কনফিগারেশন প্রদর্শন করুন)
4. **যাচাই করুন:** সেল ১২-এ `LLM Model: qwen2.5-3b` দেখানো উচিত

---

### ডায়াগনস্টিক সেল ব্যর্থ

**সমস্যা:** সেল ১৬ "❌ Foundry Local সার্ভিস পাওয়া যায়নি!" দেখাচ্ছে

**সমাধান:**

1. সার্ভিস চালু আছে কিনা যাচাই করুন:
```bash
foundry service status
```

2. এন্ডপয়েন্ট ম্যানুয়ালি পরীক্ষা করুন:
```bash
curl http://localhost:59959/v1/models
```

3. যদি curl কাজ করে কিন্তু নোটবুক না করে:
   - নোটবুক কার্নেল পুনরায় চালু করুন
   - সেলগুলো ক্রমানুসারে পুনরায় চালান: ৬, ৮, ১০, ১২, ১৪, ১৬

4. যদি curl ব্যর্থ হয়:
   - সার্ভিস চালু করুন: `foundry service start`
   - মডেল লোড করুন: `foundry model run phi-4-mini` এবং `foundry model run qwen2.5-3b`

---

### প্রি-ফ্লাইট চেক ব্যর্থ

**সমস্যা:** সেল ২০ সংযোগ ত্রুটি দেখাচ্ছে যদিও ডায়াগনস্টিক পাস করেছে

**সমাধান:**

1. মডেল লোড করা আছে কিনা পরীক্ষা করুন:
```bash
foundry model ls
# Should show phi-4-mini and qwen2.5-3b
```

2. যদি মডেল অনুপস্থিত:
```bash
foundry model run phi-4-mini
foundry model run qwen2.5-3b
```

3. মডেল লোড করার পরে সেল ২০ পুনরায় চালান

---

### তুলনা None মান সহ ব্যর্থ

**সমস্যা:** সেল ২২ সম্পন্ন হয় কিন্তু লেটেন্সি None দেখায়

**সমাধান:**

1. প্রথমে প্রি-ফ্লাইট পাস হয়েছে কিনা পরীক্ষা করুন (সেল ২০)
2. সেল ২২ পুনরায় চালান - প্রথম অনুরোধে মডেল উষ্ণ হতে পারে
3. নিশ্চিত করুন উভয় মডেল লোড করা আছে: `foundry model ls`

---

## সেশন ০৫ নির্দিষ্ট সমস্যা

### এজেন্ট ভুল মডেল ব্যবহার করছে

**সমস্যা:** এজেন্ট প্রত্যাশিত মডেল ব্যবহার করছে না

**সমাধান:**

কনফিগারেশন যাচাই করুন:
```python
# Check which models are assigned
print(f"Researcher: {researcher.model_id}")
print(f"Editor: {editor.model_id}")
```

যদি মডেল ভুল থাকে, কার্নেল পুনরায় চালু করুন।

---

### মেমোরি কনটেক্সট ওভারফ্লো

**সমস্যা:** এজেন্টের প্রতিক্রিয়া সময়ের সাথে সাথে খারাপ হচ্ছে

**সমাধান:** এটি স্বয়ংক্রিয়ভাবে পরিচালিত হয় - এজেন্ট শুধুমাত্র শেষ ৬টি বার্তা মেমোরিতে রাখে।

---

## সেশন ০৬ নির্দিষ্ট সমস্যা

### CPU বনাম GPU মডেল বিভ্রান্তি

**সমস্যা:** ডিফল্ট কনফিগারেশন ব্যবহার করার সময় CUDA ত্রুটি দেখা যাচ্ছে

**সমাধান:** ডিফল্ট কনফিগারেশন এখন CPU মডেল ব্যবহার করে। যদি CUDA ত্রুটি দেখেন:

1. নিশ্চিত করুন আপনি ডিফল্ট CPU ক্যাটালগ ব্যবহার করছেন:
```python
# Cell should show CPU variants
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```

2. কার্নেল পুনরায় চালু করুন এবং সব সেল পুনরায় চালান

---

### ইন্টেন্ট ডিটেকশন কাজ করছে না

**সমস্যা:** প্রম্পট ভুল মডেলে রাউট হচ্ছে

**সমাধান:**

ইন্টেন্ট ডিটেকশন পরীক্ষা করুন:
```python
# Run the intent detection test cell
for prompt in test_prompts:
    intent = detect_intent(prompt)
    print(f"{prompt[:50]}... → {intent}")
```

যদি প্যাটার্নে পরিবর্তন প্রয়োজন হয়, RULES আপডেট করুন।

---

## হার্ডওয়্যার-নির্দিষ্ট সমস্যা

### NVIDIA GPU

**GPU স্ট্যাটাস পরীক্ষা করুন:**
```bash
nvidia-smi
```

**সাধারণ সমস্যা:**
- **ড্রাইভার পুরনো:** NVIDIA ড্রাইভার আপডেট করুন
- **CUDA ভার্সন মিসম্যাচ:** Foundry Local পুনরায় ইনস্টল করুন
- **GPU মেমোরি ফ্র্যাগমেন্টেড:** সিস্টেম পুনরায় চালু করুন

### Qualcomm NPU

**NPU স্ট্যাটাস পরীক্ষা করুন:**
```bash
foundry device info
```

**সাধারণ সমস্যা:**
- **NPU ড্রাইভার ইনস্টল করা হয়নি:** Qualcomm NPU ড্রাইভার ইনস্টল করুন
- **NPU ভ্যারিয়েন্ট উপলব্ধ নয়:** CPU ভ্যারিয়েন্ট ব্যবহার করুন
- **উইন্ডোজ ভার্সন খুব পুরনো:** সর্বশেষ উইন্ডোজ ১১-এ আপডেট করুন

### শুধুমাত্র CPU সিস্টেম

**প্রস্তাবিত মডেল:**
```python
CATALOG = {
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','general'],'priority':2},
}
```

**পারফরম্যান্স টিপস:**
- সবচেয়ে ছোট মডেল ব্যবহার করুন
- max_tokens কমান
- প্রথম অনুরোধের জন্য ধৈর্য ধরুন

---

## ডায়াগনস্টিক কমান্ড

### সবকিছু পরীক্ষা করুন
```bash
# Service status
foundry service status

# List models
foundry model ls

# Device info
foundry device info

# Version info
foundry --version

# Health check
curl http://localhost:55769/health
```

### পাইথনে
```python
# Check SDK import
try:
    from foundry_local import FoundryLocalManager
    print('✓ SDK imported')
except ImportError as e:
    print(f'✗ SDK import failed: {e}')

# Check service connectivity
from openai import OpenAI

try:
    client = OpenAI(base_url='http://localhost:59959/v1', api_key='test')
    models = client.models.list()
    print(f'✓ Service reachable, {len(list(models.data))} models available')
except Exception as e:
    print(f'✗ Service not reachable: {e}')
```

---

## সহায়তা পাওয়া

### ১. লগ পরীক্ষা করুন
```bash
# Windows
foundry service logs

# Or check Windows Event Viewer
# Application Logs -> Microsoft-FoundryLocal
```

### ২. GitHub ইস্যু
- বিদ্যমান ইস্যু অনুসন্ধান করুন: https://github.com/microsoft/Foundry-Local/issues
- নতুন ইস্যু তৈরি করুন:
  - ত্রুটির বার্তা (সম্পূর্ণ টেক্সট)
  - `foundry service status` এর আউটপুট
  - `foundry --version` এর আউটপুট
  - GPU/NPU তথ্য (nvidia-smi, ইত্যাদি)
  - পুনরুত্পাদনের ধাপ

### ৩. ডকুমেন্টেশন
- **মূল রিপোজিটরি:** https://github.com/microsoft/Foundry-Local
- **পাইথন SDK:** https://github.com/microsoft/Foundry-Local/tree/main/sdk/python
- **CLI রেফারেন্স:** https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-cli.md
- **সমস্যা সমাধান:** https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-troubleshooting.md

---

## দ্রুত সমাধানের চেকলিস্ট

যখন সমস্যা হয়, এইগুলো ক্রমানুসারে চেষ্টা করুন:

- [ ] সার্ভিস চালু আছে কিনা পরীক্ষা করুন: `foundry service status`
- [ ] সার্ভিস পুনরায় চালু করুন: `foundry service stop && foundry service start`
- [ ] মডেল বিদ্যমান কিনা যাচাই করুন: `foundry model ls | grep phi-4-mini`
- [ ] প্রয়োজনীয় মডেল লোড করুন: `foundry model run phi-4-mini`
- [ ] GPU মেমোরি পরীক্ষা করুন: `nvidia-smi` (যদি NVIDIA হয়)
- [ ] CPU ভ্যারিয়েন্ট চেষ্টা করুন: `phi-4-mini-cpu` ব্যবহার করুন `phi-4-mini` এর পরিবর্তে
- [ ] নোটবুক কার্নেল পুনরায় চালু করুন
- [ ] নোটবুক আউটপুট পরিষ্কার করুন এবং সব সেল পুনরায় চালান
- [ ] SDK পুনরায় ইনস্টল করুন: `pip install --upgrade --force-reinstall foundry-local-sdk`
- [ ] সিস্টেম পুনরায় চালু করুন (শেষ উপায়)

---

## প্রতিরোধমূলক টিপস

### সেরা অভ্যাস

1. **প্রথমে সার্ভিস পরীক্ষা করুন:**
   ```bash
   foundry service status
   ```

2. **ডিফল্টভাবে CPU ভ্যারিয়েন্ট ব্যবহার করুন:**
   ```python
   CATALOG = {
       'phi-4-mini-cpu': {...},
       'qwen2.5-0.5b-cpu': {...},
   }
   ```

3. **নোটবুক চালানোর আগে মডেল প্রি-লোড করুন:**
   ```bash
   foundry model run phi-4-mini
   foundry model run qwen2.5-3b
   ```

4. **সার্ভিস চালু রাখুন:**
   - অপ্রয়োজনীয়ভাবে সার্ভিস বন্ধ/চালু করবেন না
   - সেশনগুলোর মধ্যে এটি ব্যাকগ্রাউন্ডে চালু রাখুন

5. **রিসোর্স মনিটর করুন:**
   - নোটবুক চালানোর আগে GPU মেমোরি পরীক্ষা করুন
   - অপ্রয়োজনীয় GPU অ্যাপ্লিকেশন বন্ধ করুন
   - Task Manager / nvidia-smi ব্যবহার করুন

6. **নিয়মিত আপডেট করুন:**
   ```bash
   winget upgrade Microsoft.FoundryLocal
   pip install --upgrade foundry-local-sdk
   ```

---

**শেষ আপডেট:** ৮ অক্টোবর, ২০২৫

---

**অস্বীকৃতি**:  
এই নথিটি AI অনুবাদ পরিষেবা [Co-op Translator](https://github.com/Azure/co-op-translator) ব্যবহার করে অনুবাদ করা হয়েছে। আমরা যথাসাধ্য সঠিকতার জন্য চেষ্টা করি, তবে অনুগ্রহ করে মনে রাখবেন যে স্বয়ংক্রিয় অনুবাদে ত্রুটি বা অসঙ্গতি থাকতে পারে। মূল ভাষায় থাকা নথিটিকে প্রামাণিক উৎস হিসেবে বিবেচনা করা উচিত। গুরুত্বপূর্ণ তথ্যের জন্য, পেশাদার মানব অনুবাদ সুপারিশ করা হয়। এই অনুবাদ ব্যবহারের ফলে কোনো ভুল বোঝাবুঝি বা ভুল ব্যাখ্যা হলে আমরা দায়বদ্ধ থাকব না।