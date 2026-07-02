# Codex 環境配置懶人包 (Codex Environment Setup Lazy Pack)

本目錄提供 OpenAI **Codex / Codex CLI / Codex Desktop** 入門者可直接參考的 Windows 環境配置手冊。目標是讓第一次使用 Codex 的使用者，能先完成必要工具、專案記憶、權限習慣、Obsidian 與 MCP 對接的基本設定，再開始讓 Agent 協助寫程式、整理文件或維護知識庫。

本懶人包採用**純文件指引與配置範本**，不要求執行未知腳本。請依照順序完成檢查，並把實際環境狀態回報給 Codex，讓它能用正確方式協助您。

---

## 📂 建議目錄結構

```text
Codex/
├── README.md                 # Codex 入門環境設定手冊
└── skills/                   # 可複製到專案 .codex/skills/ 的 Codex 技能
    ├── imagedraw/             # 生圖/繪圖指引技能
    └── initialwork/           # 開工/收工/新專案初始化工作流技能

<您的專案>/
├── AGENTS.md                 # Codex 專案指令與工作規範
├── .codex/
│   └── skills/               # 專案專屬技能，選用
└── .mcp.json                 # 專案 MCP 設定，選用
```

---

## 📋 安裝與設定流程

### 第一步：核心系統環境檢查

請開啟 PowerShell，依序確認下列工具是否可用。若顯示找不到指令，請使用下方 Winget 指令安裝。

#### 1. Git（版本控制必備）

- **檢查指令**：`git --version`
- **安裝指令**：`winget install Git.Git`

#### 2. Node.js（前端專案、MCP 工具常用）

- **檢查指令**：`node -v`
- **安裝指令**：`winget install OpenJS.NodeJS`

#### 3. Python 3（文件、資料處理與自動化常用）

- **檢查指令**：`python --version`
- **安裝指令**：`winget install Python.Python.3`

#### 4. Obsidian（知識庫與 Markdown 筆記，選用）

- **檢查方式**：確認桌面程式可開啟，或在終端機輸入 `obsidian`。
- **安裝指令**：`winget install Obsidian.Obsidian`

> 安裝完成後，請重新開啟 PowerShell、VS Code 或 Codex Desktop，讓 PATH 環境變數生效。

---

### 第二步：安裝或啟用 Codex

Codex 的使用方式可能依您的 OpenAI 帳號與產品介面而不同，常見入口如下：

- **Codex Desktop**：適合想在桌面 App 中管理工作區、檔案、終端機與瀏覽器的使用者。
- **Codex CLI**：適合熟悉終端機、希望在專案資料夾內直接啟動 Agent 的使用者。
- **OpenAI API**：適合開發者把 Codex 能力整合進自己的工具或服務。

建議入門者先使用 Codex Desktop 或官方 CLI，並完成登入。若您使用 CLI，請在安裝後執行版本檢查與登入流程；若您使用 Desktop，請先確認目前工作區資料夾是否正確。

---

### 第三步：建立 `AGENTS.md` 專案指令

Codex 會優先參考專案中的 `AGENTS.md`。這個檔案等同於「專案工作規範」，建議放在專案根目錄。

可使用以下範本：

```markdown
# Project Instructions

## Language and Encoding
- 使用繁體中文回覆。
- 在 Windows PowerShell 執行本專案命令時，優先使用 UTF-8 輸入與輸出。
- 修改 Markdown、YAML、技能檔或中文內容時，保留 UTF-8 編碼。

## Workflow
- 修改檔案前先閱讀相關上下文。
- 不要覆蓋使用者未要求變更的內容。
- commit、push、刪除檔案或大範圍重構前，先徵求使用者確認。
- 完成後說明修改內容與已驗證項目。

## Project Notes
- 專案目的：
- 主要工作資料夾：
- 常用啟動指令：
- 測試指令：
```

若您的專案是 Obsidian vault，可再加入：

```markdown
## Obsidian Operations
- 使用 Obsidian 相關工具或 connector 操作筆記。
- 不確定 frontmatter、wikilink、canvas 或 bases 格式時，先讀取現有格式再修改。
```

---

### 第四步：安裝本懶人包預封裝的 Codex 技能（選用）

本懶人包已提供兩個 Codex 入門技能：`imagedraw`（生圖/繪圖指引）與 `initialwork`（開工/收工/新專案初始化）。請將本目錄的 `skills/` 複製到您的專案：

```text
<您的專案>/.codex/skills/<技能名稱>/SKILL.md
```

目前內建技能：

- `imagedraw`：判斷要用 Codex 內建圖片能力、SVG / Mermaid 圖表，或外部 API / MCP。
- `initialwork`：建立 Codex 開工、收工、新專案初始化流程，對應 `AGENTS.md` 與 Git 安全習慣。

您也可以再加入專案專屬技能，適合用於：

- 固定的文章審稿流程。
- 特定產業術語檢查。
- 圖片、簡報、PDF、試算表等文件製作流程。
- 專案開工、收工、任務交接與變更摘要。

入門階段建議至少安裝 `initialwork`，再依需求安裝 `imagedraw`。若暫時不使用技能，先把 `AGENTS.md` 寫清楚也能讓 Codex 穩定工作。

---

### 第五步：設定 MCP / Connector（選用）

若您希望 Codex 連接外部資料來源，例如 Obsidian、Google Calendar、GitHub、NotebookLM 或其他內部工具，可使用 Codex Desktop 的 connector / plugin 設定，或在專案中建立 `.mcp.json`。

專案層級 `.mcp.json` 範例：

```json
{
  "mcpServers": {
    "example-tool": {
      "command": "example-mcp-server",
      "args": []
    }
  }
}
```

建議原則：

- 只把專案必需的 MCP 放進專案設定。
- 含有個人帳號、token、API key 的設定優先放在使用者層級，不要提交到 Git。
- 第一次連接 MCP 後，請 Codex 幫您確認工具是否可用。

---

### 第六步：API Key 與祕密資訊管理

請不要把 API key、token、帳密或私密連線字串寫進 README、`AGENTS.md` 或 Git 可追蹤的設定檔。

建議做法：

- 使用環境變數保存 API key。
- 使用 `.env` 時，確認 `.gitignore` 已排除 `.env`。
- 在文件中只寫變數名稱，例如 `OPENAI_API_KEY`，不要寫真實值。
- 需要 Codex 使用祕密資訊時，只提供必要的變數名稱與用途。

---

## 📊 安裝結果回報與驗證

完成設定後，可把下列格式貼給 Codex，請它協助確認環境：

```markdown
## Codex 個人化設定回報
- 使用入口：[Codex Desktop / Codex CLI / OpenAI API]
- 工作區路徑：
- Git：[已安裝 / 未安裝]（版本：____）
- Node.js：[已安裝 / 未安裝]（版本：____）
- Python 3：[已安裝 / 未安裝]（版本：____）
- Obsidian：[已安裝 / 未安裝 / 不使用]
- AGENTS.md：[已建立 / 未建立]
- .codex/skills：[已建立 / 未建立 / 暫不需要]
- MCP / Connector：[已設定 / 未設定 / 暫不需要]
- Git 狀態：[乾淨 / 有未提交變更 / 非 Git 專案]
```

---

## ❓ 常見問題 (FAQ)

| 問題 | 說明與解決方法 |
|---|---|
| **Codex 不知道我的專案規則？** | 請在專案根目錄建立 `AGENTS.md`，寫明語言、編碼、測試方式、提交規範與禁止事項。 |
| **Codex 找不到某個命令？** | 請先重新開啟終端機或 Codex Desktop，再檢查 Git、Node.js、Python 是否已加入 PATH。 |
| **中文輸出變亂碼？** | PowerShell 可先設定 UTF-8：`$OutputEncoding=[Console]::OutputEncoding=[Text.UTF8Encoding]::new($false)`。 |
| **可以直接讓 Codex 改 Obsidian 筆記嗎？** | 可以，但建議優先使用 Obsidian connector / MCP。若只能用檔案方式修改，請先要求 Codex 保留 frontmatter、wikilink 與既有格式。 |
| **需要一開始就設定 MCP 嗎？** | 不需要。入門者可先完成 Git、Node.js、Python、`AGENTS.md`，等工作流程穩定後再加 MCP。 |
| **Codex 要求權限時該怎麼判斷？** | 允許讀取、測試、啟動本機服務通常風險較低；刪除檔案、重設 Git、安裝套件、推送遠端分支前應先確認目的與影響。 |

---

## 📅 更新記錄 (Change Log)

| 日期 | 版本 | 更新內容 |
|---|---|---|
| **2026-07-02** | **v1.1** | 補上 Codex 預封裝技能：`imagedraw` 與 `initialwork`，並更新 README 的技能安裝說明。 |
| **2026-07-02** | **v1.0** | 正式釋出 Codex 入門環境配置手冊，包含 Windows 基礎工具、`AGENTS.md` 範本、`.codex/skills` 建議、MCP / Connector 設定、API key 安全管理與驗證回報格式。 |

---
授權條款：MIT License




