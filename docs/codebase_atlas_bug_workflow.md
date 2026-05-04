# Codebase Atlas Bug 工作流程

## 目的

- 當使用者回報 README、skill 規則、契約、模板、workflow 或自舉 docs 有錯誤、矛盾、連結損壞、placeholder 殘留或行為描述不一致時，使用此流程。
- 不要為一般 Bug 修復重新執行 Codebase Atlas；只有 ownership 或 flow 改變時才更新相關 Atlas 文檔。

## 工作流程

1. 開啟 `codebase_atlas_index.md`，選出最可能擁有問題的模組。
1. 閱讀該模組的上游依賴、主要流程、已知風險與不要做邊界。
1. 檢查實際出錯的 README、`SKILL.md`、reference、template 或 generated docs。
1. 判斷問題是局部文字/連結錯誤，還是由上游契約或模板不一致造成。
1. 若症狀跨模組，依照「事實第一次變錯的位置」選主要模組，其它模組當作邊界模組。
1. 將修復集中在主要模組；邊界變更要有明確同步理由。
1. 修復後檢查 Markdown 連結、placeholder、workflow gate 與相關 README/contract 一致性。
1. 若 ownership 或 flow 改變，更新受影響的 Atlas docs。
1. 依交付政策收尾：commit and push。

## 修改前／修改後閘門

使用此流程時，不要先改檔。先用 Atlas 與檔案檢查分析 Bug，再向使用者提出分析報告並等待確認。

報告上半部可以包含工程細節，例如可能的主要模組、根因、受影響檔案、風險與驗證方式。最後必須只留下白話的修改前／修改後摘要：

- **修改前**：說明目前行為或文件狀態，以及哪裡錯誤、矛盾或容易誤導。
- **修改後**：說明修復後會變成什麼狀態。

在使用者明確確認後，才開始編輯檔案。

## 交付政策

commit and push
