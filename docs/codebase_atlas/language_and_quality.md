# 語言資源與品質檢查

## 目前狀態

- 此模組提供繁體中文術語一致性與 Atlas 初始化完成後的人工可讀品質檢查。
- 它補足 Markdown skill 缺少固定 runtime 測試的特性，讓代理人用文件契約與 checklist 完成收尾驗證。

## 範圍

- `references/zh-tw-glossary.md`
- `references/atlas-quality-checklist.md`

## 上游依賴

- `references/doc-output-contract.md` 要求繁體中文輸出時保留 code identifiers、file paths、commands、API names、package names 與 product names。
- `SKILL.md` 要求初始化或重建完成前執行品質檢查清單。
- `references/create-doc-skeleton-prompt.md` 要求必要時讀取 glossary 並套用品質檢查。

## 下游影響

- 繁體中文 generated docs 的用語會依 `zh-tw-glossary.md` 一致化。
- `atlas-quality-checklist.md` 影響代理人最後報告哪些項目通過、跳過或仍不確定。
- README 的自舉範例與安裝說明可引用 checklist 作為品質保證方式。

## 主要流程

- 若輸出語言是繁體中文，代理人讀取 `references/zh-tw-glossary.md`，翻譯 prose 與 headings，但保留 code identifiers 與 file paths。
- Atlas 文件產生後，代理人依 `references/atlas-quality-checklist.md` 檢查初始決策、輸出形狀、模組品質、workflow 品質、reference-assisted 品質與 final report。
- 如果 checklist 發現缺漏，代理人在報告完成前修正 docs 或明確列出剩餘不確定性。

## 常見變更入口

- 想改繁中術語：從 `references/zh-tw-glossary.md` 開始。
- 想改初始化完成後 AI 必查項目：從 `references/atlas-quality-checklist.md` 開始。
- 想把新檢查納入正式契約：同步 `references/doc-output-contract.md` 的 Final Validation。

## 變更路徑

- 新增術語時，先更新 glossary，再檢查 README.zh-TW、SKILL 說明與自舉 docs 是否需要同步用語。
- 新增品質檢查時，先更新 checklist，再同步 `SKILL.md`、`doc-output-contract.md` 與 `create-doc-skeleton-prompt.md`。
- 若品質檢查新增 placeholder 規則，同步模板與 skeleton prompt，避免代理人不知道如何通過檢查。

## 已知風險

- Checklist 是人工可讀流程，不是 CI；它提升可審計性，但不保證代理人永遠正確。
- Glossary 過度翻譯 code identifiers 會破壞文件可追蹤性；目前規則明確要求保留穩定名稱。
- 若新增英文術語但忘記補 glossary，繁體中文輸出可能出現不一致譯名。

## 不要做

- 不要用 checklist 取代實際閱讀 generated docs。
- 不要把本次執行代理人、模型或工作區工具寫進 Atlas 事實。
- 不要翻譯檔案路徑、命令、API 名稱或 package 名稱。
