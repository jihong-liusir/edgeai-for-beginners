<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "dd4a5b9ec82d35599b0abc9af89e7c9e",
  "translation_date": "2025-10-08T19:09:50+00:00",
  "source_file": "Workshop/ENV_CONFIGURATION.md",
  "language_code": "fr"
}
-->
# Guide de Configuration de l'Environnement

## Vue d'ensemble

Les exemples du Workshop utilisent des variables d'environnement pour la configuration, centralisées dans le fichier `.env` à la racine du dépôt. Cela permet une personnalisation facile sans modifier le code.

## Démarrage rapide

### 1. Vérifiez les prérequis

```bash
# Check Foundry Local is installed
foundry --version

# Check service is running
foundry service status

# Load a model
foundry model run phi-4-mini
```

### 2. Configurez l'environnement

Le fichier `.env` est déjà configuré avec des valeurs par défaut adaptées. La plupart des utilisateurs n'auront pas besoin de modifier quoi que ce soit.

**Optionnel** : Passez en revue et personnalisez les paramètres :
```bash
# Edit .env file
notepad .env  # Windows
nano .env     # macOS/Linux
```

### 3. Appliquez la configuration

**Pour les scripts Python :**
```bash
cd Workshop/samples/session01
python chat_bootstrap.py
# Environment variables automatically loaded
```

**Pour les notebooks :**
```python
# Restart kernel after .env changes
# Variables are loaded when cells execute
```

## Référence des variables d'environnement

### Configuration principale

| Variable | Par défaut | Description |
|----------|------------|-------------|
| `FOUNDRY_LOCAL_ALIAS` | `phi-4-mini` | Modèle par défaut pour les exemples |
| `FOUNDRY_LOCAL_ENDPOINT` | (vide) | Remplace le point de service |
| `PYTHONPATH` | Chemins du Workshop | Chemin de recherche des modules Python |

**Quand définir FOUNDRY_LOCAL_ENDPOINT :**
- Instance Foundry Local distante
- Configuration de port personnalisée
- Séparation développement/production

**Exemple :**
```bash
# Local custom port
FOUNDRY_LOCAL_ENDPOINT=http://localhost:8000

# Remote instance
FOUNDRY_LOCAL_ENDPOINT=http://192.168.1.50:5273/v1
```

### Variables spécifiques à la session

#### Session 02 : Pipeline RAG
| Variable | Par défaut | Objectif |
|----------|------------|----------|
| `EMBED_MODEL` | `sentence-transformers/all-MiniLM-L6-v2` | Modèle d'embedding |
| `RAG_QUESTION` | Préconfiguré | Question de test |

#### Session 03 : Benchmarking
| Variable | Par défaut | Objectif |
|----------|------------|----------|
| `BENCH_MODELS` | `phi-4-mini,qwen2.5-0.5b,gemma-2-2b` | Modèles à tester |
| `BENCH_ROUNDS` | `3` | Itérations par modèle |
| `BENCH_PROMPT` | Préconfiguré | Prompt de test |
| `BENCH_STREAM` | `0` | Mesure de la latence du premier token |

#### Session 04 : Comparaison de modèles
| Variable | Par défaut | Objectif |
|----------|------------|----------|
| `SLM_ALIAS` | `phi-4-mini` | Petit modèle de langage |
| `LLM_ALIAS` | `qwen2.5-7b` | Grand modèle de langage |
| `COMPARE_PROMPT` | Préconfiguré | Prompt de comparaison |
| `COMPARE_RETRIES` | `2` | Tentatives de réessai |

#### Session 05 : Orchestration multi-agents
| Variable | Par défaut | Objectif |
|----------|------------|----------|
| `AGENT_MODEL_PRIMARY` | `phi-4-mini` | Modèle de l'agent chercheur |
| `AGENT_MODEL_EDITOR` | `phi-4-mini` | Modèle de l'agent éditeur |
| `AGENT_QUESTION` | Préconfiguré | Question de test |

### Configuration de fiabilité

| Variable | Par défaut | Objectif |
|----------|------------|----------|
| `SHOW_USAGE` | `1` | Affiche l'utilisation des tokens |
| `RETRY_ON_FAIL` | `1` | Active la logique de réessai |
| `RETRY_BACKOFF` | `1.0` | Délai de réessai (secondes) |

## Configurations courantes

### Configuration de développement (itération rapide)
```bash
FOUNDRY_LOCAL_ALIAS=phi-4-mini
SLM_ALIAS=phi-4-mini
LLM_ALIAS=phi-4-mini
BENCH_MODELS=phi-4-mini
SHOW_USAGE=1
```

### Configuration de production (qualité optimale)
```bash
FOUNDRY_LOCAL_ALIAS=phi-4-mini
SLM_ALIAS=phi-4-mini
LLM_ALIAS=qwen2.5-7b
AGENT_MODEL_PRIMARY=phi-4-mini
AGENT_MODEL_EDITOR=qwen2.5-7b
SHOW_USAGE=0
```

### Configuration de benchmarking
```bash
BENCH_MODELS=phi-4-mini,qwen2.5-0.5b,qwen2.5-7b,gemma-2-2b
BENCH_ROUNDS=5
BENCH_STREAM=1
```

### Spécialisation multi-agents
```bash
AGENT_MODEL_PRIMARY=phi-4-mini        # Fast for research
AGENT_MODEL_EDITOR=qwen2.5-7b         # Quality for editing
```

### Développement à distance
```bash
FOUNDRY_LOCAL_ENDPOINT=http://dev-server.local:5273/v1
FOUNDRY_LOCAL_ALIAS=phi-4-mini
```

## Modèles recommandés

### Par cas d'utilisation

**Usage général :**
- `phi-4-mini` - Équilibre entre qualité et rapidité

**Réponses rapides :**
- `qwen2.5-0.5b` - Très rapide, idéal pour la classification
- `phi-4-mini` - Rapide avec une bonne qualité

**Haute qualité :**
- `qwen2.5-7b` - Meilleure qualité, utilisation de ressources plus élevée
- `phi-4-mini` - Bonne qualité, moins de ressources nécessaires

**Génération de code :**
- `deepseek-coder-1.3b` - Spécialisé pour le code
- `phi-4-mini` - Codage généraliste

### Par disponibilité des ressources

**Ressources faibles (< 8 Go RAM) :**
```bash
FOUNDRY_LOCAL_ALIAS=qwen2.5-0.5b
SLM_ALIAS=qwen2.5-0.5b
LLM_ALIAS=phi-4-mini
```

**Ressources moyennes (8-16 Go RAM) :**
```bash
FOUNDRY_LOCAL_ALIAS=phi-4-mini
SLM_ALIAS=phi-4-mini
LLM_ALIAS=qwen2.5-7b
```

**Ressources élevées (16 Go+ RAM) :**
```bash
FOUNDRY_LOCAL_ALIAS=qwen2.5-7b
SLM_ALIAS=phi-4-mini
LLM_ALIAS=qwen2.5-14b
```

## Configuration avancée

### Points de service personnalisés

```bash
# Development environment
FOUNDRY_LOCAL_ENDPOINT=http://localhost:8000

# Staging environment
FOUNDRY_LOCAL_ENDPOINT=http://staging.internal:5273/v1

# Production environment
FOUNDRY_LOCAL_ENDPOINT=http://prod.internal:5273/v1
```

### Température et échantillonnage (remplacement dans le code)

```python
# In your scripts/notebooks
os.environ['TEMPERATURE'] = '0.7'
os.environ['TOP_P'] = '0.9'
```

### Configuration hybride Azure OpenAI

```bash
# Use local for development
FOUNDRY_LOCAL_ALIAS=phi-4-mini

# Configure Azure for production fallback
AZURE_OPENAI_ENDPOINT=https://your-resource.openai.azure.com
AZURE_OPENAI_API_KEY=your-key-here
AZURE_OPENAI_API_VERSION=2024-08-01-preview
```

## Résolution des problèmes

### Variables d'environnement non chargées

**Symptômes :**
- Les scripts utilisent les mauvais modèles
- Erreurs de connexion
- Variables non reconnues

**Solutions :**
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

### Problèmes de connexion au service

**Symptômes :**
- Erreurs "Connection refused"
- "Service non disponible"
- Erreurs de timeout

**Solutions :**
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

### Modèle introuvable

**Symptômes :**
- Erreurs "Model not found"
- "Alias non reconnu"

**Solutions :**
```bash
# 1. List available models
foundry model list

# 2. Load required model
foundry model run phi-4-mini

# 3. Update .env with available model
FOUNDRY_LOCAL_ALIAS=<available-model>
```

### Erreurs d'importation

**Symptômes :**
- Erreurs "Module not found"
- "Cannot import workshop_utils"

**Solutions :**
```bash
# 1. Verify PYTHONPATH in .env
PYTHONPATH=${workspaceFolder}/Workshop/samples

# 2. Install dependencies
pip install -r requirements.txt

# 3. Activate virtual environment
.venv\Scripts\activate  # Windows
source .venv/bin/activate  # macOS/Linux
```

## Test de la configuration

### Vérifiez le chargement de l'environnement

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

### Testez la connexion à Foundry Local

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

## Bonnes pratiques de sécurité

### 1. Ne jamais commettre de secrets

```bash
# .gitignore should include:
.env
.env.local
*.key
```

### 2. Utilisez des fichiers .env séparés

```bash
.env              # Default configuration
.env.local        # Local overrides (gitignored)
.env.production   # Production config (secure storage)
```

### 3. Faites tourner les clés API

```bash
# For Azure OpenAI or other cloud services
# Regularly rotate keys and update .env
```

### 4. Utilisez une configuration spécifique à l'environnement

```bash
# Development
FOUNDRY_LOCAL_ENDPOINT=http://localhost:5273/v1

# Production (use secrets management)
FOUNDRY_LOCAL_ENDPOINT=${PROD_FOUNDRY_ENDPOINT}
```

## Documentation SDK

- **Dépôt principal** : https://github.com/microsoft/Foundry-Local
- **SDK Python** : https://github.com/microsoft/Foundry-Local/tree/main/sdk/python/foundry_local
- **Documentation API** : Consultez le dépôt SDK pour les dernières informations

## Ressources supplémentaires

- `QUICK_START.md` - Guide de démarrage
- `SDK_MIGRATION_NOTES.md` - Détails sur la mise à jour du SDK
- `Workshop/samples/*/README.md` - Guides spécifiques aux exemples

---

**Dernière mise à jour** : 08/01/2025  
**Version** : 2.0  
**SDK** : Foundry Local Python SDK (dernier)

---

**Avertissement** :  
Ce document a été traduit à l'aide du service de traduction automatique [Co-op Translator](https://github.com/Azure/co-op-translator). Bien que nous nous efforcions d'assurer l'exactitude, veuillez noter que les traductions automatisées peuvent contenir des erreurs ou des inexactitudes. Le document original dans sa langue d'origine doit être considéré comme la source faisant autorité. Pour des informations critiques, il est recommandé de recourir à une traduction humaine professionnelle. Nous déclinons toute responsabilité en cas de malentendus ou d'interprétations erronées résultant de l'utilisation de cette traduction.