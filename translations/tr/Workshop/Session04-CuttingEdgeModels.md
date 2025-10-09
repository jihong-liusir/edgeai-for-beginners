<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "d1b3c0fecfd713c2df903a0633249dc9",
  "translation_date": "2025-10-09T10:39:09+00:00",
  "source_file": "Workshop/Session04-CuttingEdgeModels.md",
  "language_code": "tr"
}
-->
# Oturum 4: En Yeni Modelleri Keşfedin – LLM'ler, SLM'ler ve Cihaz Üzerinde Çıkarım

## Özet

Yerel ve bulut tabanlı çıkarım senaryoları için Büyük Dil Modelleri (LLM'ler) ve Küçük Dil Modelleri (SLM'ler) karşılaştırmasını yapın. ONNX Runtime hızlandırması, WebGPU çalıştırması ve hibrit RAG deneyimlerinden yararlanarak dağıtım modellerini öğrenin. Yerel bir modelle bir Chainlit RAG demosu ve isteğe bağlı bir OpenWebUI keşfi içerir. WebGPU çıkarım başlangıç projesini uyarlayacak ve Phi ile GPT-OSS-20B'nin yetenek ve maliyet/performans dengelerini değerlendireceksiniz.

## Öğrenme Hedefleri

- **Karşılaştırma**: SLM ve LLM'leri gecikme, bellek ve kalite eksenlerinde karşılaştırın
- **Dağıtım**: Modelleri ONNXRuntime ve (desteklendiği yerlerde) WebGPU ile dağıtın
- **Çalıştırma**: Tarayıcı tabanlı çıkarım (gizliliği koruyan etkileşimli demo)
- **Entegrasyon**: Yerel bir SLM arka ucu ile bir Chainlit RAG hattını entegre edin
- **Değerlendirme**: Hafif kalite ve maliyet ölçütlerini kullanarak değerlendirme yapın

## Ön Koşullar

- Oturumlar 1–3 tamamlanmış olmalı
- `chainlit` kurulmuş olmalı (Module08 için `requirements.txt` içinde zaten mevcut)
- WebGPU destekli bir tarayıcı (Windows 11'de Edge / Chrome'un en son sürümü)
- Foundry Local çalışıyor olmalı (`foundry status`)

### Platformlar Arası Notlar

Windows birincil hedef ortam olmaya devam etmektedir. Yerel macOS ikili dosyalarını bekleyen geliştiriciler için:
1. Foundry Local'ı bir Windows 11 VM'de (Parallels / UTM) VEYA uzak bir Windows iş istasyonunda çalıştırın.
2. Hizmeti açın (varsayılan port 5273) ve macOS'ta ayarlayın:
```bash
export FOUNDRY_LOCAL_ENDPOINT=http://<windows-host>:5273/v1
```
3. Önceki oturumlarda olduğu gibi aynı Python sanal ortam adımlarını kullanın.

Chainlit kurulumu (her iki platformda):
```bash
pip install chainlit
```

## Demo Akışı (30 dakika)

### 1. Phi (SLM) ve GPT-OSS-20B (LLM) Karşılaştırması (6 dakika)

```powershell
foundry model run phi-4-mini
foundry model run gpt-oss-20b

# Quick capability probes (one-shot non-interactive)
foundry model run phi-4-mini   --prompt "Summarize retrieval augmented generation in 2 sentences."
foundry model run gpt-oss-20b --prompt "Summarize retrieval augmented generation in 2 sentences."

# Basic token / latency test (repeat a few times for intuition)
foundry model run phi-4-mini   --prompt "List 5 creative IoT edge AI ideas."
foundry model run gpt-oss-20b --prompt "List 5 creative IoT edge AI ideas."
```

İzlenecekler: yanıt derinliği, gerçeklik doğruluğu, stilistik zenginlik, gecikme.

### 2. ONNX Runtime Hızlandırması (5 dakika)

```powershell
foundry config set compute.onnx.enable_gpu true
# Re-run Python benchmark script for quantitative latency / throughput after enabling GPU
#   set BENCH_MODELS=phi-4-mini
#   python Workshop\samples\session03\benchmark_oss_models.py
```

GPU etkinleştirildikten sonra verimlilik değişikliklerini gözlemleyin (yalnızca CPU ile karşılaştırın).

### 3. Tarayıcıda WebGPU Çıkarımı (6 dakika)

Başlangıç `04-webgpu-inference` dosyasını uyarlayın (oluşturun: `samples/04-cutting-edge/webgpu_demo.html`):

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Foundry Local WebGPU Demo</title>
  <style>body{font-family:system-ui;margin:2rem;max-width:820px;} textarea{width:100%;height:120px;} pre{background:#111;color:#eee;padding:1rem;} .resp{white-space:pre-wrap;margin-top:1rem;border:1px solid #444;padding:1rem;border-radius:6px;}</style>
</head>
<body>
  <h1>WebGPU Inference (Experimental)</h1>
  <p>Demonstration placeholder for a WebGPU-backed transformer (concept). Replace with actual JS runtime once exposed by Foundry Local or associated runtime libs.</p>
  <textarea id="prompt" placeholder="Enter your prompt..."></textarea>
  <button id="run">Generate</button>
  <div id="out" class="resp"></div>
  <script>
    document.getElementById('run').onclick = async () => {
      const p = document.getElementById('prompt').value.trim();
      if(!p) return;
      document.getElementById('out').textContent = 'Running (simulated)...';
      // Placeholder: in a real implementation you'd call into a WASM/WebGPU pipeline or local gateway endpoint.
      const resp = await fetch('http://localhost:5273/v1/chat/completions', {
        method: 'POST', headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
          model: 'phi-4-mini',
          messages: [ { role: 'user', content: p } ],
          max_tokens: 200, temperature: 0.5
        })
      }).then(r=>r.json()).catch(e=>({error:e.toString()}));
      if(resp.error){
        document.getElementById('out').textContent = 'Error: '+resp.error;
      } else {
        document.getElementById('out').textContent = resp.choices?.[0]?.message?.content || JSON.stringify(resp,null,2);
      }
    };
  </script>
</body>
</html>
```

Dosyayı bir tarayıcıda açın; düşük gecikmeli yerel dönüşü gözlemleyin.

### 4. Chainlit RAG Sohbet Uygulaması (7 dakika)

Minimal `samples/04-cutting-edge/chainlit_app.py`:

```python
#!/usr/bin/env python3
"""Chainlit RAG demo using Foundry Local SLM as backend."""
import chainlit as cl
from openai import OpenAI

DOCS = [
  "Foundry Local enables local model execution with OpenAI-compatible APIs.",
  "RAG combines retrieval and generation for grounded answers.",
  "SLMs provide efficiency advantages on constrained hardware."  
]

client = OpenAI(base_url="http://localhost:5273/v1", api_key="not-needed")

def build_context(query: str):
    # Naive lexical scoring
    scored = sorted(DOCS, key=lambda d: sum(w in d.lower() for w in query.lower().split()), reverse=True)
    return "\n".join(scored[:2])

@cl.on_message
async def main(message: cl.Message):
    ctx = build_context(message.content)
    resp = client.chat.completions.create(
        model="phi-4-mini",
        messages=[
            {"role": "system", "content": "Answer using ONLY the provided context. If insufficient, say so."},
            {"role": "user", "content": f"Context:\n{ctx}\n\nQuestion: {message.content}"}
        ],
        max_tokens=300,
        temperature=0.3
    )
    await cl.Message(content=resp.choices[0].message.content).send()
```

Çalıştırın:

```powershell
chainlit run samples/04-cutting-edge/chainlit_app.py -w
```

### 5. Başlangıç Projesi: `04-webgpu-inference` Uyarlayın (6 dakika)

Teslimatlar:
- Yer tutucu veri alma mantığını akış token'larıyla değiştirin (`stream=True` uç nokta varyantını etkinleştirdikten sonra kullanın)
- Gecikme grafiği ekleyin (istemci tarafında) phi ve gpt-oss-20b geçişleri için
- RAG bağlamını satır içi gömün (referans belgeler için metin alanı)

## Değerlendirme Ölçütleri

| Kategori | Phi-4-mini | GPT-OSS-20B | Gözlem |
|----------|------------|-------------|--------|
| Gecikme (soğuk) | Hızlı | Daha yavaş | SLM hızlı ısınır |
| Bellek | Düşük | Yüksek | Cihaz uygunluğu |
| Bağlam uyumu | İyi | Güçlü | Daha büyük model daha ayrıntılı olabilir |
| Maliyet (yerel) | Minimal | Daha yüksek (kaynak) | Enerji/zaman dengesi |
| En iyi kullanım durumu | Uç uygulamalar | Derin akıl yürütme | Hibrit bir hat mümkün |

## Ortamı Doğrulama

```powershell
# List catalog (no --running flag; loaded models are those you have previously run)
foundry model list

# For runtime metrics use the Python benchmark script (Session 3) and OS tools (Task Manager / nvidia-smi) instead of 'model stats'
# Example:
#   set BENCH_MODELS=phi-4-mini,gpt-oss-20b
#   python Workshop\samples\session03\benchmark_oss_models.py
```

## Sorun Giderme

| Belirti | Sebep | Çözüm |
|---------|-------|-------|
| Web sayfası alınamıyor | CORS veya hizmet kapalı | Uç noktayı doğrulamak için `curl` kullanın; gerekirse CORS proxy'sini etkinleştirin |
| Chainlit boş | Ortam aktif değil | Sanal ortamı etkinleştirin ve bağımlılıkları yeniden yükleyin |
| Yüksek gecikme | Model yeni yüklendi | Küçük bir istem dizisiyle ısıtın |

## Referanslar

- Foundry Local SDK: https://github.com/microsoft/Foundry-Local/tree/main/sdk/python
- Chainlit Belgeleri: https://docs.chainlit.io
- RAG Değerlendirme (Ragas): https://docs.ragas.io

---

**Oturum Süresi**: 30 dakika  
**Zorluk**: İleri Düzey

## Örnek Senaryo ve Atölye Eşlemesi

| Atölye Çıktıları | Senaryo | Amaç | Veri / İstem Kaynağı |
|------------------|---------|------|-----------------------|
| `samples/session04/model_compare.py` / `notebooks/session04_model_compare.ipynb` | Yönetici özeti oluşturucu için SLM ve LLM değerlendiren mimari ekip | Gecikme + token kullanımı farkını ölçmek | Tek `COMPARE_PROMPT` ortam değişkeni |
| `chainlit_app.py` (RAG demo) | Dahili bilgi asistanı prototipi | Kısa yanıtları minimal sözcüksel geri alımla temellendirmek | Dosyadaki satır içi `DOCS` listesi |
| `webgpu_demo.html` | Geleceğe yönelik cihaz üzerinde tarayıcı çıkarım önizlemesi | Düşük gecikmeli yerel dönüş + UX anlatımı göster | Yalnızca canlı kullanıcı istemi |

### Senaryo Anlatımı
Ürün organizasyonu bir yönetici özet oluşturucu istiyor. Hafif bir SLM (phi-4-mini) taslak özetler oluşturur; daha büyük bir LLM (gpt-oss-20b) yalnızca yüksek öncelikli raporları iyileştirebilir. Oturum betikleri, hibrit bir tasarımı gerekçelendirmek için ampirik gecikme ve token ölçümlerini yakalar, Chainlit demosu ise küçük model yanıtlarını gerçeklere dayalı tutmanın nasıl mümkün olduğunu gösterir. WebGPU konsept sayfası, tarayıcı hızlandırması olgunlaştığında tamamen istemci tarafı işleme için bir vizyon yolu sunar.

### Minimal RAG Bağlamı (Chainlit)
```python
DOCS = [
  "Foundry Local enables local model execution with OpenAI-compatible APIs.",
  "RAG combines retrieval and generation for grounded answers.",
  "SLMs provide efficiency advantages on constrained hardware."
]
```

### Hibrit Taslak→İyileştirme Akışı (Sözde Kod)
```python
draft, _ = chat_once('phi-4-mini', messages=[{"role":"user","content":prompt}], max_tokens=280)
if len(draft) < 600:  # heuristic: escalate only for longer briefs or flagged topics
    final = draft
else:
    final, _ = chat_once('gpt-oss-20b', messages=[{"role":"user","content":f"Refine and polish:\n{draft}"}], max_tokens=220)
```

Her iki gecikme bileşenini de izleyerek ortalama maliyetin karışımını raporlayın.

### İsteğe Bağlı Geliştirmeler

| Odak | Geliştirme | Neden | Uygulama İpucu |
|------|-----------|-------|----------------|
| Karşılaştırmalı Ölçümler | Token kullanımı + ilk token gecikmesini izleyin | Kapsamlı performans görünümü | Geliştirilmiş kıyaslama betiğini kullanın (Oturum 3) `BENCH_STREAM=1` ile |
| Hibrit Hat | SLM taslağı → LLM iyileştirme | Gecikme ve maliyeti azaltın | Phi-4-mini ile oluşturun, özeti gpt-oss-20b ile iyileştirin |
| Akışlı UI | Chainlit'te daha iyi UX | Kademeli geri bildirim | Yerel akış etkinleştirildiğinde `stream=True` kullanın; parçaları biriktirin |
| WebGPU Önbellekleme | Daha hızlı JS başlatma | Derleme yükünü azaltın | Derlenmiş gölgelendirici nesnelerini önbelleğe alın (gelecekteki çalışma zamanı özelliği) |
| Deterministik QA Seti | Adil model karşılaştırması | Değişkenliği ortadan kaldırın | Sabit istem listesi + değerlendirme çalışmaları için `temperature=0` |
| Çıktı Puanlama | Yapılandırılmış kalite lensi | Anlatıların ötesine geçin | Basit bir ölçüt: tutarlılık / gerçeklik / kısalık (1–5) |
| Enerji / Kaynak Notları | Sınıf tartışması | Ticaret dengelerini gösterin | İşletim sistemi monitörlerini kullanın (`foundry system info`, Görev Yöneticisi, `nvidia-smi`) + kıyaslama betiği çıktıları |
| Maliyet Simülasyonu | Bulut öncesi gerekçe | Ölçeklendirme planı | Tokenları toplam sahip olma maliyeti anlatısı için varsayımsal bulut fiyatlandırmasına eşleyin |
| Gecikme Ayrıştırması | Darboğazları belirleyin | Optimizasyonları hedefleyin | İstem hazırlığı, istek gönderimi, ilk token, tamamlama süresi ölçümleri yapın |
| RAG + LLM Yedekleme | Kalite güvenlik ağı | Zor soruları iyileştirin | SLM yanıt uzunluğu < eşik veya düşük güven → yükseltme |

#### Örnek Hibrit Taslak/İyileştirme Deseni

```python
draft, _ = chat_once('phi-4-mini', messages=[{"role":"user","content":task}], max_tokens=300, temperature=0.4)
refine, _ = chat_once('gpt-oss-20b', messages=[{"role":"user","content":f"Improve clarity but keep facts:\n{draft}"}], max_tokens=220, temperature=0.3)
```

#### Gecikme Dağılımı Taslağı

```python
import time
t0 = time.time(); # build messages
prep_ms = (time.time()-t0)*1000
t1 = time.time(); text,_ = chat_once(alias, messages=msgs, max_tokens=180)
full_ms = (time.time()-t1)*1000
print({"prep_ms": prep_ms, "full_gen_ms": full_ms})
```

Adil karşılaştırmalar için modeller arasında tutarlı ölçüm yapısı kullanın.

---

**Feragatname**:  
Bu belge, [Co-op Translator](https://github.com/Azure/co-op-translator) adlı bir yapay zeka çeviri hizmeti kullanılarak çevrilmiştir. Doğruluk için çaba göstersek de, otomatik çevirilerin hata veya yanlışlıklar içerebileceğini lütfen unutmayın. Belgenin orijinal dilindeki hali, yetkili kaynak olarak kabul edilmelidir. Kritik bilgiler için profesyonel insan çevirisi önerilir. Bu çevirinin kullanımından kaynaklanan yanlış anlamalar veya yanlış yorumlamalardan sorumlu değiliz.