# ShiftNote LP

Google Stitchで承認した深緑・アイボリーのLPを、日本語・英語の静的HTMLとして実装しています。

- `/`: 日本語 (`index.html`)
- `/en/`: English (`en/index.html`)
- `src/styles.css`: レスポンシブ表示・アクセシビリティ調整
- `tailwind.config.cjs`: Stitch由来の色・文字・余白の定義
- `assets/site.css`: 生成済みCSS（配信にNode.jsやTailwind CDNは不要）
- `assets/site.js`: スマホメニューの閉じる操作。FAQは標準のdetails要素で動作
- `redesign/`: 承認済みStitch原本と画像
- `design-qa.md`, `design/qa/`: 表示確認・比較記録

## ローカル表示・CSSの更新

リポジトリ直下を静的配信してください。

```sh
python3 -m http.server 4317
```

CSSを編集する場合:

```sh
npm ci
npm run build
```

生成済みCSSをコミットするため、静的ホスト側でのビルドは必須ではありません。Google Fontsは外部配信を利用します。CSSを変更したときは、両HTMLのCSSクエリー文字列も更新してください。

## アプリへのリンク

登録は `https://app.shift-note.jp/signup/`、ログインは `/signin/`、デモは `/demo/` へ移動します。LP自体では認証やカレンダー権限を要求しません。

日本語・英語とも、サーバーから読めるdescription、canonical、hreflang、Open Graph、Twitter Card、既存の共有画像とアイコンを維持しています。canonicalのドメインは既存設定の `https://shiftnote.mndn.dev` を引き継いでいます。

利用規約・プライバシーポリシー・お問い合わせの正式なURLは未提供のため、フッターは準備中の非操作ラベルです。正式な文書や窓口を用意した際にリンクへ差し替えてください。

## 旧版 LP01 の保存・復元

変更前の日本語・英語LPは、ローカルブランチ `archive/lp01` と注釈付きタグ `lp01` に保存済みです。保存コミットは `c398c96`。変更前にあった「ブラウザー枠の表記をShiftNoteにする」修正も含めています。

作業ツリーがクリーンな状態で旧版を見るには:

```sh
git switch archive/lp01
python3 -m http.server 4317
# 確認後、新版へ戻る
git switch develop
```

新版を取り消して旧LPへ戻す場合は、`feat: implement Stitch landing page redesign` のコミットを `git revert <コミットID>` してください。履歴を消さずに旧版へ戻せます。将来、別の修正を重ねた場合は差分や競合を確認してください。

今回はローカルの保存とコミットのみです。push・公開・Cloudflare設定の変更は行っていません。ブランチを作るだけではCloudflare上の閲覧URLは作られません。
