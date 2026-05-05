# Codebase Atlas 模組索引

## 目的與使用方式

- 這份索引是 Codebase Atlas 對自身儲存庫的自舉範例，也可作為本專案後續維護的導航層。
- Codebase Atlas 通常只在初始化或明確重建時執行一次；日常介紹、Bug、功能、優化、調查、重構與驗證工作應直接使用本目錄中的工作流程文檔。
- 再次執行 Codebase Atlas 代表完整重新掃描目前儲存庫，並依照現況重建索引與模組文檔。
- 本次 Atlas 模式：獨立模式。
- 輸出語言：繁體中文。
- 後續工作流程交付政策：commit and push。
- 工作流程入口：`docs/` 是 canonical workflow 來源；本 repo 另提供 Codex skills 與 `.workflow/*.prompt.md` 薄入口，入口只導回對應 workflow 文檔。

## 工作流程文檔

- [介紹工作流程](codebase_atlas_introduction_workflow.md)
- [Bug 工作流程](codebase_atlas_bug_workflow.md)
- [功能工作流程](codebase_atlas_feature_workflow.md)
- [優化工作流程](codebase_atlas_optimization_workflow.md)
- [調查工作流程](codebase_atlas_investigation_workflow.md)
- [重構工作流程](codebase_atlas_refactor_workflow.md)
- [驗證工作流程](codebase_atlas_validation_workflow.md)

## 工作流程入口

- Codex skills：
  [codebase-atlas-introduction](../.agents/skills/codebase-atlas-introduction/SKILL.md)、
  [codebase-atlas-bug](../.agents/skills/codebase-atlas-bug/SKILL.md)、
  [codebase-atlas-feature](../.agents/skills/codebase-atlas-feature/SKILL.md)、
  [codebase-atlas-optimization](../.agents/skills/codebase-atlas-optimization/SKILL.md)、
  [codebase-atlas-investigation](../.agents/skills/codebase-atlas-investigation/SKILL.md)、
  [codebase-atlas-refactor](../.agents/skills/codebase-atlas-refactor/SKILL.md)、
  [codebase-atlas-validation](../.agents/skills/codebase-atlas-validation/SKILL.md)
- IDE prompt files：
  [codebase-atlas-introduction](../.workflow/codebase-atlas-introduction.prompt.md)、
  [codebase-atlas-bug](../.workflow/codebase-atlas-bug.prompt.md)、
  [codebase-atlas-feature](../.workflow/codebase-atlas-feature.prompt.md)、
  [codebase-atlas-optimization](../.workflow/codebase-atlas-optimization.prompt.md)、
  [codebase-atlas-investigation](../.workflow/codebase-atlas-investigation.prompt.md)、
  [codebase-atlas-refactor](../.workflow/codebase-atlas-refactor.prompt.md)、
  [codebase-atlas-validation](../.workflow/codebase-atlas-validation.prompt.md)

## 模組列表

- [Skill 入口與啟動規則](codebase_atlas/skill_entrypoint.md)
- [輸出契約與骨架生成規則](codebase_atlas/output_contract.md)
- [模式指南](codebase_atlas/mode_guides.md)
- [工作流程模板](codebase_atlas/workflow_templates.md)
- [索引與模組模板](codebase_atlas/module_templates.md)
- [公開 README 與授權](codebase_atlas/public_readmes.md)
- [語言資源與品質檢查](codebase_atlas/language_and_quality.md)

## 模組摘要

### Skill 入口與啟動規則

此模組擁有 `SKILL.md`，定義 Codebase Atlas 何時啟動、初始化前要問哪些決策，以及後續任務如何使用已生成的 workflow docs。
當任務涉及 skill 觸發條件、初始化流程、workflow entrypoints、Before / After gate、或 agent-neutral 約束時，應先從這裡開始。

### 輸出契約與骨架生成規則

此模組擁有 `references/doc-output-contract.md` 與 `references/create-doc-skeleton-prompt.md`，是輸出形狀、命名、掃描邊界、最終驗證與 skeleton 生成流程的來源。
當變更 docs 目錄結構、delivery policy 規則、workflow entry adapters、placeholder 規則、或最終品質閘門時，應先從這裡開始。

### 模式指南

此模組擁有 standalone 與 reference-assisted 兩種模式指南，決定掃描順序、模組切分原則、參考資料邊界與 feature parity 的語意。
當任務涉及獨立模式、參考輔助模式、參考資料是否能變成 backlog、或模組切分策略時，應先從這裡開始。

### 工作流程模板

此模組擁有 introduction、bug、feature、optimization、investigation、refactor、validation 七種 workflow 模板。
當使用者想調整日常任務如何從 Atlas 開始、何時等待人類確認、工具入口如何導回 workflow、或每種任務的驗證/交付順序時，應先從這裡開始。

### 索引與模組模板

此模組擁有 index、standalone module、reference-assisted module 與 workflow entrypoint adapter 結構模板，決定生成文檔與工具入口的骨架。
當要新增 module section、改變 module doc 的資訊密度、或同步 index/module/adapter 的 placeholder 時，應先從這裡開始。

### 公開 README 與授權

此模組擁有英文與繁體中文 README，以及 MIT 授權檔。它是使用者理解定位、安裝方式、模型建議、可選工具入口與 example output 的第一入口。
當任務涉及公開敘事、使用教學、工具入口說明、對外主張、或授權說明時，應先從這裡開始。

### 語言資源與品質檢查

此模組擁有繁體中文術語表與初始化品質檢查清單，確保中文輸出一致，並讓 AI 在完成 Atlas 後可用人工可讀的 checklist 做收尾驗證。
當任務涉及術語翻譯、Markdown skill 的品質保證、或初始化完成後的檢查項目時，應先從這裡開始。
