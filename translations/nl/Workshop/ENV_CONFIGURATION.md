<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "dd4a5b9ec82d35599b0abc9af89e7c9e",
  "translation_date": "2025-10-09T16:41:16+00:00",
  "source_file": "Workshop/ENV_CONFIGURATION.md",
  "language_code": "nl"
}
-->
# Handleiding voor Omgevingsconfiguratie

## Overzicht

De workshopvoorbeelden maken gebruik van omgevingsvariabelen voor configuratie, gecentraliseerd in het `.env`-bestand in de hoofdmap van de repository. Dit maakt eenvoudige aanpassingen mogelijk zonder de code te wijzigen.

## Snelle Start

### 1. Controleer Vereisten

```bash
# Check Foundry Local is installed
foundry --version

# Check service is running
foundry service status

# Load a model
foundry model run phi-4-mini
```

### 2. Configureer de Omgeving

Het `.env`-bestand is al geconfigureerd met logische standaardinstellingen. De meeste gebruikers hoeven niets te wijzigen.

**Optioneel**: Bekijk en pas instellingen aan:
```bash
# Edit .env file
notepad .env  # Windows
nano .env     # macOS/Linux
```

### 3. Pas Configuratie Toe

**Voor Python-scripts:**
```bash
cd Workshop/samples/session01
python chat_bootstrap.py
# Environment variables automatically loaded
```

**Voor Notebooks:**
```python
# Restart kernel after .env changes
# Variables are loaded when cells execute
```

## Referentie Omgevingsvariabelen

### Kernconfiguratie

| Variabele | Standaard | Beschrijving |
|-----------|-----------|--------------|
| `FOUNDRY_LOCAL_ALIAS` | `phi-4-mini` | Standaardmodel voor voorbeelden |
| `FOUNDRY_LOCAL_ENDPOINT` | (leeg) | Service endpoint overschrijven |
| `PYTHONPATH` | Workshop-paden | Zoekpad voor Python-modules |

**Wanneer `FOUNDRY_LOCAL_ENDPOINT` instellen:**
- Externe Foundry Local-instantie
- Aangepaste poortconfiguratie
- Scheiding tussen ontwikkeling en productie

**Voorbeeld:**
```bash
# Local custom port
FOUNDRY_LOCAL_ENDPOINT=http://localhost:8000

# Remote instance
FOUNDRY_LOCAL_ENDPOINT=http://192.168.1.50:5273/v1
```

### Sessie-specifieke variabelen

#### Sessie 02: RAG-pijplijn
| Variabele | Standaard | Doel |
|-----------|-----------|------|
| `EMBED_MODEL` | `sentence-transformers/all-MiniLM-L6-v2` | Embedding model |
| `RAG_QUESTION` | Vooraf geconfigureerd | Testvraag |

#### Sessie 03: Benchmarking
| Variabele | Standaard | Doel |
|-----------|-----------|------|
| `BENCH_MODELS` | `phi-4-mini,qwen2.5-0.5b,gemma-2-2b` | Modellen om te benchmarken |
| `BENCH_ROUNDS` | `3` | Iteraties per model |
| `BENCH_PROMPT` | Vooraf geconfigureerd | Testprompt |
| `BENCH_STREAM` | `0` | Latentie van eerste token meten |

#### Sessie 04: Modelvergelijking
| Variabele | Standaard | Doel |
|-----------|-----------|------|
| `SLM_ALIAS` | `phi-4-mini` | Klein taalmodel |
| `LLM_ALIAS` | `qwen2.5-7b` | Groot taalmodel |
| `COMPARE_PROMPT` | Vooraf geconfigureerd | Vergelijkingsprompt |
| `COMPARE_RETRIES` | `2` | Aantal herhalingen bij mislukking |

#### Sessie 05: Multi-Agent Orchestratie
| Variabele | Standaard | Doel |
|-----------|-----------|------|
| `AGENT_MODEL_PRIMARY` | `phi-4-mini` | Onderzoeker-agentmodel |
| `AGENT_MODEL_EDITOR` | `phi-4-mini` | Editor-agentmodel |
| `AGENT_QUESTION` | Vooraf geconfigureerd | Testvraag |

### Betrouwbaarheidsconfiguratie

| Variabele | Standaard | Doel |
|-----------|-----------|------|
| `SHOW_USAGE` | `1` | Print tokengebruik |
| `RETRY_ON_FAIL` | `1` | Retry-logica inschakelen |
| `RETRY_BACKOFF` | `1.0` | Vertraging bij retry (seconden) |

## Veelvoorkomende Configuraties

### Ontwikkelomgeving (Snelle Iteratie)
```bash
FOUNDRY_LOCAL_ALIAS=phi-4-mini
SLM_ALIAS=phi-4-mini
LLM_ALIAS=phi-4-mini
BENCH_MODELS=phi-4-mini
SHOW_USAGE=1
```

### Productieomgeving (Kwaliteitsfocus)
```bash
FOUNDRY_LOCAL_ALIAS=phi-4-mini
SLM_ALIAS=phi-4-mini
LLM_ALIAS=qwen2.5-7b
AGENT_MODEL_PRIMARY=phi-4-mini
AGENT_MODEL_EDITOR=qwen2.5-7b
SHOW_USAGE=0
```

### Benchmarking Configuratie
```bash
BENCH_MODELS=phi-4-mini,qwen2.5-0.5b,qwen2.5-7b,gemma-2-2b
BENCH_ROUNDS=5
BENCH_STREAM=1
```

### Multi-Agent Specialisatie
```bash
AGENT_MODEL_PRIMARY=phi-4-mini        # Fast for research
AGENT_MODEL_EDITOR=qwen2.5-7b         # Quality for editing
```

### Externe Ontwikkeling
```bash
FOUNDRY_LOCAL_ENDPOINT=http://dev-server.local:5273/v1
FOUNDRY_LOCAL_ALIAS=phi-4-mini
```

## Aanbevolen Modellen

### Per Gebruiksscenario

**Algemeen Gebruik:**
- `phi-4-mini` - Gebalanceerde kwaliteit en snelheid

**Snelle Reacties:**
- `qwen2.5-0.5b` - Zeer snel, goed voor classificatie
- `phi-4-mini` - Snel met goede kwaliteit

**Hoge Kwaliteit:**
- `qwen2.5-7b` - Beste kwaliteit, hogere resourcegebruik
- `phi-4-mini` - Goede kwaliteit, lagere resources

**Codegeneratie:**
- `deepseek-coder-1.3b` - Gespecialiseerd voor code
- `phi-4-mini` - Algemeen gebruik voor codering

### Per Resourcebeschikbaarheid

**Weinig Resources (< 8GB RAM):**
```bash
FOUNDRY_LOCAL_ALIAS=qwen2.5-0.5b
SLM_ALIAS=qwen2.5-0.5b
LLM_ALIAS=phi-4-mini
```

**Gemiddelde Resources (8-16GB RAM):**
```bash
FOUNDRY_LOCAL_ALIAS=phi-4-mini
SLM_ALIAS=phi-4-mini
LLM_ALIAS=qwen2.5-7b
```

**Hoge Resources (16GB+ RAM):**
```bash
FOUNDRY_LOCAL_ALIAS=qwen2.5-7b
SLM_ALIAS=phi-4-mini
LLM_ALIAS=qwen2.5-14b
```

## Geavanceerde Configuratie

### Aangepaste Endpoints

```bash
# Development environment
FOUNDRY_LOCAL_ENDPOINT=http://localhost:8000

# Staging environment
FOUNDRY_LOCAL_ENDPOINT=http://staging.internal:5273/v1

# Production environment
FOUNDRY_LOCAL_ENDPOINT=http://prod.internal:5273/v1
```

### Temperatuur & Sampling (Overschrijven in Code)

```python
# In your scripts/notebooks
os.environ['TEMPERATURE'] = '0.7'
os.environ['TOP_P'] = '0.9'
```

### Azure OpenAI Hybride Configuratie

```bash
# Use local for development
FOUNDRY_LOCAL_ALIAS=phi-4-mini

# Configure Azure for production fallback
AZURE_OPENAI_ENDPOINT=https://your-resource.openai.azure.com
AZURE_OPENAI_API_KEY=your-key-here
AZURE_OPENAI_API_VERSION=2024-08-01-preview
```

## Problemen Oplossen

### Omgevingsvariabelen Niet Geladen

**Symptomen:**
- Scripts gebruiken verkeerde modellen
- Verbindingsfouten
- Variabelen worden niet herkend

**Oplossingen:**
```bash
# 1. Verify .env exists in repository root
ls -la .env  # macOS/Linux
dir .env     # Windows

# 2. Check file is not .env.txt (Windows)
# Ensure no hidden extension

# 3. For notebooks: Restart kernel
# Kernel > Restart

# 4. For scripts: Check working directory
pwd  # Should be in Workshop or repository root
```

### Verbindingsproblemen met Service

**Symptomen:**
- "Connection refused"-fouten
- "Service niet beschikbaar"
- Time-out fouten

**Oplossingen:**
```bash
# 1. Check service status
foundry service status

# 2. Start if not running
foundry service start

# 3. Verify endpoint
# Check port in status output
foundry service status | grep "Port"

# 4. Update .env if needed
FOUNDRY_LOCAL_ENDPOINT=http://localhost:<port>
```

### Model Niet Gevonden

**Symptomen:**
- "Model niet gevonden"-fouten
- "Alias niet herkend"

**Oplossingen:**
```bash
# 1. List available models
foundry model list

# 2. Load required model
foundry model run phi-4-mini

# 3. Update .env with available model
FOUNDRY_LOCAL_ALIAS=<available-model>
```

### Importfouten

**Symptomen:**
- "Module niet gevonden"-fouten
- "Kan workshop_utils niet importeren"

**Oplossingen:**
```bash
# 1. Verify PYTHONPATH in .env
PYTHONPATH=${workspaceFolder}/Workshop/samples

# 2. Install dependencies
pip install -r requirements.txt

# 3. Activate virtual environment
.venv\Scripts\activate  # Windows
source .venv/bin/activate  # macOS/Linux
```

## Configuratietests

### Controleer Laden van Omgeving

```python
# test_env.py
import os
from dotenv import load_dotenv

load_dotenv()

print("Core Configuration:")
print(f"  FOUNDRY_LOCAL_ALIAS: {os.getenv('FOUNDRY_LOCAL_ALIAS')}")
print(f"  FOUNDRY_LOCAL_ENDPOINT: {os.getenv('FOUNDRY_LOCAL_ENDPOINT') or 'auto'}")

print("\nSession 04:")
print(f"  SLM_ALIAS: {os.getenv('SLM_ALIAS')}")
print(f"  LLM_ALIAS: {os.getenv('LLM_ALIAS')}")

print("\nSession 05:")
print(f"  AGENT_MODEL_PRIMARY: {os.getenv('AGENT_MODEL_PRIMARY')}")
print(f"  AGENT_MODEL_EDITOR: {os.getenv('AGENT_MODEL_EDITOR')}")
```

### Test Foundry Local Verbinding

```python
# test_connection.py
import os
from foundry_local import FoundryLocalManager

alias = os.getenv('FOUNDRY_LOCAL_ALIAS', 'phi-4-mini')
endpoint = os.getenv('FOUNDRY_LOCAL_ENDPOINT')

try:
    if endpoint:
        manager = FoundryLocalManager(alias, endpoint=endpoint)
    else:
        manager = FoundryLocalManager(alias)
    
    print(f"✓ Connected to {manager.endpoint}")
    print(f"✓ Model: {manager.get_model_info(alias).id}")
    print(f"✓ Available models: {len(manager.list_models())}")
except Exception as e:
    print(f"✗ Connection failed: {e}")
```

## Beveiligingsrichtlijnen

### 1. Nooit Geheimen Committen

```bash
# .gitignore should include:
.env
.env.local
*.key
```

### 2. Gebruik Gescheiden .env-bestanden

```bash
.env              # Default configuration
.env.local        # Local overrides (gitignored)
.env.production   # Production config (secure storage)
```

### 3. Draai API-sleutels Regelmatig

```bash
# For Azure OpenAI or other cloud services
# Regularly rotate keys and update .env
```

### 4. Gebruik Configuratie per Omgeving

```bash
# Development
FOUNDRY_LOCAL_ENDPOINT=http://localhost:5273/v1

# Production (use secrets management)
FOUNDRY_LOCAL_ENDPOINT=${PROD_FOUNDRY_ENDPOINT}
```

## SDK Documentatie

- **Hoofdrepository**: https://github.com/microsoft/Foundry-Local
- **Python SDK**: https://github.com/microsoft/Foundry-Local/tree/main/sdk/python/foundry_local
- **API Documentatie**: Bekijk de SDK-repository voor de meest recente versie

## Aanvullende Bronnen

- `QUICK_START.md` - Handleiding voor beginners
- `SDK_MIGRATION_NOTES.md` - Details over SDK-updates
- `Workshop/samples/*/README.md` - Specifieke handleidingen voor voorbeelden

---

**Laatst Bijgewerkt**: 2025-01-08  
**Versie**: 2.0  
**SDK**: Foundry Local Python SDK (laatste versie)

---

**Disclaimer**:  
Dit document is vertaald met behulp van de AI-vertalingsservice [Co-op Translator](https://github.com/Azure/co-op-translator). Hoewel we streven naar nauwkeurigheid, dient u zich ervan bewust te zijn dat geautomatiseerde vertalingen fouten of onnauwkeurigheden kunnen bevatten. Het originele document in de oorspronkelijke taal moet worden beschouwd als de gezaghebbende bron. Voor cruciale informatie wordt professionele menselijke vertaling aanbevolen. Wij zijn niet aansprakelijk voor misverstanden of verkeerde interpretaties die voortvloeien uit het gebruik van deze vertaling.