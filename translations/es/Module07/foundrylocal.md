<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "070a706937c5ac9feb45693b8c572d25",
  "translation_date": "2025-09-22T12:58:52+00:00",
  "source_file": "Module07/foundrylocal.md",
  "language_code": "es"
}
-->
# Foundry Local en Windows (Validado)

Esta guía te ayuda a instalar, ejecutar e integrar Microsoft Foundry Local en Windows. Todos los pasos y comandos están validados según la documentación de Microsoft Learn.

- Comenzar: https://learn.microsoft.com/azure/ai-foundry/foundry-local/get-started
- Arquitectura: https://learn.microsoft.com/azure/ai-foundry/foundry-local/concepts/foundry-local-architecture
- Referencia CLI: https://learn.microsoft.com/azure/ai-foundry/foundry-local/reference/reference-cli
- Integrar SDKs: https://learn.microsoft.com/azure/ai-foundry/foundry-local/how-to/how-to-integrate-with-inference-sdks
- Compilar modelos HF (BYOM): https://learn.microsoft.com/azure/ai-foundry/foundry-local/how-to/how-to-compile-hugging-face-models
- Windows AI: Local vs Cloud: https://learn.microsoft.com/windows/ai/cloud-ai#key-decision-factors-for-app-developers

## 1) Instalar / Actualizar en Windows

- Instalar:
```cmd
winget install Microsoft.FoundryLocal
```
- Actualizar:
```cmd
winget upgrade --id Microsoft.FoundryLocal
```
- Verificar versión:
```cmd
foundry --version
```

## 2) Conceptos básicos de CLI (Tres categorías)

- Modelo:
```cmd
foundry model --help
foundry model list
foundry model run gpt-oss-20b
```
- Servicio:
```cmd
foundry service --help
foundry service status
foundry service ps
```
- Caché:
```cmd
foundry cache --help
foundry cache list
```

Notas:
- El servicio expone una API REST compatible con OpenAI. El puerto del endpoint se asigna dinámicamente; usa `foundry service status` para descubrirlo.
- Utiliza los SDKs para mayor comodidad; estos manejan automáticamente el descubrimiento del endpoint donde sea compatible.

## 3) Descubrir el Endpoint Local (Puerto Dinámico)

Foundry Local asigna un puerto dinámico cada vez que el servicio se inicia:
```cmd
foundry service status
```
Usa el `http://localhost:<PORT>` reportado como tu `base_url` con rutas compatibles con OpenAI (por ejemplo, `/v1/chat/completions`).

## 4) Prueba rápida con el SDK de Python de OpenAI

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
Referencias:
- Integración con SDK: https://learn.microsoft.com/azure/ai-foundry/foundry-local/how-to/how-to-integrate-with-inference-sdks

## 5) Trae tu propio modelo (Compilar con Olive)

Si necesitas un modelo que no esté en el catálogo, compílalo a ONNX para Foundry Local usando Olive.

Flujo general (consulta la documentación para los pasos):
```cmd
foundry cache cd models
foundry cache list
foundry model run llama-3.2 --verbose
```
Documentación:
- Compilar BYOM: https://learn.microsoft.com/azure/ai-foundry/foundry-local/how-to/how-to-compile-hugging-face-models

## 6) Solución de problemas

- Verifica el estado del servicio y los registros:
```cmd
foundry service status
foundry service diag
```
- Limpia o mueve la caché:
```cmd
foundry cache list
foundry cache remove <model>
foundry cache cd <path>
```
- Actualiza a la última versión preliminar:
```cmd
winget upgrade --id Microsoft.FoundryLocal
```

## 7) Experiencia relacionada para desarrolladores en Windows

- Opciones de IA local vs en la nube en Windows, incluyendo Foundry Local y Windows ML:
  https://learn.microsoft.com/windows/ai/cloud-ai#key-decision-factors-for-app-developers
- VS Code AI Toolkit con Foundry Local (usa `foundry service status` para obtener la URL del endpoint de chat):
  https://learn.microsoft.com/azure/ai-foundry/foundry-local/concepts/foundry-local-architecture#key-components

---

