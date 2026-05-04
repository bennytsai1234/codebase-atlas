# Codebase Atlas 驗證工作流程

## 目的

- 當使用者要求檢查、驗證、審查、重現或評估風險，而不是立即改檔時，使用此流程。
- 除非使用者明確要求修復或實作，不要編輯檔案。
- 不要為一般驗證重新執行 Codebase Atlas；若發現 Atlas docs 過期，將它列為 findings。

## 工作流程

1. 保留要驗證的問題、預期行為或風險。
1. 開啟 `codebase_atlas_index.md`，選出受影響模組或邊界。
1. 閱讀相關 module docs 的範圍、依賴、下游影響、主要流程與已知風險。
1. 選擇最小有用驗證方法：Markdown link check、placeholder 掃描、front matter 檢查、workflow gate 檢查、靜態閱讀或 git 狀態檢查。
1. 只執行符合需求信心等級的檢查。
1. 分開記錄 pass、fail、blocked、skipped 與 inconclusive。
1. 若需要修復，建議下一個 workflow，不要靜默改檔。
1. 若沒有修改檔案，總結驗證狀態並說明無需 commit；若使用者明確要求修改，依交付政策收尾：commit and push。

## 驗證摘要

完成評估前提供白話摘要：

- **範圍**：這次驗證哪個變更、修復或風險？
- **地圖**：哪些模組受影響？
- **評估**：
  - **證據**：測試、檢查、diff 或文件審查顯示了什麼？
  - **信心**：對結果有多確定？
- **結論**：Pass/Fail 或風險等級 Low/Medium/High。

若驗證建議修改檔案，提供白話修改前／修改後摘要，並在使用者明確確認後才開始後續編輯。

## 交付政策

commit and push
