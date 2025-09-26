<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "bad055c54c7952c482113fd7fe1d43c1",
  "translation_date": "2025-09-26T18:22:17+00:00",
  "source_file": "Module08/README.md",
  "language_code": "tw"
}
-->
# 模組 08：深入了解 Microsoft Foundry Local - 完整開發者工具包

## 概述

[Microsoft Foundry Local](https://learn.microsoft.com/azure/ai-foundry/foundry-local/) 代表了邊緣 AI 開發的下一代技術，為開發者提供強大的工具，用於在本地構建、部署和擴展 AI 應用，同時保持與 Azure AI Foundry 的無縫整合。本模組涵蓋了 Foundry Local 的完整內容，從安裝到高級代理開發。

**核心技術：**
- Microsoft Foundry Local CLI 和 SDK
- Azure AI Foundry 整合
- 本地模型推理
- 模型緩存與優化
- 基於代理的架構

## 學習目標

完成本模組後，您將能夠：

- **精通 Foundry Local**：安裝、配置並優化 Windows 11 開發環境
- **部署多樣化模型**：使用 CLI 命令在本地運行 phi、qwen、deepseek 和 GPT 模型
- **構建生產解決方案**：利用高級提示工程和數據整合創建 AI 應用
- **利用開源生態系統**：整合 Hugging Face 模型和社群貢獻
- **開發 AI 代理**：構建具有基礎和編排能力的智能代理
- **實施企業模式**：創建模組化、可擴展的 AI 解決方案以進行生產部署

## 課程結構

### [1: 開始使用 Foundry Local](./01.FoundryLocalSetup.md)
**重點**：安裝、CLI 設置、模型部署和硬件優化

**核心主題**：完整安裝 • CLI 命令 • 模型緩存 • 硬件加速 • 多模型部署

**範例**：[REST 聊天快速入門](./samples/01/README.md) • [OpenAI SDK 整合](./samples/02/README.md) • [模型探索與基準測試](./samples/03/README.md)

**時長**：2-3 小時 | **等級**：初學者

---

### [2: 使用 Azure AI Foundry 構建 AI 解決方案](./02.AzureAIFoundryIntegration.md)
**重點**：高級提示工程、數據整合和雲端連接

**核心主題**：提示工程 • 數據整合 • Azure 工作流程 • 性能優化 • 監控

**範例**：[Chainlit RAG 應用](./samples/04/README.md)

**時長**：2-3 小時 | **等級**：中級

---

### [3: Foundry Local 的開源模型](./03.OpenSourceModels.md)
**重點**：Hugging Face 整合、BYOM 策略和社群模型

**核心主題**：HuggingFace 整合 • 自帶模型 • Model Mondays 洞察 • 社群貢獻 • 模型選擇

**範例**：[多代理編排](./samples/05/README.md)

**時長**：2-3 小時 | **等級**：中級

---

### [4: 探索尖端模型](./04.CuttingEdgeModels.md)
**重點**：LLM 與 SLM 比較、EdgeAI 實現和高級演示

**核心主題**：模型比較 • 邊緣與雲端推理 • Phi + ONNX Runtime • Chainlit RAG 應用 • WebGPU 優化

**範例**：[工具化模型路由器](./samples/06/README.md)

**時長**：3-4 小時 | **等級**：高級

---

### [5: 快速構建 AI 驅動代理](./05.AIPoweredAgents.md)
**重點**：代理架構、系統提示、基礎和編排

**核心主題**：代理設計模式 • 系統提示工程 • 基礎技術 • 多代理系統 • 生產部署

**範例**：[多代理編排](./samples/05/README.md) • [高級多代理系統](./samples/09/README.md)

**時長**：3-4 小時 | **等級**：高級

---

### [6: Foundry Local - 工具化模型](./06.ModelsAsTools.md)
**重點**：模組化 AI 解決方案、企業擴展和生產模式

**核心主題**：工具化模型 • 本地部署 • SDK/API 整合 • 企業架構 • 擴展策略

**範例**：[工具化模型路由器](./samples/06/README.md) • [Foundry 工具框架](./samples/10/README.md)

**時長**：3-4 小時 | **等級**：專家

---

### [7: 直接 API 整合模式](./samples/07/README.md)
**重點**：純 REST API 整合，無需 SDK 依賴，提供最大控制

**核心主題**：HTTP 客戶端實現 • 自定義身份驗證 • 模型健康監控 • 流式響應 • 生產錯誤處理

**範例**：[直接 API 客戶端](./samples/07/README.md)

**時長**：2-3 小時 | **等級**：中級

---

### [8: Windows 11 原生聊天應用](./samples/08/README.md)
**重點**：使用 Foundry Local 整合構建現代原生聊天應用

**核心主題**：Electron 開發 • Fluent 設計系統 • 原生 Windows 整合 • 實時流式傳輸 • 聊天界面設計

**範例**：[Windows 11 聊天應用](./samples/08/README.md)

**時長**：3-4 小時 | **等級**：高級

---

### [9: 高級多代理編排](./samples/09/README.md)
**重點**：複雜代理協調、專業任務分配和協作 AI 工作流程

**核心主題**：智能代理協調 • 函數調用模式 • 跨代理通信 • 工作流程編排 • 質量保證機制

**範例**：[高級多代理系統](./samples/09/README.md)

**時長**：4-5 小時 | **等級**：專家

---

### [10: Foundry Local 作為工具框架](./samples/10/README.md)
**重點**：以工具為核心的架構，將 Foundry Local 整合到現有應用和框架中

**核心主題**：LangChain 整合 • Semantic Kernel 函數 • REST API 框架 • CLI 工具 • Jupyter 整合 • 生產部署模式

**範例**：[Foundry 工具框架](./samples/10/README.md)

**時長**：4-5 小時 | **等級**：專家

## 先決條件

### 系統需求
- **操作系統**：Windows 11 (22H2 或更高版本)
- **記憶體**：16GB RAM（建議 32GB 用於更大模型）
- **存儲**：50GB 可用空間用於模型緩存
- **硬件**：建議使用支持 NPU 的設備（Copilot+ PC），GPU 可選
- **網絡**：高速網絡用於初始模型下載

### 開發環境
- Visual Studio Code，安裝 AI Toolkit 擴展
- Python 3.10+ 和 pip
- Git 用於版本控制
- PowerShell 或命令提示符
- Azure CLI（可選，用於雲端整合）

### 知識要求
- 基本 AI/ML 概念理解
- 命令行操作熟悉
- Python 編程基礎
- REST API 概念
- 提示工程和模型推理的基本知識

## 模組時間表

**總預估時間**：30-38 小時

| 課程 | 重點領域 | 範例 | 時間 | 複雜度 |
|------|----------|------|------|--------|
|  1 | 設置與基礎 | 01, 02, 03 | 2-3 小時 | 初學者 |
|  2 | AI 解決方案 | 04 | 2-3 小時 | 中級 |
|  3 | 開源 | 05 | 2-3 小時 | 中級 |
|  4 | 高級模型 | 06 | 3-4 小時 | 高級 |
|  5 | AI 代理 | 05, 09 | 3-4 小時 | 高級 |
|  6 | 企業工具 | 06, 10 | 3-4 小時 | 專家 |
|  7 | 直接 API 整合 | 07 | 2-3 小時 | 中級 |
|  8 | Windows 11 聊天應用 | 08 | 3-4 小時 | 高級 |
|  9 | 高級多代理 | 09 | 4-5 小時 | 專家 |
| 10 | 工具框架 | 10 | 4-5 小時 | 專家 |

## 核心資源

**官方文檔：**
- [Microsoft Foundry Local GitHub](https://github.com/microsoft/Foundry-Local) - 原始碼和官方範例
- [Azure AI Foundry 文檔](https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/) - 完整設置和使用指南
- [Model Mondays 系列](https://aka.ms/model-mondays) - 每週模型亮點和教程

**社群與支持：**
- [Foundry Local 討論區](https://github.com/microsoft/Foundry-Local/discussions) - 社群問答和功能請求
- [Microsoft AI 開發者社群](https://techcommunity.microsoft.com/category/artificialintelligence) - 最新消息和最佳實踐

## 學習成果

完成本模組後，您將具備以下能力：

### 技術精通
- **部署與管理**：在開發和生產環境中安裝和管理 Foundry Local
- **整合模型**：無縫使用 Microsoft、Hugging Face 和社群來源的多樣化模型
- **構建應用**：創建具有高級功能和優化的生產級 AI 應用
- **開發代理**：實現具有基礎、推理和工具整合的高級 AI 代理

### 策略理解
- **架構決策**：在本地與雲端部署之間做出明智選擇
- **性能優化**：在不同硬件配置中優化推理性能
- **企業擴展**：設計從本地原型到企業部署的可擴展應用
- **隱私與安全**：實施隱私保護的 AI 解決方案，使用本地推理

### 創新能力
- **快速原型**：快速構建和測試 AI 應用概念，涵蓋所有 10 個範例模式
- **社群整合**：利用開源模型並為生態系統做出貢獻
- **高級模式**：實現尖端 AI 模式，包括 RAG、代理和工具整合
- **框架精通**：專家級整合 LangChain、Semantic Kernel、Chainlit 和 Electron
- **生產部署**：從本地原型到企業系統部署可擴展 AI 解決方案
- **面向未來的開發**：構建適應新興 AI 技術和模式的應用

## 開始使用

1. **環境設置**：確保使用推薦硬件的 Windows 11（參見先決條件）
2. **安裝 Foundry Local**：按照課程 1 完成安裝和配置
3. **運行範例 01**：從基本的 REST API 整合開始，驗證設置
4. **完成範例**：完成範例 01-10，全面掌握技能

## 成功指標

通過所有 10 個全面範例來跟蹤您的進度：

### 基礎級別（範例 01-03）
- [ ] 成功安裝並配置 Foundry Local
- [ ] 完成 REST API 整合（範例 01）
- [ ] 實現 OpenAI SDK 兼容性（範例 02）
- [ ] 執行模型探索和基準測試（範例 03）

### 應用級別（範例 04-06）
- [ ] 部署並運行至少 4 種不同的模型系列
- [ ] 構建功能性 RAG 聊天應用（範例 04）
- [ ] 創建多代理編排系統（範例 05）
- [ ] 實現智能模型路由（範例 06）

### 高級整合級別（範例 07-10）
- [ ] 構建生產級 API 客戶端（範例 07）
- [ ] 開發 Windows 11 原生聊天應用（範例 08）
- [ ] 實現高級多代理系統（範例 09）
- [ ] 創建全面的工具框架（範例 10）

### 精通指標
- [ ] 成功運行所有 10 個範例，無錯誤
- [ ] 為特定用例自定義至少 3 個範例
- [ ] 在類似生產環境中部署 2+ 範例
- [ ] 為範例代碼做出改進或擴展
- [ ] 將 Foundry Local 模式整合到個人/專業項目中

## 快速入門指南 - 所有 10 個範例

### 環境設置（所有範例必需）

```powershell
# 1. Clone and navigate to Module08
cd Module08

# 2. Create Python virtual environment
py -m venv .venv
.\.venv\Scripts\activate

# 3. Install base dependencies
pip install -r requirements.txt

# 4. Install Foundry Local (if not already installed)
winget install Microsoft.FoundryLocal

# 5. Verify Foundry Local installation
foundry --version
foundry model list
```

### 核心基礎範例（01-06）

**範例 01：REST 聊天快速入門**
```powershell
# Start Foundry Local service
foundry model run phi-4-mini

# Run REST chat demo
python samples/01/chat_quickstart.py
```

**範例 02：OpenAI SDK 整合**
```powershell
# Ensure model is running
foundry status

# Run SDK demo
python samples/02/sdk_quickstart.py
```

**範例 03：模型探索與基準測試**
```powershell
# Run comprehensive model testing
samples/03/list_and_bench.cmd

# Or run individual components
foundry model list --available
foundry model download qwen2.5-0.5b
foundry model benchmark phi-4-mini
```

**範例 04：Chainlit RAG 應用**
```powershell
# Install Chainlit dependencies
pip install chainlit langchain chromadb

# Start RAG chat application
chainlit run samples/04/app.py -w
# Opens browser at http://localhost:8000
```

**範例 05：多代理編排**
```powershell
# Run agent coordinator demo
python -m samples.05.agents.coordinator

# Run specific agent examples
python samples/05/examples/specialists_demo.py
```

**範例 06：工具化模型路由器**
```powershell
# Configure environment
set BASE_URL=http://localhost:8000
set GENERAL_MODEL=phi-4-mini
set CODE_MODEL=qwen2.5-7b-instruct

# Run intelligent router
python samples/06/router.py "Analyze this Python code for performance issues"
```

### 高級整合範例（07-10）

**範例 07：直接 API 客戶端**
```powershell
# Navigate to sample directory
cd samples/07

# Install additional dependencies
pip install -r requirements.txt

# Run basic API examples
python examples/basic_usage.py

# Try streaming responses
python examples/streaming.py

# Test production patterns
python examples/production.py
```

**範例 08：Windows 11 聊天應用**
```powershell
# Navigate to sample directory
cd samples/08

# Install Node.js dependencies
npm install

# Start Electron application
npm start

# Or build for production
npm run build
```

**範例 09：高級多代理系統**
```powershell
# Navigate to sample directory
cd samples/09

# Install agent system dependencies
pip install -r requirements.txt

# Run basic coordination example
python examples/basic_coordination.py

# Try complex workflow
python examples/complex_workflow.py

# Interactive agent demo
python examples/interactive_demo.py
```

**範例 10：Foundry 工具框架**
```powershell
# Navigate to sample directory
cd samples/10

# Install framework dependencies
pip install -r requirements.txt

# Run basic tools demo
python examples/basic_tools.py

# Start REST API server
python examples/rest_api_server.py
# API available at http://localhost:8080

# Try CLI application
python examples/cli_application.py --help

# Launch Jupyter notebook
jupyter notebook examples/jupyter_notebook.ipynb

# Test LangChain integration
python examples/langchain_demo.py
```

### 常見問題排查

**Foundry Local 連接錯誤**
```powershell
# Check service status
foundry status

# Restart if needed
foundry restart

# Verify endpoint accessibility
curl http://localhost:5273/v1/models
```

**模型加載問題**
```powershell
# Check available models
foundry model list --cached

# Download missing models
foundry model download phi-4-mini
foundry model download qwen2.5-0.5b

# Force reload if needed
foundry model unload --all
foundry model run phi-4-mini
```

**依賴問題**
```powershell
# Upgrade pip and reinstall
python -m pip install --upgrade pip
pip install -r requirements.txt --force-reinstall

# For Node.js samples
npm cache clean --force
npm install
```

## 總結
此模組代表了邊緣 AI 開發的最前沿，結合了 Microsoft 企業級工具與開源生態系統的靈活性與創新性。透過掌握 Foundry Local 的全部 10 個綜合範例，您將站在 AI 應用開發的最前線。

**完整學習路徑：**
- **基礎**（範例 01-03）：API 整合與模型管理
- **應用**（範例 04-06）：RAG、代理與智能路由
- **進階**（範例 07-10）：生產框架與企業整合

關於 Azure OpenAI 整合（第二節），請參閱各範例的 README 文件以了解所需的環境變數和 API 版本設定。

---

