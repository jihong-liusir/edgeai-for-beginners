<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "ddaad917d0c16fc3d498a6b4eabc8088",
  "translation_date": "2025-10-09T09:51:02+00:00",
  "source_file": "Workshop/notebooks/quickstart.md",
  "language_code": "bn"
}
-->
# ওয়ার্কশপ নোটবুক - দ্রুত শুরু গাইড

## বিষয়সূচি

- [প্রয়োজনীয়তা](../../../../Workshop/notebooks)
- [প্রাথমিক সেটআপ](../../../../Workshop/notebooks)
- [সেশন ০৪: মডেল তুলনা](../../../../Workshop/notebooks)
- [সেশন ০৫: মাল্টি-এজেন্ট অর্কেস্ট্রেটর](../../../../Workshop/notebooks)
- [সেশন ০৬: উদ্দেশ্য-ভিত্তিক মডেল রাউটিং](../../../../Workshop/notebooks)
- [পরিবেশ ভেরিয়েবল](../../../../Workshop/notebooks)
- [সাধারণ কমান্ড](../../../../Workshop/notebooks)

---

## প্রয়োজনীয়তা

### ১. ফাউন্ড্রি লোকাল ইনস্টল করুন

**উইন্ডোজ:**
```bash
winget install Microsoft.FoundryLocal
```

**ম্যাকওএস:**
```bash
brew tap microsoft/foundrylocal
brew install foundrylocal
```

**ইনস্টলেশন যাচাই করুন:**
```bash
foundry --version
```

### ২. পাইথন ডিপেন্ডেন্সি ইনস্টল করুন

```bash
cd Workshop
pip install -r requirements.txt
```

অথবা আলাদাভাবে ইনস্টল করুন:
```bash
pip install foundry-local-sdk openai numpy requests
```

---

## প্রাথমিক সেটআপ

### ফাউন্ড্রি লোকাল সার্ভিস চালু করুন

**যেকোনো নোটবুক চালানোর আগে প্রয়োজনীয়:**

```bash
# Start the service
foundry service start

# Verify it's running
foundry service status
```

প্রত্যাশিত আউটপুট:
```
✅ Service started successfully
Endpoint: http://localhost:59959
```

### মডেল ডাউনলোড এবং লোড করুন

নোটবুকগুলো ডিফল্টভাবে এই মডেলগুলো ব্যবহার করে:

```bash
# Download models (first time only - may take several minutes)
foundry model download phi-4-mini
foundry model download qwen2.5-3b
foundry model download phi-3.5-mini
foundry model download qwen2.5-0.5b

# Load models into memory
foundry model run phi-4-mini
foundry model run qwen2.5-3b
foundry model run phi-3.5-mini
```

### সেটআপ যাচাই করুন

```bash
# List loaded models
foundry model ls

# Check service health
curl http://localhost:59959/v1/models
```

---

## সেশন ০৪: মডেল তুলনা

### উদ্দেশ্য
ছোট ভাষা মডেল (SLM) এবং বড় ভাষা মডেল (LLM)-এর পারফরম্যান্স তুলনা করুন।

### দ্রুত সেটআপ

```bash
# Start service (if not already running)
foundry service start

# Load required models
foundry model run phi-4-mini
foundry model run qwen2.5-3b
```

### নোটবুক চালানো

1. **খুলুন** `session04_model_compare.ipynb` VS Code বা Jupyter-এ
2. **কর্ণেল পুনরায় চালু করুন** (Kernel → Restart Kernel)
3. **সব সেল চালান** ক্রমানুসারে

### মূল কনফিগারেশন

**ডিফল্ট মডেল:**
- **SLM:** `phi-4-mini` (~4GB RAM, দ্রুত)
- **LLM:** `qwen2.5-3b` (~3GB RAM, মেমোরি-অপ্টিমাইজড)

**পরিবেশ ভেরিয়েবল (ঐচ্ছিক):**
```python
import os
os.environ['SLM_ALIAS'] = 'phi-4-mini'
os.environ['LLM_ALIAS'] = 'qwen2.5-3b'
os.environ['FOUNDRY_LOCAL_ENDPOINT'] = 'http://localhost:59959/v1'
```

### প্রত্যাশিত আউটপুট

```
================================================================================
COMPARISON SUMMARY
================================================================================
Alias                Latency(s)      Tokens     Route               
--------------------------------------------------------------------------------
phi-4-mini           1.234           150        chat.completions    
qwen2.5-3b           2.456           180        chat.completions    
================================================================================

💡 SLM is 1.99x faster than LLM for this prompt
```

### কাস্টমাইজেশন

**বিভিন্ন মডেল ব্যবহার করুন:**
```python
os.environ['SLM_ALIAS'] = 'phi-3.5-mini'
os.environ['LLM_ALIAS'] = 'qwen2.5-1.5b'
```

**কাস্টম প্রম্পট:**
```python
os.environ['COMPARE_PROMPT'] = 'Explain quantum computing in simple terms'
```

### যাচাই চেকলিস্ট

- [ ] সেল ১২ সঠিক মডেল দেখায় (phi-4-mini, qwen2.5-3b)
- [ ] সেল ১২ সঠিক এন্ডপয়েন্ট দেখায় (পোর্ট ৫৯৯৫৯)
- [ ] সেল ১৬ ডায়াগনস্টিক পাস করে (✅ সার্ভিস চালু আছে)
- [ ] সেল ২০ প্রি-ফ্লাইট চেক পাস করে (উভয় মডেল ঠিক আছে)
- [ ] সেল ২২ তুলনা সম্পন্ন হয় লেটেন্সি মান সহ
- [ ] সেল ২৪ যাচাই দেখায় 🎉 সব চেক পাস হয়েছে!

### সময়ের আনুমানিকতা
- **প্রথমবার চালানো:** ৫-১০ মিনিট (মডেল ডাউনলোড সহ)
- **পরবর্তী চালানো:** ১-২ মিনিট

---

## সেশন ০৫: মাল্টি-এজেন্ট অর্কেস্ট্রেটর

### উদ্দেশ্য
ফাউন্ড্রি লোকাল SDK ব্যবহার করে মাল্টি-এজেন্ট সহযোগিতা প্রদর্শন করুন - এজেন্টরা একসাথে কাজ করে উন্নত আউটপুট তৈরি করে।

### দ্রুত সেটআপ

```bash
# Start service
foundry service start

# Load models
foundry model run phi-4-mini  # Primary model
foundry model run qwen2.5-7b  # Optional: higher quality editor
```

### নোটবুক চালানো

1. **খুলুন** `session05_agents_orchestrator.ipynb`
2. **কর্ণেল পুনরায় চালু করুন**
3. **সব সেল চালান** ক্রমানুসারে

### মূল কনফিগারেশন

**ডিফল্ট সেটআপ (উভয় এজেন্টের জন্য একই মডেল):**
```python
PRIMARY_ALIAS = 'phi-4-mini'
EDITOR_ALIAS = 'phi-4-mini'  # Uses same model
```

**উন্নত সেটআপ (বিভিন্ন মডেল):**
```python
import os
os.environ['AGENT_MODEL_PRIMARY'] = 'phi-4-mini'     # Fast for research
os.environ['AGENT_MODEL_EDITOR'] = 'qwen2.5-7b'      # High quality for editing
```

### আর্কিটেকচার

```
User Question
    ↓
Researcher Agent (phi-4-mini)
  → Gathers bullet points
    ↓
Editor Agent (phi-4-mini or qwen2.5-7b)
  → Refines into executive summary
    ↓
Final Output
```

### প্রত্যাশিত আউটপুট

```
================================================================================
[Pipeline] Question: Explain why edge AI matters for compliance.
================================================================================

[Stage 1: Research]
Output: • Edge AI processes data locally, reducing transmission...

[Stage 2: Editorial Refinement]
Output: Executive Summary: Edge AI enhances compliance by keeping data...

[FINAL OUTPUT]
Executive Summary: Edge AI enhances compliance by keeping sensitive data 
on-premises and reduces latency through local processing.

[METADATA]
Models used: {'researcher': 'phi-4-mini', 'editor': 'phi-4-mini'}
```

### এক্সটেনশন

**আরও এজেন্ট যোগ করুন:**
```python
critic = Agent(
    name='Critic',
    system='Review content for accuracy',
    client=client,
    model_id=model_id
)
```

**ব্যাচ টেস্টিং:**
```python
test_questions = [
    "What are benefits of local AI?",
    "How does RAG improve accuracy?",
]

for q in test_questions:
    result = pipeline(q, verbose=False)
    print(result['final'])
```

### সময়ের আনুমানিকতা
- **প্রথমবার চালানো:** ৩-৫ মিনিট
- **পরবর্তী চালানো:** প্রতি প্রশ্নে ১-২ মিনিট

---

## সেশন ০৬: উদ্দেশ্য-ভিত্তিক মডেল রাউটিং

### উদ্দেশ্য
উদ্দেশ্য সনাক্ত করে বিশেষায়িত মডেলে প্রম্পট রাউট করুন।

### দ্রুত সেটআপ

```bash
# Start service
foundry service start

# Load all routing models (CPU variants recommended)
foundry model run phi-4-mini-cpu
foundry model run qwen2.5-0.5b-cpu
foundry model run phi-3.5-mini-cpu
```

**নোট:** সেশন ০৬ CPU মডেলগুলোতে ডিফল্ট থাকে সর্বাধিক সামঞ্জস্যতার জন্য।

### নোটবুক চালানো

1. **খুলুন** `session06_models_router.ipynb`
2. **কর্ণেল পুনরায় চালু করুন**
3. **সব সেল চালান** ক্রমানুসারে

### মূল কনফিগারেশন

**ডিফল্ট ক্যাটালগ (CPU মডেল):**
```python
CATALOG = {
    'phi-4-mini-cpu': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b-cpu': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini-cpu': {'capabilities':['code','refactor'],'priority':3},
}
```

**বিকল্প (GPU মডেল):**
```python
# Uncomment GPU catalog in Cell #6 if you have sufficient VRAM (8GB+)
CATALOG = {
    'phi-4-mini': {'capabilities':['general','summarize'],'priority':2},
    'qwen2.5-0.5b': {'capabilities':['classification','fast'],'priority':1},
    'phi-3.5-mini': {'capabilities':['code','refactor'],'priority':3},
}
```

### উদ্দেশ্য সনাক্তকরণ

রাউটার রেগেক্স প্যাটার্ন ব্যবহার করে উদ্দেশ্য সনাক্ত করে:

| উদ্দেশ্য | প্যাটার্ন উদাহরণ | রাউটেড টু |
|---------|------------------|-----------|
| `code` | "refactor", "implement function" | phi-3.5-mini-cpu |
| `classification` | "categorize", "classify this" | qwen2.5-0.5b-cpu |
| `summarize` | "summarize", "tl;dr" | phi-4-mini-cpu |
| `general` | অন্যান্য সব | phi-4-mini-cpu |

### প্রত্যাশিত আউটপুট

```
✓ Using CPU-optimized models (default configuration)
  Models: phi-4-mini-cpu, qwen2.5-0.5b-cpu, phi-3.5-mini-cpu

Routing prompts to specialized models...
============================================================

Prompt: Refactor this Python function for readability
  Intent: code           | Model: phi-3.5-mini-cpu
  Output: Here's a refactored version...
  Tokens: 156

Prompt: Categorize this email as urgent or normal
  Intent: classification | Model: qwen2.5-0.5b-cpu
  Output: Category: Normal
  Tokens: 45

✓ Success! All prompts routed correctly.
```

### কাস্টমাইজেশন

**কাস্টম উদ্দেশ্য যোগ করুন:**
```python
import re

# Add to RULES
RULES.append((re.compile('translate|翻译', re.I), 'translation'))

# Add capability to catalog
CATALOG['phi-4-mini-cpu']['capabilities'].append('translation')
```

**টোকেন ট্র্যাকিং সক্ষম করুন:**
```python
import os
os.environ['SHOW_USAGE'] = '1'
```

### GPU মডেলে স্যুইচ করা

যদি আপনার কাছে ৮GB+ VRAM থাকে:

1. **সেল #৬**-এ CPU ক্যাটালগ কমেন্ট করুন
2. GPU ক্যাটালগ আনকমেন্ট করুন
3. GPU মডেল লোড করুন:
   ```bash
   foundry model run phi-4-mini
   foundry model run qwen2.5-0.5b
   foundry model run phi-3.5-mini
   ```
4. কর্ণেল পুনরায় চালু করুন এবং নোটবুক পুনরায় চালান

### সময়ের আনুমানিকতা
- **প্রথমবার চালানো:** ৫-১০ মিনিট (মডেল লোডিং)
- **পরবর্তী চালানো:** প্রতি টেস্টে ৩০-৬০ সেকেন্ড

---

## পরিবেশ ভেরিয়েবল

### গ্লোবাল কনফিগারেশন

Jupyter/VS Code শুরু করার আগে সেট করুন:

**উইন্ডোজ (কমান্ড প্রম্পট):**
```cmd
set FOUNDRY_LOCAL_ENDPOINT=http://localhost:59959/v1
set SHOW_USAGE=1
set RETRY_ON_FAIL=1
```

**উইন্ডোজ (পাওয়ারশেল):**
```powershell
$env:FOUNDRY_LOCAL_ENDPOINT="http://localhost:59959/v1"
$env:SHOW_USAGE="1"
$env:RETRY_ON_FAIL="1"
```

**ম্যাকওএস/লিনাক্স:**
```bash
export FOUNDRY_LOCAL_ENDPOINT=http://localhost:59959/v1
export SHOW_USAGE=1
export RETRY_ON_FAIL=1
```

### নোটবুকের ভিতরে কনফিগারেশন

যেকোনো নোটবুকের শুরুতে সেট করুন:

```python
import os

# Foundry Local configuration
os.environ['FOUNDRY_LOCAL_ENDPOINT'] = 'http://localhost:59959/v1'

# Model selection
os.environ['SLM_ALIAS'] = 'phi-4-mini'
os.environ['LLM_ALIAS'] = 'qwen2.5-3b'

# Agent models
os.environ['AGENT_MODEL_PRIMARY'] = 'phi-4-mini'
os.environ['AGENT_MODEL_EDITOR'] = 'qwen2.5-7b'

# Debugging
os.environ['SHOW_USAGE'] = '1'       # Show token usage
os.environ['RETRY_ON_FAIL'] = '1'    # Enable retries
os.environ['RETRY_BACKOFF'] = '2.0'  # Retry delay
```

---

## সাধারণ কমান্ড

### সার্ভিস ম্যানেজমেন্ট

```bash
# Start service
foundry service start

# Check status
foundry service status

# Stop service
foundry service stop

# View logs
foundry service logs
```

### মডেল ম্যানেজমেন্ট

```bash
# List all available models in catalog
foundry model catalog

# List loaded models
foundry model ls

# Download a model
foundry model download phi-4-mini

# Load a model
foundry model run phi-4-mini

# Unload a model
foundry model unload phi-4-mini

# Remove a model
foundry model remove phi-4-mini

# Get model info
foundry model info phi-4-mini
```

### এন্ডপয়েন্ট টেস্টিং

```bash
# Check service health
curl http://localhost:59959/health

# List available models via API
curl http://localhost:59959/v1/models

# Test model completion
curl http://localhost:59959/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "phi-4-mini",
    "messages": [{"role":"user","content":"Hello"}],
    "max_tokens": 50
  }'
```

### ডায়াগনস্টিক কমান্ড

```bash
# Check everything
foundry --version
foundry service status
foundry model ls
foundry device info

# GPU status (NVIDIA)
nvidia-smi

# NPU status (Qualcomm)
foundry device info
```

---

## সেরা অনুশীলন

### যেকোনো নোটবুক শুরু করার আগে

1. **সার্ভিস চালু আছে কিনা দেখুন:**
   ```bash
   foundry service status
   ```

2. **মডেল লোড হয়েছে কিনা যাচাই করুন:**
   ```bash
   foundry model ls
   ```

3. **নোটবুক কর্ণেল পুনরায় চালু করুন** যদি পুনরায় চালান

4. **সব আউটপুট মুছুন** একটি পরিষ্কার রান নিশ্চিত করতে

### রিসোর্স ম্যানেজমেন্ট

1. **ডিফল্টভাবে CPU মডেল ব্যবহার করুন** সামঞ্জস্যতার জন্য
2. **GPU মডেলে স্যুইচ করুন** যদি আপনার কাছে ৮GB+ VRAM থাকে
3. **GPU অ্যাপ্লিকেশন বন্ধ করুন** চালানোর আগে
4. **সার্ভিস চালু রাখুন** নোটবুক সেশনের মধ্যে
5. **রিসোর্স ব্যবহার পর্যবেক্ষণ করুন** Task Manager / nvidia-smi দিয়ে

### সমস্যা সমাধান

1. **প্রথমে সার্ভিস চেক করুন** কোড ডিবাগ করার আগে
2. **কর্ণেল পুনরায় চালু করুন** যদি পুরনো কনফিগারেশন দেখেন
3. **ডায়াগনস্টিক সেল পুনরায় চালান** যেকোনো পরিবর্তনের পরে
4. **মডেল নাম যাচাই করুন** যা লোড করা হয়েছে তার সাথে মিলে কিনা
5. **এন্ডপয়েন্ট পোর্ট যাচাই করুন** সার্ভিস স্ট্যাটাসের সাথে মিলে কিনা

---

## দ্রুত রেফারেন্স: মডেল এলিয়াস

### সাধারণ মডেল

| এলিয়াস | সাইজ | সেরা ব্যবহার | RAM/VRAM | ভ্যারিয়েন্ট |
|---------|------|--------------|----------|--------------|
| `phi-4-mini` | ~4B | সাধারণ চ্যাট, সারাংশ তৈরি | ৪-৬GB | `-cpu`, `-cuda-gpu`, `-npu` |
| `phi-3.5-mini` | ~3.5B | কোড জেনারেশন, রিফ্যাক্টরিং | ৩-৫GB | `-cpu`, `-cuda-gpu`, `-npu` |
| `qwen2.5-3b` | ~3B | সাধারণ কাজ, দক্ষ | ৩-৪GB | `-cpu`, `-cuda-gpu` |
| `qwen2.5-1.5b` | ~1.5B | দ্রুত, কম রিসোর্স | ২-৩GB | `-cpu`, `-cuda-gpu` |
| `qwen2.5-0.5b` | ~0.5B | শ্রেণীবিভাগ, ন্যূনতম রিসোর্স | ১-২GB | `-cpu`, `-cuda-gpu` |

### ভ্যারিয়েন্ট নামকরণ

- **বেস নাম** (যেমন, `phi-4-mini`): আপনার হার্ডওয়্যারের জন্য সেরা ভ্যারিয়েন্ট স্বয়ংক্রিয়ভাবে নির্বাচন করে
- **`-cpu`**: CPU-অপ্টিমাইজড, সর্বত্র কাজ করে
- **`-cuda-gpu`**: NVIDIA GPU অপ্টিমাইজড, ৮GB+ VRAM প্রয়োজন
- **`-npu`**: Qualcomm NPU অপ্টিমাইজড, NPU ড্রাইভার প্রয়োজন

**প্রস্তাবনা:** বেস নাম ব্যবহার করুন (সাফিক্স ছাড়া) এবং ফাউন্ড্রি লোকাল সেরা ভ্যারিয়েন্ট স্বয়ংক্রিয়ভাবে নির্বাচন করতে দিন।

---

## সফলতার সূচক

আপনি প্রস্তুত যখন দেখবেন:

✅ `foundry service status` "running" দেখায়  
✅ `foundry model ls` আপনার প্রয়োজনীয় মডেল দেখায়  
✅ সার্ভিস সঠিক এন্ডপয়েন্টে অ্যাক্সেসযোগ্য  
✅ হেলথ চেক ২০০ OK ফেরত দেয়  
✅ নোটবুক ডায়াগনস্টিক সেল পাস করে  
✅ আউটপুটে কোনো সংযোগ ত্রুটি নেই  

---

## সাহায্য পাওয়া

### ডকুমেন্টেশন
- **মেইন রিপোজিটরি**: https://github.com/microsoft/Foundry-Local  
- **পাইথন SDK**: https://github.com/microsoft/Foundry-Local/tree/main/sdk/python  
- **CLI রেফারেন্স**: https://github.com/microsoft/Foundry-Local/blob/main/docs/reference/reference-cli.md  
- **সমস্যা সমাধান**: এই ডিরেক্টরির `troubleshooting.md` দেখুন  

### গিটহাব ইস্যু
- https://github.com/microsoft/Foundry-Local/issues  
- https://github.com/microsoft/edgeai-for-beginners/issues  

---

**শেষ আপডেট:** অক্টোবর ৮, ২০২৫  
**ভার্সন:** ওয়ার্কশপ নোটবুক ২.০  

---

**অস্বীকৃতি**:  
এই নথিটি AI অনুবাদ পরিষেবা [Co-op Translator](https://github.com/Azure/co-op-translator) ব্যবহার করে অনুবাদ করা হয়েছে। আমরা যথাসম্ভব সঠিক অনুবাদের চেষ্টা করি, তবে অনুগ্রহ করে মনে রাখবেন যে স্বয়ংক্রিয় অনুবাদে ত্রুটি বা অসঙ্গতি থাকতে পারে। মূল ভাষায় লেখা নথিটিকেই প্রামাণিক উৎস হিসেবে বিবেচনা করা উচিত। গুরুত্বপূর্ণ তথ্যের জন্য পেশাদার মানব অনুবাদ ব্যবহার করার পরামর্শ দেওয়া হচ্ছে। এই অনুবাদ ব্যবহারের ফলে সৃষ্ট কোনো ভুল বোঝাবুঝি বা ভুল ব্যাখ্যার জন্য আমরা দায়ী নই।