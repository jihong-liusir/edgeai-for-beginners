<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a887b7e85782dadd3fd1216cd63b6c23",
  "translation_date": "2025-10-08T20:55:48+00:00",
  "source_file": "Workshop/QUICK_REFERENCE.md",
  "language_code": "es"
}
-->
# Muestras del Taller - Tarjeta de Referencia Rápida

**Última Actualización**: 8 de octubre de 2025

---

## 🚀 Inicio Rápido

```bash
# 1. Ensure Foundry Local is running
foundry service status
foundry model run phi-4-mini

# 2. Install dependencies
pip install -r Workshop/requirements.txt

# 3. Run a sample
cd Workshop/samples/session01
python chat_bootstrap.py "What is edge AI?"
```

---

## 📂 Resumen de Muestras

| Sesión | Muestra | Propósito | Tiempo |
|--------|---------|-----------|--------|
| 01 | `chat_bootstrap.py` | Chat básico + streaming | ~30s |
| 02 | `rag_pipeline.py` | RAG con embeddings | ~45s |
| 02 | `rag_eval_ragas.py` | Evaluación de RAG | ~60s |
| 03 | `benchmark_oss_models.py` | Evaluación de modelos | ~2m |
| 04 | `model_compare.py` | SLM vs LLM | ~45s |
| 05 | `agents_orchestrator.py` | Sistema multi-agente | ~60s |
| 06 | `models_router.py` | Enrutamiento por intención | ~45s |
| 06 | `models_pipeline.py` | Pipeline de múltiples pasos | ~60s |

---

## 🛠️ Variables de Entorno

### Esenciales
```bash
# Choose model
set FOUNDRY_LOCAL_ALIAS=phi-4-mini

# Override endpoint (optional)
set FOUNDRY_LOCAL_ENDPOINT=http://localhost:8000

# Show token usage
set SHOW_USAGE=1
```

### Específicas de la Sesión
```bash
# Session 02: RAG
set RAG_QUESTION="What is local inference?"
set EMBED_MODEL=sentence-transformers/all-MiniLM-L6-v2

# Session 03: Benchmarking
set BENCH_MODELS=phi-4-mini,qwen2.5-0.5b
set BENCH_ROUNDS=3
set BENCH_STREAM=1

# Session 04: Comparison
set SLM_ALIAS=phi-4-mini
set LLM_ALIAS=qwen2.5-7b

# Session 05: Agents
set AGENT_MODEL_PRIMARY=phi-4-mini
set AGENT_QUESTION="Why use edge AI?"

# Session 06: Pipeline
set PIPELINE_TASK="Your task here"
```

---

## ✅ Validación y Pruebas

```bash
# Validate syntax and imports
python scripts/validate_samples.py

# Validate specific session
python scripts/validate_samples.py --session 01

# Run smoke tests
python scripts/test_samples.py --quick

# Verbose testing
python scripts/test_samples.py --verbose
```

---

## 🐛 Resolución de Problemas

### Error de Conexión
```bash
# Check Foundry Local
foundry service status

# Start if needed
foundry service start
foundry model run phi-4-mini
```

### Error de Importación
```bash
# Install missing dependencies
pip install sentence-transformers ragas datasets

# Or install all
pip install -r Workshop/requirements.txt
```

### Modelo No Encontrado
```bash
# List available models
foundry model ls

# Download model
foundry model download phi-4-mini
```

### Rendimiento Lento
```bash
# Use smaller model
set FOUNDRY_LOCAL_ALIAS=qwen2.5-0.5b

# Reduce benchmark rounds
set BENCH_ROUNDS=1
```

---

## 📖 Patrones Comunes

### Chat Básico
```python
from workshop_utils import chat_once

text, usage = chat_once(
    'phi-4-mini',
    messages=[{"role": "user", "content": "Hello"}],
    max_tokens=100,
    temperature=0.7
)
```

### Obtener Cliente
```python
from workshop_utils import get_client

manager, client, model_id = get_client(
    alias='phi-4-mini',
    endpoint=None  # Auto-detect
)
```

### Manejo de Errores
```python
try:
    manager, client, model_id = get_client(alias)
except Exception as e:
    print(f"[ERROR] Failed: {e}")
    print("[INFO] Check: foundry service status")
    sys.exit(1)
```

### Streaming
```python
stream = client.chat.completions.create(
    model=model_id,
    messages=messages,
    stream=True
)

for chunk in stream:
    if chunk.choices[0].delta.content:
        print(chunk.choices[0].delta.content, end="", flush=True)
```

---

## 📊 Selección de Modelos

| Modelo | Tamaño | Mejor Para | Velocidad |
|--------|--------|------------|-----------|
| `qwen2.5-0.5b` | 0.5B | Clasificación rápida | ⚡⚡⚡ |
| `qwen2.5-coder-0.5b` | 0.5B | Generación rápida de código | ⚡⚡⚡ |
| `gemma-2-2b` | 2B | Escritura creativa | ⚡⚡ |
| `phi-3.5-mini` | 3.5B | Código, refactorización | ⚡⚡ |
| `phi-4-mini` | 4B | General, resúmenes | ⚡⚡ |
| `qwen2.5-7b` | 7B | Razonamiento complejo | ⚡ |

---

## 🔗 Recursos

- **Documentación SDK**: https://github.com/microsoft/Foundry-Local/tree/main/sdk/python
- **Referencia Rápida**: `Workshop/FOUNDRY_SDK_QUICKREF.md`
- **Resumen de Actualizaciones**: `Workshop/SAMPLES_UPDATE_SUMMARY.md`
- **Notas de Migración**: `Workshop/SDK_MIGRATION_NOTES.md`

---

## 💡 Consejos

1. **Cachear clientes**: `workshop_utils` lo hace por ti
2. **Usar modelos más pequeños**: Comienza con `qwen2.5-0.5b` para pruebas
3. **Habilitar estadísticas de uso**: Configura `SHOW_USAGE=1` para rastrear tokens
4. **Procesamiento por lotes**: Procesa múltiples prompts de forma secuencial
5. **Reducir max_tokens**: Disminuye la latencia para respuestas rápidas

---

## 🎯 Flujos de Trabajo de Muestras

### Probar Todo
```bash
python scripts/validate_samples.py
python scripts/test_samples.py --quick
```

### Evaluar Modelos
```bash
cd samples/session03
set BENCH_MODELS=phi-4-mini,qwen2.5-0.5b,gemma-2-2b
set BENCH_ROUNDS=3
python benchmark_oss_models.py
```

### Pipeline de RAG
```bash
cd samples/session02
set RAG_QUESTION="What is RAG?"
python rag_pipeline.py
```

### Sistema Multi-Agente
```bash
cd samples/session05
set AGENT_QUESTION="Why edge AI for healthcare?"
python agents_orchestrator.py
```

---

**Ayuda Rápida**: Ejecuta cualquier muestra con `--help` o revisa el docstring:
```bash
python chat_bootstrap.py --help
# or
python -c "import chat_bootstrap; help(chat_bootstrap)"
```

---

**Todas las muestras actualizadas en octubre de 2025 con las mejores prácticas del SDK Foundry Local** ✨

---

**Descargo de responsabilidad**:  
Este documento ha sido traducido utilizando el servicio de traducción automática [Co-op Translator](https://github.com/Azure/co-op-translator). Aunque nos esforzamos por garantizar la precisión, tenga en cuenta que las traducciones automatizadas pueden contener errores o imprecisiones. El documento original en su idioma nativo debe considerarse como la fuente autorizada. Para información crítica, se recomienda una traducción profesional realizada por humanos. No nos hacemos responsables de malentendidos o interpretaciones erróneas que puedan surgir del uso de esta traducción.