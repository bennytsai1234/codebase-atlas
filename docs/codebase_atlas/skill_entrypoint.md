# Skill 入口與啟動規則

## 目前狀態

- `SKILL.md` 是 Codebase Atlas 的主要 skill 入口，包含 front matter、使用時機、初始化前簡報、初始決策、workflow entrypoint preference、核心流程與後續 Atlas 使用規則。
- 此模組負責讓代理人在掃描前先解釋輸出、確認決策，並在一般後續開發中改用已生成的 workflow docs。

## 範圍

- `SKILL.md`
- 入口描述：`name: codebase-atlas` 與 `description`
- 主要區段：`Opening Briefing`、`First Decisions`、`Core Workflow`、`Skeleton Prompt`、`Core Philosophy: Plain Before / After`、`Atlas Usage For Later Code Changes`

## 上游依賴

- `references/doc-output-contract.md` 定義初始決策、輸出形狀與最終驗證。
- `references/create-doc-skeleton-prompt.md` 定義建立或擴充 docs 的可重用流程。
- `references/atlas-quality-checklist.md` 是初始化或完整重建後的最終人工可讀品質閘門。

## 下游影響

- README 的使用說明需要與 `SKILL.md` 保持一致，否則使用者會收到不同的初始化期待。
- `assets/templates/*_workflow.md` 的 Before / After gate 與 delivery policy 必須符合 skill 的核心哲學。
- 本目錄的自舉 Atlas 若 workflow 行為改變，也需要同步更新。

## 主要流程

- 使用者要求初始化、建立、重建、刷新或重新掃描 Atlas 時，代理人讀取 `SKILL.md`。
- 代理人先說明 Codebase Atlas 會產生 `docs/`、模組索引、模組筆記、風險、變更入口與 workflow docs。
- 代理人解析或詢問輸出語言、Atlas 模式、交付政策、workflow entrypoints 與 reference-assisted feature parity。
- 掃描後產生 docs，最後用輸出契約與品質檢查清單驗證。

## 常見變更入口

- 想改 skill 何時啟動：從 `SKILL.md` front matter 的 `description` 開始。
- 想改初始化前必問事項：從 `SKILL.md` 的 `First Decisions` 與 `references/doc-output-contract.md` 的 `Initial Decisions` 同步修改。
- 想改工具入口偏好：從 `SKILL.md` 的 `First Decisions`、`Core Workflow` 與 output contract 的 `Workflow Entry Adapters` 同步修改。
- 想改 Before / After gate：從 `SKILL.md` 的 `Core Philosophy` 開始，再同步 workflow templates。

## 變更路徑

- 改初始決策時，先更新 `references/doc-output-contract.md`，再同步 `SKILL.md`、`references/create-doc-skeleton-prompt.md`、README 與相關 workflow 模板。
- 改 workflow entrypoints 時，先更新 output contract，再同步 `SKILL.md`、skeleton prompt、adapter templates 與自舉 docs。
- 改一般後續任務規則時，先更新 `SKILL.md` 的 `Atlas Usage For Later Code Changes`，再檢查七個 workflow 模板是否仍一致。
- 改品質驗證規則時，先更新 `references/atlas-quality-checklist.md`，再同步 `SKILL.md` 與 `references/doc-output-contract.md` 的 final validation 語句。

## 已知風險

- `SKILL.md` 是代理人最先讀到的檔案；若它和契約或模板不一致，後續生成的 Atlas 會跟著漂移。
- 此 skill 刻意不依賴 runtime 或腳本，因此品質保證主要靠文件契約、workflow gate 與 checklist，而不是自動測試。
- front matter 描述如果過寬，可能讓一般開發任務誤觸完整 Atlas 重建。
- workflow entrypoints 若描述不清，使用者可能誤以為 adapter 是第二份 workflow；`SKILL.md` 必須維持 `docs/` 為 source of truth。

## 不要做

- 不要在 `SKILL.md` 寫入特定代理人、模型、CLI、編輯器或本次會話工具作為專案依賴。
- 不要把一般 Bug 修復或功能開發導回完整 Codebase Atlas 掃描。
- 不要繞過初始化前決策，直接掃描並生成 docs。
- 不要讓可選工具入口取代 canonical workflow docs。
