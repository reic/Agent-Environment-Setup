---
name: initialwork
description: Claude Code 開工/收工/新專案初始化流程。說「開工」「收工」「初始化專案」時載入。
---

# 開工 / 收工 / 新專案初始化

## 開工
1. 讀取專案根目錄 `CLAUDE.md`（Claude Code 會自動載入，若無則提醒使用者是否要建立）
2. 讀取專案筆記重點（Obsidian 或其他知識庫）
3. `git status` + 最近 commit（`git log -5 --oneline`）
4. 回報狀態與建議下一步
5. 不自動 pull/commit/push

## 收工
1. 檢查敏感資料（API key、token、學生真名等），確認未被寫入即將提交的檔案
2. 更新專案筆記（完成事項、下一步、踩坑）
3. 只在規則改變時更新 `CLAUDE.md`
4. 檢查 `git status` + `git diff`
5. 只 stage 本次相關檔案（不用 `git add -A` / `git add .`）
6. 確認後 commit + push（除非使用者已於 `CLAUDE.md` 中明確授權自動化，否則需先徵求確認）
7. 回報同步結果

## 新專案初始化
先問：名稱、用途、資料夾、是否 GitHub repo、公開/私有、是否部署。
建立：`CLAUDE.md`、README.md、`.gitignore`、`.claude/settings.json`（可選）、Git repo、GitHub repo、專案筆記。
若已存在 → 盤點後只補缺口，不覆蓋。
