<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "48d0fb38be925084a6ebd957d4b045e5",
  "translation_date": "2025-10-09T10:51:30+00:00",
  "source_file": "Workshop/Readme.md",
  "language_code": "pa"
}
-->
# EdgeAI ਸ਼ੁਰੂਆਤੀ ਲਈ - ਵਰਕਸ਼ਾਪ

> **ਪ੍ਰੋਡਕਸ਼ਨ-ਤਿਆਰ ਐਜ AI ਐਪਲੀਕੇਸ਼ਨ ਬਣਾਉਣ ਲਈ ਹੱਥ-ਅਨੁਭਵ ਸਿੱਖਣ ਦਾ ਰਾਹ**
>
> Microsoft Foundry Local ਨਾਲ ਸਥਾਨਕ AI ਡਿਪਲੌਇਮੈਂਟ ਵਿੱਚ ਮਾਹਰ ਬਣੋ, ਪਹਿਲੀ ਚੈਟ ਪੂਰੀ ਕਰਨ ਤੋਂ ਲੈ ਕੇ 6 ਤਰੱਕੀਸ਼ੀਲ ਸੈਸ਼ਨਾਂ ਵਿੱਚ ਮਲਟੀ-ਏਜੰਟ ਆਰਕੇਸਟ੍ਰੇਸ਼ਨ ਤੱਕ।

---

## 🎯 ਪਰਿਚਯ

**EdgeAI ਸ਼ੁਰੂਆਤੀ ਲਈ ਵਰਕਸ਼ਾਪ** ਵਿੱਚ ਤੁਹਾਡਾ ਸਵਾਗਤ ਹੈ - ਸਥਾਨਕ ਹਾਰਡਵੇਅਰ 'ਤੇ ਪੂਰੀ ਤਰ੍ਹਾਂ ਚਲਣ ਵਾਲੀਆਂ ਬੁੱਧੀਮਾਨ ਐਪਲੀਕੇਸ਼ਨ ਬਣਾਉਣ ਲਈ ਤੁਹਾਡਾ ਪ੍ਰਯੋਗਕਰਤਾ, ਹੱਥ-ਅਨੁਭਵ ਗਾਈਡ। ਇਹ ਵਰਕਸ਼ਾਪ ਸਿਧਾਂਤਕ Edge AI ਧਾਰਨਾਵਾਂ ਨੂੰ ਵਾਸਤਵਿਕ ਦੁਨੀਆ ਦੇ ਹੁਨਰਾਂ ਵਿੱਚ ਬਦਲ ਦਿੰਦੀ ਹੈ, ਜੋ ਕਿ Microsoft Foundry Local ਅਤੇ Small Language Models (SLMs) ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਤਰੱਕੀਸ਼ੀਲ ਚੁਣੌਤੀਪੂਰਨ ਅਭਿਆਸਾਂ ਰਾਹੀਂ।

### ਇਹ ਵਰਕਸ਼ਾਪ ਕਿਉਂ?

**Edge AI ਕ੍ਰਾਂਤੀ ਆ ਗਈ ਹੈ**

ਸੰਸਾਰ ਭਰ ਵਿੱਚ ਸੰਗਠਨ ਤਿੰਨ ਮਹੱਤਵਪੂਰਨ ਕਾਰਨਾਂ ਲਈ ਕਲਾਉਡ-ਨਿਰਭਰਤ AI ਤੋਂ ਐਜ ਕੰਪਿਊਟਿੰਗ ਵੱਲ ਬਦਲ ਰਹੇ ਹਨ:

1. **ਗੋਪਨੀਯਤਾ ਅਤੇ ਅਨੁਕੂਲਤਾ** - ਸੰਵੇਦਨਸ਼ੀਲ ਡਾਟਾ ਨੂੰ ਸਥਾਨਕ ਤੌਰ 'ਤੇ ਪ੍ਰਕਿਰਿਆ ਕਰੋ ਬਿਨਾਂ ਕਲਾਉਡ ਟ੍ਰਾਂਸਮਿਸ਼ਨ ਦੇ (HIPAA, GDPR, ਵਿੱਤੀ ਨਿਯਮ)
2. **ਪ੍ਰਦਰਸ਼ਨ** - ਨੈਟਵਰਕ ਲੈਟੈਂਸੀ ਨੂੰ ਖਤਮ ਕਰੋ (50-500ms ਸਥਾਨਕ ਵਿਰੁੱਧ 500-2000ms ਕਲਾਉਡ ਰਾਊਂਡ-ਟ੍ਰਿਪ)
3. **ਲਾਗਤ ਦਾ ਨਿਯੰਤਰਣ** - ਪ੍ਰਤੀ-ਟੋਕਨ API ਲਾਗਤਾਂ ਨੂੰ ਹਟਾਓ ਅਤੇ ਕਲਾਉਡ ਖਰਚਾਂ ਤੋਂ ਬਿਨਾਂ ਸਕੇਲ ਕਰੋ

**ਪਰ Edge AI ਵੱਖਰਾ ਹੈ**

ਸਥਾਨਕ ਤੌਰ 'ਤੇ AI ਚਲਾਉਣ ਲਈ ਨਵੇਂ ਹੁਨਰਾਂ ਦੀ ਲੋੜ ਹੁੰਦੀ ਹੈ:
- ਸਰੋਤਾਂ ਦੀ ਪਾਬੰਦੀ ਲਈ ਮਾਡਲ ਚੋਣ ਅਤੇ ਅਨੁਕੂਲਤਾ
- ਸਥਾਨਕ ਸੇਵਾ ਪ੍ਰਬੰਧਨ ਅਤੇ ਹਾਰਡਵੇਅਰ ਐਕਸਲੇਰੇਸ਼ਨ
- ਛੋਟੇ ਮਾਡਲਾਂ ਲਈ ਪ੍ਰੋਮਪਟ ਇੰਜੀਨੀਅਰਿੰਗ
- ਐਜ ਡਿਵਾਈਸਾਂ ਲਈ ਪ੍ਰੋਡਕਸ਼ਨ ਡਿਪਲੌਇਮੈਂਟ ਪੈਟਰਨ

**ਇਹ ਵਰਕਸ਼ਾਪ ਉਹ ਹੁਨਰ ਪ੍ਰਦਾਨ ਕਰਦਾ ਹੈ**

6 ਕੇਂਦਰਿਤ ਸੈਸ਼ਨਾਂ (~3 ਘੰਟੇ ਕੁੱਲ) ਵਿੱਚ, ਤੁਸੀਂ "ਹੈਲੋ ਵਰਲਡ" ਤੋਂ ਪ੍ਰੋਡਕਸ਼ਨ-ਤਿਆਰ ਮਲਟੀ-ਏਜੰਟ ਸਿਸਟਮਾਂ ਨੂੰ ਡਿਪਲੌਇ ਕਰਨ ਤੱਕ ਤਰੱਕੀ ਕਰੋਗੇ - ਸਾਰੇ ਸਥਾਨਕ ਤੌਰ 'ਤੇ ਤੁਹਾਡੇ ਮਸ਼ੀਨ 'ਤੇ ਚਲ ਰਹੇ ਹਨ।

---

## 📚 ਸਿੱਖਣ ਦੇ ਉਦੇਸ਼

ਇਸ ਵਰਕਸ਼ਾਪ ਨੂੰ ਪੂਰਾ ਕਰਨ ਦੁਆਰਾ, ਤੁਸੀਂ ਇਹ ਕਰਨ ਦੇ ਯੋਗ ਹੋਵੋਗੇ:

### ਮੁੱਖ ਯੋਗਤਾਵਾਂ
1. **ਸਥਾਨਕ AI ਸੇਵਾਵਾਂ ਨੂੰ ਡਿਪਲੌਇ ਅਤੇ ਪ੍ਰਬੰਧਿਤ ਕਰੋ**
   - Microsoft Foundry Local ਨੂੰ ਇੰਸਟਾਲ ਅਤੇ ਕਨਫਿਗਰ ਕਰੋ
   - ਐਜ ਡਿਪਲੌਇਮੈਂਟ ਲਈ ਉਚਿਤ ਮਾਡਲ ਚੁਣੋ
   - ਮਾਡਲ ਲਾਈਫਸਾਈਕਲ (ਡਾਊਨਲੋਡ, ਲੋਡ, ਕੈਸ਼) ਪ੍ਰਬੰਧਿਤ ਕਰੋ
   - ਸਰੋਤਾਂ ਦੀ ਵਰਤੋਂ ਦੀ ਨਿਗਰਾਨੀ ਕਰੋ ਅਤੇ ਪ੍ਰਦਰਸ਼ਨ ਨੂੰ ਅਨੁਕੂਲ ਬਣਾਓ

2. **AI-ਚਾਲਤ ਐਪਲੀਕੇਸ਼ਨ ਬਣਾਓ**
   - ਸਥਾਨਕ ਤੌਰ 'ਤੇ OpenAI-ਅਨੁਕੂਲ ਚੈਟ ਪੂਰੀਆਂ ਲਾਗੂ ਕਰੋ
   - Small Language Models ਲਈ ਪ੍ਰਭਾਵਸ਼ਾਲੀ ਪ੍ਰੋਮਪਟ ਡਿਜ਼ਾਈਨ ਕਰੋ
   - ਬਿਹਤਰ UX ਲਈ ਸਟ੍ਰੀਮਿੰਗ ਜਵਾਬਾਂ ਨੂੰ ਸੰਭਾਲੋ
   - ਸਥਾਨਕ ਮਾਡਲਾਂ ਨੂੰ ਮੌਜੂਦਾ ਐਪਲੀਕੇਸ਼ਨਾਂ ਵਿੱਚ ਇੰਟੀਗ੍ਰੇਟ ਕਰੋ

3. **RAG (Retrieval Augmented Generation) ਸਿਸਟਮ ਬਣਾਓ**
   - ਐਮਬੈਡਿੰਗਸ ਨਾਲ ਸੈਮਾਂਟਿਕ ਖੋਜ ਬਣਾਓ
   - LLM ਜਵਾਬਾਂ ਨੂੰ ਡੋਮੇਨ-ਵਿਸ਼ੇਸ਼ ਗਿਆਨ ਵਿੱਚ ਜਮ੍ਹਾ ਕਰੋ
   - ਉਦਯੋਗ-ਮਿਆਰੀ ਮਾਪਦੰਡਾਂ ਨਾਲ RAG ਗੁਣਵੱਤਾ ਦਾ ਮੁਲਾਂਕਣ ਕਰੋ
   - ਪ੍ਰੋਟੋਟਾਈਪ ਤੋਂ ਪ੍ਰੋਡਕਸ਼ਨ ਤੱਕ ਸਕੇਲ ਕਰੋ

4. **ਮਾਡਲ ਪ੍ਰਦਰਸ਼ਨ ਨੂੰ ਅਨੁਕੂਲ ਬਣਾਓ**
   - ਤੁਹਾਡੇ ਉਪਯੋਗ ਮਾਮਲੇ ਲਈ ਕਈ ਮਾਡਲਾਂ ਦਾ ਬੈਂਚਮਾਰਕ ਕਰੋ
   - ਲੈਟੈਂਸੀ, ਥਰੂਪੁੱਟ, ਅਤੇ ਪਹਿਲੇ ਟੋਕਨ ਸਮੇਂ ਨੂੰ ਮਾਪੋ
   - ਗਤੀ/ਗੁਣਵੱਤਾ ਦੇ ਵਪਾਰ-ਬਦਲਾਂ ਦੇ ਆਧਾਰ 'ਤੇ ਉਚਿਤ ਮਾਡਲ ਚੁਣੋ
   - ਅਸਲ ਸਥਿਤੀਆਂ ਵਿੱਚ SLM ਵਿਰੁੱਧ LLM ਵਪਾਰ-ਬਦਲਾਂ ਦੀ ਤੁਲਨਾ ਕਰੋ

5. **ਮਲਟੀ-ਏਜੰਟ ਸਿਸਟਮਾਂ ਨੂੰ ਆਰਕੇਸਟ੍ਰੇਟ ਕਰੋ**
   - ਵੱਖ-ਵੱਖ ਕੰਮਾਂ ਲਈ ਵਿਸ਼ੇਸ਼ ਏਜੰਟਾਂ ਡਿਜ਼ਾਈਨ ਕਰੋ
   - ਏਜੰਟ ਮੈਮੋਰੀ ਅਤੇ ਸੰਦਰਭ ਪ੍ਰਬੰਧਨ ਲਾਗੂ ਕਰੋ
   - ਜਟਿਲ ਵਰਕਫਲੋਜ਼ ਵਿੱਚ ਏਜੰਟਾਂ ਨੂੰ ਸਮਨਵਿਤ ਕਰੋ
   - ਕਈ ਮਾਡਲਾਂ ਵਿੱਚ ਬੁੱਧੀਮਾਨੀ ਨਾਲ ਬੇਨਤੀਆਂ ਨੂੰ ਰੂਟ ਕਰੋ

6. **ਪ੍ਰੋਡਕਸ਼ਨ-ਤਿਆਰ ਹੱਲਾਂ ਨੂੰ ਡਿਪਲੌਇ ਕਰੋ**
   - ਗਲਤੀ ਸੰਭਾਲਣ ਅਤੇ ਦੁਬਾਰਾ ਕੋਸ਼ਿਸ਼ ਕਰਨ ਦੀ ਲਾਜ਼ਮੀ ਲਾਗੂ ਕਰੋ
   - ਟੋਕਨ ਦੀ ਵਰਤੋਂ ਅਤੇ ਸਿਸਟਮ ਸਰੋਤਾਂ ਦੀ ਨਿਗਰਾਨੀ ਕਰੋ
   - ਮਾਡਲ-ਜਿਵੇਂ-ਟੂਲ ਪੈਟਰਨ ਨਾਲ ਸਕੇਲਯੋਗ ਆਰਕੀਟੈਕਚਰ ਬਣਾਓ
   - ਐਜ ਤੋਂ ਹਾਈਬ੍ਰਿਡ (ਐਜ + ਕਲਾਉਡ) ਤੱਕ ਮਾਈਗ੍ਰੇਸ਼ਨ ਪਾਥ ਦੀ ਯੋਜਨਾ ਬਣਾਓ

---

## 🎓 ਸਿੱਖਣ ਦੇ ਨਤੀਜੇ

### ਤੁਸੀਂ ਕੀ ਬਣਾਓਗੇ

ਵਰਕਸ਼ਾਪ ਦੇ ਅੰਤ ਤੱਕ, ਤੁਸੀਂ ਇਹ ਬਣਾਇਆ ਹੋਵੇਗਾ:

| ਸੈਸ਼ਨ | ਡਿਲੀਵਰੇਬਲ | ਪ੍ਰਦਰਸ਼ਿਤ ਹੁਨਰ |
|---------|-------------|---------------------|
| **1** | ਸਟ੍ਰੀਮਿੰਗ ਨਾਲ ਚੈਟ ਐਪਲੀਕੇਸ਼ਨ | ਸੇਵਾ ਸੈਟਅਪ, ਬੁਨਿਆਦੀ ਪੂਰੀਆਂ, ਸਟ੍ਰੀਮਿੰਗ UX |
| **2** | RAG ਸਿਸਟਮ ਮੁਲਾਂਕਣ ਨਾਲ | ਐਮਬੈਡਿੰਗਸ, ਸੈਮਾਂਟਿਕ ਖੋਜ, ਗੁਣਵੱਤਾ ਮਾਪਦੰਡ |
| **3** | ਮਲਟੀ-ਮਾਡਲ ਬੈਂਚਮਾਰਕ ਸੂਟ | ਪ੍ਰਦਰਸ਼ਨ ਮਾਪ, ਮਾਡਲ ਤੁਲਨਾ |
| **4** | SLM ਵਿਰੁੱਧ LLM ਤੁਲਨਾਕਾਰ | ਵਪਾਰ-ਬਦਲ ਵਿਸ਼ਲੇਸ਼ਣ, ਅਨੁਕੂਲਤਾ ਰਣਨੀਤੀਆਂ |
| **5** | ਮਲਟੀ-ਏਜੰਟ ਆਰਕੇਸਟ੍ਰੇਟਰ | ਏਜੰਟ ਡਿਜ਼ਾਈਨ, ਮੈਮੋਰੀ ਪ੍ਰਬੰਧਨ, ਸਮਨਵਯ |
| **6** | ਬੁੱਧੀਮਾਨ ਰੂਟਿੰਗ ਸਿਸਟਮ | ਇਰਾਦਾ ਪਛਾਣ, ਮਾਡਲ ਚੋਣ, ਸਕੇਲਯੋਗਤਾ |

### ਯੋਗਤਾ ਮੈਟ੍ਰਿਕਸ

| ਹੁਨਰ ਪੱਧਰ | ਸੈਸ਼ਨ 1-2 | ਸੈਸ਼ਨ 3-4 | ਸੈਸ਼ਨ 5-6 |
|-------------|-------------|-------------|-------------|
| **ਸ਼ੁਰੂਆਤੀ** | ✅ ਸੈਟਅਪ ਅਤੇ ਬੁਨਿਆਦੀਆਂ | ⚠️ ਚੁਣੌਤੀਪੂਰਨ | ❌ ਬਹੁਤ ਅਗਰ |
| **ਮੱਧਮ** | ✅ ਤੇਜ਼ ਸਮੀਖਾ | ✅ ਮੁੱਖ ਸਿੱਖਣ | ⚠️ ਖਿੱਚ ਦੇ ਲਕਸ਼ |
| **ਅਗਰ** | ✅ ਆਸਾਨੀ ਨਾਲ | ✅ ਸੁਧਾਰ | ✅ ਪ੍ਰੋਡਕਸ਼ਨ ਪੈਟਰਨ |

### ਕਰੀਅਰ-ਤਿਆਰ ਹੁਨਰ

**ਇਸ ਵਰਕਸ਼ਾਪ ਦੇ ਬਾਅਦ, ਤੁਸੀਂ ਤਿਆਰ ਹੋਵੋਗੇ:**

✅ **ਗੋਪਨੀਯਤਾ-ਪਹਿਲਾਂ ਐਪਲੀਕੇਸ਼ਨ ਬਣਾਓ**
- ਸਥਾਨਕ ਤੌਰ 'ਤੇ PHI/PII ਨੂੰ ਸੰਭਾਲਣ ਵਾਲੀਆਂ ਹੈਲਥਕੇਅਰ ਐਪਸ
- ਅਨੁਕੂਲਤਾ ਦੀ ਲੋੜ ਵਾਲੀਆਂ ਵਿੱਤੀ ਸੇਵਾਵਾਂ
- ਡਾਟਾ ਸਾਰਵਭੌਮਤਾ ਦੀ ਲੋੜ ਵਾਲੇ ਸਰਕਾਰੀ ਸਿਸਟਮ

✅ **ਐਜ ਵਾਤਾਵਰਣਾਂ ਲਈ ਅਨੁਕੂਲ ਬਣਾਓ**
- ਸੀਮਿਤ ਸਰੋਤਾਂ ਵਾਲੇ IoT ਡਿਵਾਈਸ
- ਆਫਲਾਈਨ-ਪਹਿਲਾਂ ਮੋਬਾਈਲ ਐਪਲੀਕੇਸ਼ਨ
- ਘੱਟ-ਲੈਟੈਂਸੀ ਰੀਅਲ-ਟਾਈਮ ਸਿਸਟਮ

✅ **ਬੁੱਧੀਮਾਨ ਆਰਕੀਟੈਕਚਰ ਡਿਜ਼ਾਈਨ ਕਰੋ**
- ਜਟਿਲ ਵਰਕਫਲੋਜ਼ ਲਈ ਮਲਟੀ-ਏਜੰਟ ਸਿਸਟਮ
- ਹਾਈਬ੍ਰਿਡ ਐਜ-ਕਲਾਉਡ ਡਿਪਲੌਇਮੈਂਟ
- ਲਾਗਤ-ਅਨੁਕੂਲ AI ਇੰਫਰਾਸਟਰਕਚਰ

✅ **ਐਜ AI ਪਹਲਾਂ ਦੀ ਅਗਵਾਈ ਕਰੋ**
- ਪ੍ਰੋਜੈਕਟਾਂ ਲਈ Edge AI ਸੰਭਾਵਨਾ ਦਾ ਮੁਲਾਂਕਣ ਕਰੋ
- ਉਚਿਤ ਮਾਡਲ ਅਤੇ ਫਰੇਮਵਰਕ ਚੁਣੋ
- ਸਕੇਲਯੋਗ ਸਥਾਨਕ AI ਹੱਲਾਂ ਦੀ ਆਰਕੀਟੈਕਚਰ ਬਣਾਓ

---

## 🗺️ ਵਰਕਸ਼ਾਪ ਦੀ ਬਣਤਰ

### ਸੈਸ਼ਨ ਝਲਕ (6 ਸੈਸ਼ਨ × 30 ਮਿੰਟ = 3 ਘੰਟੇ)

| ਸੈਸ਼ਨ | ਵਿਸ਼ਾ | ਕੇਂਦਰ | ਅਵਧੀ |
|---------|-------|-------|----------|
| **1** | Foundry Local ਨਾਲ ਸ਼ੁਰੂਆਤ | ਇੰਸਟਾਲ, ਵੈਲਿਡੇਟ, ਪਹਿਲੀਆਂ ਪੂਰੀਆਂ | 30 ਮਿੰਟ |
| **2** | RAG ਨਾਲ AI ਹੱਲ ਬਣਾਉਣਾ | ਪ੍ਰੋਮਪਟ ਇੰਜੀਨੀਅਰਿੰਗ, ਐਮਬੈਡਿੰਗਸ, ਮੁਲਾਂਕਣ | 30 ਮਿੰਟ |
| **3** | ਖੁੱਲੇ ਸਰੋਤ ਮਾਡਲ | ਮਾਡਲ ਖੋਜ, ਬੈਂਚਮਾਰਕਿੰਗ, ਚੋਣ | 30 ਮਿੰਟ |
| **4** | ਅਗਰ ਮਾਡਲ | SLM ਵਿਰੁੱਧ LLM, ਅਨੁਕੂਲਤਾ, ਫਰੇਮਵਰਕ | 30 ਮਿੰਟ |
| **5** | AI-ਚਾਲਤ ਏਜੰਟ | ਏਜੰਟ ਡਿਜ਼ਾਈਨ, ਆਰਕੇਸਟ੍ਰੇਸ਼ਨ, ਮੈਮੋਰੀ | 30 ਮਿੰਟ |
| **6** | ਮਾਡਲ ਜਿਵੇਂ ਟੂਲ | ਰੂਟਿੰਗ, ਚੇਨਿੰਗ, ਸਕੇਲਿੰਗ ਰਣਨੀਤੀਆਂ | 30 ਮਿੰਟ |

---

## 🚀 ਤੇਜ਼ ਸ਼ੁਰੂਆਤ

### ਪੂਰਵ ਸ਼ਰਤਾਂ

**ਸਿਸਟਮ ਦੀਆਂ ਲੋੜਾਂ:**
- **OS**: Windows 10/11, macOS 11+, ਜਾਂ Linux (Ubuntu 20.04+)
- **RAM**: ਘੱਟੋ-ਘੱਟ 8GB, 16GB+ ਸਿਫਾਰਸ਼ੀ
- **ਸਟੋਰੇਜ**: ਮਾਡਲਾਂ ਲਈ 10GB+ ਖਾਲੀ ਜਗ੍ਹਾ
- **CPU**: AVX2 ਸਹਾਇਕ ਆਧੁਨਿਕ ਪ੍ਰੋਸੈਸਰ
- **GPU** (ਵਿਕਲਪਿਕ): CUDA-ਅਨੁਕੂਲ ਜਾਂ Qualcomm NPU ਐਕਸਲੇਰੇਸ਼ਨ ਲਈ

**ਸੌਫਟਵੇਅਰ ਦੀਆਂ ਲੋੜਾਂ:**
- **Python 3.8+** ([ਡਾਊਨਲੋਡ](https://www.python.org/downloads/))
- **Microsoft Foundry Local** ([ਇੰਸਟਾਲੇਸ਼ਨ ਗਾਈਡ](../../../Workshop))
- **Git** ([ਡਾਊਨਲੋਡ](https://git-scm.com/downloads))
- **Visual Studio Code** (ਸਿਫਾਰਸ਼ੀ) ([ਡਾਊਨਲੋਡ](https://code.visualstudio.com/))

### 3 ਕਦਮਾਂ ਵਿੱਚ ਸੈਟਅਪ

#### 1. Foundry Local ਇੰਸਟਾਲ ਕਰੋ

**Windows:**
```powershell
winget install Microsoft.FoundryLocal
```

**macOS:**
```bash
brew tap microsoft/foundrylocal
brew install foundrylocal
```

**ਇੰਸਟਾਲੇਸ਼ਨ ਦੀ ਪੁਸ਼ਟੀ ਕਰੋ:**
```bash
foundry --version
foundry service status
```

#### 2. ਰਿਪੋਜ਼ਟਰੀ ਕਲੋਨ ਕਰੋ ਅਤੇ Dependencies ਇੰਸਟਾਲ ਕਰੋ

```bash
# Clone repository
git clone https://github.com/microsoft/edgeai-for-beginners.git
cd edgeai-for-beginners/Workshop

# Create virtual environment
python -m venv .venv

# Activate virtual environment
# Windows:
.\.venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

#### 3. ਆਪਣਾ ਪਹਿਲਾ ਸੈਂਪਲ ਚਲਾਓ

```bash
# Start Foundry Local and load a model
foundry model run phi-4-mini

# Run the chat bootstrap sample
cd samples/session01
python chat_bootstrap.py "What is edge AI?"
```

**✅ ਸਫਲਤਾ!** ਤੁਹਾਨੂੰ Edge AI ਬਾਰੇ ਸਟ੍ਰੀਮਿੰਗ ਜਵਾਬ ਦੇਖਣਾ ਚਾਹੀਦਾ ਹੈ।

---

## 📦 ਵਰਕਸ਼ਾਪ ਸਰੋਤ

### Python ਸੈਂਪਲ

ਹਰ ਧਾਰਨਾ ਨੂੰ ਦਰਸਾਉਣ ਵਾਲੇ ਤਰੱਕੀਸ਼ੀਲ ਹੱਥ-ਅਨੁਭਵ ਉਦਾਹਰਨ:

| ਸੈਸ਼ਨ | ਸੈਂਪਲ | ਵੇਰਵਾ | ਚਲਾਉਣ ਦਾ ਸਮਾਂ |
|---------|--------|-------------|----------|
| 1 | [`chat_bootstrap.py`](../../../Workshop/samples/session01/chat_bootstrap.py) | ਬੁਨਿਆਦੀ ਅਤੇ ਸਟ੍ਰੀਮਿੰਗ ਚੈਟ | ~30s |
| 2 | [`rag_pipeline.py`](../../../Workshop/samples/session02/rag_pipeline.py) | ਐਮਬੈਡਿੰਗਸ ਨਾਲ RAG | ~45s |
| 2 | [`rag_eval_ragas.py`](../../../Workshop/samples/session02/rag_eval_ragas.py) | RAG ਗੁਣਵੱਤਾ ਮੁਲਾਂਕਣ | ~60s |
| 3 | [`benchmark_oss_models.py`](../../../Workshop/samples/session03/benchmark_oss_models.py) | ਮਲਟੀ-ਮਾਡਲ ਬੈਂਚਮਾਰਕਿੰਗ | ~2-3m |
| 4 | [`model_compare.py`](../../../Workshop/samples/session04/model_compare.py) | SLM ਵਿਰੁੱਧ LLM ਤੁਲਨਾ | ~45s |
| 5 | [`agents_orchestrator.py`](../../../Workshop/samples/session05/agents_orchestrator.py) | ਮਲਟੀ-ਏਜੰਟ ਸਿਸਟਮ | ~60s |
| 6 | [`models_router.py`](../../../Workshop/samples/session06/models_router.py) | ਇਰਾਦਾ-ਅਧਾਰਿਤ ਰੂਟਿੰਗ | ~45s |
| 6 | [`models_pipeline.py`](../../../Workshop/samples/session06/models_pipeline.py) | ਮਲਟੀ-ਸਟੈਪ ਪਾਈਪਲਾਈਨ | ~60s |

### Jupyter Notebooks

ਵਿਆਖਿਆਵਾਂ ਅਤੇ ਵਿਜ਼ੁਅਲਾਈਜ਼ੇਸ਼ਨ ਨਾਲ ਇੰਟਰੈਕਟਿਵ ਪੜਚੋਲ:

| ਸੈਸ਼ਨ | ਨੋਟਬੁੱਕ | ਵੇਰਵਾ | ਮੁਸ਼ਕਲ |
|---------|----------|-------------|------------|
| 1 | [`session01_chat_bootstrap.ipynb`](./notebooks/session01_chat_bootstrap.ipynb) | ਚੈਟ ਬੁਨਿਆਦੀਆਂ ਅਤੇ ਸਟ੍ਰੀਮਿੰਗ | ⭐ ਸ਼ੁਰੂਆਤੀ |
| 2 | [`session02_rag_pipeline.ipynb`](./notebooks/session02_rag_pipeline.ipynb) | RAG ਸਿਸਟਮ ਬਣਾਓ | ⭐⭐ ਮੱਧਮ |
| 2 | [`session02_rag_eval_ragas.ipynb`](./notebooks/session02_rag_eval_ragas.ipynb) | RAG ਗੁਣਵੱਤਾ ਦਾ ਮੁਲਾਂਕਣ ਕਰੋ | ⭐⭐ ਮੱਧਮ |
| 3 | [`session03_benchmark_oss_models.ipynb`](./notebooks/session03_benchmark_oss_models.ipynb) | ਮਾਡਲ ਬੈਂਚਮਾਰਕਿੰਗ | ⭐⭐ ਮੱਧਮ |
| 4 | [`session04_model_compare.ipynb`](./notebooks/session04_model_compare.ipynb) | ਮਾਡਲ ਤੁਲਨਾ | ⭐⭐ ਮੱਧਮ |
| 5 | [`session05_agents
ਹਰ ਸੈਸ਼ਨ ਫਾਈਲ ਵਿੱਚ ਸ਼ਾਮਲ ਹੈ: ਸੰਖੇਪ, ਸਿੱਖਣ ਦੇ ਉਦੇਸ਼, 30‑ਮਿੰਟ ਦਾ ਡੈਮੋ ਫਲੋ, ਸ਼ੁਰੂਆਤੀ ਪ੍ਰੋਜੈਕਟ, ਵੈਧਤਾ ਚੈੱਕਲਿਸਟ, ਸਮੱਸਿਆ ਹੱਲ, ਅਤੇ Foundry Local Python SDK ਦੇ ਅਧਿਕਾਰਕ ਸੰਦਰਭ।

### ਨਮੂਨਾ ਸਕ੍ਰਿਪਟ

ਵਰਕਸ਼ਾਪ ਡਿਪੈਂਡੈਂਸੀਜ਼ ਇੰਸਟਾਲ ਕਰੋ (Windows):

```powershell
cd Workshop
py -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt
```

macOS / Linux:

```bash
cd Workshop
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

ਜੇਕਰ Foundry Local ਸੇਵਾ ਨੂੰ macOS ਤੋਂ ਵੱਖਰੇ (Windows) ਮਸ਼ੀਨ ਜਾਂ VM 'ਤੇ ਚਲਾਇਆ ਜਾ ਰਿਹਾ ਹੈ, ਤਾਂ ਐਂਡਪੌਇੰਟ ਐਕਸਪੋਰਟ ਕਰੋ:

```bash
export FOUNDRY_LOCAL_ENDPOINT=http://<windows-host>:5273/v1
```

| ਸੈਸ਼ਨ | ਸਕ੍ਰਿਪਟ(ਸ) | ਵੇਰਵਾ |
|-------|------------|--------|
| 1 | `samples/session01/chat_bootstrap.py` | ਬੂਟਸਟਰੈਪ ਸੇਵਾ ਅਤੇ ਸਟ੍ਰੀਮਿੰਗ ਚੈਟ |
| 2 | `samples/session02/rag_pipeline.py` | ਘੱਟੋ-ਘੱਟ RAG (ਇਨ-ਮੇਮੋਰੀ ਐਮਬੈਡਿੰਗ) |
|   | `samples/session02/rag_eval_ragas.py` | RAG ਮੁਲਾਂਕਣ ragas ਮੈਟ੍ਰਿਕਸ ਨਾਲ |
| 3 | `samples/session03/benchmark_oss_models.py` | ਮਲਟੀ-ਮਾਡਲ ਲੈਟੈਂਸੀ ਅਤੇ ਥਰੂਪੁੱਟ ਬੈਂਚਮਾਰਕਿੰਗ |
| 4 | `samples/session04/model_compare.py` | SLM ਵਿਰੁੱਧ LLM ਤੁਲਨਾ (ਲੈਟੈਂਸੀ ਅਤੇ ਨਮੂਨਾ ਆਉਟਪੁੱਟ) |
| 5 | `samples/session05/agents_orchestrator.py` | ਦੋ-ਏਜੰਟ ਰਿਸਰਚ → ਐਡੀਟੋਰਿਅਲ ਪਾਈਪਲਾਈਨ |
| 6 | `samples/session06/models_router.py` | ਇਰਾਦੇ-ਅਧਾਰਿਤ ਰਾਊਟਿੰਗ ਡੈਮੋ |
|   | `samples/session06/models_pipeline.py` | ਮਲਟੀ-ਸਟੈਪ ਯੋਜਨਾ/ਅਮਲ/ਸੁਧਾਰ ਚੇਨ |

### ਵਾਤਾਵਰਣ ਵੈਰੀਏਬਲ (ਸਾਰੇ ਨਮੂਨਿਆਂ ਵਿੱਚ ਸਾਂਝੇ)

| ਵੈਰੀਏਬਲ | ਉਦੇਸ਼ | ਉਦਾਹਰਨ |
|----------|-------|---------|
| `FOUNDRY_LOCAL_ALIAS` | ਬੁਨਿਆਦੀ ਨਮੂਨਿਆਂ ਲਈ ਡਿਫਾਲਟ ਸਿੰਗਲ ਮਾਡਲ ਅਲਿਆਸ | `phi-4-mini` |
| `SLM_ALIAS` / `LLM_ALIAS` | SLM ਵਿਰੁੱਧ ਵੱਡੇ ਮਾਡਲ ਦੀ ਸਪਸ਼ਟ ਤੁਲਨਾ | `phi-4-mini` / `gpt-oss-20b` |
| `BENCH_MODELS` | ਬੈਂਚਮਾਰਕ ਕਰਨ ਲਈ ਅਲਿਆਸ ਦੀ ਕਾਮਾ ਸੂਚੀ | `qwen2.5-0.5b,gemma-2-2b,mistral-7b` |
| `BENCH_ROUNDS` | ਪ੍ਰਤੀ ਮਾਡਲ ਬੈਂਚਮਾਰਕ ਦੁਹਰਾਈਆਂ | `3` |
| `BENCH_PROMPT` | ਬੈਂਚਮਾਰਕਿੰਗ ਵਿੱਚ ਵਰਤਿਆ ਗਿਆ ਪ੍ਰੋਮਪਟ | `Explain retrieval augmented generation briefly.` |
| `EMBED_MODEL` | ਸੈਂਟੈਂਸ-ਟ੍ਰਾਂਸਫਾਰਮਰ ਐਮਬੈਡਿੰਗ ਮਾਡਲ | `sentence-transformers/all-MiniLM-L6-v2` |
| `RAG_QUESTION` | RAG ਪਾਈਪਲਾਈਨ ਲਈ ਟੈਸਟ ਕਵੈਰੀ ਨੂੰ ਓਵਰਰਾਈਡ ਕਰੋ | `Why use RAG with local inference?` |
| `AGENT_QUESTION` | ਏਜੰਟ ਪਾਈਪਲਾਈਨ ਕਵੈਰੀ ਨੂੰ ਓਵਰਰਾਈਡ ਕਰੋ | `Explain why edge AI matters for compliance.` |
| `AGENT_MODEL_PRIMARY` | ਰਿਸਰਚ ਏਜੰਟ ਲਈ ਮਾਡਲ ਅਲਿਆਸ | `phi-4-mini` |
| `AGENT_MODEL_EDITOR` | ਐਡੀਟਰ ਏਜੰਟ ਲਈ ਮਾਡਲ ਅਲਿਆਸ (ਵੱਖਰਾ ਹੋ ਸਕਦਾ ਹੈ) | `gpt-oss-20b` |
| `SHOW_USAGE` | ਜਦੋਂ `1`, ਪ੍ਰਤੀ ਪੂਰਨਤਾ ਟੋਕਨ ਵਰਤੋਂ ਪ੍ਰਿੰਟ ਕਰਦਾ ਹੈ | `1` |
| `RETRY_ON_FAIL` | ਜਦੋਂ `1`, ਅਸਥਾਈ ਚੈਟ ਗਲਤੀਆਂ 'ਤੇ ਇੱਕ ਵਾਰ ਮੁੜ ਕੋਸ਼ਿਸ਼ ਕਰੋ | `1` |
| `RETRY_BACKOFF` | ਮੁੜ ਕੋਸ਼ਿਸ਼ ਕਰਨ ਤੋਂ ਪਹਿਲਾਂ ਰੁਕਣ ਲਈ ਸਕਿੰਟ | `1.0` |

ਜੇਕਰ ਕੋਈ ਵੈਰੀਏਬਲ ਸੈਟ ਨਹੀਂ ਹੈ, ਤਾਂ ਸਕ੍ਰਿਪਟ ਸਮਝਦਾਰ ਡਿਫਾਲਟ 'ਤੇ ਵਾਪਸ ਆ ਜਾਂਦੇ ਹਨ। ਸਿੰਗਲ-ਮਾਡਲ ਡੈਮੋਜ਼ ਲਈ ਤੁਹਾਨੂੰ ਆਮ ਤੌਰ 'ਤੇ ਸਿਰਫ `FOUNDRY_LOCAL_ALIAS` ਦੀ ਲੋੜ ਹੁੰਦੀ ਹੈ।

### ਯੂਟਿਲਿਟੀ ਮੋਡਿਊਲ

ਸਾਰੇ ਨਮੂਨੇ ਹੁਣ ਇੱਕ ਸਹਾਇਕ `samples/workshop_utils.py` ਸਾਂਝੇ ਕਰਦੇ ਹਨ ਜੋ ਪ੍ਰਦਾਨ ਕਰਦਾ ਹੈ:

* Cached `FoundryLocalManager` + OpenAI ਕਲਾਇੰਟ ਬਣਾਉਣ
* `chat_once()` ਸਹਾਇਕ, ਵਿਕਲਪਿਕ ਮੁੜ ਕੋਸ਼ਿਸ਼ + ਵਰਤੋਂ ਪ੍ਰਿੰਟਿੰਗ ਨਾਲ
* ਸਧਾਰਨ ਟੋਕਨ ਵਰਤੋਂ ਰਿਪੋਰਟਿੰਗ (`SHOW_USAGE=1` ਰਾਹੀਂ ਐਨਬਲ ਕਰੋ)

ਇਹ ਨਕਲ ਨੂੰ ਘਟਾਉਂਦਾ ਹੈ ਅਤੇ ਕੁਸ਼ਲ ਸਥਾਨਕ ਮਾਡਲ ਆਰਕੇਸਟ੍ਰੇਸ਼ਨ ਲਈ ਵਧੀਆ ਅਭਿਆਸਾਂ ਨੂੰ ਉਜਾਗਰ ਕਰਦਾ ਹੈ।

## ਵਿਕਲਪਿਕ ਸੁਧਾਰ (ਕ੍ਰਾਸ-ਸੈਸ਼ਨ)

| ਥੀਮ | ਸੁਧਾਰ | ਸੈਸ਼ਨ | Env / Toggle |
|------|-------|-------|-------------|
| ਨਿਰਧਾਰਤਾ | ਫਿਕਸਡ ਟੈਂਪਰੇਚਰ + ਸਥਿਰ ਪ੍ਰੋਮਪਟ ਸੈੱਟ | 1–6 | `temperature=0`, `top_p=1` ਸੈਟ ਕਰੋ |
| ਟੋਕਨ ਵਰਤੋਂ ਦ੍ਰਿਸ਼ਮਾਨਤਾ | ਲਾਗਤ/ਕੁਸ਼ਲਤਾ ਸਿਖਲਾਈ | 1–6 | `SHOW_USAGE=1` |
| ਸਟ੍ਰੀਮਿੰਗ ਪਹਿਲਾ ਟੋਕਨ | ਲੈਟੈਂਸੀ ਮੈਟ੍ਰਿਕ | 1,3,4,6 | `BENCH_STREAM=1` (ਬੈਂਚਮਾਰਕ) |
| ਮੁੜ ਕੋਸ਼ਿਸ਼ ਲਚੀਲਾਪਨ | ਅਸਥਾਈ ਠੰਡੇ ਸ਼ੁਰੂਆਤ ਨੂੰ ਸੰਭਾਲਦਾ ਹੈ | ਸਾਰੇ | `RETRY_ON_FAIL=1` + `RETRY_BACKOFF` |
| ਮਲਟੀ-ਮਾਡਲ ਏਜੰਟ | ਹੇਟਰੋਜੀਨਸ ਰੋਲ ਸਪੈਸ਼ਲਾਈਜ਼ੇਸ਼ਨ | 5 | `AGENT_MODEL_PRIMARY`, `AGENT_MODEL_EDITOR` |
| ਅਡਾਪਟਿਵ ਰਾਊਟਿੰਗ | ਇਰਾਦਾ + ਲਾਗਤ ਹਿਊਰਿਸਟਿਕਸ | 6 | ਰਾਊਟਰ ਨੂੰ ਐਸਕਲੇਸ਼ਨ ਲਾਜਿਕ ਨਾਲ ਵਧਾਓ |
| ਵੈਕਟਰ ਮੈਮਰੀ | ਲੰਬੇ ਸਮੇਂ ਦੀ ਸੈਮੈਂਟਿਕ ਰੀਕਾਲ | 2,5,6 | FAISS/Chroma ਐਮਬੈਡਿੰਗ ਇੰਡੈਕਸ ਨੂੰ ਇੰਟੀਗਰੇਟ ਕਰੋ |
| ਟ੍ਰੇਸ ਐਕਸਪੋਰਟ | ਆਡਿਟਿੰਗ ਅਤੇ ਮੁਲਾਂਕਣ | 2,5,6 | ਪ੍ਰਤੀ ਕਦਮ JSON ਲਾਈਨਾਂ ਸ਼ਾਮਲ ਕਰੋ |
| ਗੁਣਵੱਤਾ ਰੂਬ੍ਰਿਕਸ | ਗੁਣਾਤਮਕ ਟ੍ਰੈਕਿੰਗ | 3–6 | ਸੈਕੰਡਰੀ ਸਕੋਰਿੰਗ ਪ੍ਰੋਮਪਟ |
| ਸਮੋਕ ਟੈਸਟ | ਵਰਕਸ਼ਾਪ ਤੋਂ ਪਹਿਲਾਂ ਤੇਜ਼ ਚੈੱਕ | ਸਾਰੇ | `python Workshop/tests/smoke.py` |

### ਨਿਰਧਾਰਤ ਤੇਜ਼ ਸ਼ੁਰੂਆਤ

```powershell
set FOUNDRY_LOCAL_ALIAS=phi-4-mini
set SHOW_USAGE=1
python Workshop\tests\smoke.py
```

ਇਕਸਾਰ ਟੋਕਨ ਗਿਣਤੀ ਦੀ ਉਮੀਦ ਕਰੋ ਜਦੋਂ ਇੱਕੋ ਜਿਹੇ ਇਨਪੁਟ ਦੁਹਰਾਏ ਜਾਂਦੇ ਹਨ।

### RAG ਮੁਲਾਂਕਣ (ਸੈਸ਼ਨ 2)

`rag_eval_ragas.py` ਵਰਤੋ ਜਵਾਬ ਦੀ ਸਬੰਧਤਾ, ਸੱਚਾਈ, ਅਤੇ ਸੰਦਰਭ ਸਹੀਤਾ ਦੀ ਗਣਨਾ ਕਰਨ ਲਈ ਇੱਕ ਛੋਟੇ ਸਿੰਥੇਟਿਕ ਡੇਟਾਸੈਟ 'ਤੇ:

```powershell
python samples/session02/rag_eval_ragas.py
```

ਇਸਨੂੰ ਵਧਾਓ ਜੇਕਰ ਵੱਡੇ JSONL ਪ੍ਰਸ਼ਨਾਂ, ਸੰਦਰਭਾਂ, ਅਤੇ ਗਰਾਊਂਡ ਸੱਚਾਈਆਂ ਦੀ ਸਪਲਾਈ ਕੀਤੀ ਜਾਵੇ, ਫਿਰ ਇਸਨੂੰ Hugging Face `Dataset` ਵਿੱਚ ਰੂਪਾਂਤਰਿਤ ਕਰੋ।

## CLI ਕਮਾਂਡ ਸਹੀਤਾ ਐਪੈਂਡਿਕਸ

ਵਰਕਸ਼ਾਪ ਜ਼ਰੂਰਤਮੰਦ ਤੌਰ 'ਤੇ ਸਿਰਫ ਮੌਜੂਦਾ ਦਸਤਾਵੇਜ਼/ਸਥਿਰ Foundry Local CLI ਕਮਾਂਡਾਂ ਦੀ ਵਰਤੋਂ ਕਰਦਾ ਹੈ।

### ਸਥਿਰ ਕਮਾਂਡਾਂ ਦਾ ਸੰਦਰਭ

| ਸ਼੍ਰੇਣੀ | ਕਮਾਂਡ | ਉਦੇਸ਼ |
|--------|-------|-------|
| ਕੋਰ | `foundry --version` | ਇੰਸਟਾਲ ਕੀਤੀ ਵਰਜਨ ਦਿਖਾਓ |
| ਕੋਰ | `foundry init` | ਕਨਫਿਗਰੇਸ਼ਨ ਸ਼ੁਰੂ ਕਰੋ |
| ਸੇਵਾ | `foundry service start` | ਸਥਾਨਕ ਸੇਵਾ ਸ਼ੁਰੂ ਕਰੋ (ਜੇਕਰ ਆਟੋ ਨਹੀਂ) |
| ਸੇਵਾ | `foundry status` | ਸੇਵਾ ਦੀ ਸਥਿਤੀ ਦਿਖਾਓ |
| ਮਾਡਲ | `foundry model list` | ਕੈਟਾਲੌਗ / ਉਪਲਬਧ ਮਾਡਲਾਂ ਦੀ ਸੂਚੀ |
| ਮਾਡਲ | `foundry model download <alias>` | ਮਾਡਲ ਵਜ਼ਨ ਕੈਸ਼ ਵਿੱਚ ਡਾਊਨਲੋਡ ਕਰੋ |
| ਮਾਡਲ | `foundry model run <alias>` | ਮਾਡਲ ਨੂੰ ਸਥਾਨਕ ਤੌਰ 'ਤੇ ਚਲਾਓ; `--prompt` ਨਾਲ ਇੱਕ-ਸ਼ਾਟ ਲਈ ਜੋੜੋ |
| ਮਾਡਲ | `foundry model unload <alias>` / `foundry model stop <alias>` | ਮਾਡਲ ਨੂੰ ਮੈਮੋਰੀ ਤੋਂ ਅਨਲੋਡ ਕਰੋ (ਜੇਕਰ ਸਹਾਇਕ ਹੈ) |
| ਕੈਸ਼ | `foundry cache list` | ਕੈਸ਼ ਕੀਤੇ (ਡਾਊਨਲੋਡ ਕੀਤੇ) ਮਾਡਲਾਂ ਦੀ ਸੂਚੀ |
| ਸਿਸਟਮ | `foundry system info` | ਹਾਰਡਵੇਅਰ ਅਤੇ ਐਕਸਲੇਰੇਸ਼ਨ ਸਮਰੱਥਾ ਸਨੈਪਸ਼ਾਟ |
| ਸਿਸਟਮ | `foundry system gpu-info` | GPU ਡਾਇਗਨੋਸਟਿਕ ਜਾਣਕਾਰੀ |
| ਕਨਫਿਗ | `foundry config list` | ਮੌਜੂਦਾ ਕਨਫਿਗ ਮੁੱਲ ਦਿਖਾਓ |
| ਕਨਫਿਗ | `foundry config set <key> <value>` | ਕਨਫਿਗਰੇਸ਼ਨ ਅਪਡੇਟ ਕਰੋ |

### ਇੱਕ-ਸ਼ਾਟ ਪ੍ਰੋਮਪਟ ਪੈਟਰਨ

ਪੁਰਾਣੇ `model chat` ਸਬਕਮਾਂਡ ਦੀ ਬਜਾਏ, ਵਰਤੋ:

```powershell
foundry model run <alias> --prompt "Your question here"
```

ਇਹ ਇੱਕ ਪ੍ਰੋਮਪਟ/ਜਵਾਬ ਚੱਕਰ ਨੂੰ ਚਲਾਉਂਦਾ ਹੈ ਅਤੇ ਫਿਰ ਬੰਦ ਕਰਦਾ ਹੈ।

### ਹਟਾਏ ਗਏ / ਬਚਾਏ ਗਏ ਪੈਟਰਨ

| ਪੁਰਾਣੇ / ਅਣਦਸਤਾਵੇਜ਼ | ਬਦਲ / ਮਾਰਗਦਰਸ਼ਨ |
|---------------------|------------------|
| `foundry model chat <model> "..."` | `foundry model run <model> --prompt "..."` |
| `foundry model list --running` | ਸਧਾਰਨ `foundry model list` + ਹਾਲੀਆ ਗਤੀਵਿਧੀ / ਲੌਗ |
| `foundry model list --cached` | `foundry cache list` |
| `foundry model stats <model>` | ਬੈਂਚਮਾਰਕ ਪਾਈਥਨ ਸਕ੍ਰਿਪਟ + OS ਟੂਲ (ਟਾਸਕ ਮੈਨੇਜਰ / `nvidia-smi`) |
| `foundry model benchmark ...` | `samples/session03/benchmark_oss_models.py` |

### ਬੈਂਚਮਾਰਕਿੰਗ ਅਤੇ ਟੈਲੀਮੈਟਰੀ

- ਲੈਟੈਂਸੀ, p95, ਟੋਕਨ/ਸੈਕੰਡ: `samples/session03/benchmark_oss_models.py`
- ਪਹਿਲਾ-ਟੋਕਨ ਲੈਟੈਂਸੀ (ਸਟ੍ਰੀਮਿੰਗ): `BENCH_STREAM=1` ਸੈਟ ਕਰੋ
- ਸਰੋਤ ਵਰਤੋਂ: OS ਮਾਨੀਟਰ (ਟਾਸਕ ਮੈਨੇਜਰ, ਐਕਟਿਵਿਟੀ ਮਾਨੀਟਰ, `nvidia-smi`) + `foundry system info`.

ਜਿਵੇਂ ਨਵੇਂ CLI ਟੈਲੀਮੈਟਰੀ ਕਮਾਂਡ ਉੱਪਰ ਸਥਿਰ ਹੁੰਦੇ ਹਨ, ਉਹਨਾਂ ਨੂੰ ਸੈਸ਼ਨ ਮਾਰਕਡਾਊਨ ਵਿੱਚ ਘੱਟੋ-ਘੱਟ ਸੋਧਾਂ ਨਾਲ ਸ਼ਾਮਲ ਕੀਤਾ ਜਾ ਸਕਦਾ ਹੈ।

### ਆਟੋਮੈਟਿਕ ਲਿੰਟ ਗਾਰਡ

ਇੱਕ ਆਟੋਮੈਟਿਕ ਲਿੰਟਰ ਪੁਰਾਣੇ CLI ਪੈਟਰਨਾਂ ਨੂੰ ਮਾਰਕਡਾਊਨ ਫਾਈਲਾਂ ਦੇ fenced ਕੋਡ ਬਲਾਕਾਂ ਵਿੱਚ ਮੁੜ ਸ਼ਾਮਲ ਕਰਨ ਤੋਂ ਰੋਕਦਾ ਹੈ:

ਸਕ੍ਰਿਪਟ: `Workshop/scripts/lint_markdown_cli.py`

ਪੁਰਾਣੇ ਪੈਟਰਨਾਂ ਨੂੰ ਕੋਡ ਫੈਂਸਾਂ ਦੇ ਅੰਦਰ ਰੋਕਿਆ ਜਾਂਦਾ ਹੈ।

ਸੁਝਾਏ ਬਦਲ:
| ਪੁਰਾਣੇ | ਬਦਲ |
|-------|-----|
| `foundry model chat <a> "..."` | `foundry model run <a> --prompt "..."` |
| `model list --running` | `model list` |
| `model list --cached` | `cache list` |
| `model stats` | ਬੈਂਚਮਾਰਕ ਸਕ੍ਰਿਪਟ + ਸਿਸਟਮ ਟੂਲ |
| `model benchmark` | `samples/session03/benchmark_oss_models.py` |
| `model list --available` | `model list` |

ਸਥਾਨਕ ਤੌਰ 'ਤੇ ਚਲਾਓ:
```powershell
python Workshop\scripts\lint_markdown_cli.py --verbose
```

GitHub ਐਕਸ਼ਨ: `.github/workflows/markdown-cli-lint.yml` ਹਰ ਪੁਸ਼ ਅਤੇ PR 'ਤੇ ਚਲਦਾ ਹੈ।

ਵਿਕਲਪਿਕ ਪ੍ਰੀ-ਕਮਿਟ ਹੁੱਕ:
```bash
echo "python Workshop/scripts/lint_markdown_cli.py" > .git/hooks/pre-commit
chmod +x .git/hooks/pre-commit
```

## ਤੇਜ਼ CLI → SDK ਮਾਈਗ੍ਰੇਸ਼ਨ ਟੇਬਲ

| ਕੰਮ | CLI ਇੱਕ-ਲਾਈਨਰ | SDK (Python) ਸਮਕਾਲੀ | ਨੋਟ |
|-----|---------------|---------------------|-----|
| ਮਾਡਲ ਨੂੰ ਇੱਕ ਵਾਰ ਚਲਾਓ (ਪ੍ਰੋਮਪਟ) | `foundry model run phi-4-mini --prompt "Hello"` | `manager=FoundryLocalManager("phi-4-mini"); client=OpenAI(base_url=manager.endpoint, api_key=manager.api_key or "not-needed"); client.chat.completions.create(model=manager.get_model_info("phi-4-mini").id, messages=[{"role":"user","content":"Hello"}])` | SDK ਸੇਵਾ ਅਤੇ ਕੈਸ਼ਿੰਗ ਨੂੰ ਆਟੋਮੈਟਿਕ ਤੌਰ 'ਤੇ ਸ਼ੁਰੂ ਕਰਦਾ ਹੈ |
| ਮਾਡਲ ਡਾਊਨਲੋਡ (ਕੈਸ਼) | `foundry model download qwen2.5-0.5b` | `FoundryLocalManager("qwen2.5-0.5b")  # triggers download/load` | ਮੈਨੇਜਰ ਵਧੀਆ ਵਰਜਨ ਚੁਣਦਾ ਹੈ ਜੇਕਰ ਅਲਿਆਸ ਕਈ ਬਿਲਡਾਂ ਨਾਲ ਮੈਪ ਕਰਦਾ ਹੈ |
| ਕੈਟਾਲੌਗ ਦੀ ਸੂਚੀ | `foundry model list` | `# use manager for each alias or maintain known list` | CLI ਇਕੱਠਾ ਕਰਦਾ ਹੈ; SDK ਮੌਜੂਦਾ ਪ੍ਰਤੀ-ਅਲਿਆਸ |
| ਕੈਸ਼ ਕੀਤੇ ਮਾਡਲਾਂ ਦੀ ਸੂਚੀ | `foundry cache list` | `manager.list_cached_models()` | ਮੈਨੇਜਰ ਸ਼ੁਰੂ ਕਰਨ ਤੋਂ ਬਾਅਦ (ਕੋਈ ਵੀ ਅਲਿਆਸ) |
| GPU ਐਕਸਲੇਰੇਸ਼ਨ ਐਨਬਲ ਕਰੋ | `foundry config set compute.onnx.enable_gpu true` | `# CLI action; SDK assumes config already applied` | ਕਨਫਿਗਰੇਸ਼ਨ ਬਾਹਰੀ ਸਾਈਡ ਇਫੈਕਟ ਹੈ |
| ਐਂਡਪੌਇੰਟ URL ਪ੍ਰਾਪਤ ਕਰੋ | (ਅਸਪਸ਼ਟ) | `manager.endpoint` | OpenAI-ਅਨੁਕੂਲ ਕਲਾਇੰਟ ਬਣਾਉਣ ਲਈ ਵਰਤਿਆ |
| ਮਾਡਲ ਨੂੰ ਗਰਮ ਕਰੋ | `foundry model run <alias>` ਫਿਰ ਪਹਿਲਾ ਪ੍ਰੋਮਪਟ | `chat_once(alias, messages=[...])` (ਯੂਟਿਲਿਟੀ) | ਯੂਟਿਲਿਟੀਜ਼ ਸ਼ੁਰੂਆਤੀ ਠੰਡੇ ਲੈਟੈਂਸੀ ਵਾਰਮਅਪ ਨੂੰ ਸੰਭਾਲਦੇ ਹਨ |
| ਲੈਟੈਂਸੀ ਮਾਪੋ | `python benchmark_oss_models.py` | `import benchmark_oss_models` (ਜਾਂ ਨਵਾਂ ਐਕਸਪੋਰਟਰ ਸਕ੍ਰਿਪਟ) | ਸਥਿਰ ਮੈਟ੍ਰਿਕਸ ਲਈ ਸਕ੍ਰਿਪਟ ਨੂੰ ਤਰਜੀਹ ਦਿਓ |
| ਮਾਡਲ ਨੂੰ ਰੋਕੋ / ਅਨਲੋਡ ਕਰੋ | `foundry model unload <alias>` |

---

**ਅਸਵੀਕਰਤੀ**:  
ਇਹ ਦਸਤਾਵੇਜ਼ AI ਅਨੁਵਾਦ ਸੇਵਾ [Co-op Translator](https://github.com/Azure/co-op-translator) ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਅਨੁਵਾਦ ਕੀਤਾ ਗਿਆ ਹੈ। ਜਦੋਂ ਕਿ ਅਸੀਂ ਸਹੀ ਹੋਣ ਦੀ ਕੋਸ਼ਿਸ਼ ਕਰਦੇ ਹਾਂ, ਕਿਰਪਾ ਕਰਕੇ ਧਿਆਨ ਦਿਓ ਕਿ ਸਵੈਚਾਲਿਤ ਅਨੁਵਾਦਾਂ ਵਿੱਚ ਗਲਤੀਆਂ ਜਾਂ ਅਸੁਚਤਤਾਵਾਂ ਹੋ ਸਕਦੀਆਂ ਹਨ। ਇਸ ਦੀ ਮੂਲ ਭਾਸ਼ਾ ਵਿੱਚ ਮੂਲ ਦਸਤਾਵੇਜ਼ ਨੂੰ ਅਧਿਕਾਰਤ ਸਰੋਤ ਮੰਨਿਆ ਜਾਣਾ ਚਾਹੀਦਾ ਹੈ। ਮਹੱਤਵਪੂਰਨ ਜਾਣਕਾਰੀ ਲਈ, ਪੇਸ਼ੇਵਰ ਮਨੁੱਖੀ ਅਨੁਵਾਦ ਦੀ ਸਿਫਾਰਸ਼ ਕੀਤੀ ਜਾਂਦੀ ਹੈ। ਇਸ ਅਨੁਵਾਦ ਦੀ ਵਰਤੋਂ ਤੋਂ ਪੈਦਾ ਹੋਣ ਵਾਲੇ ਕਿਸੇ ਵੀ ਗਲਤ ਫਹਿਮੀ ਜਾਂ ਗਲਤ ਵਿਆਖਿਆ ਲਈ ਅਸੀਂ ਜ਼ਿੰਮੇਵਾਰ ਨਹੀਂ ਹਾਂ।