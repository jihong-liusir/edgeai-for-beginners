<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "48d0fb38be925084a6ebd957d4b045e5",
  "translation_date": "2025-10-08T12:11:16+00:00",
  "source_file": "Workshop/Readme.md",
  "language_code": "my"
}
-->
# EdgeAI အတွက် အခြေခံသင်တန်း - Workshop

> **ထုတ်လုပ်မှုအဆင့် Edge AI အက်ပလီကေးရှင်းများ တည်ဆောက်ရန် လက်တွေ့လေ့လာရေးလမ်းကြောင်း**
>
> Microsoft Foundry Local ကို အသုံးပြု၍ ပထမဆုံး chat completion မှ multi-agent orchestration အထိ ၆ ခုသော အဆင့်ဆင့် session များတွင် ဒေသခံ AI deployment ကို ကျွမ်းကျင်ပါ။

---

## 🎯 အကျဉ်းချုပ်

**EdgeAI အတွက် အခြေခံသင်တန်း Workshop** သို့ ကြိုဆိုပါသည်။ ဒေသခံ hardware ပေါ်တွင် အပြည့်အဝ လည်ပတ်နိုင်သော ဉာဏ်ရည်ရှိသော အက်ပလီကေးရှင်းများ တည်ဆောက်ရန် လက်တွေ့လမ်းညွှန်ဖြစ်သည်။ ဒီ workshop သည် Microsoft Foundry Local နှင့် Small Language Models (SLMs) ကို အသုံးပြု၍ Edge AI အယူအဆများကို လက်တွေ့ကျကျ ကျွမ်းကျင်မှုများအဖြစ် ပြောင်းလဲပေးပါသည်။

### ဒီ Workshop ကို ဘာကြောင့် လိုအပ်သလဲ?

**Edge AI တိုးတက်မှုက စတင်နေပြီ**

ကမ္ဘာတစ်ဝှမ်းရှိ အဖွဲ့အစည်းများသည် cloud မှာ အခြေခံထားသော AI မှ edge computing သို့ ပြောင်းလဲနေကြသည်။ အဓိကအကြောင်းရင်း ၃ ခုမှာ -

1. **Privacy & Compliance** - အရေးကြီးသော ဒေတာများကို cloud သို့ ပို့ဆောင်ခြင်းမရှိဘဲ ဒေသတွင်ပင် လုပ်ဆောင်ခြင်း (HIPAA, GDPR, ငွေကြေးဆိုင်ရာ စည်းမျဉ်းများ)
2. **Performance** - network latency ကို ဖယ်ရှားခြင်း (ဒေသတွင် 50-500ms vs cloud round-trip 500-2000ms)
3. **Cost Control** - per-token API ကုန်ကျစရိတ်များကို ဖယ်ရှားပြီး cloud ကုန်ကျစရိတ်မရှိဘဲ scale လုပ်နိုင်ခြင်း

**Edge AI သည် ကွဲပြားခြားနားသည်**

On-premises AI ကို လည်ပတ်ရန် ကျွမ်းကျင်မှုအသစ်များ လိုအပ်သည် -
- အရင်းအမြစ်ကန့်သတ်ချက်များအတွက် မော်ဒယ်ရွေးချယ်ခြင်းနှင့် optimization
- ဒေသခံ service စီမံခန့်ခွဲမှုနှင့် hardware acceleration
- Smaller models အတွက် prompt engineering
- Edge devices အတွက် production deployment patterns

**ဒီ Workshop သည် အဆိုပါ ကျွမ်းကျင်မှုများကို ပေးစွမ်းသည်**

6 ခုသော အဓိက session များ (~3 နာရီ စုစုပေါင်း) တွင် "Hello World" မှ production-ready multi-agent systems ကို သင်တန်းသား၏ စက်ပေါ်တွင် ဒေသခံအဖြစ် လည်ပတ်စေမည်။

---

## 📚 သင်ယူရမည့် ရည်မှန်းချက်များ

ဒီ workshop ကို ပြီးမြောက်ပါက သင်တန်းသားသည် အောက်ပါများကို လုပ်ဆောင်နိုင်မည်ဖြစ်သည် -

### အဓိက ကျွမ်းကျင်မှုများ
1. **ဒေသခံ AI Services ကို Deploy နှင့် စီမံခန့်ခွဲခြင်း**
   - Microsoft Foundry Local ကို install နှင့် configure လုပ်ခြင်း
   - Edge deployment အတွက် သင့်လျော်သော မော်ဒယ်များ ရွေးချယ်ခြင်း
   - မော်ဒယ် lifecycle ကို စီမံခန့်ခွဲခြင်း (download, load, cache)
   - အရင်းအမြစ်အသုံးပြုမှုကို စောင့်ကြည့်ပြီး performance ကို optimize လုပ်ခြင်း

2. **AI-Powered Applications တည်ဆောက်ခြင်း**
   - OpenAI-compatible chat completions ကို ဒေသတွင် လုပ်ဆောင်ခြင်း
   - Small Language Models အတွက် ထိရောက်သော prompts ကို ဒီဇိုင်းဆွဲခြင်း
   - UX အတွက် streaming responses ကို ကိုင်တွယ်ခြင်း
   - ဒေသခံမော်ဒယ်များကို ရှိပြီးသား အက်ပလီကေးရှင်းများနှင့် ပေါင်းစပ်ခြင်း

3. **RAG (Retrieval Augmented Generation) Systems တည်ဆောက်ခြင်း**
   - Embeddings ဖြင့် semantic search တည်ဆောက်ခြင်း
   - LLM responses ကို domain-specific knowledge တွင် အခြေခံခြင်း
   - RAG quality ကို စက်မှုစံချိန်များဖြင့် အကဲဖြတ်ခြင်း
   - Prototype မှ production သို့ scale လုပ်ခြင်း

4. **မော်ဒယ် performance ကို optimize လုပ်ခြင်း**
   - သင့်အသုံးအတွက် မော်ဒယ်များကို benchmark လုပ်ခြင်း
   - latency, throughput, နှင့် first-token time ကို တိုင်းတာခြင်း
   - speed/quality tradeoffs အပေါ် အကောင်းဆုံး မော်ဒယ်များ ရွေးချယ်ခြင်း
   - SLM vs LLM trade-offs ကို လက်တွေ့အခြေအနေများတွင် နှိုင်းယှဉ်ခြင်း

5. **Multi-Agent Systems ကို စီမံခန့်ခွဲခြင်း**
   - အလုပ်အမျိုးမျိုးအတွက် အထူး agent များ ဒီဇိုင်းဆွဲခြင်း
   - Agent memory နှင့် context ကို စီမံခန့်ခွဲခြင်း
   - ရှုပ်ထွေးသော workflow များတွင် agent များကို coordinate လုပ်ခြင်း
   - မော်ဒယ်များအကြား requests ကို အကျိုးရှိစွာ route လုပ်ခြင်း

6. **Production-Ready Solutions ကို Deploy လုပ်ခြင်း**
   - Error handling နှင့် retry logic ကို implement လုပ်ခြင်း
   - Token usage နှင့် system resources ကို စောင့်ကြည့်ခြင်း
   - Model-as-tools patterns ဖြင့် scalable architectures တည်ဆောက်ခြင်း
   - Edge မှ hybrid (edge + cloud) သို့ ပြောင်းလဲမှုလမ်းကြောင်းများကို စီစဉ်ခြင်း

---

## 🎓 သင်ယူရမည့် ရလဒ်များ

### သင်တန်းသား တည်ဆောက်မည့် အရာများ

Workshop ပြီးဆုံးချိန်တွင် သင်တန်းသားသည် အောက်ပါများကို တည်ဆောက်ထားမည်ဖြစ်သည် -

| Session | Deliverable | Skills Demonstrated |
|---------|-------------|---------------------|
| **1** | Streaming ဖြင့် chat application | Service setup, basic completions, streaming UX |
| **2** | RAG system with evaluation | Embeddings, semantic search, quality metrics |
| **3** | Multi-model benchmark suite | Performance measurement, model comparison |
| **4** | SLM vs LLM comparator | Trade-off analysis, optimization strategies |
| **5** | Multi-agent orchestrator | Agent design, memory management, coordination |
| **6** | Intelligent routing system | Intent detection, model selection, scalability |

### ကျွမ်းကျင်မှု အဆင့်ဇယား

| Skill Level | Session 1-2 | Session 3-4 | Session 5-6 |
|-------------|-------------|-------------|-------------|
| **Beginner** | ✅ Setup & basics | ⚠️ Challenging | ❌ Too advanced |
| **Intermediate** | ✅ Quick review | ✅ Core learning | ⚠️ Stretch goals |
| **Advanced** | ✅ Breeze through | ✅ Refinement | ✅ Production patterns |

### အလုပ်အကိုင်အတွက် အသင့်ဖြစ်သော ကျွမ်းကျင်မှုများ

**ဒီ workshop ပြီးဆုံးပါက သင်တန်းသားသည် အောက်ပါများကို လုပ်ဆောင်နိုင်မည် -**

✅ **Privacy-First Applications တည်ဆောက်ခြင်း**
- PHI/PII ကို ဒေသတွင် လုပ်ဆောင်သော Healthcare apps
- Compliance လိုအပ်ချက်များနှင့် ငွေကြေးဆိုင်ရာ ဝန်ဆောင်မှုများ
- ဒေတာအာဏာပိုင်အခြေခံသော အစိုးရစနစ်များ

✅ **Edge Environments အတွက် Optimize လုပ်ခြင်း**
- အရင်းအမြစ်ကန့်သတ်ထားသော IoT devices
- Offline-first mobile applications
- Low-latency real-time systems

✅ **Intelligent Architectures ကို ဒီဇိုင်းဆွဲခြင်း**
- ရှုပ်ထွေးသော workflow များအတွက် Multi-agent systems
- Hybrid edge-cloud deployments
- ကုန်ကျစရိတ်ကို optimize လုပ်ထားသော AI infrastructure

✅ **Edge AI Initiatives ကို ဦးဆောင်ခြင်း**
- Project များအတွက် Edge AI feasibility ကို အကဲဖြတ်ခြင်း
- သင့်လျော်သော မော်ဒယ်များနှင့် frameworks ကို ရွေးချယ်ခြင်း
- Scalable local AI solutions ကို architect လုပ်ခြင်း

---

## 🗺️ Workshop ဖွဲ့စည်းမှု

### Session အကျဉ်းချုပ် (6 Sessions × 30 မိနစ် = 3 နာရီ)

| Session | Topic | Focus | Duration |
|---------|-------|-------|----------|
| **1** | Foundry Local ဖြင့် စတင်ခြင်း | Install, validate, first completions | 30 min |
| **2** | RAG ဖြင့် AI Solutions တည်ဆောက်ခြင်း | Prompt engineering, embeddings, evaluation | 30 min |
| **3** | Open Source Models | Model discovery, benchmarking, selection | 30 min |
| **4** | Cutting Edge Models | SLM vs LLM, optimization, frameworks | 30 min |
| **5** | AI-Powered Agents | Agent design, orchestration, memory | 30 min |
| **6** | Models as Tools | Routing, chaining, scaling strategies | 30 min |

---

## 🚀 အမြန်စတင်ခြင်း

### လိုအပ်ချက်များ

**System Requirements:**
- **OS**: Windows 10/11, macOS 11+, or Linux (Ubuntu 20.04+)
- **RAM**: အနည်းဆုံး 8GB, အကြံပြု 16GB+
- **Storage**: မော်ဒယ်များအတွက် အခမဲ့နေရာ 10GB+
- **CPU**: AVX2 support ပါသော နောက်ဆုံးပေါ် processor
- **GPU** (optional): CUDA-compatible သို့မဟုတ် Qualcomm NPU acceleration

**Software Requirements:**
- **Python 3.8+** ([Download](https://www.python.org/downloads/))
- **Microsoft Foundry Local** ([Installation Guide](../../../Workshop))
- **Git** ([Download](https://git-scm.com/downloads))
- **Visual Studio Code** (အကြံပြု) ([Download](https://code.visualstudio.com/))

### 3 ခြေလှမ်းဖြင့် Setup

#### 1. Foundry Local ကို Install လုပ်ပါ

**Windows:**
```powershell
winget install Microsoft.FoundryLocal
```

**macOS:**
```bash
brew tap microsoft/foundrylocal
brew install foundrylocal
```

**Verify Installation:**
```bash
foundry --version
foundry service status
```

#### 2. Repository ကို Clone လုပ်ပြီး Dependencies ကို Install လုပ်ပါ

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

#### 3. သင့်ပထမဆုံး Sample ကို Run လုပ်ပါ

```bash
# Start Foundry Local and load a model
foundry model run phi-4-mini

# Run the chat bootstrap sample
cd samples/session01
python chat_bootstrap.py "What is edge AI?"
```

**✅ Success!** Edge AI အကြောင်း streaming response ကို တွေ့ရမည်။

---

## 📦 Workshop Resources

### Python Samples

အဓိကအယူအဆများကို သရုပ်ပြသော လက်တွေ့လေ့လာရေး ဥပမာများ -

| Session | Sample | Description | Run Time |
|---------|--------|-------------|----------|
| 1 | [`chat_bootstrap.py`](../../../Workshop/samples/session01/chat_bootstrap.py) | Basic & streaming chat | ~30s |
| 2 | [`rag_pipeline.py`](../../../Workshop/samples/session02/rag_pipeline.py) | RAG with embeddings | ~45s |
| 2 | [`rag_eval_ragas.py`](../../../Workshop/samples/session02/rag_eval_ragas.py) | RAG quality evaluation | ~60s |
| 3 | [`benchmark_oss_models.py`](../../../Workshop/samples/session03/benchmark_oss_models.py) | Multi-model benchmarking | ~2-3m |
| 4 | [`model_compare.py`](../../../Workshop/samples/session04/model_compare.py) | SLM vs LLM comparison | ~45s |
| 5 | [`agents_orchestrator.py`](../../../Workshop/samples/session05/agents_orchestrator.py) | Multi-agent system | ~60s |
| 6 | [`models_router.py`](../../../Workshop/samples/session06/models_router.py) | Intent-based routing | ~45s |
| 6 | [`models_pipeline.py`](../../../Workshop/samples/session06/models_pipeline.py) | Multi-step pipeline | ~60s |

### Jupyter Notebooks

ရှင်းလင်းချက်များနှင့် visualization များပါသော interactive exploration -

| Session | Notebook | Description | Difficulty |
|---------|----------|-------------|------------|
| 1 | [`session01_chat_bootstrap.ipynb`](./notebooks/session01_chat_bootstrap.ipynb) | Chat basics & streaming | ⭐ Beginner |
| 2 | [`session02_rag_pipeline.ipynb`](./notebooks/session02_rag_pipeline.ipynb) | Build RAG system | ⭐⭐ Intermediate |
| 2 | [`session02_rag_eval_ragas.ipynb`](./notebooks/session02_rag_eval_ragas.ipynb) | Evaluate RAG quality | ⭐⭐ Intermediate |
| 3 | [`session03_benchmark_oss_models.ipynb`](./notebooks/session03_benchmark_oss_models.ipynb) | Model benchmarking | ⭐⭐ Intermediate |
| 4 | [`session04_model_compare.ipynb`](./notebooks/session04_model_compare.ipynb) | Model comparison | ⭐⭐ Intermediate |
| 5 | [`session05_agents_orchestrator.ipynb`](./notebooks/session05_agents_orchestrator.ipynb) | Agent orchestration | ⭐⭐⭐ Advanced |
| 6 | [`session06_models_router.ipynb`](./notebooks/session06_models_router.ipynb) | Intent routing | ⭐⭐⭐ Advanced |
| 6 | [`session06_models_pipeline.ipynb`](./notebooks/session06_models_pipeline.ipynb) | Pipeline orchestration | ⭐⭐⭐ Advanced |

### Documentation

လမ်းညွှန်များနှင့် ရည်ညွှန်းချက်များ -

| Document | Description | Use When |
|----------|-------------|----------|
| [QUICK_START.md](./QUICK_START.md) | Fast-track setup guide | Starting from scratch |
| [QUICK_REFERENCE.md](./QUICK_REFERENCE.md) | Command & API cheat sheet | Need quick answers |
| [FOUNDRY_SDK_QUICKREF.md](./FOUNDRY_SDK_QUICKREF.md) | SDK patterns & examples | Writing code |
| [ENV_CONFIGURATION.md](./ENV_CONFIGURATION.md) | Environment variable guide | Configuring samples |
| [SAMPLES_UPDATE_SUMMARY.md](./SAMPLES_UPDATE_SUMMARY.md) | Latest sample improvements | Understanding changes |
| [SDK_MIGRATION_NOTES.md](./SDK_MIGRATION_NOTES.md) | Migration guide | Upgrading code |
| [notebooks/TROUBLESHOOTING.md](./notebooks/TROUBLESHOOTING.md) | Common issues & fixes | Debugging problems |

---

## 🎓 သင်ယူရေးလမ်းကြောင်း အကြံပြုချက်များ

### Beginner များအတွက် (3-4 နာရီ)
1. ✅ Session 1: စတင်ခြင်း (setup နှင့် basic chat အပေါ် အာရုံစိုက်ပါ)
2. ✅ Session 2: RAG Basics (evaluation ကို စတင်ချိန်တွင် ကျော်သွားပါ)
3. ✅ Session 3: ရိုးရှင်းသော Benchmarking (မော်ဒယ် 2 ခုသာ)
4. ⏭️ Session 4-6 ကို ယာယီ ကျော်သွားပါ
5. 🔄 ပထမဆုံး application တည်ဆောက်ပြီးနောက် Session 4-6 သို့ ပြန်လာပါ

### Intermediate Developer များအတွက် (3 နာရီ)
1. ⚡ Session 1: Setup validation ကို အမြန်ပြုလုပ်ပါ
2. ✅ Session 2: RAG pipeline ကို evaluation ဖြင့် ပြည့်စုံစွာ ပြုလုပ်ပါ
3. ✅ Session 3: Benchmarking suite အပြည့်အစုံ
4. ✅ Session 4: Model optimization
5. ✅ Session 5-6: Architecture patterns အပေါ် အာရုံစိုက်ပါ

### Advanced Practitioners များအတွက် (2-3 နာရီ)
1. ⚡ Session 1-3: အမြန်ပြုလုပ်ပြီး validation
2. ✅ Session 4: Optimization deep-dive
3. ✅ Session 5: Multi-agent architecture
4. ✅ Session 6: Production patterns နှင့် scaling
5. 🚀 Extend: Custom routing logic နှင့် hybrid deployments တည်ဆောက်ပါ

---

## Workshop Session Pack (30 မိနစ် အချိန်တို Labs)

Condensed 6-session workshop format ကို လိုက်နာပါက အောက်ပါ dedicated guides များကို အသုံးပြုပါ (တစ်ခုချင်းစီသည် module docs များနှင့် အပြည့်အဝ လိုက်ဖက်သည်) -

| Workshop Session | Guide | Core Focus |
|------------------|-------|------------|
| 1 | [Session01-GettingStartedFoundryLocal](./Session01-GettingStartedFoundryLocal.md) | Install, validate, run phi & GPT-OSS-20B, acceleration |
| 2 | [Session02-BuildAISolutionsRAG](./Session02-BuildAISolutionsRAG.md) | Prompt engineering, RAG patterns, CSV & document grounding, migration |
| 3 | [Session03-OpenSourceModels](./Session03-OpenSourceModels.md) | Hugging Face integration, benchmarking, model selection |
| 4 | [Session04-CuttingEdgeModels](./Session04-CuttingEdgeModels.md) | SLM vs LLM, WebGPU, Chainlit RAG, ONNX acceleration |
| 5 | [Session05-AIPoweredAgents](./Session05-AIPoweredAgents.md) | Agent roles, memory, tools, orchestration |
| 6 | [Session06-ModelsAsTools](./Session06-ModelsAsTools.md) | Routing, chaining, scaling path to Azure |
တစ်ခုချင်းစီသော session ဖိုင်တွင် ပါဝင်သောအရာများမှာ- အကျဉ်းချုပ်၊ သင်ယူရမည့်ရည်မှန်းချက်များ၊ ၃၀ မိနစ်အတွင်း ပြသမှုစဉ်၊ စတင်ရန်ပရိုဂရမ်၊ အတည်ပြုစာရင်း၊ ပြဿနာဖြေရှင်းခြင်းနှင့် Foundry Local Python SDK အတည်ပြုချက်များကို ရည်ညွှန်းခြင်းတို့ဖြစ်ပါသည်။

### နမူနာ Scripts

Workshop အတွက်လိုအပ်သော dependencies များကို ထည့်သွင်းရန် (Windows):

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

Foundry Local service ကို macOS မှ Windows သို့မဟုတ် VM တစ်ခုအခြားတွင် လည်ပတ်နေစဉ် endpoint ကို export လုပ်ရန်:

```bash
export FOUNDRY_LOCAL_ENDPOINT=http://<windows-host>:5273/v1
```

| Session | Script(s) | ဖော်ပြချက် |
|---------|-----------|-------------|
| 1 | `samples/session01/chat_bootstrap.py` | Bootstrap service & streaming chat |
| 2 | `samples/session02/rag_pipeline.py` | အနည်းဆုံး RAG (in-memory embeddings) |
|   | `samples/session02/rag_eval_ragas.py` | RAG အကဲဖြတ်မှု ragas metrics ဖြင့် |
| 3 | `samples/session03/benchmark_oss_models.py` | Multi-model latency & throughput benchmarking |
| 4 | `samples/session04/model_compare.py` | SLM နှင့် LLM နှိုင်းယှဉ်မှု (latency & sample output) |
| 5 | `samples/session05/agents_orchestrator.py` | Two‑agent research → editorial pipeline |
| 6 | `samples/session06/models_router.py` | Intent-based routing demo |
|   | `samples/session06/models_pipeline.py` | Multi-step plan/execute/refine chain |

### ပတ်ဝန်းကျင် Variables (နမူနာများအတွက် အများအားဖြင့်)

| Variable | ရည်ရွယ်ချက် | နမူနာ |
|----------|---------|---------|
| `FOUNDRY_LOCAL_ALIAS` | အခြေခံနမူနာများအတွက် ပုံမှန် single model alias | `phi-4-mini` |
| `SLM_ALIAS` / `LLM_ALIAS` | SLM နှင့် LLM ကြီးကြီးမားမားများကို နှိုင်းယှဉ်ရန် | `phi-4-mini` / `gpt-oss-20b` |
| `BENCH_MODELS` | Benchmark အတွက် aliases များကို comma ဖြင့် ဖော်ပြရန် | `qwen2.5-0.5b,gemma-2-2b,mistral-7b` |
| `BENCH_ROUNDS` | Model တစ်ခုစီအတွက် Benchmark ပြန်လည်လုပ်ဆောင်မှု | `3` |
| `BENCH_PROMPT` | Benchmarking တွင် အသုံးပြုသော Prompt | `Explain retrieval augmented generation briefly.` |
| `EMBED_MODEL` | Sentence-transformers embedding model | `sentence-transformers/all-MiniLM-L6-v2` |
| `RAG_QUESTION` | RAG pipeline အတွက် စမ်းသပ်မေးခွန်းကို override လုပ်ရန် | `Why use RAG with local inference?` |
| `AGENT_QUESTION` | Agents pipeline query ကို override လုပ်ရန် | `Explain why edge AI matters for compliance.` |
| `AGENT_MODEL_PRIMARY` | Research agent အတွက် Model alias | `phi-4-mini` |
| `AGENT_MODEL_EDITOR` | Editor agent အတွက် Model alias (ကွဲပြားနိုင်သည်) | `gpt-oss-20b` |
| `SHOW_USAGE` | `1` ဖြစ်ပါက, token အသုံးပြုမှုကို ပြသမည် | `1` |
| `RETRY_ON_FAIL` | `1` ဖြစ်ပါက, transient chat errors တွင် တစ်ကြိမ်ပြန်လည်ကြိုးစားမည် | `1` |
| `RETRY_BACKOFF` | ပြန်လည်ကြိုးစားမည့်အချိန် (စက္ကန့်) | `1.0` |

Variable များကို မသတ်မှတ်ထားပါက, scripts များသည် ပုံမှန် default များကို fallback လုပ်ပါမည်။ Single‑model demos များအတွက် သင်သည် `FOUNDRY_LOCAL_ALIAS` ကိုသာ လိုအပ်ပါသည်။

### Utility Module

နမူနာအားလုံးသည် ယခု `samples/workshop_utils.py` helper ကို မျှဝေထားပြီး:

* Cached `FoundryLocalManager` + OpenAI client ဖန်တီးခြင်း
* `chat_once()` helper (optional retry + usage printing ပါဝင်သည်)
* ရိုးရှင်းသော token usage အစီရင်ခံချက် (enable via `SHOW_USAGE=1`)

ဤအရာသည် ထပ်တူထပ်မျှဖြစ်မှုများကို လျှော့ချပြီး, efficient local model orchestration အတွက် အကောင်းဆုံးလေ့ကျင့်မှုများကို အထူးပြုထားသည်။

## Optional Enhancements (Cross-Session)

| အဓိကအကြောင်းအရာ | တိုးတက်မှု | Sessions | Env / Toggle |
|--------------------|-----------|----------|--------------|
| Determinism | Fixed temperature + stable prompt sets | 1–6 | Set `temperature=0`, `top_p=1` |
| Token Usage Visibility | အကျိုးကျေးဇူး/ထိရောက်မှု သင်ကြားမှု | 1–6 | `SHOW_USAGE=1` |
| Streaming First Token | Perceived latency metric | 1,3,4,6 | `BENCH_STREAM=1` (benchmark) |
| Retry Resilience | Transient cold-start ကို ကိုင်တွယ်ခြင်း | All | `RETRY_ON_FAIL=1` + `RETRY_BACKOFF` |
| Multi-Model Agents | Heterogeneous role specialization | 5 | `AGENT_MODEL_PRIMARY`, `AGENT_MODEL_EDITOR` |
| Adaptive Routing | Intent + cost heuristics | 6 | Extend router with escalation logic |
| Vector Memory | Long-term semantic recall | 2,5,6 | Integrate FAISS/Chroma embedding index |
| Trace Export | Auditing & evaluation | 2,5,6 | Append JSON lines per step |
| Quality Rubrics | Qualitative tracking | 3–6 | Secondary scoring prompts |
| Smoke Tests | Workshop မတိုင်မီ အတည်ပြုမှု | All | `python Workshop/tests/smoke.py` |

### Deterministic Quick Start

```powershell
set FOUNDRY_LOCAL_ALIAS=phi-4-mini
set SHOW_USAGE=1
python Workshop\tests\smoke.py
```

တူညီသော input များကို ထပ်ခါတလဲလဲ ထည့်သွင်းခြင်းဖြင့် တည်ငြိမ်သော token အရေအတွက်ကို မျှော်လင့်ပါ။

### RAG အကဲဖြတ်မှု (Session 2)

`rag_eval_ragas.py` ကို အသုံးပြု၍ အလွန်သေးငယ်သော synthetic dataset တွင် အဖြေတိကျမှု၊ သစ္စာရှိမှုနှင့် အကြောင်းအရာတိကျမှုတို့ကိုတွက်ချက်ပါ:

```powershell
python samples/session02/rag_eval_ragas.py
```

မေးခွန်းများ၊ အကြောင်းအရာများနှင့် ground truths များပါဝင်သော JSONL ကြီးကို ထည့်သွင်းခြင်းဖြင့် တိုးချဲ့ပြီး, ထို့နောက် Hugging Face `Dataset` သို့ ပြောင်းလဲပါ။

## CLI Command Accuracy Appendix

Workshop သည် လက်ရှိ မှတ်တမ်းတင်ထားသော / တည်ငြိမ်သော Foundry Local CLI commands များကိုသာ အသုံးပြုသည်။

### Stable Commands Referenced

| အမျိုးအစား | Command | ရည်ရွယ်ချက် |
|-------------|---------|-------------|
| Core | `foundry --version` | ထည့်သွင်းထားသော version ကို ပြရန် |
| Core | `foundry init` | Configuration ကို စတင်ရန် |
| Service | `foundry service start` | Local service ကို စတင်ရန် (မစတင်ထားပါက) |
| Service | `foundry status` | Service status ကို ပြရန် |
| Models | `foundry model list` | Catalog / ရနိုင်သော models များကို ပြရန် |
| Models | `foundry model download <alias>` | Model weights များကို cache ထဲသို့ ဒေါင်းလုပ်လုပ်ရန် |
| Models | `foundry model run <alias>` | Model တစ်ခုကို locally စတင်ရန်; `--prompt` နှင့်ပေါင်းစပ်၍ တစ်ကြိမ်ပြုလုပ်ရန် |
| Models | `foundry model unload <alias>` / `foundry model stop <alias>` | Model တစ်ခုကို memory မှ Unload လုပ်ရန် (ထောက်ပံ့မှုရှိပါက) |
| Cache | `foundry cache list` | Cached (downloaded) models များကို ပြရန် |
| System | `foundry system info` | Hardware & acceleration capabilities snapshot |
| System | `foundry system gpu-info` | GPU diagnostic info |
| Config | `foundry config list` | လက်ရှိ config တန်ဖိုးများကို ပြရန် |
| Config | `foundry config set <key> <value>` | Configuration ကို ပြောင်းရန် |

### One‑Shot Prompt Pattern

`model chat` subcommand ကို မသုံးတော့ဘဲ, အစား:

```powershell
foundry model run <alias> --prompt "Your question here"
```

ဤသည်သည် prompt/response cycle တစ်ခုကို ပြုလုပ်ပြီးနောက် ထွက်သွားမည်။

### ဖယ်ရှားထားသော / မသုံးသင့်သော Pattern များ

| ဖယ်ရှားထားသော / မမှတ်တမ်းတင်ထားသော | အစားထိုးမှု / လမ်းညွှန်ချက် |
|-------------------------------------|-----------------------------|
| `foundry model chat <model> "..."` | `foundry model run <model> --prompt "..."` |
| `foundry model list --running` | `model list` + recent activity / logs ကို အသုံးပြုပါ |
| `foundry model list --cached` | `cache list` |
| `foundry model stats <model>` | Benchmark Python script + OS tools (Task Manager / `nvidia-smi`) ကို အသုံးပြုပါ |
| `foundry model benchmark ...` | `samples/session03/benchmark_oss_models.py` |

### Benchmarking & Telemetry

- Latency, p95, tokens/sec: `samples/session03/benchmark_oss_models.py`
- First‑token latency (streaming): `BENCH_STREAM=1` ကို environment တွင် သတ်မှတ်ပါ
- Resource usage: OS monitors (Task Manager, Activity Monitor, `nvidia-smi`) + `foundry system info` ကို အသုံးပြုပါ။

CLI telemetry commands အသစ်များကို upstream တွင် တည်ငြိမ်လာသည်နှင့်အမျှ, session markdown များတွင် အလွယ်တကူ ထည့်သွင်းနိုင်ပါသည်။

### Automated Lint Guard

Automated linter တစ်ခုသည် markdown ဖိုင်များ၏ fenced code blocks အတွင်း deprecated CLI patterns များ ပြန်လည်ထည့်သွင်းခြင်းကို တားဆီးပေးသည်:

Script: `Workshop/scripts/lint_markdown_cli.py`

Deprecated patterns များကို fenced code fences အတွင်းတွင် တားဆီးထားသည်။

အစားထိုးမှုများအတွက် အကြံပြုချက်များ:
| Deprecated | Replacement |
|------------|-------------|
| `foundry model chat <a> "..."` | `foundry model run <a> --prompt "..."` |
| `model list --running` | `model list` |
| `model list --cached` | `cache list` |
| `model stats` | Benchmark script + system tools |
| `model benchmark` | `samples/session03/benchmark_oss_models.py` |
| `model list --available` | `model list` |

Local တွင် run လုပ်ရန်:
```powershell
python Workshop\scripts\lint_markdown_cli.py --verbose
```

GitHub Action: `.github/workflows/markdown-cli-lint.yml` သည် push & PR တိုင်းတွင် run လုပ်သည်။

Optional pre-commit hook:
```bash
echo "python Workshop/scripts/lint_markdown_cli.py" > .git/hooks/pre-commit
chmod +x .git/hooks/pre-commit
```

## Quick CLI → SDK Migration Table

| Task | CLI One-Liner | SDK (Python) Equivalent | မှတ်ချက်များ |
|------|---------------|-------------------------|---------------|
| Run a model once (prompt) | `foundry model run phi-4-mini --prompt "Hello"` | `manager=FoundryLocalManager("phi-4-mini"); client=OpenAI(base_url=manager.endpoint, api_key=manager.api_key or "not-needed"); client.chat.completions.create(model=manager.get_model_info("phi-4-mini").id, messages=[{"role":"user","content":"Hello"}])` | SDK သည် service & caching ကို အလိုအလျောက် bootstrap လုပ်သည် |
| Download (cache) model | `foundry model download qwen2.5-0.5b` | `FoundryLocalManager("qwen2.5-0.5b")  # triggers download/load` | Manager သည် alias ကို map လုပ်ထားသော build များအနက် အကောင်းဆုံးကို ရွေးချယ်သည် |
| List catalog | `foundry model list` | `# use manager for each alias or maintain known list` | CLI သည် aggregate လုပ်သည်; SDK သည် လက်ရှိအခြေအနေတွင် per-alias instantiation ကိုသာ ထောက်ပံ့သည် |
| List cached models | `foundry cache list` | `manager.list_cached_models()` | Manager ကို initialize ပြီးနောက် |
| Enable GPU acceleration | `foundry config set compute.onnx.enable_gpu true` | `# CLI action; SDK assumes config already applied` | Configuration သည် အပြင်ဘက် side effect ဖြစ်သည် |
| Get endpoint URL | (implicit) | `manager.endpoint` | OpenAI-compatible client ဖန်တီးရန် အသုံးပြုသည် |
| Warm a model | `foundry model run <alias>` then first prompt | `chat_once(alias, messages=[...])` (utility) | Utilities များသည် initial cold latency warmup ကို ကိုင်တွယ်သည် |
| Measure latency | `python benchmark_oss_models.py` | `import benchmark_oss_models` (or new exporter script) | Consistent metrics အတွက် script ကို သုံးရန် အကြံပြုသည် |
| Stop / unload model | `foundry model unload <alias>` | (Not exposed – restart service / process) | Workshop flow အတွက် မလိုအပ်ပါ |
| Retrieve token usage | (view output) | `resp.usage.total_tokens` | Backend သည် usage object ကို ပြန်ပေးပါက ရရှိသည် |

## Benchmark Markdown Export

`Workshop/scripts/export_benchmark_markdown.py` script ကို အသုံးပြု၍ (logic သည် `samples/session03/benchmark_oss_models.py` နှင့် တူသည်) အသစ်သော benchmark ကို run လုပ်ပြီး GitHub-friendly Markdown table နှင့် raw JSON ကို ထုတ်ပေးပါ။

### နမူနာ

```powershell
python Workshop\scripts\export_benchmark_markdown.py --models "qwen2.5-0.5b,gemma-2-2b,mistral-7b" --prompt "Explain retrieval augmented generation briefly." --rounds 3 --output benchmark_report.md
```

ထုတ်လုပ်ထားသော ဖိုင်များ:
| ဖိုင် | အကြောင်းအရာ |
|------|---------------|
| `benchmark_report.md` | Markdown table + အဓိပ္ပါယ်ဖော်ပြချက် |
| `benchmark_report.json` | Raw metrics array (for diffing / trend tracking) |

Environment တွင် `BENCH_STREAM=1` ကို သတ်မှတ်ထားပါက, first-token latency ကို ထည့်သွင်းပါမည်။

---

**အကြောင်းကြားချက်**:  
ဤစာရွက်စာတမ်းကို AI ဘာသာပြန်ဝန်ဆောင်မှု [Co-op Translator](https://github.com/Azure/co-op-translator) ကို အသုံးပြု၍ ဘာသာပြန်ထားပါသည်။ ကျွန်ုပ်တို့သည် တိကျမှုအတွက် ကြိုးစားနေသော်လည်း အလိုအလျောက် ဘာသာပြန်မှုများတွင် အမှားများ သို့မဟုတ် မမှန်ကန်မှုများ ပါဝင်နိုင်သည်ကို သတိပြုပါ။ မူရင်းဘာသာစကားဖြင့် ရေးသားထားသော စာရွက်စာတမ်းကို အာဏာတရားရှိသော ရင်းမြစ်အဖြစ် သတ်မှတ်သင့်ပါသည်။ အရေးကြီးသော အချက်အလက်များအတွက် လူက ဘာသာပြန်မှုကို အသုံးပြုရန် အကြံပြုပါသည်။ ဤဘာသာပြန်မှုကို အသုံးပြုခြင်းမှ ဖြစ်ပေါ်လာသော အလွဲအမှားများ သို့မဟုတ် အနားယူမှုများအတွက် ကျွန်ုပ်တို့သည် တာဝန်မယူပါ။