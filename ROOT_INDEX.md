# ROOT_INDEX（これ見たらわかるにゃ！）

## 0) 作業の原則（事故防止）
- ブラウザは Cloudflare だけ叩く（GAS URL / API_GATE_KEY をクライアントに出さない）
- PowerShell の curl.exe は JSON直書き禁止（ファイル方式 or ps1生成のみ）
- 引っ越し時は：PROJECT_LOG の LATEST 更新 → handoff push → 魔法の言葉

---

## 1) ルート一覧（どこが何の拠点にゃ？）

### A. Cloudflare（jakethecrow-pages / APIリレー）
- ローカル：`G:\マイドライブ\会員管理\コード8\jakethecrow-pages`（職場は H: でも同じ構造）
- 触る場所：
  - `functions/api/**` … APIルート本体
  - `tools/*.ps1` … 疎通テスト＆運用固定
- 目的：
  - GASへ中継、/api未定義は JSON 404 固定、debug整理済み

### B. GAS 開発（code_8 / スプレッドシート連携の本体）
- ローカル：`G:\マイドライブ\会員管理\コード8\code_8`（職場は H:）
- 触る場所：
  - `*.gs / *.html / appsscript.json` … clasp push対象
- 目的：
  - config/設定/data/log中心のノーコード運用を実現

### C. GAS 本番（触らないゾーン）
- ローカル：`G:\マイドライブ\会員管理\コード8\code_8_production`（職場は H:）
- 注意：
  - 今は本番の詳細はここに書かない（混同防止）
  - 触るときは必ず「本番」宣言してから

### D. handoff（公開 / 引っ越し用）
- ローカル作業：`G:\マイドライブ\会員管理\コード8\jakethecrow-pages\code_8_handoff`（職場は H:）
- GitHub（公開）：`greenlab723/code_8_handoff`
- 置くもの：
  - `CONTEXT.md`（憲法）
  - `PROJECT_LOG.md`（航海日誌）
  - `HANDOFF.md`（魔法の言葉）
  - `ROOT_INDEX.md`（←これ）

---

## 2) 主要ファイル早見表（よく触る順にゃ）

### Cloudflare側（jakethecrow-pages）
- `functions/api/[[path]].ts` … /api未定義を JSON 404 にする番人
- `functions/api/debug/_middleware.ts` … /api/debug/* を 404 JSON 固定
- `functions/api/member/token.ts` … token API（最小化済み）
- `tools/test_health.ps1` … health確認
- `tools/test_debug_404.ps1` … debugが404固定か確認
- `tools/test_token.ps1` … token POST/GET確認（ファイル方式）

### GAS側（code_8）
- `Api.gs` … switch(route) ルーティング（JSON API）
- `Admin.gs` … 管理者API（adminTokenなど）
- `Helpers.gs` … 設定/採番/共通
- `Mail.gs` … メール認証/送信
- `Main.gs` … doGet/フロント入口

---

## 3) 環境の紐づき（公開用：リンクは伏せるにゃ）
※スプレッドシートURLは公開に置かない。ID末尾だけメモするにゃ。

- 開発用Spreadsheet：ID末尾 `...ksHI`
- 本番用Spreadsheet：ID末尾 `...qEs`

---

## 4) 作業別チートシート

### 引っ越し（handoff更新）1発
- `.\tools\handoff_update.ps1` を実行

### Cloudflare疎通チェック
- `tools/test_health.ps1`
- `tools/test_debug_404.ps1`
- `tools/test_token.ps1`
