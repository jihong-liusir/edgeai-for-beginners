<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "7f0c6af41a1ae2c5a770c8170da8bd6e",
  "translation_date": "2025-09-30T22:52:10+00:00",
  "source_file": "Module08/samples/06/README.md",
  "language_code": "en"
}
-->
# Session 6 Sample: Models as Tools

This sample demonstrates a basic router combined with a tool registry that selects a model based on the user's input and interacts with Foundry Local’s OpenAI-compatible endpoint.

## Files
- `router.py`: A simple registry and heuristic-based routing; includes endpoint discovery and health checks.

## Run (cmd.exe)
```cmd
cd Module08
.\.venv\Scripts\activate
REM Start whatever models you plan to route to
foundry model run phi-4-mini
foundry model run qwen2.5-7b
foundry model run deepseek-r1-7b

python samples\06\router.py "Explain how local-first AI improves privacy in two sentences."
```

## Notes
- The router uses straightforward keyword-based heuristics to choose between `general`, `reasoning`, and `code` tools, and displays `/v1/models` upon startup.
- Configuration is done through environment variables:
```cmd
set BASE_URL=http://localhost:8000
set API_KEY=
REM Override models per tool
set GENERAL_MODEL=phi-4-mini
set REASONING_MODEL=deepseek-r1-7b
set CODE_MODEL=qwen2.5-7b
REM Or provide a full JSON registry
set TOOL_REGISTRY={"general":{"model":"phi-4-mini"},"reasoning":{"model":"deepseek-r1-7b"},"code":{"model":"qwen2.5-7b"}}
```

## References
- Foundry Local (Learn): https://learn.microsoft.com/azure/ai-foundry/foundry-local/
- Integration with inference SDKs: https://learn.microsoft.com/azure/ai-foundry/foundry-local/how-to/how-to-integrate-with-inference-sdks

---

**Disclaimer**:  
This document has been translated using the AI translation service [Co-op Translator](https://github.com/Azure/co-op-translator). While we aim for accuracy, please note that automated translations may contain errors or inaccuracies. The original document in its native language should be regarded as the authoritative source. For critical information, professional human translation is recommended. We are not responsible for any misunderstandings or misinterpretations resulting from the use of this translation.