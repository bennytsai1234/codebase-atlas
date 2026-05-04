# 工作流程模板

## 目前狀態

- 此模組包含七種日常任務 workflow 模板，讓後續代理人從 Atlas 出發，而不是重新掃描整個專案。
- 會修改檔案的 workflow 透過 Before / After gate 要求先分析、再等待人類確認，降低錯誤理解直接落地的風險。

## 範圍

- `assets/templates/introduction_workflow.md`
- `assets/templates/bug_workflow.md`
- `assets/templates/feature_workflow.md`
- `assets/templates/optimization_workflow.md`
- `assets/templates/investigation_workflow.md`
- `assets/templates/refactor_workflow.md`
- `assets/templates/validation_workflow.md`

## 上游依賴

- `references/doc-output-contract.md` 定義 workflow 文件必須包含的行為。
- `SKILL.md` 的 `Core Philosophy: Plain Before / After` 定義所有 code-changing workflow 的信任規則。
- `assets/templates/index.md` 提供 workflow links 的索引位置。

## 下游影響

- 所有 generated workflow docs 都會從這些模板衍生。
- README 的 standard development workflows 範例應與模板語意一致。
- 自舉 `docs/codebase_atlas_*_workflow.md` 需要在模板行為改變時同步更新。

## 主要流程

- 每個 workflow 都先打開 index，選擇 owning module 或 boundary module。
- Bug、feature、optimization、refactor 要在編輯前提出 Before / After summary 並等待確認。
- Investigation 與 validation 主要用於理解或驗證；若後續需要改檔，也必須提出 Before / After summary。
- Workflow 結尾依照 delivery policy 收束，並在 ownership、API、flow 或 boundary 改變時更新 Atlas docs。

## 常見變更入口

- 想改 bug 修復路徑：從 `assets/templates/bug_workflow.md` 開始。
- 想改新增功能的 scope 定義：從 `assets/templates/feature_workflow.md` 開始。
- 想改驗證報告格式：從 `assets/templates/validation_workflow.md` 開始。
- 想改所有 workflow 的共同規則：先改 `references/doc-output-contract.md` 與 `SKILL.md`，再逐一同步模板。

## 變更路徑

- 改 Before / After wording 時，同步 `SKILL.md`、`references/zh-tw-glossary.md`、四個 code-changing workflow 模板與自舉 workflow docs。
- 改 delivery policy 結尾時，同步七個 workflow 模板與 `references/doc-output-contract.md` 的 Delivery Policy。
- 新增 workflow 類型時，需同步 `assets/templates/`、`references/doc-output-contract.md`、`references/create-doc-skeleton-prompt.md`、README 與 index template。

## 已知風險

- Workflow 模板太薄會讓後續代理人只做形式上的 Atlas 閱讀；目前每個模板都要求先選 module 並檢查相關 docs。
- Before / After gate 如果被改得太工程化，使用者會不容易判斷代理人是否真的理解問題。
- Optimization template 有 `REFERENCE_STEP` placeholder，standalone output 必須替換成空字串。

## 不要做

- 不要讓 workflow 在分析前直接要求編輯 source files、tests、config 或 docs。
- 不要在 workflow 裡要求重新執行 Codebase Atlas，除非任務明確是完整 rebuild。
- 不要把 validation workflow 變成靜默修復流程。
