# Codebase Atlas

**用於人工智慧輔助開發的代碼庫導航協議與工程架構治理系統**

## 專案願景

Codebase Atlas 是一套專為解決 AI 代理人（AI Agents）在處理大型且複雜代碼庫時常見的「上下文迷失」與「架構漂移」問題而設計的系統化協議。它不單是一個文檔生成工具，更是一個將專案智慧（Project Intelligence）從易失的對話上下文轉化為持久化、可版本化資產的工程方案。

透過這套系統，開發者能為 AI 代理人建立一套完整的「導航層」，使其在動手修改代碼前，能先理解模組邊界、依賴關係、潛在風險以及必須遵循的工程規範。

## 核心價值：「一次性初始化，多次重複使用」戰略

目前的 AI 工具通常在每次會話中重新探索代碼庫，造成顯著的資源浪費。Codebase Atlas 提倡角色分離的戰略：

*   **建築師模式（強模型初始化）**：建議調用最強的模型進行深度掃描。此模型扮演資深架構師的角色，識別隱藏模式、定義模組邊界、分析跨模組影響，並構建 Atlas 地圖。
*   **工人模式（標準模型執行）**：地圖建立後，日常開發任務可由更經濟的模型處理。這些模型遵循「架構師」預定義的地圖與工作流，以極低的上下文負擔達成高質量的產出。

## 運作模型

### 1. 初始化與決策機制
當協議啟動時，AI 代理人不會立即開始掃描。它必須先與使用者確認四個關鍵決策，以確保 Atlas 符合專案需求：

1.  **輸出語言**：繁體中文或英文。
2.  **Atlas 模式**：獨立模式（以現有代碼為唯一事實）或參考輔助模式（借鏡外部儲存庫或規格書）。
3.  **交付規則**：為未來任務紀錄規範（不提交、僅提交、或提交並推送）。
4.  **功能對齊工作流**：（僅限參考輔助模式）是否需要啟用用於遷移對齊或功能擴張的特定工作流。

### 2. Atlas 構建流程
AI 代理人會深度掃描儲存庫，忽略非原始碼目錄（如 node_modules, dist, .git），並根據產品或架構邊界將程式碼劃分為 6-20 個穩定模組。

### 3. 工作流嵌入
系統會將具體的工程標準嵌入到未來 AI 任務的執行路徑中，確保每一次變更都經過 Atlas 的驗證並產出文檔紀錄。

## 產出物結構

產出的地圖存放在專案根目錄的 `docs/` 資料夾下：

### 獨立專案模式
```text
docs/
  <project>_index.md
  <project>/
    <module_slug>.md
  <project>_bug_workflow.md
  <project>_feature_workflow.md
  <project>_optimization_workflow.md
  <project>_investigation_workflow.md
  <project>_refactor_workflow.md
  <project>_validation_workflow.md
```

### 參考輔助模式
```text
docs/
  <project>_<reference>_index.md
  <project>_<reference>/
    <module_slug>.md
  <project>_<reference>_bug_workflow.md
  <project>_<reference>_optimization_workflow.md
  <project>_<reference>_investigation_workflow.md
  <project>_<reference>_refactor_workflow.md
  <project>_<reference>_validation_workflow.md
  <project>_<reference>_feature_workflow.md (選配：用於功能對齊)
```

## 詳細模式選擇

### 獨立模式 (Standalone Mode)
當目標專案是其自身的主要事實來源時使用。AI 專注於現有代碼來推導邊界與流程。

### 參考輔助模式 (Reference-Assisted Mode)
當目標專案需要搭配參考儲存庫、資料夾、API 規格書或設計文件來理解時使用。
*   **借鏡而非盲目對齊**：預設情況下，參考資料用於引導架構、邊界與穩定化模式，而不會自動變成待辦功能清單。
*   **適用場景**：架構遷移、重構以符合某種標準，或實作特定的 API 模式。

## 標準開發工作流範例

地圖建立完成後，一般的開發任務請直接指引 AI 使用產出的工作流文檔：

*   **錯誤修復**：`請讀取 docs/<project>_bug_workflow.md，並依照規範修復此問題：[描述]`
*   **功能開發**：`請讀取 docs/<project>_feature_workflow.md，並實作以下功能：[描述]`
*   **優化整理**：`請讀取 docs/<project>_optimization_workflow.md，優化此區塊：[描述]`
*   **調查行為**：`請讀取 docs/<project>_investigation_workflow.md，調查此邏輯：[描述]`
*   **系統重構**：`請讀取 docs/<project>_refactor_workflow.md，重構此結構：[描述]`
*   **變更驗證**：`請讀取 docs/<project>_validation_workflow.md，驗證此改動：[描述]`

## 技術特性

*   **代理人中立協議**：適用於任何具備檔案讀寫能力的 AI 代理人。
*   **純文字移植性**：基於 Markdown，無需安裝資料庫、腳本或特定執行環境。
*   **雙語一致性**：內建繁體中文術語表，確保專業術語的一致性（如：上游依賴、下游影響）。
*   **邊界強制執行**：在每個模組文檔中明確定義「常用修改入口」與「已知風險」。

## 安裝方式

1.  克隆儲存庫：
    ```bash
    git clone https://github.com/bennytsai1234/codebase-atlas.git
    ```
2.  指引你的 AI 代理人讀取該目錄下的 `SKILL.md` 文件。

## 授權協議

MIT
