<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "4f786f5ea706270620f8e5dfb088e0c0",
  "translation_date": "2025-09-22T18:34:20+00:00",
  "source_file": "Module08/samples/05/README.md",
  "language_code": "pa"
}
-->
# ਸੈਸ਼ਨ 5 ਨਮੂਨਾ: ਮਲਟੀ-ਏਜੰਟ ਆਰਕਸਟ੍ਰੇਸ਼ਨ

ਇਹ ਨਮੂਨਾ Foundry Local ਦੇ OpenAI-ਅਨੁਕੂਲ ਐਂਡਪੌਇੰਟ ਦੀ ਵਰਤੋਂ ਕਰਦੇ ਹੋਏ ਇੱਕ ਕੋਆਰਡੀਨੇਟਰ + ਸਪੈਸ਼ਲਿਸਟ ਪੈਟਰਨ ਨੂੰ ਦਰਸਾਉਂਦਾ ਹੈ।

## ਚਲਾਓ (cmd.exe)
```cmd
cd Module08
.\.venv\Scripts\activate
foundry model run phi-4-mini
python -m samples.05.agents.coordinator
```

## ਵੈਧਤਾ
```cmd
curl http://localhost:8000/v1/models
```

## ਸਮੱਸਿਆ ਹੱਲ
- ਜੇ VS Code `import specialists` ਨੂੰ `coordinator.py` ਵਿੱਚ ਅਣਸੁਲਝਿਆ ਦਿਖਾਉਂਦਾ ਹੈ, ਤਾਂ ਯਕੀਨੀ ਬਣਾਓ ਕਿ ਤੁਸੀਂ ਮੌਡਿਊਲ ਵਜੋਂ ਚਲਾ ਰਹੇ ਹੋ ਅਤੇ ਇੰਟਰਪ੍ਰੀਟਰ `Module08/.venv` ਨੂੰ ਪੋਇੰਟ ਕਰਦਾ ਹੈ:
	- ਚਲਾਓ: `python -m samples.05.agents.coordinator`
	- ਇੰਟਰਪ੍ਰੀਟਰ ਚੁਣੋ: `Module08/.venv/Scripts/python.exe` (Ctrl+Shift+P → Python: Select Interpreter)

## ਹਵਾਲੇ
- Foundry Local (ਸਿੱਖੋ): https://learn.microsoft.com/azure/ai-foundry/foundry-local/
- Azure AI Agents ਝਲਕ: https://learn.microsoft.com/azure/ai-services/agents/overview
- ਫੰਕਸ਼ਨ ਕਾਲਿੰਗ ਨਮੂਨਾ (Foundry Local): https://github.com/microsoft/Foundry-Local/tree/main/samples/python/functioncalling

---

