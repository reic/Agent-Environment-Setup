---
name: imagedraw
description: Claude Code 生圖/繪圖指引。說「生圖」「畫圖」「產生圖片」時載入。
---

# 生圖（Claude Code 版）

Claude Code（Claude 模型本身）**沒有內建的點陣圖片生成能力**，與 Antigravity（Gemini）不同。可用下列三條路線：

## 三條路

| 路線 | 說明 | 需求 |
|------|------|------|
| A：向量圖 / 圖表 (SVG) | Claude 直接輸出 SVG 原始碼繪製圖示、流程圖、示意圖 | 不需 API Key，Claude Code 原生可寫檔 |
| B：外部圖片生成 MCP | 透過已註冊的圖片生成 MCP 伺服器（如 Stable Diffusion、DALL·E 等第三方工具）呼叫 | 需先用 `claude mcp add` 註冊對應 MCP |
| C：手動走 API 路線 | 呼叫 OpenAI Images API 或其他圖片模型 API，由使用者提供腳本或工具 | 需 `OPENAI_API_KEY` 或對應服務金鑰 |

## 建議提示格式

```
生成一張圖片/圖表：
用途：
尺寸比例：
主題：
畫面內容：
風格：
色彩：
文字：
限制：
輸出位置：
```

## 注意
- 若使用者要求「照片級」圖片，需先確認是否已註冊路線 B 或 C 的工具/MCP，否則直接告知 Claude Code 無法原生產生點陣圖片
- 路線 A（SVG）適合圖示、架構圖、流程圖，不適合寫實照片
- 重要中文文字建議後製（生圖模型可能出錯）
- 專案圖片放 `assets/` 資料夾
- 不把 API Key 寫進 repo（用環境變數或 `.env` 並加入 `.gitignore`）
