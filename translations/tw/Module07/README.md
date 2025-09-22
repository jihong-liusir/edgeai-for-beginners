<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "cb6eadc312d5658a0cd71c0085b43742",
  "translation_date": "2025-09-22T11:33:12+00:00",
  "source_file": "Module07/README.md",
  "language_code": "tw"
}
-->
# 第七章：EdgeAI 範例

Edge AI 是人工智慧與邊緣運算的結合，能夠直接在設備上進行智能處理，而不依賴雲端連接。本章探討了五種不同平台和框架上的 EdgeAI 實現，展示了在邊緣運行 AI 模型的多樣性和強大功能。

## 1. NVIDIA Jetson Orin Nano 的 EdgeAI

NVIDIA Jetson Orin Nano 是一項突破性的邊緣 AI 計算平台，提供高達 67 TOPS 的 AI 性能，並以信用卡大小的緊湊形式呈現。這款強大的邊緣 AI 平台使生成式 AI 的開發變得更加普及，適合愛好者、學生和專業開發者。

### 主要特點
- 提供高達 67 TOPS 的 AI 性能，比前代提升 1.7 倍
- 配備 1024 CUDA 核心和最多 32 個 Tensor 核心進行 AI 處理
- 6 核 Arm Cortex-A78AE v8.2 64 位 CPU，最高頻率達 1.5 GHz
- 價格僅 $249，為開發者、學生和創客提供最實惠且易於使用的平台

### 應用場景
Jetson Orin Nano 擅長運行現代生成式 AI 模型，包括視覺變換器、大型語言模型和視覺語言模型。它專為生成式 AI 用例設計，現在可以在掌上設備上運行多種 LLM。常見應用包括 AI 驅動的機器人、智能無人機、智能攝像機和自主邊緣設備。

**了解更多**：[NVIDIA 的 Jetson Orin Nano 超級計算機：邊緣 AI 的下一個大事件](https://medium.com/data-science-in-your-pocket/nvidias-jetson-orin-nano-supercomputer-the-next-big-thing-in-edgeai-e9eff687ae62)

## 2. 使用 .NET MAUI 和 ONNX Runtime GenAI 的移動應用 EdgeAI

此解決方案展示了如何使用 .NET MAUI（多平台應用 UI）和 ONNX Runtime GenAI 將生成式 AI 和大型語言模型（LLMs）集成到跨平台移動應用中。此方法使 .NET 開發者能夠構建在 Android 和 iOS 設備上原生運行的高級 AI 驅動移動應用。

### 主要特點
- 基於 .NET MAUI 框架，提供 Android 和 iOS 應用的單一代碼基
- ONNX Runtime GenAI 集成使生成式 AI 模型能直接在移動設備上運行
- 支援多種針對移動設備的硬體加速器，包括 CPU、GPU 和專用移動 AI 處理器
- 平台特定優化，例如 iOS 的 CoreML 和 Android 的 NNAPI，通過 ONNX Runtime 實現
- 實現完整的生成式 AI 流程，包括前後處理、推理、logits 處理、搜索和採樣，以及 KV 緩存管理

### 開發優勢
使用 .NET MAUI 方法，開發者可以利用現有的 C# 和 .NET 技能，同時構建跨平台 AI 應用。ONNX Runtime GenAI 框架支援多種模型架構，包括 Llama、Mistral、Phi、Gemma 等。優化的 ARM64 核心加速 INT4 量化矩陣乘法，確保在移動硬體上高效運行，同時保持熟悉的 .NET 開發體驗。

### 使用場景
此解決方案非常適合希望使用 .NET 技術構建 AI 驅動移動應用的開發者，包括智能聊天機器人、圖像識別應用、語言翻譯工具和個性化推薦系統，這些應用完全在設備上運行，提供更高的隱私性和離線能力。

**了解更多**：[.NET MAUI ONNX Runtime GenAI 範例](https://github.com/microsoft/onnxruntime-genai/tree/jialli/genny-maui/examples/csharp/GennyMaui)

## 3. 使用 Azure 的小型語言模型引擎進行 EdgeAI

Microsoft 的基於 Azure 的 EdgeAI 解決方案專注於在雲邊緣混合環境中高效部署小型語言模型（SLMs）。此方法彌合了雲端 AI 服務與邊緣部署需求之間的差距。

### 架構優勢
- 與 Azure AI 服務無縫整合
- 使用 ONNX Runtime 在設備和雲端上運行 SLMs/LLMs 和多模態模型
- 為企業級部署進行優化
- 支援持續的模型更新和管理

### 使用場景
Azure EdgeAI 在需要企業級 AI 部署和雲端管理能力的場景中表現出色，包括智能文檔處理、實時分析和利用雲端與邊緣計算資源的混合 AI 工作流。

**了解更多**：[Azure EdgeAI SLM 引擎](https://github.com/microsoft/onnxruntime-genai/tree/main/examples/slm_engine)

## 4. 使用 Windows ML 的 EdgeAI

Windows ML 是 Microsoft 的尖端運行時，專為高效的設備端模型推理和簡化部署而優化，並作為 Windows AI Foundry 的基礎。此平台使開發者能夠創建利用 PC 硬體的 AI 驅動 Windows 應用。

### 平台能力
- 適用於所有運行 Windows 11 版本 24H2（build 26100）或更高版本的 PC
- 支援所有 x64 和 ARM64 PC 硬體，即使是沒有 NPU 或 GPU 的 PC
- 允許開發者使用自己的模型，並高效部署到包括 AMD、Intel、NVIDIA 和 Qualcomm 在內的矽合作夥伴生態系統，涵蓋 CPU、GPU、NPU
- 利用基礎設施 API，開發者不再需要為不同的矽目標創建多個應用版本

### 開發者優勢
Windows ML 抽象了硬體和執行提供者，因此您可以專注於編寫代碼。此外，Windows ML 會自動更新以支援最新的 NPU、GPU 和 CPU。該平台為 Windows 硬體生態系統提供統一的 AI 開發框架。

**了解更多**：
- [Windows ML 概述](https://learn.microsoft.com/en-us/windows/ai/new-windows-ml/overview)
- [Windows EdgeAI 開發指南](../windowdeveloper.md) - Windows Edge AI 開發的全面指南

## 5. 使用 Foundry Local 應用進行 EdgeAI

Foundry Local 使開發者能夠使用本地資源在 .NET 中構建檢索增強生成（RAG）應用，結合本地語言模型與語義搜索功能。此方法提供完全在本地基礎設施上運行的隱私保護 AI 解決方案。

### 技術架構
- 結合 Phi 語言模型、本地嵌入和語義核心，創建 RAG 場景
- 使用嵌入作為浮點值數組（向量），表示內容及其語義含義
- 語義核心作為主要協調器，整合 Phi 和智能組件，創建無縫的 RAG 管道
- 支援本地向量數據庫，包括 SQLite 和 Qdrant

### 實現優勢
RAG，即檢索增強生成，本質上是「查找一些內容並將其放入提示中」。此本地實現確保數據隱私，同時提供基於自定義知識庫的智能回應。此方法對於需要數據主權和離線操作能力的企業場景特別有價值。

**了解更多**：[Foundry Local RAG 範例](https://github.com/microsoft/Foundry-Local/tree/main/samples/dotNET/rag)

### Windows Foundry Local

Microsoft Foundry Local 提供了一個基於 ONNX Runtime 的 OpenAI 兼容 REST 伺服器，用於在 Windows 上本地運行模型。以下是快速驗證摘要；完整細節請參閱官方文檔。

- 開始使用：https://learn.microsoft.com/azure/ai-foundry/foundry-local/get-started
- 架構：https://learn.microsoft.com/azure/ai-foundry/foundry-local/concepts/foundry-local-architecture
- CLI 參考：https://learn.microsoft.com/azure/ai-foundry/foundry-local/reference/reference-cli
- 本 repo 中的完整 Windows 指南：[foundrylocal.md](./foundrylocal.md)

在 Windows 上安裝或升級（cmd.exe）：
```cmd
winget install Microsoft.FoundryLocal
winget upgrade --id Microsoft.FoundryLocal
foundry --version
```

探索 CLI 類別：
```cmd
foundry model --help
foundry service --help
foundry cache --help
```

運行模型並發現動態端點：
```cmd
foundry model run gpt-oss-20b
foundry service status
```

快速 REST 檢查列出模型（替換狀態中的 PORT）：
```cmd
curl -s http://localhost:PORT/v1/models
```

提示：
- SDK 集成：https://learn.microsoft.com/azure/ai-foundry/foundry-local/how-to/how-to-integrate-with-inference-sdks
- 使用自己的模型（編譯）：https://learn.microsoft.com/azure/ai-foundry/foundry-local/how-to/how-to-compile-hugging-face-models

## Windows EdgeAI 開發資源

針對專門面向 Windows 平台的開發者，我們創建了一份全面指南，涵蓋完整的 Windows EdgeAI 生態系統。此資源提供有關 Windows AI Foundry 的詳細信息，包括 API、工具和 Windows 上 EdgeAI 開發的最佳實踐。

### Windows AI Foundry 平台
Windows AI Foundry 平台提供了一套專門設計的工具和 API，專為 Windows 設備上的 Edge AI 開發而設計。包括對 NPU 加速硬體的專門支援、Windows ML 集成以及平台特定的優化技術。

**全面指南**：[Windows EdgeAI 開發指南](../windowdeveloper.md)

此指南涵蓋：
- Windows AI Foundry 平台概述及組件
- Phi Silica API，用於 NPU 硬體上的高效推理
- 計算機視覺 API，用於圖像處理和 OCR
- Windows ML 運行時集成與優化
- Foundry Local CLI，用於本地開發和測試
- Windows 設備的硬體優化策略
- 實際實現範例和最佳實踐

### Edge AI 開發的 AI 工具包
對於使用 Visual Studio Code 的開發者，AI 工具包擴展提供了一個專門設計的開發環境，用於構建、測試和部署 Edge AI 應用。此工具包簡化了整個 Edge AI 開發工作流程。

**開發指南**：[Edge AI 開發的 AI 工具包](../aitoolkit.md)

AI 工具包指南涵蓋：
- 邊緣部署的模型發現與選擇
- 本地測試與優化工作流程
- ONNX 和 Ollama 集成，用於邊緣模型
- 模型轉換與量化技術
- 用於邊緣場景的代理開發
- 性能評估與監控
- 部署準備與最佳實踐

## 結論

這五種 EdgeAI 實現展示了當今邊緣 AI 解決方案的成熟度和多樣性。從像 Jetson Orin Nano 這樣的硬體加速邊緣設備，到像 ONNX Runtime GenAI 和 Windows ML 這樣的軟體框架，開發者擁有前所未有的選擇來在邊緣部署智能應用。

這些平台的共同特點是 AI 能力的普及化，使得複雜的機器學習對不同技能水平和使用場景的開發者都變得可及。無論是構建移動應用、桌面軟體還是嵌入式系統，這些 EdgeAI 解決方案都為下一代高效且隱私友好的邊緣智能應用奠定了基礎。

每個平台都提供獨特的優勢：Jetson Orin Nano 用於硬體加速邊緣計算，ONNX Runtime GenAI 用於跨平台移動開發，Azure EdgeAI 用於企業雲邊緣整合，Windows ML 用於 Windows 原生應用，Foundry Local 用於隱私保護的 RAG 實現。它們共同構成了一個全面的 EdgeAI 開發生態系統。

---

