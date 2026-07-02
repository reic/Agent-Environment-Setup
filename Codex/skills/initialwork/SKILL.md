---
name: initialwork
description: Codex 開工/收工/新專案初始化流程。使用者說「開工」「收工」「初始化專案」「整理工作區」時載入。
---

# 開工 / 收工 / 新專案初始化（Codex 版）

本技能用來讓 Codex 在專案開始、每日開工、收工整理與新專案建立時保持一致流程。核心原則是：先讀上下文、保護使用者既有變更、避免未確認的破壞性操作。

## 開工

1. 讀取專案根目錄 `AGENTS.md`，確認語言、編碼、工作規範與禁止事項。
2. 讀取 README、近期筆記或使用者指定的 Obsidian / 專案文件。
3. 檢查 Git 狀態與最近 commit，例如 `git status`、`git log -5 --oneline`。
4. 若工作區已有未提交變更，先判斷是否與本次任務相關，不要覆蓋使用者變更。
5. 回報目前狀態、已讀到的關鍵規範與建議下一步。
6. 不自動 pull、commit、push、刪除檔案或大範圍重構。

## 收工

1. 檢查本次修改範圍，確認沒有 API key、token、帳密、個資或不該提交的暫存檔。
2. 更新必要的專案筆記、README 或 TODO；只有規則改變時才更新 `AGENTS.md`。
3. 檢查 Git 狀態與 diff，說明哪些檔案是本次修改、哪些是既有變更。
4. 只 stage 本次相關檔案，不使用 `git add .` 或 `git add -A` 作為預設做法。
5. commit、push、建立 PR 前，除非使用者明確要求，否則先取得確認。
6. 回報完成事項、驗證方式、尚未處理事項與建議接續工作。

## 新專案初始化

先向使用者確認：

- 專案名稱與用途。
- 專案資料夾位置。
- 是否需要 Git / GitHub repo。
- repo 要公開或私有。
- 是否需要部署、測試、CI 或文件站。
- 是否會使用 Obsidian、MCP、Connector 或專屬技能。

建議建立：

- `AGENTS.md`：Codex 專案指令與工作規範。
- `README.md`：專案說明與啟動方式。
- `.gitignore`：排除 `.env`、暫存檔、build output、依賴資料夾。
- `.codex/skills/`：專案專屬技能，選用。
- `.mcp.json`：專案 MCP 設定，選用，避免寫入私密 token。
- 基礎測試或檢查指令。

若專案已存在，先盤點後補缺口，不覆蓋既有內容。

## Windows / 中文環境注意事項

- 執行會讀寫中文內容的 PowerShell 命令前，優先設定 UTF-8 輸入輸出。
- Markdown、YAML、技能檔、Obsidian 筆記一律保留 UTF-8。
- Obsidian vault 內操作時，保留 frontmatter、wikilink、canvas、bases 與既有 Markdown 風格。
