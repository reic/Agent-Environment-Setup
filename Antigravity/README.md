# Agent環境設定 (Agent Environment Setup Lazy Pack)

本專案是一個專為 Windows 環境下 AI Coding Agent (如 Google Antigravity, Claude Code 等) 打造的**一鍵式環境建置與優化懶人包**。

本懶人包不使用任何自動化指令碼（如 Shell Script 或 PowerShell 腳本），而是透過**純文檔指引與預配置檔案**的方式進行安裝，避開指令碼執行權限與安全性問題。請依照本說明書，依序檢查系統環境並完成設定。

---

## 📂 儲存庫結構
```text
Agent環境設定/
├── README.md                 # 本安裝說明文件
└── skills/                  # 預封裝的 AI Agent 專屬技能
    ├── 04-draw/             # 生圖指引技能
    └── 05-workflow/         # 開工/收工/專案初始化工作流技能
```

---

## 📋 安裝與設定流程

### 第一步：⚙️ 核心系統環境檢查與安裝
請開啟您的 PowerShell 或命令提示字元 (CMD)，依序輸入下列測試指令。若系統提示「找不到指令」，請使用下方的 **Winget** 指令進行安裝：

#### 1. Node.js (執行 MCP 伺服器核心)
*   **檢查指令**：`node -v`
*   **安裝指令**：`winget install OpenJS.NodeJS`

#### 2. Git (版本控制與複製套件)
*   **檢查指令**：`git --version`
*   **安裝指令**：`winget install Git.Git`

#### 3. Python 3 (執行自動化工具)
*   **檢查指令**：`python --version`
*   **安裝指令**：`winget install Python.Python.3`

#### 4. Obsidian (個人知識庫系統)
*   **檢查指令**：直接確認桌面程式，或輸入 `obsidian`。
*   **安裝指令**：`winget install Obsidian.Obsidian`
*   *註：安裝完成後，建議重啟終端機使環境變數生效。*

---

### 第二步：🔌 註冊 NotebookLM MCP 伺服器
若您希望 AI Agent 能直接讀取您的 NotebookLM 知識庫，請將其註冊至 AI 的 MCP 設定檔中：

1.  開啟此設定檔案（若檔案不存在請自行建立）：
    `C:\Users\<您的使用者名稱>\.gemini\antigravity\mcp_config.json`
2.  在檔案中加入或編輯下列 JSON 內容：
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
3.  存檔後即完成註冊。

---

### 第三步：🌐 安裝 Steph Ango 官方 Obsidian 技能集
這些技能由 Obsidian 官方提供，可防止 AI Agent 破壞 Wikilink、.canvas 或屬性格式：

1.  開啟終端機，切換到臨時目錄並複製該套件：
    ```powershell
    git clone https://github.com/kepano/obsidian-skills.git
    ```
2.  將複製出來的 `obsidian-skills/skills/` 底下的所有子資料夾（`defuddle`, `json-canvas`, `obsidian-bases`, `obsidian-cli`, `obsidian-markdown`）：
    *   **複製到**：您的專案工作區目錄底下的 `.agents/skills/` 資料夾中。

---

### 第四步：🚀 安裝本懶人包預封裝的專屬技能 (Workflow & Draw)
本專案已在 `skills/` 目錄中為您預先配置好專屬的工作流與生圖技能：

1.  請將本儲存庫中 `skills/` 下的兩個資料夾：
    *   `drawguide` (生圖指引)
    *   `workflow_prefer` (開工/收工/專案初始化工作流)
2.  **複製並覆蓋到**：您的專案工作區目錄底下的 `.agents/skills/` 資料夾中。
    *   *PowerShell 快速複製範例（請將目標路徑替換成您的專案路徑）：*
        ```powershell
        Copy-Item -Path ".\skills\*" -Destination "C:\您的專案路徑\.agents\skills\" -Recurse -Force
        ```
3.  *(選用)* 在您專案工作區的根目錄下，建立一個 `ANTIGRAVITY.md` 檔案，並填入以下工作範本以啟用開工/收工功能：
    ```markdown
    # <專案名稱> - ANTIGRAVITY.md
    ## 專案入口
    *   專案簡介：
    *   主要工作分支：
    *   GitHub 倉庫：
    ## 工作規範
    *   使用繁體中文。
    *   使用 PowerShell 語言。
    *   開工時讀取此檔，收工時更新此檔並檢查 Git 變更。
    ## 今日進度 / TODO
    - [ ] 待辦事項
    ```

---

## 📊 安裝結果回報與驗證

完成上述手動設定後，請複製以下「安裝結果回報」格式貼給您的 AI Agent，讓 Agent 能確認環境對接狀況：

```markdown
## Anti-Gravity 個人化設定回報
- Node.js：[已安裝 / 未安裝]
- Git：[已安裝 / 未安裝]
- Python 3：[已安裝 / 未安裝]
- Obsidian：[已安裝 / 未安裝]
- NotebookLM MCP：[已安裝 / 待登入 / 未安裝]
- Obsidian Skills (kepano)：[已安裝 / 未安裝]
- Workflow 工作流技能：[已安裝 / 未安裝]
- 規劃檔案 ANTIGRAVITY.md：[已建立 / 未建立]
- Git 狀態：[乾淨 / 有未提交變更]
```

---

## ❓ 常見問題 (FAQ)

| 問題 | 說明與解決方法 |
|---|---|
| **安裝完 Node/Git/Python 後，系統仍提示找不到該指令？** | 安裝完成後，**必須重啟您的終端機（PowerShell/CMD）或開發編輯器（如 VS Code）**，新寫入的系統環境變數（PATH）才會生效。 |
| **Winget 提示需要授權或彈出使用者帳戶控制 (UAC) 視窗？** | 這是正常現象，請在彈出視窗點選「是」以授權 Winget 進行系統級別的軟體安裝。 |
| **Obsidian 技能載入後，使用 obsidian CLI 提示錯誤？** | 請確認您的 Obsidian 桌面程式已開啟，且已至「設定 (Settings) -> 一般 (General) -> 命令行介面 (Command line interface)」點擊「註冊 (Register)」。 |
| **NotebookLM MCP 無法登入或連線出錯？** | 請使用 `nlm login` 重新進行 OAuth 授權，並確認您的網路連線正常。若有 OAuth 憑證過期問題，請輸入 `nlm logout` 後再重新登入。 |
| **Windows 系統上顯示中文亂碼或編碼錯誤？** | 請在終端機中先執行 `$env:PYTHONIOENCODING = "utf-8"` 與 `[Console]::OutputEncoding = [System.Text.Encoding]::UTF8` 以修正編碼。 |

---

## 📅 更新記錄 (Change Log)

| 日期 | 版本 | 更新內容 |
|---|---|---|
| **2026-07-02** | **v1.0** (最新版) | 🚀 專案首版發布。棄用自動化腳本改以純文檔指引安裝。整合系統基礎環境 Winget 檢測安裝指引，支援 NotebookLM MCP、`kepano/obsidian-skills` 官方套件與本專案內置的 `04-draw`、`05-workflow` 技能安裝手冊。 |

---
授權條款：MIT License
