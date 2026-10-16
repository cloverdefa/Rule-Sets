# Rule-Sets

個人維護的網路規則與 Surge 模組，包含 AdGuard Home 網域封鎖／允許清單，以及 Surge 的分流、拒絕和本機網域規則。

## AdGuard Home

| 清單 | 用途 | 訂閱網址 |
| --- | --- | --- |
| `AGH/block-list.txt` | 詐騙、釣魚等網域封鎖規則 | [訂閱](https://raw.githubusercontent.com/cloverdefa/Rule-Sets/main/AGH/block-list.txt) |
| `AGH/allow-list.txt` | 自訂允許規則，包含 DAST 服務及 Microsoft 登入／遙測相關網域 | [訂閱](https://raw.githubusercontent.com/cloverdefa/Rule-Sets/main/AGH/allow-list.txt) |

在 AdGuard Home 的 DNS 封鎖清單設定中加入需要的網址。允許清單請依自己的規則優先順序設定，並確認它與其他封鎖清單的搭配符合預期。

## Surge

以下為可直接加入 Surge 設定的規則集網址：

| 規則集 | 用途 | 訂閱網址 |
| --- | --- | --- |
| `Direct.list` | 指定網域直連 | [訂閱](https://raw.githubusercontent.com/cloverdefa/Rule-Sets/main/Surge/Direct.list) |
| `WARP.list` | Cloudflare WARP 相關網域與服務 | [訂閱](https://raw.githubusercontent.com/cloverdefa/Rule-Sets/main/Surge/WARP.list) |
| `Telegram.list` | Telegram IP 網段 | [訂閱](https://raw.githubusercontent.com/cloverdefa/Rule-Sets/main/Surge/Telegram.list) |
| `Reject.list` | WPAD 自動代理設定請求的 URL 規則 | [訂閱](https://raw.githubusercontent.com/cloverdefa/Rule-Sets/main/Surge/Reject.list) |
| `Reject-Drop.list` | LINE VOOM 相關 URL 規則 | [訂閱](https://raw.githubusercontent.com/cloverdefa/Rule-Sets/main/Surge/Reject-Drop.list) |
| `localdomain.list` | `.home.arpa`、`.localdomain`、`.local` 本機網域 | [訂閱](https://raw.githubusercontent.com/cloverdefa/Rule-Sets/main/Surge/localdomain.list) |

在 Surge 設定的 `[Rule]` 區段引用規則集，並依需求指定策略，例如：

```ini
RULE-SET,https://raw.githubusercontent.com/cloverdefa/Rule-Sets/main/Surge/Direct.list,DIRECT
RULE-SET,https://raw.githubusercontent.com/cloverdefa/Rule-Sets/main/Surge/Telegram.list,PROXY
```

請將 `PROXY` 換成你設定中的策略名稱。拒絕類規則集也要依需求選擇 Surge 支援的策略。

### YouTube 增強模組

模組支援 YouTube 與 YouTube Music，可設定隱藏上傳、沉浸式選段及 Shorts 按鈕，也可設定字幕翻譯語言與除錯模式。模組會修改 YouTube API 回應，並使用 MITM 主機 `*.googlevideo.com`、`youtubei.googleapis.com`。

- [安裝模組](https://raw.githubusercontent.com/cloverdefa/Rule-Sets/main/Surge/Modules/YouTube.Enhance.sgmodule)
- [模組腳本](https://raw.githubusercontent.com/cloverdefa/Rule-Sets/main/Surge/Modules/youtube.response.js)（由模組引用）

在 Surge 中匯入模組後，依需要調整模組參數；啟用前請確認已在 Surge 設定所需的 MITM 憑證與主機名。

## 專案內容

```text
AGH/
  allow-list.txt
  block-list.txt
Surge/
  Direct.list
  localdomain.list
  Reject-Drop.list
  Reject.list
  Telegram.list
  WARP.list
  Modules/
    YouTube.Enhance.sgmodule
    youtube.response.js
```

規則集中的更新日期與統計資料以各檔案標頭為準。

## 授權

本專案採用 MIT License，詳見 [LICENSE.md](LICENSE.md)。
