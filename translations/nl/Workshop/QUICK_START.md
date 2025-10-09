<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "20ef6223850f0ab7b6e546a6df0d7d68",
  "translation_date": "2025-10-09T16:39:16+00:00",
  "source_file": "Workshop/QUICK_START.md",
  "language_code": "nl"
}
-->
# Workshop Snelle Startgids

## Vereisten

### 1. Installeer Foundry Local

Volg de officiële installatiehandleiding:  
https://github.com/microsoft/Foundry-Local

```bash
# Start Foundry Local service
foundry service start

# Load a model (phi-4-mini recommended for workshop)
foundry model run phi-4-mini

# Verify service is running
foundry service status
```

### 2. Installeer Python-afhankelijkheden

Vanuit de Workshop-map:

```bash
# Create virtual environment (recommended)
python -m venv .venv

# Activate virtual environment
# Windows:
.venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate

# Install requirements
pip install -r requirements.txt
```

## Workshopvoorbeelden uitvoeren

### Sessie 01: Basis Chat

```bash
cd Workshop/samples/session01
python chat_bootstrap.py "What are the benefits of local AI?"
```

**Omgevingsvariabelen:**  
```bash
set FOUNDRY_LOCAL_ALIAS=phi-4-mini
set SHOW_USAGE=1
```

### Sessie 02: RAG Pipeline

```bash
cd Workshop/samples/session02
python rag_pipeline.py
```

**Omgevingsvariabelen:**  
```bash
set FOUNDRY_LOCAL_ALIAS=phi-4-mini
set RAG_QUESTION="Why use RAG with local inference?"
set EMBED_MODEL=sentence-transformers/all-MiniLM-L6-v2
```

### Sessie 02: RAG Evaluatie (Ragas)

```bash
python rag_eval_ragas.py
```

**Opmerking**: Vereist extra afhankelijkheden geïnstalleerd via `requirements.txt`

### Sessie 03: Benchmarking

```bash
cd Workshop/samples/session03
python benchmark_oss_models.py
```

**Omgevingsvariabelen:**  
```bash
set BENCH_MODELS=phi-4-mini,qwen2.5-0.5b,gemma-2-2b
set BENCH_ROUNDS=5
set BENCH_PROMPT="Explain RAG briefly"
set BENCH_STREAM=1
```

**Uitvoer**: JSON met latentie, doorvoer en eerste-token-metrics

### Sessie 04: Modelvergelijking

```bash
cd Workshop/samples/session04
python model_compare.py
```

**Omgevingsvariabelen:**  
```bash
set SLM_ALIAS=phi-4-mini
set LLM_ALIAS=qwen2.5-7b
set COMPARE_PROMPT="List 5 benefits of local AI inference"
```

### Sessie 05: Multi-Agent Orchestratie

```bash
cd Workshop/samples/session05
python agents_orchestrator.py
```

**Omgevingsvariabelen:**  
```bash
set AGENT_MODEL_PRIMARY=phi-4-mini
set AGENT_MODEL_EDITOR=phi-4-mini
set AGENT_QUESTION="Explain why edge AI matters for compliance"
```

### Sessie 06: Model Router

```bash
cd Workshop/samples/session06
python models_router.py
```

**Test routeringslogica** met meerdere intenties (code, samenvatten, classificatie)

### Sessie 06: Pipeline

```bash
python models_pipeline.py
```

**Complexe meerstaps-pipeline** met planning, uitvoering en verfijning

## Scripts

### Benchmarkrapport exporteren

```bash
cd Workshop/scripts
python export_benchmark_markdown.py \
    --models "phi-4-mini,qwen2.5-0.5b" \
    --prompt "Explain RAG briefly" \
    --rounds 3 \
    --output benchmark_report.md
```

**Uitvoer**: Markdown-tabel + JSON-metrics

### Markdown CLI-patronen linten

```bash
python lint_markdown_cli.py --verbose
```

**Doel**: Verouderde CLI-patronen in documentatie detecteren

## Testen

### Smoke Tests

```bash
cd Workshop
python -m tests.smoke
```

**Tests**: Basisfunctionaliteit van belangrijke voorbeelden

## Problemen oplossen

### Service werkt niet

```bash
# Check status
foundry service status

# Start if not running
foundry service start

# Load a model
foundry model run phi-4-mini
```

### Module importfouten

```bash
# Ensure virtual environment is activated
.venv\Scripts\activate  # Windows
source .venv/bin/activate  # macOS/Linux

# Reinstall dependencies
pip install -r requirements.txt
```

### Verbindingsfouten

```bash
# Check endpoint
foundry service status

# Set explicit endpoint if needed
set FOUNDRY_LOCAL_ENDPOINT=http://localhost:8000
```

### Model niet gevonden

```bash
# List available models
foundry model list

# Download and run a model
foundry model run phi-4-mini
```

## Referentie omgevingsvariabelen

### Kernconfiguratie
| Variabele | Standaard | Beschrijving |
|-----------|-----------|--------------|
| `FOUNDRY_LOCAL_ALIAS` | Verschillend | Modelalias om te gebruiken |
| `FOUNDRY_LOCAL_ENDPOINT` | Auto | Service endpoint overschrijven |
| `SHOW_USAGE` | `0` | Toon tokengebruikstatistieken |
| `RETRY_ON_FAIL` | `1` | Retry-logica inschakelen |
| `RETRY_BACKOFF` | `1.0` | Initiële retry-vertraging (seconden) |

### Sessie-specifiek
| Variabele | Standaard | Beschrijving |
|-----------|-----------|--------------|
| `EMBED_MODEL` | `sentence-transformers/all-MiniLM-L6-v2` | Embedding model |
| `RAG_QUESTION` | Zie voorbeeld | RAG testvraag |
| `BENCH_MODELS` | Verschillend | Komma-gescheiden modellen |
| `BENCH_ROUNDS` | `3` | Benchmark iteraties |
| `BENCH_PROMPT` | Zie voorbeeld | Benchmark prompt |
| `BENCH_STREAM` | `0` | Meet eerste-token latentie |
| `AGENT_MODEL_PRIMARY` | `phi-4-mini` | Primair agentmodel |
| `AGENT_MODEL_EDITOR` | Primair | Editor agentmodel |
| `SLM_ALIAS` | `phi-4-mini` | Klein taalmodel |
| `LLM_ALIAS` | `qwen2.5-7b` | Groot taalmodel |
| `COMPARE_PROMPT` | Zie voorbeeld | Vergelijkingsprompt |

## Aanbevolen modellen

### Ontwikkeling & Testen
- **phi-4-mini** - Gebalanceerde kwaliteit en snelheid
- **qwen2.5-0.5b** - Zeer snel voor classificatie
- **gemma-2-2b** - Goede kwaliteit, gemiddelde snelheid

### Productiescenario's
- **phi-4-mini** - Algemeen gebruik
- **deepseek-coder-1.3b** - Codegeneratie
- **qwen2.5-7b** - Hoge kwaliteit antwoorden

## SDK Documentatie

- **Foundry Local**: https://github.com/microsoft/Foundry-Local  
- **Python SDK**: https://github.com/microsoft/Foundry-Local/tree/main/sdk/python/foundry_local

## Hulp krijgen

1. Controleer servicestatus: `foundry service status`  
2. Bekijk logs: Controleer Foundry Local service logs  
3. Bekijk SDK-documentatie: https://github.com/microsoft/Foundry-Local  
4. Bekijk voorbeeldcode: Alle voorbeelden hebben gedetailleerde docstrings

## Volgende stappen

1. Voltooi alle workshopsessies in volgorde  
2. Experimenteer met verschillende modellen  
3. Pas voorbeelden aan voor jouw gebruiksscenario's  
4. Bekijk `SDK_MIGRATION_NOTES.md` voor geavanceerde patronen

---

**Laatst bijgewerkt**: 2025-01-08  
**Workshopversie**: Laatste  
**SDK**: Foundry Local Python SDK

---

**Disclaimer**:  
Dit document is vertaald met behulp van de AI-vertalingsservice [Co-op Translator](https://github.com/Azure/co-op-translator). Hoewel we streven naar nauwkeurigheid, dient u zich ervan bewust te zijn dat geautomatiseerde vertalingen fouten of onnauwkeurigheden kunnen bevatten. Het originele document in de oorspronkelijke taal moet worden beschouwd als de gezaghebbende bron. Voor cruciale informatie wordt professionele menselijke vertaling aanbevolen. Wij zijn niet aansprakelijk voor misverstanden of verkeerde interpretaties die voortvloeien uit het gebruik van deze vertaling.