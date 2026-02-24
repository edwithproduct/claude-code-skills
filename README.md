# Claude Code Skills — PDM Toolkit

這個 repo 收錄了為 **Product Manager 日常工作**設計的 Claude Code Skills，透過 `/skill-name` 指令快速觸發，協助產出標準化的產品文件。

## 什麼是 Claude Code Skills？

Skills 是 Claude Code 的自訂指令模組。將 skill 放置於 `~/.claude/skills/` 目錄後，即可在 Claude Code 對話中透過 `/skill-name` 手動觸發，或由 Claude 根據對話內容自動載入。

## 安裝方式

將此 repo clone 至 `~/.claude/skills/`：

```bash
git clone https://github.com/edwithproduct/claude-code-skills ~/.claude/skills
```

若 `~/.claude/skills/` 已存在其他內容，可改為 clone 至暫存位置後手動移入各 skill 資料夾。

---

## Skills 列表

### 1. `/prd-generator`

**用途**：根據初始想法，產出完整的產品需求文件（PRD）

**觸發方式**：手動 `/prd-generator` 或由 Claude 自動觸發

**使用方式**：
```
/prd-generator 問題：xxx 目標使用者：xxx 解決方案方向：xxx
```

**產出內容**：
- Problem（問題定義、目標客群、數據支持）
- Goals（Output Goal、Input Metrics、本次範圍、Out of Scope）
- Requirements & User Flow（核心概念、User Flow、Feature 列表）
- 上線計畫（API 完成 / 進入測試 / 測試完成 / App 送審 / 上線時間）
- 待確認問題

**PRD 架構說明**：
- Feature 列表整合 UI/UX 設計重點、欄位說明、錯誤處理，避免重工
- 上線計畫自動判斷：功能涉及接案者 → 含 App 送審；僅發案者 → 僅 Web 上線

---

### 2. `/test-plan-generator`

**用途**：根據 PRD 文件與 Figma 設計稿，產出 Given-When-Then 結構的測試計畫

**觸發方式**：僅限手動觸發（`/test-plan-generator`）

**使用方式**：
```
/test-plan-generator PRD 檔案路徑：xxx Figma 連結：xxx（選填）
```

**產出內容**：
- 功能測試（Functional Test）
- 邊界條件測試（Edge Case Test）
- 跨平台測試（Cross-Platform Test，Web vs App）

**產出檔案**：自動存於 PRD 同目錄，命名為 `[PRD 檔名]-test-plan.md`

**測試案例格式**：

| Step | Given | When | Then |
|------|-------|------|------|
| 1 | 前置條件 | 使用者行為 | 預期結果 |

---

## 建議工作流程

```
初始想法
   │
   ▼
/prd-generator → 產出 PRD 草稿
   │
   ▼
補充 [待補充] 欄位、確認待確認問題
   │
   ▼
/test-plan-generator → 產出測試計畫
```

---

## 更新 Skills

修改 skill 後，推送至 GitHub：

```bash
cd ~/.claude/skills
git add .
git commit -m "your message"
git push
```
