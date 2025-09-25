<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "b64f4a8cbb9b8d57863b1101b111b05d",
  "translation_date": "2025-09-24T09:59:25+00:00",
  "source_file": "Module08/samples/04/open-webui-guide.md",
  "language_code": "hk"
}
-->
# Open WebUI + Foundry Local 整合指南

本指南展示如何將 Open WebUI 連接到 Microsoft Foundry Local，打造一個由本地 AI 模型驅動的專業 ChatGPT 介面。

## 概述

Open WebUI 提供了一個現代化、易於使用的聊天介面，可連接到任何兼容 OpenAI 的 API。通過連接到 Foundry Local，您可以獲得以下功能：

- **專業介面**：類似 ChatGPT 的現代化設計
- **本地隱私**：所有處理均在您的設備上進行
- **模型切換**：輕鬆切換不同的本地模型
- **對話歷史**：持久的聊天記錄和上下文
- **文件上傳**：文檔分析和文件處理功能
- **自定義角色**：系統提示和角色定制

## 先決條件

### 所需軟件

```cmd
# Verify Foundry Local installation
foundry --version

# Verify Docker installation
docker --version

# Start Foundry Local service
foundry service start
```

### 加載模型

```cmd
# List available models
foundry model list

# Load your preferred model
foundry model run phi-4-mini

# Verify model is running
foundry service ps
```

## 快速設置（推薦）

### 步驟 1：使用 Docker 運行 Open WebUI

```cmd
# Pull the latest Open WebUI image
docker pull ghcr.io/open-webui/open-webui:main

# Run Open WebUI connected to Foundry Local
docker run -d \
  --name open-webui \
  -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  -v open-webui-data:/app/backend/data \
  ghcr.io/open-webui/open-webui:main
```

**Windows PowerShell：**
```powershell
docker run -d `
  --name open-webui `
  -p 3000:8080 `
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 `
  -e OPENAI_API_KEY=foundry-local-key `
  -v open-webui-data:/app/backend/data `
  ghcr.io/open-webui/open-webui:main
```

### 步驟 2：初始設置

1. **打開瀏覽器**：導航到 `http://localhost:3000`
2. **創建帳戶**：設置管理員用戶（第一個用戶將成為管理員）
3. **驗證連接**：模型應自動出現在下拉菜單中

### 步驟 3：測試連接

1. 從下拉菜單中選擇您的模型（例如 "phi-4-mini"）
2. 輸入測試消息："你好！可以介紹一下自己嗎？"
3. 您應該能看到來自本地模型的流式響應

## 高級配置

### 環境變量

| 變量 | 用途 | 默認值 | 示例 |
|------|------|--------|------|
| `OPENAI_API_BASE_URL` | Foundry Local 端點 | - | `http://host.docker.internal:51211/v1` |
| `OPENAI_API_KEY` | API 密鑰（必需但本地未使用） | - | `foundry-local-key` |
| `WEBUI_SECRET_KEY` | 會話加密密鑰 | 自動生成 | `your-secret-key` |
| `ENABLE_SIGNUP` | 允許新用戶註冊 | `True` | `False` |

### 手動配置（替代方案）

如果環境變量無法正常工作，可手動配置：

1. **打開設置**：點擊設置（齒輪圖標）
2. **導航到連接**：設置 → 連接 → OpenAI
3. **設置 API 詳細信息**：
   - API 基本 URL：`http://host.docker.internal:51211/v1`
   - API 密鑰：`foundry-local-key`（任意值均可）
4. **保存並測試**：點擊 "保存"，然後使用模型進行測試

### 持久化數據存儲

要持久化保存對話和設置：

```cmd
# Windows - Create data directory
mkdir %USERPROFILE%\openwebui-data

# Run with persistent storage
docker run -d \
  --name open-webui \
  -p 3000:8080 \
  -v "%USERPROFILE%\openwebui-data:/app/backend/data" \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```

## 故障排除

### 連接問題

**問題**："連接被拒絕" 或模型未加載

**解決方案**：
```cmd
# 1. Verify Foundry Local is running
foundry service status
foundry service ps

# 2. Test API endpoint directly
curl http://localhost:51211/v1/models

# 3. Check Docker container logs
docker logs open-webui

# 4. Restart Open WebUI container
docker restart open-webui
```

### 模型未顯示

**問題**：Open WebUI 的下拉菜單中未顯示模型

**調試步驟**：
```cmd
# Check if model is loaded in Foundry Local
foundry model list

# Test API response
curl -X GET http://localhost:51211/v1/models \
  -H "Content-Type: application/json"

# Verify correct port (should be 51211 for Foundry Local)
netstat -ano | findstr :51211
```

**修復**：確保模型已正確加載：
```cmd
# Stop and restart model
foundry model stop phi-4-mini
foundry model run phi-4-mini

# Wait for model to fully load, then refresh Open WebUI
```

### Docker 網絡問題

**問題**：`host.docker.internal` 無法解析

**Windows 解決方案**：
```cmd
# Use localhost alternative (may need admin privileges)
docker run -d \
  --name open-webui \
  -p 3000:8080 \
  --add-host=host.docker.internal:host-gateway \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-key \
  ghcr.io/open-webui/open-webui:main
```

**替代方案**：查找您的機器 IP：
```cmd
ipconfig | findstr IPv4
# Use your actual IP instead of host.docker.internal
# Example: http://192.168.1.100:51211/v1
```

### 性能問題

**響應速度慢**：
1. 檢查模型是否使用 GPU 加速：`foundry service ps`
2. 確保系統資源充足（RAM/GPU 記憶體）
3. 考慮使用較小的模型進行測試

**內存問題**：
```cmd
# Check Docker container memory usage
docker stats open-webui

# Restart Docker if needed
docker restart open-webui
```

## 使用指南

### 基本聊天

1. **選擇模型**：從下拉菜單中選擇 Foundry Local 模型
2. **輸入消息**：使用底部的文本輸入框
3. **發送**：按 Enter 或點擊發送按鈕
4. **查看響應**：實時查看流式響應

### 高級功能

**文件上傳**：
1. 點擊回形針圖標
2. 上傳文檔（PDF、TXT 等）
3. 提問有關內容的問題
4. 模型將根據文檔進行分析並響應

**自定義系統提示**：
1. 設置 → 個性化
2. 設置自定義系統提示
3. 創建一致的 AI 個性/行為

**對話管理**：
- **新聊天**：點擊 "+" 開始新的對話
- **聊天歷史**：從側邊欄訪問之前的對話
- **導出**：以文本/JSON 格式下載聊天記錄

**模型比較**：
1. 在多個瀏覽器標籤中打開相同的 Open WebUI
2. 在每個標籤中選擇不同的模型
3. 比較相同提示的響應

### 整合模式

**開發工作流**：
```cmd
# Terminal 1: Start Foundry Local with development model
foundry model run phi-4-mini

# Terminal 2: Start Open WebUI for testing
docker run --rm -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=dev-key \
  ghcr.io/open-webui/open-webui:main

# Terminal 3: Test API directly for debugging
curl -X POST http://localhost:51211/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{"model":"phi-4-mini","messages":[{"role":"user","content":"test"}]}'
```

## 生產部署

### 安全設置

```cmd
# Generate secure secret key
openssl rand -base64 32

# Production deployment with security
docker run -d \
  --name open-webui-prod \
  -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-local-prod \
  -e WEBUI_SECRET_KEY=your-secure-key-here \
  -e ENABLE_SIGNUP=False \
  -v /path/to/secure/storage:/app/backend/data \
  --restart unless-stopped \
  ghcr.io/open-webui/open-webui:main
```

### 多用戶設置

```cmd
# Allow controlled user registration
docker run -d \
  --name open-webui-team \
  -p 3000:8080 \
  -e OPENAI_API_BASE_URL=http://host.docker.internal:51211/v1 \
  -e OPENAI_API_KEY=foundry-team \
  -e ENABLE_SIGNUP=True \
  -e WEBUI_SECRET_KEY=team-secret-key \
  -v team-data:/app/backend/data \
  ghcr.io/open-webui/open-webui:main
```

### 監控和日誌

```cmd
# View real-time logs
docker logs -f open-webui

# Monitor container resources
docker stats open-webui

# Check container health
docker inspect open-webui | grep -i health
```

## 清理

```cmd
# Stop Open WebUI
docker stop open-webui

# Remove container
docker rm open-webui

# Remove data volume (WARNING: deletes all chats)
docker volume rm open-webui-data

# Remove image
docker rmi ghcr.io/open-webui/open-webui:main
```

## 下一步

### 增強建議

1. **自定義模型**：向 Foundry Local 添加您自己的微調模型
2. **API 整合**：通過 Open WebUI 功能連接外部 API
3. **文檔處理**：設置高級 RAG 管道
4. **多模態**：配置視覺模型進行圖像分析

### 擴展考量

- **負載均衡**：在反向代理後運行多個 Foundry Local 實例
- **模型路由**：針對不同用例使用不同模型
- **資源管理**：為並發用戶優化 GPU 記憶體
- **備份策略**：定期備份對話數據和配置

## 參考資料

- [Open WebUI 文檔](https://docs.openwebui.com/)
- [Open WebUI GitHub 儲存庫](https://github.com/open-webui/open-webui)
- [Foundry Local 文檔](https://learn.microsoft.com/azure/ai-foundry/foundry-local/)
- [Docker 安裝指南](https://docs.docker.com/get-docker/)

---

