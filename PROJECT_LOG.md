# PROJECT_LOG（航海日誌）
このファイルは「現在地」と「直近の変更」と「次の一手」を固定するにゃあ。
憲法（思想・原則）は CONTEXT.md を正とするにゃあ。

---

## LATEST（ここだけ見れば現在地）
### ✅ 勝利状態（確認済み）
- Pages（本番/開発どちらでも同様に確認済み）:
  - https://jakethecrow-pages.pages.dev
  - （開発アカウント側URLも確認済み）
- 確認結果:
  - GET /api/member/token → {"ok":true,...}
  - POST /api/member/token → success:true
  - /api/debug/relay → 404 JSON 固定
  - /api/no-such-route → 404 JSON {"ok":false,"error":"Not Found"}

### 🔧 直近の変更点（要点だけ）
- debug系の整理:
  - functions/api/debug/relay.ts 削除
  - functions/api/debug/_middleware.ts で /api/debug/* を 404 JSON 固定
- /api 未定義が Pages HTML(200) に吸われる問題を解決:
  - functions/api/[[path]].ts を追加し /api/* 未定義は JSON 404
- member/token の debug 分岐撤去（最小化）:
  - functions/api/member/token.ts

### 🧪 運用テスト（PowerShellは直書き禁止）
- tools/test_health.ps1
- tools/test_debug_404.ps1
- tools/test_token.ps1
※ curl.exe への JSON 直書きは禁止（ファイル方式 or ps1生成のみ）

### 🧭 次にやる候補（A/B/C）
A) request-edit → token → view を ps1 化して運用固定
B) admin/login → admin/view を ps1 化して運用固定
C) 変更点を運用手順書として最終まとめ

---

## CHANGELOG（時系列ログ）
### 2026-01-19
- 勝利状態の確認（token OK / debug404 OK / api 404 JSON OK）
- /api 未定義の吸い込み対策（[[path]].ts）
- tools/*.ps1 を整備して運用固定

（ここに追記していくにゃあ）
