# newgrads-replay — 新卒｜RE:PLAY（スポーツ経験者向け）

- 公開URL: https://reflame.co.jp/lp/newgrads/replay/
- 担当: 鈴村さん
- 仕組みの元: [reflameinc/midcareer-teacher](https://github.com/reflameinc/midcareer-teacher)（プルリクエストをマージすると本番に反映される仕組み）
- 困ったとき: 有川へ。画面に出た文をそのまま貼ってください

**このリポジトリは、プルリクエストを main にマージした時点で本番（公開URL）に出ます。** 2026-11-06 に公開済み。
LPの状態（公開済みか・直せるか）は、reflame-marketing の LP 対応表（`.claude/skills/lp/config.json`）で見ます。この README には書きません。

### このLPだけの違い（midcareer-teacher との差）

- 転送先は `/lp/newgrads/replay/` に固定。初回の転送で `replay/` フォルダが作られる（サーバーで事前に作る必要はない）。
- どのLPの公開も削除同期をしないので、親のLPの公開でこのLPが消えることはない。

## 作業B: LPのファイルを入れて公開する（鈴村さんのPC・2026-11-06 済み）

1. reflame-marketing のフォルダで Claude Code を開く。
2. 下の文の `<　>` を、LPの元ファイルが入っているフォルダの場所に書き換えて貼る。

```
RE:PLAY（スポーツ経験者向け）（newgrads-replay）に最初のファイルを入れて公開まで進めたいです。
LPの元ファイルは <このPCのフォルダの場所> にあります。
入れ方の決まりは reflameinc/newgrads-replay の README.md の「作業B」に書いてあるので、先に読んでから始めてください。
```

3. Claude Code の質問に答えながら進める。「公開しますか」で「公開する」を選ぶと、本番に出る。
4. 公開できたら、Claude Code の案内どおりに本番でテスト予約を1件入れてすぐ取り消し、有川へ「RE:PLAY（スポーツ経験者向け）を公開しました」と連絡する。

赤い × が出たときは、🛑 が付いた行を Claude Code に貼って「これを直して」と頼みます。直らなければ、その行を有川へ送ってください。

### 決まり（Claude Code はここを読んで作業する）

- **入れるもの**: `index.html` と `assets/` の中だけ。`.DS_Store` などは入れない。
- **置き方**: `index.html` はいちばん上の階層。画像・CSS・JS・フォント・動画は、すべて `assets/` の中に置く。本番へ送られるのは `index.html` と `assets/` だけ。
- **このLPで直すこと**: なし（2026-11-06 の初回投入で、GTM・着地時の計測・予約完了の `lead_submit`・プライバシーポリシーのリンクを入れ済み）。予約枠 `ng-replay` は `cvEnabled=false` なので、LP 側の `lead_submit` が予約完了を送る唯一の場所。消さない
- **`lp` の値**: `newgrads_replay`（公開後は変えない）。
- **`assets/` に置ける種類**: png・jpg・jpeg・webp・gif・avif・ico・css・js・woff・woff2・mp4・webm。ファイル名は英数字と `_` `-` `.` だけ、拡張子は小文字。svg は置けない。
- **noindex は残す**: 広告・SNS からの流入専用のため、`<meta name="robots" content="noindex, nofollow">` は消さない（消すと検品で止まる）。
- **上の点以外の見た目・文言は変えない**: 迷ったら、勝手に決めず担当に見せて決めてもらう。
- **公開の前に**: reflame-marketing の `reflame-lp-standard` の静的チェック（`audit.py lp/newgrads-replay --online`）で 🛑 の要修正が無いことを確かめる。
- **main に直接は入れられない**: ブランチを作る → プルリクエストを作る → 検品（check）が緑 → マージ（＝公開）、の順。
- **`.github/` と `scripts/` は触らない**: 変えると中山さんのレビューが必要になる。
- **検品は GitHub の画面で見る**: Mac に最初から入っている bash では `scripts/check.sh` がエラーで止まる。手元で動かなくても、プルリクエストの check が緑なら問題ない。

## ふだんの直し方

reflame-marketing のフォルダで Claude Code に「RE:PLAY（スポーツ経験者向け）のここを直して」と頼みます（`lp` スキル）。ブランチを作る → 直す → プルリクエスト → check が緑 → マージ、の順で、マージした時点で本番に反映されます。戻すときは、マージ済みプルリクエストの「Revert」を押し、できたプルリクエストをマージします。

**GitHub に入れたLPは、サーバーへ直接上げない（FileZilla 等を使わない）。** 直接上げると、次の公開で GitHub の中身に上書きされて消えます。
