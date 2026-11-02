# newgrads-replay — 新卒｜RE:PLAY（スポーツ経験者向け）

- 公開URL: https://reflame.co.jp/lp/newgrads/replay/
- 担当: 鈴村さん
- 仕組みの元: [reflameinc/midcareer-teacher](https://github.com/reflameinc/midcareer-teacher)（プルリクエストをマージすると本番に反映される仕組み）
- 困ったとき: 有川へ。画面に出た文をそのまま貼ってください

## いまの状態（2026-11-02 時点）

| 項目 | 状態 | やる人 |
|---|---|---|
| 自動反映の設定ファイル（`.github/`・`scripts/`） | 済み。midcareer-teacher と同じ内容で、転送先だけこのLP用 | — |
| main を守るルール・production 環境・サーバーの指紋（`DEPLOY_KNOWN_HOSTS`） | 済み | — |
| サーバーに入る鍵（`DEPLOY_SSH_KEY`） | 有川が登録係で登録する | 有川 |
| LPのファイル（`index.html`・`assets/`） | **未**（作業B） | 鈴村さん |
| 本番へ反映するスイッチ（`DEPLOY_ENABLED`） | **オフ**（予行演習モード。マージしても本番は変わらない） | 有川 |
| 公開後の確認（作業Cの4） | 未 | 鈴村さん・有川 |

### このLPだけの違い（midcareer-teacher との差）

- 転送先は `/lp/newgrads/replay/` に固定。初回の転送で `replay/` フォルダが作られる（サーバーで事前に作る必要はない）。
- `/lp/newgrads/`（新卒メインLP）の配下にあるが、新卒メインLPの公開は削除同期をしないので、このLPが消えることはない。

## 作業A: サーバーに入る鍵を登録する（有川）

有川が登録係（`reflameinc/lp-deploy-key`）で登録する。担当の作業はない。

## 作業B: LPのファイルを入れる（鈴村さんのPC）

制作したLP（2026-11-02 に共有した `RE_PLAY_LP_公開用` フォルダ）を、このリポジトリに入れます。

1. reflame-marketing のフォルダで Claude Code を開く。
2. 下の文の `<　>` を、LPの元ファイルが入っているフォルダの場所に書き換えて貼る。

```
RE:PLAY LP（newgrads-replay）に最初のファイルを入れて公開まで進めたいです。
LPの元ファイルは <このPCのフォルダの場所> にあります。
入れ方の決まりは reflameinc/newgrads-replay の README.md の「作業B」に書いてあるので、先に読んでから始めてください。
```

3. Claude Code の質問に答えながら進める。プルリクエストができたら、表示されたURLをブラウザで開く。
4. 画面の下のほうに、緑のチェックと「check」の文字が出るまで待つ（1〜2分）。
5. 緑になったら「Merge pull request」→「Confirm merge」を押す（この時点ではまだ本番は変わらない）。
6. 有川へ「newgrads-replay にLPを入れてマージしました」と連絡する（作業Cへ）。

赤い × が出たときは、×の横の「Details」を開き、🛑 が付いた行を Claude Code に貼って「これを直して」と頼みます。直らなければ、その行を有川へ送ってください。

### 決まり（Claude Code はここを読んで作業する）

- **入れるもの**: `index.html` と `assets/` の33ファイル（画像31・フォント2）だけ。`.DS_Store` などは入れない。
- **置き方**: `index.html` はいちばん上の階層。画像・CSS・JS・フォント・動画は、すべて `assets/` の中に置く（元ファイルはこの形になっている）。本番へ送られるのは `index.html` と `assets/` だけ。
- **このLPで直すこと（元ファイルのままでは公開できない2点。どちらも計測）**:
  1. GTM（`GTM-5KH7WRCP`）のタグを入れる。`</head>` の直前と `<body>` の直後の2か所。入れ方は [reflameinc/justdoito](https://github.com/reflameinc/justdoito) の `index.html` と同じ（`</head>` の直前には、着地時に `lp` と流入情報を積む `dataLayer.push` も入れる）。
  2. 予約完了の計測を入れる。justdoito の `index.html` の「計測」のブロック（`</body>` の直前・`reflame-booking:done` を受けて `lead_submit` を送るもの）を同じ形で入れる。予約枠 `ng-replay` は `cvEnabled=false`（2026-11-02 に config API で確認）なので、LP 側の `lead_submit` が予約完了を送る唯一の場所になる。
  - どちらも `lp` は `'newgrads_replay'` にする（ほかのLPと見分けるため。公開後に変えない）。
- **検品の WARN について**: 「14px未満のfont-size指定」の WARN が1件出る。元のデザインどおりなので、STOP でなければ進めてよい。
- **`assets/` に置ける種類**: png・jpg・jpeg・webp・gif・avif・ico・css・js・woff・woff2・mp4・webm。ファイル名は英数字と `_` `-` `.` だけ、拡張子は小文字。
- **noindex は残す**: 広告・SNS からの流入専用のため、`<meta name="robots" content="noindex, nofollow">` は消さない（消すと検品で止まる）。
- **上の2点以外の見た目・文言は変えない**: 文言は原本のまま（`index.html` 冒頭のコメントのとおり）。迷ったら、勝手に決めず担当に見せて決めてもらう。
- **main に直接は入れられない**: ブランチを作る → プルリクエストを作る → 検品（check）が緑 → マージ、の順。
- **`.github/` と `scripts/` は触らない**: 変えると中山さんのレビューが必要になる。
- **検品は GitHub の画面で見る**: Mac に最初から入っている bash では `scripts/check.sh` がエラーで止まる。手元で動かなくても、プルリクエストの check が緑なら問題ない。

## 作業C: 本番へ反映するスイッチを入れる（有川）

1. 作業Bのマージ後、Actions の `deploy` が「▶ 予行演習モード」で動き、「転送予定 N 件」の一覧に `index.html`・`assets/…` が出ていることを有川が確かめる。
2. 有川がリポジトリ変数 `DEPLOY_ENABLED` を `true` にして、`deploy` をやり直す。
3. 本番へ転送され、「✓ 本番の index.html がリポジトリと一致」「✓ assets 全て HTTP 200」が出れば完了。
4. 担当が本番を開き、予約ボタン（ヘッダー・ファーストビュー・特典の行・画面下の固定ボタン）で予約欄へ移ること、予約フォームが表示されること（reflame.co.jp 上でしか表示されない）を確かめる。1件予約し、計測が動くことを有川と確かめる。

## 作業A〜Cが終わったあとの、ふだんの直し方

reflame-marketing のフォルダで Claude Code に「RE:PLAY LPのここを直して」と頼みます（`lp` スキル）。ブランチを作る → 直す → プルリクエスト → check が緑 → マージ、の順で、マージした時点で本番に反映されます。戻すときは、マージ済みプルリクエストの「Revert」を押し、できたプルリクエストをマージします。

**GitHub に入れたLPは、サーバーへ直接上げない（FileZilla 等を使わない）。** 直接上げると、次の公開で GitHub の中身に上書きされて消えます。
