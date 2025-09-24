<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "7a474b8e201d5316c0095cdbc3bf0555",
  "translation_date": "2025-09-24T14:31:40+00:00",
  "source_file": "Module08/samples/04/webgpu-demo/README.md",
  "language_code": "mo"
}
-->
# WebGPU + ONNX Runtime 示範

此示範展示如何使用 WebGPU 進行硬體加速以及 ONNX Runtime Web，在瀏覽器中直接執行 AI 模型。

## 此示範的內容

- **基於瀏覽器的 AI**：完全在瀏覽器中執行模型
- **WebGPU 加速**：在可用時進行硬體加速推論
- **隱私優先**：資料不會離開您的設備
- **零安裝**：在任何相容的瀏覽器中運作
- **平滑回退**：若 WebGPU 不可用，則回退至 CPU

## 系統需求

**瀏覽器相容性：**
- Chrome/Edge 113+ 並啟用 WebGPU
- 檢查 WebGPU 狀態：`chrome://gpu`
- 啟用 WebGPU：`chrome://flags/#enable-unsafe-webgpu`

## 執行示範

### 選項 1：本地伺服器（推薦）

```cmd
# Navigate to the demo directory
cd Module08\samples\04\webgpu-demo

# Start a local server
python -m http.server 5173

# Open browser to http://localhost:5173
```

### 選項 2：VS Code Live Server

1. 在 VS Code 中安裝 "Live Server" 擴展
2. 右鍵點擊 `index.html` → "Open with Live Server"
3. 示範會自動在瀏覽器中開啟

## 您將看到的內容

1. **WebGPU 檢測**：檢查瀏覽器相容性
2. **模型載入**：下載並初始化 MNIST 分類器
3. **推論執行**：對樣本資料進行預測
4. **效能指標**：顯示載入時間和推論速度
5. **結果展示**：預測信心和原始輸出

## 預期效能

| 執行提供者       | 模型載入 | 推論       | 備註               |
|-------------------|----------|------------|--------------------|
| **WebGPU**        | ~2-5秒   | ~10-50毫秒 | 硬體加速           |
| **CPU (WASM)**    | ~2-5秒   | ~50-200毫秒| 軟體回退           |

## 疑難排解

**WebGPU 不可用：**
- 更新至 Chrome/Edge 113+
- 在 `chrome://flags` 中啟用 WebGPU
- 檢查 GPU 驅動程式是否為最新
- 示範會自動回退至 CPU

**載入錯誤：**
- 確保您是通過 HTTP 提供服務（而非 file://）
- 檢查網路連線以下載模型
- 確認 CORS 未阻擋 ONNX 模型

**效能問題：**
- WebGPU 比 CPU 提供顯著的速度提升
- 第一次執行可能較慢，因為需要下載模型
- 後續執行會使用瀏覽器快取

## 與 Foundry Local 的整合

此 WebGPU 示範補充了 Foundry Local，展示了：

- **客戶端推論**以實現最終的隱私
- **離線功能**在無網路時運作  
- **邊緣部署**適用於資源受限的環境
- **混合架構**結合本地和伺服器推論

對於生產應用，建議：
- 使用 Foundry Local 進行伺服器端推論
- 使用 WebGPU 進行客戶端的預處理/後處理
- 實現本地/遠端推論之間的智能路由

## 技術細節

**使用的模型：**
- MNIST 數字分類器（ONNX 格式）
- 輸入：28x28 灰度圖像
- 輸出：10類概率分佈
- 大小：約500KB（快速下載）

**ONNX Runtime Web：**
- WebGPU 執行提供者，用於 GPU 加速
- WASM 執行提供者，用於 CPU 回退
- 自動優化和圖形優化

**瀏覽器 API：**
- WebGPU 用於硬體存取
- Web Workers 用於背景處理（未來增強）
- WebAssembly 用於高效計算

## 下一步

- 嘗試使用自定義 ONNX 模型
- 實現真實圖像上傳和分類
- 添加大型模型的流式推論
- 與相機/麥克風輸入整合

---

