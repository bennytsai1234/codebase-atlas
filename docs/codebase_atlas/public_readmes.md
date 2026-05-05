# 公開 README 與授權

## 目前狀態

- 此模組是使用者理解 Codebase Atlas 的公開入口，包含英文 README、繁體中文 README 與 MIT license。
- README 說明專案願景、模型建議、輸出結構、自舉範例、可選工具入口、工作流程範例與安裝方式。

## 範圍

- `README.md`
- `README.zh-TW.md`
- `LICENSE`

## 上游依賴

- `SKILL.md` 定義實際 skill 行為，README 不應宣稱 skill 不會做的事情。
- `references/doc-output-contract.md` 定義輸出結構與 workflow 種類。
- `docs/` 自舉 Atlas 提供 README 可指向的 example output。

## 下游影響

- 新使用者通常先讀 README；README 的說法會決定他們期待 Codebase Atlas 是 app、runtime、還是 Markdown skill。
- README 的模型建議會影響初始化時使用者選擇強模型或標準模型。
- README 的工具入口說明會影響使用者是否期待 Codex skills、IDE prompt files 或純 docs workflow。
- README 的安裝步驟會影響代理人是否正確讀取 `SKILL.md`。

## 主要流程

- 使用者先讀 README，理解 Codebase Atlas 是 agent-neutral、text-only、zero-dependency 的 Markdown protocol。
- 使用者 clone repo，指引代理人讀 `SKILL.md`。
- 初始化後，使用者改用 generated workflow docs 進行日常任務。
- 如果使用者要求命令或選單呼叫，README 說明可選 adapter 仍應導回 canonical `docs/` workflow。
- 如果使用者要看成品，README 指向 `docs/codebase_atlas_index.md` 作為 self-bootstrap example。

## 常見變更入口

- 想改對外定位：從 README 開頭的 tagline 與 Vision 開始。
- 想改模型建議：從 `Recommended Initialization Model` / `初始化模型建議` 開始。
- 想改使用方式：從 `Installation` / `安裝方式` 與 workflow examples 開始。
- 想改工具入口：從 `Optional Workflow Entrypoints` / `可選 workflow 入口` 開始，並同步 output contract。
- 想改授權：檢查 `LICENSE`，再同步 README 的 License section。

## 變更路徑

- 改 skill 行為時，先改 `SKILL.md` 與 contract，再同步 README 的使用說明。
- 改 output structure 時，同步 README、doc-output-contract、自舉 docs 與 skeleton prompt。
- 改可選工具入口時，同步 README、doc-output-contract、skeleton prompt、adapter templates 與自舉 index。
- 改 hallucination 相關措辭時，保留「執行前可被看見與攔截」的精準語意，避免保證模型永不犯錯。

## 已知風險

- README 若過度像產品網站，可能讓使用者期待可執行 app；目前 README 已明確說明 zero-dependency Markdown。
- Benchmark 或模型比較若寫得太死，外部讀者會期待可重現評測資料；目前改為模型等級建議。
- 工具入口若寫得太像獨立 workflow，會削弱 `docs/` 作為 source of truth 的定位。
- 英文與繁中 README 需同步維護，否則兩邊使用者會收到不同承諾。

## 不要做

- 不要在 README 宣稱此 repo 提供 runtime server、CLI 或 web app。
- 不要承諾完全避免所有幻覺；應描述為讓可能的幻覺在執行前可被暴露、檢查與攔截。
- 不要把 LICENSE 當成可任意省略的周邊檔案。
- 不要把可選工具入口描述成會取代 `docs/` workflow。
