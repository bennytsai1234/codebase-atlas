# Codebase Atlas 介紹工作流程

## 目的

- 當使用者想快速理解 Codebase Atlas 這個專案在做什麼時，使用此流程。
- 輸出應使用白話說明，不要變成完整架構審計或逐檔案清單，除非使用者明確要求。
- 此流程不應修改檔案。
- 不要為一般介紹重新執行 Codebase Atlas；使用既有 Atlas 文檔即可。

## 工作流程

1. 開啟 `codebase_atlas_index.md`，閱讀專案目的、模組摘要與工作流程列表。
1. 只閱讀足以回答問題的模組文檔。
1. 若 Atlas 內容不足以解釋使用者可理解的行為，再檢查 README、`SKILL.md` 或 references。
1. 用白話說明：
   - 它是什麼
   - 它服務誰或什麼工作
   - 它主要完成哪些任務
   - 哪些邊界對理解有幫助
1. 避免列出所有模組、依賴、檔案或技術細節。
1. 若使用者要求更深技術脈絡，建議改用調查工作流程。
1. 若沒有修改檔案，說明無需 commit；若因使用者明確要求而修改文檔，依交付政策收尾：commit and push。

## 白話介紹

先用幾段清楚文字說明 Codebase Atlas 是一套純 Markdown 的 AI 導航協議，不是 app、server 或套件 runtime。接著說明它如何透過 module index、module docs、workflow docs、Before / After gate 與品質檢查清單，讓後續代理人先理解再動手。

## 交付政策

commit and push
