# ChatGPT から編集部デスクを見る・動かす

Mid 90s Club のゴルフメディア用 Instagram 投稿は、Claude の「編集部デスク」（候補の採用／却下）と自動投稿ルーティンで動いています。
デスクのデータベースは Claude の中にあるので、外（ChatGPT など）からはこのリポジトリを窓口にします。

## 見る（読むだけ・認証不要）
- 現在の状態: `https://raw.githubusercontent.com/gcconinfo/mid90s-cards/claude/desk/desk/STATE.md`（ブランチ `claude/desk`。ルーティンが毎回 push する）
  - 候補（採用待ち）、投稿予定と日時、保留、失敗と理由、直近の投稿済み（Instagram リンク）、次の空き枠、コマンドの処理結果
  - 同じ内容の JSON: `.../desk/state.json`
- 処理ログ: `.../desk/LOG.md`
- 更新タイミング: 投稿ルーティンが毎時36分ごろに書き換える。朝9時の候補集めの結果は 9:36 ごろに載る。

## 動かす（GitHub の Issue を立てる）
このリポジトリに Issue を立てると、次のルーティン実行（毎時36分ごろ）が読み取って反映し、結果をコメントして Issue を閉じます。
**オーナー（gcconinfo）が立てた Issue だけが有効**。他人の Issue は無視されます。

題名だけで済むコマンド:

| 題名 | 意味 |
|---|---|
| `approve 20260918-03` | 採用。次の空き枠（1本目 21:00、以後 120分間隔）に入る |
| `approve 20260918-03 2026-09-19 21:00` | 日時を指定して採用 |
| `schedule 20260918-03 2026-09-20 21:00` | 投稿予定の日時を変える |
| `reject 20260918-03` | 却下 |
| `hold 20260918-03` | 保留 |
| `unapprove 20260918-03` | 候補に戻す（投稿予定・保留・却下から） |
| `retry 20260917-10` | 失敗したものを次の空き枠で再投稿 |

編集は本文に JSON（題名は自由）:
```json
{"action": "edit", "id": "20260918-03",
 "headline_photo": "1行目\n2行目",
 "caption": "キャプション全文",
 "mode": "photo",
 "use_video": true, "video_start": 600, "video_seconds": 30,
 "cover_video": false,
 "images": [{"url": "https://…/photo.jpg", "credit": "媒体名"}]}
```
- 使える項目: `title`, `headline_photo`（表紙の見出し。2行、各12字前後）, `caption`, `mode`（`photo` 写真 / `ai` AI生成イメージ / `text` 緑カード）, `image_prompt`（AI イメージの英語の場面描写。変えると次回生成し直す）, `cover_video`, `use_video`, `video_start`, `video_seconds`, `images`, `kicker`, `summary`
- 複数コマンドは JSON の配列を本文に（1つの Issue でまとめてよい）
- 本文の JSON は ```json フェンスで囲んでも可

## ルール
- 投稿済み（posted）のものは変更できない
- ID は `STATE.md` にある `YYYYMMDD-NN` をそのまま使う（作らない・推測しない）
- 急ぎのときは Yu が Claude Code のルーティン「Mid 90s Club 投稿」で「今すぐ実行」を押す（ChatGPT からは押せない）
- ルーティンが Issue を閉じられなかったとき（`STATE.md` の処理結果に出ているのに Issue が開いたまま）は、ChatGPT 側で閉じてよい
- 投稿そのもの（画像・キャプションの生成、Instagram への送信）はルーティンの仕事。ChatGPT は「何を・いつ」を決めて Issue にするだけ
