<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "4f786f5ea706270620f8e5dfb088e0c0",
  "translation_date": "2025-09-22T21:53:38+00:00",
  "source_file": "Module08/samples/05/README.md",
  "language_code": "he"
}
-->
# דוגמה למפגש 5: תזמור רב-סוכנים

דוגמה זו מציגה תבנית של מתאם + מומחים באמצעות נקודת הקצה התואמת ל-OpenAI של Foundry Local.

## הפעלה (cmd.exe)
```cmd
cd Module08
.\.venv\Scripts\activate
foundry model run phi-4-mini
python -m samples.05.agents.coordinator
```

## אימות
```cmd
curl http://localhost:8000/v1/models
```

## פתרון בעיות
- אם VS Code מסמן את `import specialists` כלא פתור ב-`coordinator.py`, ודא שאתה מפעיל כמודול והפרשן מצביע על `Module08/.venv`:
	- הפעלה: `python -m samples.05.agents.coordinator`
	- בחירת פרשן: `Module08/.venv/Scripts/python.exe` (Ctrl+Shift+P → Python: Select Interpreter)

## הפניות
- Foundry Local (לימוד): https://learn.microsoft.com/azure/ai-foundry/foundry-local/
- סקירה כללית של סוכני Azure AI: https://learn.microsoft.com/azure/ai-services/agents/overview
- דוגמת קריאת פונקציות (Foundry Local): https://github.com/microsoft/Foundry-Local/tree/main/samples/python/functioncalling

---

