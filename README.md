# Agent環境配置 (AI Coding Agent Environment Configuration Packs)

本專案是一個整合各類 AI Coding Agent（如 Codex、Claude Code、Google Antigravity 等）的 **Windows 環境優化與技能安裝懶人包**。

專案目標是透過純文件與配置檔指引，協助開發者快速建置適合 AI Agent 運行的系統環境，並依需求對接 Obsidian 知識管理系統與各類 MCP（Model Context Protocol）伺服器。

---

## 📂 專案目錄結構與支援的 AI Agent

請點選下方連結，閱讀對應 AI Agent 的專用安裝手冊：

### 1. 🤖 [Google Antigravity](./Antigravity/)

- **特點**：專為 Google Gemini 系列設計的 Coding Agent，具備 `.agents/AGENTS.md` 安全規則、`ANTIGRAVITY.md` 寫作規範載入與 `.agents/skills/` 擴充技能系統。
- **包含內容**：專屬配置（`.agents/AGENTS.md` 與 `ANTIGRAVITY.md` 規範檔）、Node/Git/Python/Obsidian Winget 安裝指引、NotebookLM MCP 註冊指南、Steph Ango 官方 `obsidian-skills` 技能包配置，以及專屬的**開工/收工/專案初始化工作流 (workflow) 技能**。

### 2. 🪐 [Claude Code](./Claude-Code/)

- **特點**：由 Anthropic 開發的 CLI 終端機 AI 程式助理，具備 `CLAUDE.md` 專案記憶、`.claude/skills/` 技能系統與 `claude mcp` 伺服器管理機制。
- **包含內容**：`.claude/` 目錄專屬配置（`CLAUDE.md`、`settings.json`）、NotebookLM MCP 註冊指南、Steph Ango 官方 `obsidian-skills` 技能包配置，以及專屬的**開工/收工/專案初始化工作流 (workflow)** 與**生圖指引**技能。

### 3. 💻 [Codex](./Codex/)

- **特點**：OpenAI 的程式協作 Agent，可透過 Codex Desktop、Codex CLI 或 API 形式協助讀寫程式碼、整理文件、操作工作區與串接工具。
- **包含內容**：Windows 基礎環境檢查、Codex 使用入口說明、`AGENTS.md` 專案指令範本、`.codex/skills` 技能資料夾建議、預封裝的 `imagedraw` / `initialwork` 技能、MCP / Connector 設定方式、API key 安全管理與入門驗證回報格式。

---

## 🛠️ 基本環境要求

不論您使用哪一個 AI Agent，建議先確認 Windows 系統中已安裝以下基礎工具：

- **Git**：版本控制必備。
- **Node.js**：前端專案與各類 MCP 工具常用。
- **Python 3**：文件處理、資料處理與自動化常用。
- **Obsidian**：專案筆記與個人知識沉澱，選用。

如果尚未安裝，可用系統管理員身分開啟 PowerShell，執行以下 Winget 指令：

```powershell
# 安裝 Git
winget install Git.Git

# 安裝 Node.js
winget install OpenJS.NodeJS

# 安裝 Python 3
winget install Python.Python.3

# 安裝 Obsidian
winget install Obsidian.Obsidian
```

安裝完成後，請重新開啟 PowerShell、VS Code 或對應的 Agent 桌面程式，讓 PATH 環境變數生效。

---

## 🔐 設定原則

- 優先使用各 Agent 官方支援的記憶或指令檔，例如 Codex 的 `AGENTS.md`、Claude Code 的 `CLAUDE.md`。
- API key、token、帳密與私密連線字串不要提交到 Git。
- 修改 Obsidian vault 時，請保留 frontmatter、wikilink、canvas、bases 與既有 Markdown 格式。
- 在 Windows 環境處理中文內容時，請優先使用 UTF-8 讀寫。
- 大範圍重構、刪除檔案、commit、push 或安裝套件前，建議先要求 Agent 說明影響範圍並取得確認。

---

## 📅 更新記錄 (Change Log)

| 日期 | 版本 | 更新內容 |
|---|---|---|
| **2026-07-02** | **v1.3** | 補齊 **Codex** 預封裝技能 `imagedraw` 與 `initialwork`，讓 Codex 懶人包與其它 Agent 配置一致。 |
| **2026-07-02** | **v1.2** | 正式釋出 **Codex** 入門環境配置手冊，補上 `AGENTS.md` 範本、`.codex/skills` 建議、MCP / Connector 設定與 API key 安全管理。 |
| **2026-07-02** | **v1.1** | 正式釋出 **Claude Code** 的手動環境配置與技能包（`CLAUDE.md`、NotebookLM MCP、`obsidian-skills`、`imagedraw`、`initialwork`）。 |
| **2026-07-02** | **v1.0** | 專案初始化。正式釋出 **Google Antigravity** 的手動環境配置與技能包。新增 `Claude-Code` 與 `Codex` 設定專區預留位置。 |

---
授權條款：MIT License



