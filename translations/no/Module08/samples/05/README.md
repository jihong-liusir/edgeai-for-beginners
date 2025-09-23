<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "4f786f5ea706270620f8e5dfb088e0c0",
  "translation_date": "2025-09-22T20:26:00+00:00",
  "source_file": "Module08/samples/05/README.md",
  "language_code": "no"
}
-->
# Sesjon 5 Eksempel: Orkestrering av flere agenter

Dette eksemplet demonstrerer et koordinator + spesialister-mønster ved bruk av Foundry Locals OpenAI-kompatible endepunkt.

## Kjør (cmd.exe)
```cmd
cd Module08
.\.venv\Scripts\activate
foundry model run phi-4-mini
python -m samples.05.agents.coordinator
```

## Valider
```cmd
curl http://localhost:8000/v1/models
```

## Feilsøking
- Hvis VS Code markerer `import specialists` som uløst i `coordinator.py`, sørg for at du kjører som et modul og at tolken peker til `Module08/.venv`:
	- Kjør: `python -m samples.05.agents.coordinator`
	- Velg tolk: `Module08/.venv/Scripts/python.exe` (Ctrl+Shift+P → Python: Select Interpreter)

## Referanser
- Foundry Local (Lær): https://learn.microsoft.com/azure/ai-foundry/foundry-local/
- Oversikt over Azure AI-agenter: https://learn.microsoft.com/azure/ai-services/agents/overview
- Eksempel på funksjonskall (Foundry Local): https://github.com/microsoft/Foundry-Local/tree/main/samples/python/functioncalling

---

