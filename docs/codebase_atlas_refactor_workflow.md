# Codebase Atlas 重構工作流程

## 目的

- 當使用者要求調整文件結構、模組 ownership、模板 section、命名、重複內容或規則邊界，同時保持既有意圖不變時，使用此流程。
- 不要用重構包裝無關功能或行為變更。
- 不要為一般重構重新執行 Codebase Atlas；但 ownership、API、flow 或 boundary 改變時必須更新受影響的 Atlas docs。

## 工作流程

1. 保留使用者原始需求，並辨識必須保持不變的行為或公開承諾。
1. 開啟 `codebase_atlas_index.md`，選出主要模組與必要邊界模組。
1. 閱讀相關 module docs 的範圍、依賴、下游影響、常見變更入口與已知風險。
1. 定義最小重構邊界與明確 non-goals。
1. 若重構跨模組，依 ownership 被澄清或移動的位置選主要模組，並分別說明每個邊界調整。
1. 找出可保護不變行為的檢查方式：Markdown 連結、placeholder 掃描、workflow gate 檢查、README/contract 一致性檢查。
1. 分步重構，保持對外語意穩定，除非介面變更就是明確目標。
1. 驗證下游 README、templates、references 與 self-bootstrap docs 仍一致。
1. 更新 Atlas docs 中改變的 ownership、API、flow 或 boundary。
1. 依交付政策收尾：commit and push。

## 修改前／修改後閘門

使用此流程時，不要先改檔。先用 Atlas 與檔案檢查分析重構，再向使用者提出分析報告並等待確認。

報告上半部可以包含工程細節，例如 ownership、邊界、可能檔案、風險與檢查方式。最後必須只留下白話的修改前／修改後摘要：

- **修改前**：說明目前結構或 ownership，以及它為什麼難以維護或容易混淆。
- **修改後**：說明重構後會形成什麼結構或 ownership，並如何保留既有行為。

在使用者明確確認後，才開始編輯檔案。

## 交付政策

commit and push
