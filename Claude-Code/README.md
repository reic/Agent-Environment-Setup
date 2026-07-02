# Claude Code 環境設定 (Claude Code Environment Setup Lazy Pack)

本專案是一個專為 Windows 環境下 Anthropic **Claude Code** CLI 打造的**一鍵式環境建置與優化懶人包**。

本懶人包不使用任何自動化指令碼（如 Shell Script 或 PowerShell 腳本），而是透過**純文檔指引與預配置檔案**的方式進行安裝，避開指令碼執行權限與安全性問題。請依照本說明書，依序檢查系統環境並完成設定。

---

## 📂 儲存庫結構
```text
Claude-Code/
├── README.md                 # 本安裝說明文件
└── skills/                  # 預封裝的 Claude Code 專屬技能
    ├── imagedraw/             # 生圖/繪圖指引技能
    └── initialwork/         # 開工/收工/專案初始化工作流技能
```

---

## 📋 安裝與設定流程

### 第一步：⚙️ 核心系統環境檢查與安裝
請開啟您的 PowerShell 或命令提示字元 (CMD)，依序輸入下列測試指令。若系統提示「找不到指令」，請使用下方的 **Winget / npm** 指令進行安裝：

#### 1. Node.js（Claude Code 執行環境）
*   **檢查指令**：`node -v`
*   **安裝指令**：`winget install OpenJS.NodeJS`

#### 2. Git（版本控制與複製套件）
*   **檢查指令**：`git --version`
*   **安裝指令**：`winget install Git.Git`

#### 3. Python 3（執行自動化工具，選用）
*   **檢查指令**：`python --version`
*   **安裝指令**：`winget install Python.Python.3`

#### 4. Obsidian（個人知識庫系統，選用）
*   **檢查指令**：直接確認桌面程式，或輸入 `obsidian`。
*   **安裝指令**：`winget install Obsidian.Obsidian`
*   *註：安裝完成後，建議重啟終端機使環境變數生效。*

#### 5. Claude Code CLI 本體
*   **檢查指令**：`claude --version`
*   **安裝指令**：
    ```powershell
    npm install -g @anthropic-ai/claude-code
    ```
*   **登入驗證**：於終端機輸入 `claude`，依提示以瀏覽器完成 Anthropic 帳號（或 Claude Pro/Max/Console API Key）登入。
*   **健康檢查**：安裝完成後可執行 `claude doctor` 檢查環境設定是否正常。

---

### 第二步：🔌 註冊 NotebookLM MCP 伺服器
若您希望 Claude Code 能直接讀取您的 NotebookLM 知識庫，可透過 CLI 或設定檔註冊：

**方式 A：CLI 指令（建議，於專案根目錄執行）**
```powershell
claude mcp add notebooklm --scope project -- notebooklm-mcp
```

**方式 B：手動編輯專案設定檔**
1.  於專案根目錄開啟（若不存在請自行建立）：`.mcp.json`
2.  加入或編輯下列 JSON 內容：
    ```json
    {
      "mcpServers": {
        "notebooklm": {
          "command": "notebooklm-mcp",
          "args": []
        }
      }
    }
    ```
3.  存檔後，於 Claude Code 內輸入 `/mcp` 確認伺服器連線狀態。
    *   若僅想在自己帳號全域生效（而非提交進 repo），可改用 `--scope user`，設定會寫入使用者層級設定而非專案的 `.mcp.json`。

---

### 第三步：🌐 安裝 Steph Ango 官方 Obsidian 技能集
這些技能由 Obsidian 官方提供，可防止 AI Agent 破壞 Wikilink、.canvas 或屬性格式：

1.  開啟終端機，切換到臨時目錄並複製該套件：
    ```powershell
    git clone https://github.com/kepano/obsidian-skills.git
    ```
2.  將複製出來的 `obsidian-skills/skills/` 底下的所有子資料夾（`defuddle`, `json-canvas`, `obsidian-bases`, `obsidian-cli`, `obsidian-markdown`）：
    *   **複製到**：您的專案工作區目錄底下的 `.claude/skills/` 資料夾中。
    *   *（也可用 `--scope user` 概念，改放到 `~/.claude/skills/` 使其對所有專案生效。）*

---

### 第四步：🚀 安裝本懶人包預封裝的專屬技能 (Workflow & Draw)
本專案已在 `skills/` 目錄中為您預先配置好專屬的工作流與生圖技能：

1.  請將本儲存庫中 `skills/` 下的兩個資料夾：
    *   `imagedraw` (生圖/繪圖指引)
    *   `initialwork` (開工/收工/專案初始化工作流)
2.  **複製並覆蓋到**：您的專案工作區目錄底下的 `.claude/skills/` 資料夾中。
    *   *PowerShell 快速複製範例（請將目標路徑替換成您的專案路徑）：*
        ```powershell
        Copy-Item -Path ".\skills\*" -Destination "C:\您的專案路徑\.claude\skills\" -Recurse -Force
        ```
3.  *(選用)* 在您專案工作區的根目錄下，建立一個 `CLAUDE.md` 檔案（Claude Code 每次啟動會自動載入此檔作為專案記憶），並填入以下工作範本以啟用開工/收工功能：
    ```markdown
    # <專案名稱> - CLAUDE.md
    ## 專案入口
    *   專案簡介：
    *   主要工作分支：
    *   GitHub 倉庫：
    ## 工作規範
    *   使用繁體中文。
    *   使用 PowerShell 語言。
    *   開工時讀取此檔，收工時更新此檔並檢查 Git 變更。
    *   commit / push 前需先徵求使用者確認。
    ## 今日進度 / TODO
    - [ ] 待辦事項
    ```
4.  *(選用)* 若需限制 Claude Code 可自動執行的指令範圍，可於 `.claude/settings.json` 設定權限白名單，例如：
    ```json
    {
      "permissions": {
        "allow": [
          "Bash(git status:*)",
          "Bash(git diff:*)",
          "Bash(git log:*)"
        ]
      }
    }
    ```

---

## 📊 安裝結果回報與驗證

完成上述手動設定後，請複製以下「安裝結果回報」格式貼給您的 Claude Code，讓 Agent 能確認環境對接狀況：

```markdown
## Claude Code 個人化設定回報
- Node.js：[已安裝 / 未安裝]
- Git：[已安裝 / 未安裝]
- Python 3：[已安裝 / 未安裝]
- Obsidian：[已安裝 / 未安裝]
- Claude Code CLI：[已安裝 / 未安裝]（版本：____）
- NotebookLM MCP：[已安裝 / 待登入 / 未安裝]
- Obsidian Skills (kepano)：[已安裝 / 未安裝]
- Workflow / 生圖技能：[已安裝 / 未安裝]
- 規劃檔案 CLAUDE.md：[已建立 / 未建立]
- Git 狀態：[乾淨 / 有未提交變更]
```

---

## ❓ 常見問題 (FAQ)

| 問題 | 說明與解決方法 |
|---|---|
| **安裝完 Node/Git/Python 後，系統仍提示找不到該指令？** | 安裝完成後，**必須重啟您的終端機（PowerShell/CMD）或開發編輯器（如 VS Code）**，新寫入的系統環境變數（PATH）才會生效。 |
| **`claude` 指令找不到，但 npm install 顯示成功？** | 請確認 npm 全域安裝路徑已加入系統 PATH（可用 `npm config get prefix` 查詢路徑），或重新開啟終端機。 |
| **技能 (Skill) 沒有被自動載入？** | 確認 `SKILL.md` 是否放在 `.claude/skills/<技能名稱>/SKILL.md` 的正確層級，且 YAML frontmatter 內的 `name`、`description` 欄位齊全。 |
| **CLAUDE.md 內容感覺沒被讀取？** | 確認檔案放在專案**根目錄**，且 Claude Code 是在該目錄（或其子目錄）下啟動的；也可用 `/memory` 指令檢查目前已載入的記憶檔案。 |
| **MCP 伺服器顯示已註冊卻連不上？** | 於 Claude Code 內輸入 `/mcp` 查看連線狀態與錯誤訊息；若為需要 OAuth 的伺服器，請確認已完成登入授權流程。 |
| **Windows 系統上顯示中文亂碼或編碼錯誤？** | 請在終端機中先執行 `[Console]::OutputEncoding = [System.Text.Encoding]::UTF8` 以修正編碼。 |
| **想避免 Claude Code 每次都跳出權限詢問？** | 可在 `.claude/settings.json`（專案）或 `~/.claude/settings.json`（使用者全域）內設定 `permissions.allow` 白名單，或於互動模式輸入 `/permissions` 調整。 |

---

## 📅 更新記錄 (Change Log)

| 日期 | 版本 | 更新內容 |
|---|---|---|
| **2026-07-02** | **v1.0** (最新版) | 🚀 專案首版發布。棄用自動化腳本改以純文檔指引安裝。整合系統基礎環境 Winget/npm 檢測安裝指引，支援 NotebookLM MCP、`kepano/obsidian-skills` 官方套件與本專案內置的 `imagedraw`、`initialwork` 技能安裝手冊。 |

---
授權條款：MIT License
