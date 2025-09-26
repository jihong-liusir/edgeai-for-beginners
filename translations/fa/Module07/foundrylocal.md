<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "02b037f55de779607eb12edcc7a7fcf2",
  "translation_date": "2025-09-26T18:17:15+00:00",
  "source_file": "Module07/foundrylocal.md",
  "language_code": "fa"
}
-->
# Foundry Local در ویندوز و مک

این راهنما به شما کمک می‌کند تا Microsoft Foundry Local را در ویندوز و مک نصب، اجرا و یکپارچه کنید. تمامی مراحل و دستورات با مستندات Microsoft Learn تأیید شده‌اند.

- شروع به کار: https://learn.microsoft.com/azure/ai-foundry/foundry-local/get-started
- معماری: https://learn.microsoft.com/azure/ai-foundry/foundry-local/concepts/foundry-local-architecture
- مرجع CLI: https://learn.microsoft.com/azure/ai-foundry/foundry-local/reference/reference-cli
- یکپارچه‌سازی SDKها: https://learn.microsoft.com/azure/ai-foundry/foundry-local/how-to/how-to-integrate-with-inference-sdks
- کامپایل مدل‌های HF (BYOM): https://learn.microsoft.com/azure/ai-foundry/foundry-local/how-to/how-to-compile-hugging-face-models
- هوش مصنوعی ویندوز: محلی در مقابل ابری: https://learn.microsoft.com/windows/ai/cloud-ai#key-decision-factors-for-app-developers

## 1) نصب / ارتقا در ویندوز

- نصب:
```cmd
winget install Microsoft.FoundryLocal
```
- ارتقا:
```cmd
winget upgrade --id Microsoft.FoundryLocal
```
- بررسی نسخه:
```cmd
foundry --version
```
     
**نصب / مک**

**MacOS**: 
یک ترمینال باز کنید و دستور زیر را اجرا کنید:
```bash
   brew tap microsoft/foundrylocal
   brew install foundrylocal
```

## 2) اصول CLI (سه دسته)

- مدل:
```cmd
foundry model --help
foundry model list
foundry model run gpt-oss-20b
```
- سرویس:
```cmd
foundry service --help
foundry service status
foundry service ps
```
- کش:
```cmd
foundry cache --help
foundry cache list
```

نکات:
- سرویس یک API REST سازگار با OpenAI را ارائه می‌دهد. پورت نقطه پایانی به صورت پویا تخصیص داده می‌شود؛ از `foundry service status` برای کشف آن استفاده کنید.
- برای راحتی از SDKها استفاده کنید؛ آن‌ها کشف نقطه پایانی را به صورت خودکار انجام می‌دهند، جایی که پشتیبانی می‌شود.

## 3) کشف نقطه پایانی محلی (پورت پویا)

Foundry Local هر بار که سرویس شروع می‌شود یک پورت پویا تخصیص می‌دهد:
```cmd
foundry service status
```
از `http://localhost:<PORT>` گزارش شده به عنوان `base_url` خود با مسیرهای سازگار با OpenAI استفاده کنید (برای مثال، `/v1/chat/completions`).

## 4) آزمایش سریع با OpenAI Python SDK

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
مراجع:
- یکپارچه‌سازی SDK: https://learn.microsoft.com/azure/ai-foundry/foundry-local/how-to/how-to-integrate-with-inference-sdks

## 5) مدل خود را بیاورید (کامپایل با Olive)

اگر به مدلی نیاز دارید که در کاتالوگ موجود نیست، آن را با استفاده از Olive به ONNX برای Foundry Local کامپایل کنید.

جریان کلی (برای مراحل به مستندات مراجعه کنید):
```cmd
foundry cache cd models
foundry cache list
foundry model run llama-3.2 --verbose
```
مستندات:
- کامپایل BYOM: https://learn.microsoft.com/azure/ai-foundry/foundry-local/how-to/how-to-compile-hugging-face-models

## 6) رفع اشکال

- بررسی وضعیت سرویس و لاگ‌ها:
```cmd
foundry service status
foundry service diag
```
- پاک کردن یا انتقال کش:
```cmd
foundry cache list
foundry cache remove <model>
foundry cache cd <path>
```
- به‌روزرسانی به آخرین پیش‌نمایش:
```cmd
winget upgrade --id Microsoft.FoundryLocal
```

## 7) تجربه مرتبط توسعه‌دهندگان ویندوز

- انتخاب‌های هوش مصنوعی محلی در مقابل ابری ویندوز، شامل Foundry Local و Windows ML:
  https://learn.microsoft.com/windows/ai/cloud-ai#key-decision-factors-for-app-developers
- ابزار هوش مصنوعی VS Code با Foundry Local (از `foundry service status` برای دریافت URL نقطه پایانی چت استفاده کنید):
  https://learn.microsoft.com/azure/ai-foundry/foundry-local/concepts/foundry-local-architecture#key-components

---

