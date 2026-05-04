# 輸出契約與骨架生成規則

## 目前狀態

- 此模組定義 Codebase Atlas 生成文檔時必須遵循的輸出契約與 skeleton 建立流程。
- 它把「Markdown skill 很難用 CI 測」轉化為可審計的結構規則、placeholder 規則、連結規則與最終驗證清單。

## 範圍

- `references/doc-output-contract.md`
- `references/create-doc-skeleton-prompt.md`
- 與最終驗證相關的 `references/atlas-quality-checklist.md`

## 上游依賴

- `SKILL.md` 會要求代理人在掃描前讀取輸出契約。
- `assets/templates/` 提供契約所引用的起始模板。
- `references/standalone-mode.md` 與 `references/reference-assisted-mode.md` 補充模式特定規則。

## 下游影響

- `docs/` 產出的檔名、目錄結構、連結、workflow 清單、module section 與 delivery policy 都受此模組約束。
- README 的輸出結構說明應與契約一致。
- 模板中的 placeholder 必須能被 skeleton 流程完整替換。

## 主要流程

- `doc-output-contract.md` 定義初始決策、命名、source of truth、語言、交付政策、掃描邊界、standalone/reference-assisted output 與 final validation。
- `create-doc-skeleton-prompt.md` 將契約轉成實作流程，要求先掃描 target repo，再選模式指南、填模板、檢查 placeholder 與執行品質檢查。
- `atlas-quality-checklist.md` 在生成後作為人工可讀的最後檢查。

## 常見變更入口

- 想改輸出樹：從 `references/doc-output-contract.md` 的 `Standalone Output` 或 `Reference-Assisted Output` 開始。
- 想改命名或連結規則：從 `Naming` 與 `Final Validation` 開始。
- 想改 skeleton 生成步驟：從 `references/create-doc-skeleton-prompt.md` 的 `Follow this process` 開始。

## 變更路徑

- 改 output shape 時，先更新 `doc-output-contract.md`，再同步 `create-doc-skeleton-prompt.md`、README 的 output structure，以及 `assets/templates/index.md` 是否需要新 placeholder。
- 改 final validation 時，先更新 `atlas-quality-checklist.md`，再同步 `doc-output-contract.md` 與 `SKILL.md`。
- 改 scan boundaries 時，同步 standalone 與 reference-assisted mode guides，避免模式指南與契約分歧。

## 已知風險

- 契約過度抽象會讓代理人生成薄弱的 module summaries；契約目前要求 routing-oriented summaries 與 change routes 來抵抗這個問題。
- Placeholder 若新增但沒有在 skeleton prompt 中說明替換方式，會造成生成 docs 殘留模板標記。
- Delivery policy 同時出現在 index 與 workflow docs，變更時容易漏同步。

## 不要做

- 不要把執行環境、當前模型或本次工具鏈寫成 module dependency。
- 不要把未完成標記當成未檢查內容的替代品；這類標記只能表示 repo 或 reference 中真實存在的不確定性。
- 不要在契約裡加入需要 runtime server、資料庫或固定 CI 的要求，除非 skill 的定位也同步改變。
