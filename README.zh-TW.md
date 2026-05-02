# Codebase Atlas

Codebase Atlas 是一個不綁特定 Agent 的 skill，用來把 repository 轉成可導航的工程地圖。它會建立專案文檔、模組摘要、依賴與影響範圍說明，以及後續 bug、feature、optimization 的工作流。

## 安裝方式

把 skill clone 到任何 Agent 可以讀取的位置：

```bash
git clone https://github.com/bennytsai1234/codebase-atlas.git
```

接著請你的 coding agent 讀取 clone 下來的 `SKILL.md`：

```text
請讀取 /path/to/codebase-atlas/SKILL.md，並使用 Codebase Atlas skill 處理這個 repo。
```

## 使用方式

請 Agent 先讀這個 skill，並在掃描前先詢問設定：

```text
請使用 Codebase Atlas skill 處理這個 repo。
開始掃描前，請先問我：
1. 產出要使用英文還是繁體中文？
2. 這次要使用「獨立專案模式（standalone，不使用參考資料）」，
   還是「參考資料輔助模式（reference-assisted，使用參考資料）」？
```

如果選擇「參考資料輔助模式」，請在 Agent 開始完整掃描前提供參考資料的路徑、URL 或檔案。

只有要重建時才再次執行：

```text
請使用 Codebase Atlas skill 重新掃描整個 repo，並依照目前程式碼重建 atlas。
```

## 後續開發

atlas 建立完成後，普通開發不要再次執行 Codebase Atlas。請改用產出的 workflow docs：

```text
請讀取 docs/<project>_bug_workflow.md，並依照它修復這個 bug：...
請讀取 docs/<project>_feature_workflow.md，並依照它實作這個功能：...
請讀取 docs/<project>_optimization_workflow.md，並依照它優化這個區塊：...
```

## 內容結構

- `SKILL.md`：主要 Agent 指令。
- `references/`：模式說明與輸出規格。
- `assets/templates/`：產生 atlas docs 用的 Markdown 模板。

這個 package 不綁特定 Agent runtime。任何 coding agent 都可以透過讀取 `SKILL.md`、相關 reference files 和 templates 來使用。

## 授權

MIT
