# AGENT_SETUP：外部工具連接指南

本資料夾為 AI Agent 外部工具與技能連接設定之專屬工作區。

---

## 📌 外部工具連接與整合總覽

AI Agent 支援透過多種方式擴充能力與連接外部系統：

### 1. Agent Skills (技能擴充)
- **存放目錄**：`~/.gemini/config/skills/` 或插件目錄 `~/.gemini/config/plugins/`
- **架構**：每個 Skill 包含 `SKILL.md`（定義觸發條件與 SOP）以及輔助 Python 腳本/工具。
- **常見技能範例**：
  - `video-audio-downloader`：YouTube 字幕/音訊自動化下載與重整。
  - `yaml-assa-abloy-pptx-generator`：簡報自動化繪製與 COM 導出。
  - `soil-presentation-skills`：SOIL 教學簡報架構轉換。

---

### 2. 本地 CLI 與系統工具 (CLI Tools)
代理程式可呼叫以下系統環境工具以完成自動化任務：
- **`python` / `uv`**：執行數據分析、`python-pptx` 簡報繪製、`pywin32` (PowerPoint COM) 自動化。
- **`yt-dlp`**：串流影音 metadata 與字幕抓取。
- **`PowerPoint` (COM Automation)**：本地簡報渲染與 JPG/PNG 圖片導出。

---

### 3. API 憑證與金鑰管理 (Credentials)
- **環境變數設定**：例如 `PYTHONIOENCODING=utf-8`。
- **金鑰儲存**：可將敏感憑證集中存放於系統 key store 或指定 `.env` 檔案（確保加入 `.gitignore`）。

---

## 📂 本資料夾建置建議

您可在本資料夾中放置以下內容：
1. **`tools_config.json`** / **`settings.yaml`**：外部 API 與工具之連線設定檔。
2. **工具調用測試腳本**：用於驗證本地 CLI 或 MCP 服務連接狀態。
3. **說明文獻與操作手冊**：記錄特定外部工具（如 API 節點、Webhook 網址）之對接規範。

*提示：如需協助為您撰寫特定的工具連線腳本或詳細手冊，請直接告知需求！*
