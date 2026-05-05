# 模式指南

## 目前狀態

- 此模組定義 Codebase Atlas 的兩種掃描模式：獨立模式與參考輔助模式。
- 它決定代理人如何從 target repo 與 reference material 推導模組邊界、使用參考資料，以及避免把參考資料誤變成 feature backlog。

## 範圍

- `references/standalone-mode.md`
- `references/reference-assisted-mode.md`

## 上游依賴

- `references/doc-output-contract.md` 定義模式選擇、feature parity 與 reference-assisted output shape。
- `SKILL.md` 的 `Mode Decision` 要求代理人根據使用者輸入選擇其中一種模式。

## 下游影響

- `docs/` 的 module docs section 會因 standalone 或 reference-assisted 模式不同而改變。
- Feature workflow 在 reference-assisted mode 中是否能把 reference 當成 parity source，受此模組語意影響。
- 若產生 workflow entrypoints，mode guides 要求它們只作為導回 canonical docs 的薄 adapter。
- README 的 detailed mode selection 必須維持與此模組一致。

## 主要流程

- Standalone mode 先讀現有 docs、manifest、entrypoint、source roots、tests 與 build/config files，再推導 6-20 個穩定模組。
- Reference-assisted mode 先理解 target repo，再檢查 reference counterpart，並明確保留 target project 作為主體。
- Feature parity 預設停用；只有使用者明確要求 parity、compatibility、migration equivalence 或 reference-driven expansion 時才啟用。
- Workflow entrypoints 不改變 standalone/reference-assisted 的掃描規則，只改變使用者如何呼叫 workflow。

## 常見變更入口

- 想調整一般 repo 的掃描順序：從 `references/standalone-mode.md` 的 `Exploration` 開始。
- 想調整參考資料使用邊界：從 `references/reference-assisted-mode.md` 的 `Reference Boundary` 開始。
- 想調整 module split 原則：先看 standalone 的 `Module Split`，再確認 reference-assisted 是否需要同樣限制。
- 想調整 entrypoint 與 mode 的關係：從兩份 mode guide 的 `Workflows` 段落開始。

## 變更路徑

- 改 reference semantics 時，先更新 `reference-assisted-mode.md`，再同步 `doc-output-contract.md` 的 feature parity 說明、feature workflow template 與 README。
- 改 module count 或切分原則時，先更新 standalone mode，再更新品質檢查清單中的 module quality 項目。
- 改 workflow 產出種類時，同步兩個 mode guides、doc-output-contract 與 `assets/templates/`。
- 改工具入口行為時，同步 mode guides、doc-output-contract、skeleton prompt 與 adapter templates。

## 已知風險

- Reference-assisted mode 最容易產生 scope creep；`Do Not Do` 與 feature parity disabled 預設是主要防線。
- 小型 repo 可能不足以自然拆出 6 個以上模組；standalone guide 已要求不要為了數字硬拆。
- 模式指南若和模板不一致，代理人可能生成 section 不完整的 module docs。
- 工具入口若被誤解為 mode-specific 規則，可能造成 adapter 影響掃描策略；目前規則要求 adapter 只影響呼叫入口。

## 不要做

- 不要讓 reference 取代 target repo 的真實狀態。
- 不要在 feature parity disabled 時把 reference 的缺失差異列為 bug。
- 不要把資料夾結構機械地等同於工程模組邊界。
- 不要讓 workflow entrypoint 改變 mode selection 或 module split。
