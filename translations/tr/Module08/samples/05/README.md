<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "4f786f5ea706270620f8e5dfb088e0c0",
  "translation_date": "2025-09-22T18:34:34+00:00",
  "source_file": "Module08/samples/05/README.md",
  "language_code": "tr"
}
-->
# Oturum 5 Örneği: Çoklu Ajan Orkestrasyonu

Bu örnek, Foundry Local’ın OpenAI uyumlu uç noktasını kullanarak bir koordinatör + uzmanlar modelini göstermektedir.

## Çalıştır (cmd.exe)
```cmd
cd Module08
.\.venv\Scripts\activate
foundry model run phi-4-mini
python -m samples.05.agents.coordinator
```

## Doğrulama
```cmd
curl http://localhost:8000/v1/models
```

## Sorun Giderme
- Eğer VS Code `coordinator.py` dosyasında `import specialists` ifadesini çözümlenmemiş olarak işaretliyorsa, modül olarak çalıştırdığınızdan ve yorumlayıcının `Module08/.venv` dizinine işaret ettiğinden emin olun:
	- Çalıştır: `python -m samples.05.agents.coordinator`
	- Yorumlayıcı seç: `Module08/.venv/Scripts/python.exe` (Ctrl+Shift+P → Python: Select Interpreter)

## Referanslar
- Foundry Local (Öğren): https://learn.microsoft.com/azure/ai-foundry/foundry-local/
- Azure AI Ajanları genel bakış: https://learn.microsoft.com/azure/ai-services/agents/overview
- Fonksiyon çağırma örneği (Foundry Local): https://github.com/microsoft/Foundry-Local/tree/main/samples/python/functioncalling

---

