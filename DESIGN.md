# Batch Docs 公開サイト — 設計ルール（エージェント向け）

制定：2026-11-10（Astryx 採用ルールの静的サイト適用。ASTRYX-ADOPTION.md 参照）
このサイトは静的 HTML が妥当な構成のため React/Astryx 本体は使わない。代わりに
Astryx の原則――「文書化された部品とルールで組む。推測で作らない。設計ルールを
エージェント指示に明記する」――を本書と `styles.css` で担保する。

## ルール（絶対）
1. スタイルは `styles.css` のみ。全ページがこれを読み込む。ページ内 `<style>` と
   インライン `style=""` は禁止（2026-11-10 に全廃済み）。
2. 色・余白などの値は `:root` のトークンを使う。新しい値が必要ならトークンを
   追加して本書にも記録する。直書きの色コードを増やさない。
3. 新しい見た目の要素が必要になったら、まず既存コンポーネントで表現できないか
   確認する。新規コンポーネントは `styles.css` に追加し、本書のコンポーネント
   一覧に1行足してから使う。
4. 見た目の判断基準は AI-DESIGN-ANTI-PATTERNS.md と UX-REVIEW が上位。
   本サイトの「Google 製品の文法に寄せる」判断（下記）は主題由来の理由として
   文書化済みで、安易に崩さない。

## トークン（styles.css :root）
- --ink #222（本文）／ --mut #5f6368（補助）／ --line #e2e2e2（罫）／
  --blue #0b57d0（Google blue、リンクと主ボタン）／ --bg #f8fafd（ヒーロー地）／
  --code-bg #f3f3f3 ／ --footer-ink #666
- フォント：システムスタック（-apple-system, "Segoe UI", Roboto, 游ゴシック系）。
  Web フォントは読み込まない。
- 数値基準：本文テキスト 16px、ボタン padding 12px 22px（タップ目標 約44px）、
  フッター 14px、行間 1.7（2026-11-06 UX 数値基準）。

## レイアウト
- ランディング（index 系）：`body` 素のまま＋ `.wrap`（最大 880px）。
- ドキュメント（ポリシー系・404）：`<body class="doc">`（最大 760px、本文書体裁）。

## コンポーネント一覧（styles.css 定義済み）
- nav＋.brand（全ページ共通ヘッダー）／ .lang-switch（言語切替、右寄せ）
- .hero（.tag 見出し文）／ .btns＋.btn.primary／.btn.ghost
- .cards＋.card ／ .stepnum（手順番号）／ .price（.plan／.amount）
- footer ／ code ／ .lang（ページ下部の言語セクション）

## 主題由来の判断（AI-DESIGN 照合、2026-11-06 記録の再掲）
Batch Docs は Google Workspace のアドオンで、利用者は Google Sheets の中で
日常的に Google の UI に触れている。その文法（Google blue、システムフォント、
罫線だけのカード）に寄せること自体が信頼の仕組みになるため、SaaS カードキット
寄りの見た目を意図的に採る。逸脱点：影なし、装飾グラデーションなし、
Inter 不使用、大数字ヒーローなし、ポリシーは1カラム。
