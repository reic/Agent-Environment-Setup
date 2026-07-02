# Agent環境配置 (AI Coding Agent Environment Configuration Packs)

本專案是一個整合各類 AI Coding Agent (如 Codex, Claude Code, Google Antigravity 等) 的** Windows 環境優化與技能安裝懶人包**。

專案目標是透過純文檔與配置檔的指引，協助開發者快速且無痛地建置最適合 AI Agent 運行的系統環境，並對接 Obsidian 知識管理系統與各類 MCP (Model Context Protocol) 伺服器。

---

## 📂 專案目錄結構與支援的 AI Agent

請點選下方連結，閱讀對應 AI Agent 的專用安裝手冊：

### 1. 🤖 [Google Antigravity](./Antigravity/)
*   **特點**：專為 Google Gemini 系列設計的強大 Coding Agent。
*   **包含內容**：Node/Git/Python/Obsidian Winget 安裝指引、NotebookLM MCP 註冊指南、Steph Ango 官方 `obsidian-skills` 技能包配置，以及專屬的**開工/收工/專案初始化工作流 (workflow) 技能**。

### 2. 🪐 [Claude Code](./Claude-Code/)
*   **特點**：由 Anthropic 開發的 CLI 終端機 AI 程式助理，具備 `CLAUDE.md` 專案記憶、`.claude/skills/` 技能系統與 `claude mcp` 伺服器管理機制。
*   **包含內容**：`.claude/` 目錄專屬配置（`CLAUDE.md`、`settings.json`）、NotebookLM MCP 註冊指南、Steph Ango 官方 `obsidian-skills` 技能包配置，以及專屬的**開工/收工/專案初始化工作流 (workflow)** 與**生圖指引**技能。

### 3. 💻 [Codex](./Codex/) (規劃中)
*   **特點**：基於 OpenAI 模型的強大程式撰寫工具。
*   **規劃內容**：API 金鑰管理規範、開發環境檢查、以及熱門 IDE（如 VS Code）插件與快速鍵對接。

---

## 🛠️ 基本環境要求
不論您使用哪一個 AI Agent，我們建議您先確保 Windows 系統中已安裝以下基礎工具：
- **Git**：版本控制必備。
- **Node.js**：執行各類 MCP 工具底層。
- **Python 3**：自動化編譯與指令處理。
- **Obsidian**：專案筆記與個人知識沉澱。

如果您尚未安裝，請以管理員身分開啟 PowerShell 並執行 Winget 進行一鍵安裝：
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

---

## 📅 更新記錄 (Change Log)
| 日期 | 版本 | 更新內容 |
|---|---|---|
| **2026-07-02** | **v1.1** | 🪐 正式釋出 **Claude Code** 的手動環境配置與技能包（`CLAUDE.md`、NotebookLM MCP、`obsidian-skills`、`imagedraw`、`initialwork`）。 |
| **2026-07-02** | **v1.0** | 🚀 專案初始化。正式釋出 **Google Antigravity** 的手動環境配置與技能包。新增 `Claude-Code` 與 `Codex` 設定專區預留位置。 |

---
授權條款：MIT License
