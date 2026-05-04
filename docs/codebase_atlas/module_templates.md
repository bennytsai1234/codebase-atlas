# 索引與模組模板

## 目前狀態

- 此模組提供生成 index 與 module docs 的起始模板。
- 模板保留 placeholder 與待填項目，是給代理人在初始化時替換與填寫的骨架，不是最終產出。

## 範圍

- `assets/templates/index.md`
- `assets/templates/standalone_module.md`
- `assets/templates/reference_module.md`

## 上游依賴

- `references/doc-output-contract.md` 定義 index document、standalone module document 與 reference-assisted module document 必填內容。
- `references/create-doc-skeleton-prompt.md` 定義如何替換 placeholder 與填入 inspected facts。
- `references/standalone-mode.md` 與 `references/reference-assisted-mode.md` 決定要使用哪個 module template。

## 下游影響

- Generated index 是否包含 workflow links、module links、routing-oriented summaries 與 delivery policy，取決於 `index.md`。
- Generated module docs 是否包含 change entry points、change routes、known risks 與 do-not-do boundaries，取決於 module templates 與 contract。

## 主要流程

- 初始化時，代理人複製或依照模板建立 index、module docs 與 workflow docs。
- Placeholder 名稱包含 `ATLAS_TITLE`、`DELIVERY_POLICY`、`WORKFLOW_LINKS`、`MODULE_LINKS`、`MODULE_SUMMARIES` 等，必須被具體內容替換。
- Module template 中的待填項目必須被 repo 事實取代；只有真實不確定性才能保留未完成標記。

## 常見變更入口

- 想改 index 必填區塊：從 `assets/templates/index.md` 與 `references/doc-output-contract.md` 的 `Index Document` 開始。
- 想改 standalone module section：從 `assets/templates/standalone_module.md` 開始。
- 想改 reference-assisted module section：從 `assets/templates/reference_module.md` 開始。

## 變更路徑

- 新增 module section 時，先更新 contract，再更新相對應 module template，最後更新 skeleton prompt 與 checklist。
- 新增 index placeholder 時，必須同步 skeleton prompt 的替換規則與 final validation，避免 generated docs 殘留 placeholder。
- 改待填項目規則時，同步 contract、template 與 quality checklist。

## 已知風險

- 模板中保留待填項目是正常的，但 generated docs 不應把未完成標記當作省略檢查的理由。
- Index summaries 容易退化成檔案描述；契約要求 2-4 行 routing-oriented summary 來避免這點。
- Reference module template 若缺少 target-specific entry points，後續代理人會被 reference 帶偏。

## 不要做

- 不要把模板 placeholder 寫成最終輸出。
- 不要讓 module docs 只列檔案而不說明何時從此模組開始。
- 不要把 standalone 與 reference-assisted 的 section 混用，除非 contract 已同步更新。
