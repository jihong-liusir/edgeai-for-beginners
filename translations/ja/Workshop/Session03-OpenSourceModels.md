<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "d6ad6c8b4a0e3ecef3afb86a6f578e1c",
  "translation_date": "2025-10-08T19:22:01+00:00",
  "source_file": "Workshop/Session03-OpenSourceModels.md",
  "language_code": "ja"
}
-->
# セッション3: Foundry Localでのオープンソースモデル

## 概要

Hugging Faceやその他のオープンソースモデルをFoundry Localに導入する方法を学びます。モデル選択戦略、コミュニティ貢献ワークフロー、性能比較の方法論、カスタムモデル登録によるFoundryの拡張方法について解説します。このセッションは毎週の「Model Mondays」の探求テーマに対応しており、オープンソースモデルをローカルで評価・運用し、Azureへのスケールアップを目指すためのスキルを提供します。

## 学習目標

セッション終了時には以下ができるようになります：

- **発見と評価**: 質とリソースのトレードオフを考慮し、候補モデル（mistral、gemma、qwen、deepseek）を特定する。
- **ロードと実行**: Foundry Local CLIを使用してコミュニティモデルをダウンロード、キャッシュ、起動する。
- **ベンチマーク**: 一貫したレイテンシー + トークンスループット + 品質の指標を適用する。
- **拡張**: SDK互換パターンに従ってカスタムモデルラッパーを登録または適応させる。
- **比較**: SLMと中規模LLMの選択決定のための構造化された比較を作成する。

## 前提条件

- セッション1と2を完了していること
- `foundry-local-sdk`がインストールされたPython環境
- 複数モデルキャッシュ用に少なくとも15GBの空きディスク容量
- オプション: GPU/WebGPUアクセラレーションが有効（`foundry config list`）

### クロスプラットフォーム環境のクイックスタート

Windows PowerShell:
```powershell
py -m venv .venv
 .\.venv\Scripts\Activate.ps1
pip install --upgrade pip
pip install foundry-local-sdk openai numpy
```

macOS / Linux:
```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install foundry-local-sdk openai numpy
```

macOSからWindowsホストサービスをベンチマークする場合は以下を設定：
```bash
export FOUNDRY_LOCAL_ENDPOINT=http://<windows-host>:5273/v1
```


## デモフロー (30分)

### 1. CLIでHugging Faceモデルをロード (8分)

```powershell
# List catalog entries (filter manually if needed)
foundry model list

# Download a set of comparison targets
foundry model download mistral-7b
foundry model download gemma-2-2b
foundry model download qwen2.5-0.5b

# Verify cache
foundry cache list
```


### 2. 実行と簡易プローブ (5分)

```powershell
foundry model run qwen2.5-0.5b
foundry model run qwen2.5-0.5b --prompt "List three benefits of local inference."

foundry model run mistral-7b
foundry model run mistral-7b --prompt "Explain retrieval augmented generation in one paragraph."
```


### 3. ベンチマークスクリプト (8分)

`samples/03-oss-models/benchmark_models.py`を作成：

```python
#!/usr/bin/env python3
"""Lightweight benchmarking for open-source models in Foundry Local.
Metrics: first token latency, total latency, tokens/sec (approx via usage), model size indicator.
Reference SDK: https://github.com/microsoft/Foundry-Local/tree/main/sdk/python
"""

import time, statistics, json
from openai import OpenAI

MODELS = [
    "qwen2.5-0.5b",
    "gemma-2-2b",
    "mistral-7b",
]

PROMPT = "Explain the principle of retrieval augmented generation in 2 sentences."
ROUNDS = 3

client = OpenAI(base_url="http://localhost:5273/v1", api_key="not-needed")

def run_round(model: str):
    start = time.time()
    resp = client.chat.completions.create(
        model=model,
        messages=[{"role": "user", "content": PROMPT}],
        max_tokens=150,
        temperature=0.2,
        stream=False
    )
    end = time.time()
    usage = getattr(resp, "usage", None)
    total_tokens = usage.total_tokens if usage else None
    return {
        "latency_sec": end - start,
        "total_tokens": total_tokens,
        "tokens_per_sec": (total_tokens / (end - start)) if (total_tokens and (end-start) > 0) else None,
        "sample_response": resp.choices[0].message.content[:160].replace("\n", " ")
    }

def benchmark_model(model: str):
    results = [run_round(model) for _ in range(ROUNDS)]
    latencies = [r["latency_sec"] for r in results]
    tps = [r["tokens_per_sec"] for r in results if r["tokens_per_sec"]]
    return {
        "model": model,
        "rounds": ROUNDS,
        "latency_avg": statistics.mean(latencies),
        "latency_p95": statistics.quantiles(latencies, n=20)[-1] if len(latencies) > 1 else latencies[0],
        "tokens_per_sec_avg": statistics.mean(tps) if tps else None,
        "sample": results[-1]["sample_response"]
    }

def main():
    summary = [benchmark_model(m) for m in MODELS]
    print(json.dumps(summary, indent=2))
    print("\nInterpretation Tips:\n- latency_avg: lower better\n- tokens_per_sec_avg: higher better\n- Compare quality manually on sample outputs.")

if __name__ == "__main__":
    main()
```

実行：

```powershell
python samples/03-oss-models/benchmark_models.py
```


### 4. パフォーマンス比較 (5分)

トレードオフを議論：ロード時間、メモリ使用量（タスクマネージャー / `nvidia-smi` / OSリソースモニターを観察）、出力品質と速度。Pythonベンチマークスクリプト（セッション3）を使用してレイテンシーとスループットを測定し、GPUアクセラレーションを有効にした後に再実行。

### 5. スタータープロジェクト (4分)

ベンチマークスクリプトを拡張してMarkdown形式のレポート生成機能を追加。

## スタータープロジェクト: `03-huggingface-models`の拡張

既存のサンプルを以下のように強化：

1. ベンチマーク集計 + CSV/Markdown出力を追加。
2. 簡易的な定性的スコアリング（プロンプトペアセット + 手動アノテーションスタブファイル）を実装。
3. プラグイン可能なモデルリストとプロンプトセット用のJSON設定（`models.json`）を導入。

## 検証チェックリスト

```powershell
foundry cache list
foundry model run qwen2.5-0.5b
curl http://localhost:5273/v1/models
```

すべてのターゲットモデルが表示され、プローブチャットリクエストに応答すること。

## サンプルシナリオとワークショップマッピング

| ワークショップスクリプト | シナリオ | 目標 | プロンプト / データセットソース |
|-----------------|----------|------|-------------------------|
| `samples/session03/benchmark_oss_models.py` / `notebooks/session03_benchmark_oss_models.ipynb` | エッジプラットフォームチームが埋め込み要約機能のデフォルトSLMを選択 | 候補モデル間でレイテンシー + p95 + トークン/秒の比較を生成 | インライン`PROMPT`変数 + 環境`BENCH_MODELS`リスト |

### シナリオの概要
プロダクトエンジニアリングチームは、オフライン会議メモ機能のデフォルト軽量要約モデルを選択する必要があります。固定されたプロンプトセット（以下の例を参照）を使用して、制御された決定論的ベンチマーク（temperature=0）を実行し、GPUアクセラレーションの有無でレイテンシーとスループットのメトリクスを収集します。

### プロンプトセットJSONの例（拡張可能）
```json
[
    "Explain the principle of retrieval augmented generation in 2 sentences.",
    "List 3 privacy benefits of local inference.",
    "Summarize why model size impacts latency on consumer hardware.",
    "Provide two scenarios where an SLM is preferable to an LLM."
]
```

各モデルごとにプロンプトをループし、プロンプトごとのレイテンシーをキャプチャして分布メトリクスを導出し、外れ値を検出します。

## モデル選択フレームワーク

| 次元 | メトリクス | 重要性 |
|----------|--------|----------------|
| レイテンシー | 平均 / p95 | ユーザー体験の一貫性 |
| スループット | トークン/秒 | バッチとストリーミングのスケーラビリティ |
| メモリ | 常駐サイズ | デバイス適合性と同時実行性 |
| 品質 | ルーブリックプロンプト | タスク適合性 |
| フットプリント | ディスクキャッシュ | 配布と更新 |
| ライセンス | 使用許可 | 商業的コンプライアンス |

## カスタムモデルによる拡張

高レベルパターン（擬似コード）：

```python
# pseudo_adapter.py (conceptual)
class CustomModelAdapter:
    def load(self, weights_path: str): ...
    def generate(self, prompt: str, **params) -> str: ...

# Register with local routing (future extensibility point)
```

進化するアダプターインターフェースについては公式リポジトリを参照：
https://github.com/microsoft/Foundry-Local/tree/main/sdk/python

## トラブルシューティング

| 問題 | 原因 | 解決策 |
|-------|-------|-----|
| mistral-7bでOOM | RAM/GPU不足 | 他のモデルを停止するか、より小型のバリアントを試す |
| 初回応答が遅い | コールドロード | 軽量プロンプトを定期的に送信してウォーム状態を維持 |
| ダウンロードが停止 | ネットワーク不安定 | 再試行するか、オフピーク時にプリフェッチ |

## 参考資料

- Foundry Local SDK: https://github.com/microsoft/Foundry-Local/tree/main/sdk/python
- Model Mondays: https://aka.ms/model-mondays
- Hugging Face Model Discovery: https://huggingface.co/models

---

**セッション時間**: 30分 (+ オプションの詳細解説)  
**難易度**: 中級

### オプションの強化

| 強化 | 利点 | 方法 |
|-------------|---------|-----|
| ストリーミング初回トークンレイテンシー | 知覚される応答性を測定 | `BENCH_STREAM=1`でベンチマークを実行（`Workshop/samples/session03`の拡張スクリプト） |
| 決定論的モード | 安定した回帰比較 | `temperature=0`、固定プロンプトセット、バージョン管理下でJSON出力をキャプチャ |
| 品質ルーブリックスコアリング | 定性的次元を追加 | `prompts.json`を維持し、期待される側面を記載；スコア（1–5）を手動またはセカンダリモデルでアノテート |
| CSV / Markdown出力 | 共有可能なレポート | スクリプトを拡張して`benchmark_report.md`をテーブルとハイライト付きで書き出し |
| モデル能力タグ | 後の自動ルーティングに役立つ | `{alias: {capabilities:[], size_mb:..}}`を含む`models.json`を維持 |
| キャッシュウォームアップフェーズ | コールドスタートバイアスを削減 | タイミングループ前に1回ウォームラウンドを実行（既に実装済み） |
| パーセンタイル精度 | 頑健な尾部レイテンシー | numpyパーセンタイルを使用（既にリファクタリング済みスクリプトに含まれる） |
| トークンコスト推定 | 経済的比較 | 推定コスト = (トークン/秒 * リクエストごとの平均トークン数) * エネルギー指標 |
| 失敗したモデルの自動スキップ | バッチ実行の回復力 | 各ベンチマークをtry/exceptでラップし、ステータスフィールドをマーク |

#### 最小Markdown出力スニペット

```python
with open("benchmark_report.md", "w") as f:
        f.write("|Model|Avg Latency|p95|TPS|\n|---|---|---|---|\n")
        for row in summary:
                f.write(f"|{row['alias']}|{row['latency_avg']:.2f}|{row['latency_p95']:.2f}|{(row.get('tokens_per_sec_avg') or 0):.1f}|\n")
```


#### 決定論的プロンプトセット例

```json
[
    "Summarize retrieval augmented generation.",
    "List 3 privacy benefits of local inference.",
    "Explain when to choose an SLM over an LLM."
]
```

固定リストをループして、コミット間で比較可能なメトリクスを取得。

---

**免責事項**:  
この文書は、AI翻訳サービス[Co-op Translator](https://github.com/Azure/co-op-translator)を使用して翻訳されています。正確性を追求しておりますが、自動翻訳には誤りや不正確な部分が含まれる可能性があることをご承知ください。元の言語で記載された文書が正式な情報源とみなされるべきです。重要な情報については、専門の人間による翻訳を推奨します。この翻訳の使用に起因する誤解や誤解釈について、当方は一切の責任を負いません。