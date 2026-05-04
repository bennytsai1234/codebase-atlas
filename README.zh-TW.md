# Codebase Atlas

**一個確保 AI 代理人能精確定位並解決真實問題的工程協議。它透過持久化地圖與人機協作（Human-in-the-Loop）工作流，確保 AI 在執行前真正理解問題所在。**

## 專案願景

Codebase Atlas 是一個確保 AI 代理人能精確定位並解決真實問題的工程協議。它以「地圖推理」與「人類確認」取代了 AI 的「盲目編輯」。本協議強迫 AI 必須先提供白話文的理解摘要與「修改計畫」，讓人類開發者能直觀地判斷 AI 是否真的找到了問題點，而非胡編亂造。這種人機協作的設計，讓可能的幻覺在執行前被暴露、檢查與攔截。

透過這套系統，開發者能為 AI 代理人建立一套完整的「導航層」，使其在動手修改代碼前，能先理解模組邊界、依賴關係、潛在風險以及必須遵循的工程規範。

## 為什麼選擇 Codebase Atlas？

### 優於單純的提示詞
單純的提示詞是瞬時且具備隨機性的。當你要求 AI 「找找看哪裡可以修改 X」時，它進行的是一種淺層搜尋，且在下次會話中就會被遺忘。Codebase Atlas 則是**基於事實且持久的**。它為代碼庫建立了一份物理地圖，錨定了 AI 的推理邏輯，確保每一項任務都始於對專案架構的深層理解，而非憑運氣的猜測。

### 優於重型的基礎設施
雖然重型的代碼情報系統（如圖譜解析引擎或外部數據庫）功能強大，但對於 90% 的開發任務來說往往過於沉重。Codebase Atlas 提供了一種**「夠用且好用」的方案**：一套輕量級、基於純文本的協議，在不增加系統複雜度、不需要維護專門伺服器或侵入性索引的前提下，為 AI 代理人提供必要的架構邊界與工作流。

## 核心價值：「一次性初始化，多次重複使用」戰略

目前的 AI 工具通常在每次會話中重新探索代碼庫，造成顯著的資源浪費。Codebase Atlas 提倡角色分離的戰略：

*   **建築師模式（強模型初始化）**：建議調用最強的模型進行深度掃描。初始化或重建 Atlas 時，強烈建議使用 GPT-5.5 以上，或同等級的 frontier model，以確保模組邊界、工作流程文檔與修改前／修改後閘門能被一致地產生並遵循。
*   **工人模式（標準模型執行）**：地圖建立後，日常開發任務可由更經濟的模型處理。這些模型遵循「架構師」預定義的地圖與工作流，以極低的上下文負擔達成高質量的產出。

### 初始化模型建議

Codebase Atlas 初始化是一種設定架構地圖的任務：模型必須同時掌握跨檔案約束、保留工作流程閘門，並寫出一致的模組邊界。初始化或重建 Atlas 時，建議使用 GPT-5.5，或同等規格的 frontier-level model。

較小或較快的模型在強 Atlas 建好後，仍然適合處理日常後續任務，因為它們可以遵循已生成的工作流程文檔。但除非人類會仔細審查模組切分、工作流程閘門、交付政策與已知風險，否則不建議把它們作為主要初始化模型。

## 設計哲學與系統架構

Codebase Atlas 建立在**「結構化持久性 (Structural Persistence)」**的原則之上。與將代碼切割成碎片化區塊的 RAG（檢索增強生成）不同，Codebase Atlas 將儲存庫提煉為具備層級感、語義明確的地圖。

### 1. 四階段生命週期
系統透過結構化的「決策-掃描-提煉-治理」流程運作：
*   **決策階段 (Decision Phase)**：在進行任何分析前，明確解決專案特定的約束（模式、語言、策略），防止 AI 做出偏離開發者意圖的假設。
*   **掃描階段 (Scanning Phase)**：高速的現狀鎖定過程，忽略噪音（依賴、緩存），專注於架構入口、清單文件（Manifests）以及定義邊界的關鍵檔案。
*   **提煉階段 (Distillation Phase)**：將數千個檔案壓縮為 6-20 個穩定模組。這種「資訊密度控制」確保 AI 的上下文視窗被花在理解高層級關係，而非冗餘的檔案細節。
*   **治理階段 (Governance Phase)**：生成具備狀態感的工作流文檔，作為「執行鎖」，強制未來的 AI 代理人遵循預先驗證過的工程路徑。

### 2. 為什麼選擇零依賴的 Markdown？
我們刻意避開了資料庫與重型解析引擎，理由有三：
*   **可審計性**：人類可以輕鬆閱讀並驗證 Atlas。如果 AI 對模組邊界產生幻覺，開發者只需簡單的文字編輯即可修正。
*   **可版本化**：Atlas 存在於 Git 儲存庫內。它隨代碼演進，提供了架構意圖的歷史紀錄。
*   **代理人移交**：一個代理人可以建立 Atlas，另一個完全不同的代理人（甚至在不同的平台上）可以立即使用它，無需任何同步狀態或共享資料庫。

## 運作模型

### 1. 初始化與決策機制
當協議啟動時，AI 代理人不會立即開始掃描。它必須先與使用者確認四個關鍵決策，以確保 Atlas 符合專案需求：

1.  **輸出語言**：繁體中文或英文。
2.  **Atlas 模式**：獨立模式（以現有代碼為唯一事實）或參考輔助模式（借鏡外部儲存庫或規格書）。
3.  **交付規則**：為未來任務紀錄規範（不提交、僅提交、或提交並推送）。
4.  **功能對齊**：（僅限參考輔助模式）是否允許參考資料驅動遷移對齊或功能擴張。功能工作流程本身一律產生。

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
  <project>_introduction_workflow.md
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
  <project>_<reference>_introduction_workflow.md
  <project>_<reference>_bug_workflow.md
  <project>_<reference>_feature_workflow.md
  <project>_<reference>_optimization_workflow.md
  <project>_<reference>_investigation_workflow.md
  <project>_<reference>_refactor_workflow.md
  <project>_<reference>_validation_workflow.md
```

### 自舉範例

這個儲存庫已經把自身跑過一次 Codebase Atlas，並將結果放在 `docs/`。它同時是本專案可用的導航層，也是產出格式的具體範例：

*   從 `docs/codebase_atlas_index.md` 開始。
*   模組筆記位於 `docs/codebase_atlas/`。
*   工作流程文檔與索引同層，例如 `docs/codebase_atlas_bug_workflow.md`。
*   初始化品質檢查清單位於 `references/atlas-quality-checklist.md`。

## 詳細模式選擇

### 獨立模式 (Standalone Mode)
當目標專案是其自身的主要事實來源時使用。AI 專注於現有代碼來推導邊界與流程。

### 參考輔助模式 (Reference-Assisted Mode)
當目標專案需要搭配參考儲存庫、資料夾、API 規格書或設計文件來理解時使用。
*   **借鏡而非盲目對齊**：預設情況下，參考資料用於引導架構、邊界與穩定化模式，而不會自動變成待辦功能清單。
*   **適用場景**：架構遷移、重構以符合某種標準，或實作特定的 API 模式。

## 標準開發工作流範例

地圖建立完成後，**一般的開發任務請勿再次執行 Codebase Atlas。** 重複進行全量掃描是資源的浪費。請直接指引 AI 使用產出的流程文檔。這些工作流的設計初衷是將 AI 從一個「魯莽的編輯者」轉變為一個「深思熟慮的協作者」。

*   **錯誤修復**：`請讀取 docs/<project>_bug_workflow.md，並依照規範修復此問題：[描述]`
*   **功能開發**：`請讀取 docs/<project>_feature_workflow.md，並實作以下功能：[描述]`
*   **優化整理**：`請讀取 docs/<project>_optimization_workflow.md，優化此區塊：[描述]`
*   **調查行為**：`請讀取 docs/<project>_investigation_workflow.md，調查此邏輯：[描述]`
*   **系統重構**：`請讀取 docs/<project>_refactor_workflow.md，重構此結構：[描述]`
*   **變更驗證**：`請讀取 docs/<project>_validation_workflow.md，驗證此改動：[描述]`
*   **專案介紹**：`請讀取 docs/<project>_introduction_workflow.md，用白話介紹這個專案在做什麼`

### 為什麼這些工作流有效：以推理取代幻覺

Codebase Atlas 的強大之處在於其**「基於地圖的推理」**與**「人機協作 (Human-in-the-Loop, HITL)」**的設計：

1.  **精確定位**：AI 不再盲目猜測 Bug 的位置，而是透過 Atlas 索引與模組筆記，識別出確切的「修改入口」與「下游影響」。地圖提供了能在編輯開始前辨識泛泛幻覺的確鑿上下文。
2.  **深思熟慮的分析**：每一套工作流都要求 AI 在動手改代碼前，先總結其理解、識別相關模組並提出具體計畫。這強迫 AI 在寫入任何一行代碼前先進行「思考」與「追蹤」。
3.  **人類作為最終把關者**：本協議的核心是 AI 必須向人類使用者提交其分析結果與計畫以供確認。這種 HITL 模式確保了 AI 的邏輯是正確的，並且在執行開始前已真正理解了問題。
4.  **確保意圖達成**：透過「先總結後執行」的方式，使用者可以立即發現 AI 是否誤解了 Bug 或需求。這能有效防止高昂的重工成本，並確保最終方案既精準又安全。

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
3.  第一次使用時，請要求代理人為目標儲存庫初始化 Codebase Atlas。代理人應先確認輸出語言、Atlas 模式、交付政策，以及參考輔助模式中的功能對齊偏好，再開始掃描。
4.  Atlas 建好後，日常任務請直接使用生成的工作流程文檔。例如：`請讀取 docs/<project>_bug_workflow.md，並依照規範修復此問題：[描述]`。
5.  只有在你明確要求完整重建、刷新、重新生成或重新掃描 Atlas 時，才再次執行 Codebase Atlas。

## 授權協議

MIT
