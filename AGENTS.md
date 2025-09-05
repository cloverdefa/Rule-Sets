# Repository Guidelines

本文件為貢獻者快速指南，協助你安全、可預期地更新規則集。

## Project Structure & Module Organization
- `AGH/`: AdGuard Home 規則（Adblock/AdGuard 語法）。例如：`block-list.txt`、`allow-list.txt`。
- `Surge/`: Surge 規則清單。現有檔案：`Blocks.list`、`Direct.list`、`WARP.list`。
- `.github/workflows/`: 自動化流程（推送通知、部分 PR 自動合併）。

## Build, Test, and Development Commands
- 無需建置。請以簡單檢查確保品質：
  - 計算有效規則行：`rg -v '^(#|!|\s*$)' AGH/block-list.txt | wc -l`
  - 檢查尾端空白：`rg -n "\s+$" AGH Surge`
  - 檢視差異：`git diff`、提交前自我審閱。

## Coding Style & Naming Conventions
- 編碼：UTF-8、LF、檔尾保留換行；避免尾端空白與 Tab。
- 命名：AdGuard 用 `*.txt`；Surge 用 `*.list`；遵循現有名稱大小寫（如 `Blocks.list`）。
- 註解：AdGuard 使用 `!`；Surge 使用 `#`。一行一規則，避免過長行（建議 ≤ 100 字元）。
- AdGuard 範例：`||example.com^`（網域封鎖）。
- Surge 範例：`DOMAIN-SUFFIX,example.com,REJECT` 或純清單時一行一網域。

## Testing Guidelines
- 功能驗證：
  - 臨時匯入 `AGH/block-list.txt` 或 `Surge/Blocks.list` 的 Raw URL 至目標工具測試。
  - 盡量最小化誤封（針對網域、子網域精準匹配）。
- 來源註記：新增規則時於 PR 描述附上來源或截圖，便於審核。

## Commit & Pull Request Guidelines
- Commit 格式：建議 Conventional Commits，例如：
  - `feat(agh): 新增台灣簡訊詐騙網域`
  - `fix(surge): 更正規則語法與註解日期`
- PR 要求：說明目的、影響範圍、測試方式；如為大規模調整，附分組策略或樣本。
- CI 與自動化：
  - 推送至 `main` 會觸發 Telegram 通知。
  - 維護者提交的 PR 可能在檢查通過後自動合併。

## Security & Configuration Tips
- 避免使用過度廣泛萬用字元造成誤封；優先精準網域。
- 不得加入個資或敏感資訊於註解。
- 大幅變更前，先以小批量 PR 驗證影響。

