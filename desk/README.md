# desk/ — 編集部デスクの窓口（ブランチ claude/desk）

Claude の自動投稿ルーティン（毎時36分ごろ）がここを読み書きします。

| ファイル | 誰が書く | 内容 |
|---|---|---|
| `STATE.md` / `state.json` | ルーティン（毎回上書き） | 候補・投稿予定・保留・失敗・直近の投稿済み・次の空き枠・コマンド処理結果 |
| `LOG.md` | ルーティン（追記） | Issue コマンドの処理ログ（新しい順） |
| `processed.json` | ルーティン | 処理済み Issue の番号と結果（同じ Issue を二度処理しないため） |
| `CHATGPT.md` | ルーティン（pipeline から上書き） | ChatGPT 向けの使い方（コマンド一覧） |
| `README.md` | ルーティン（pipeline から上書き） | このファイル |

コマンドの受け口はこのリポジトリの **Issues**（オーナーが立てたものだけ有効）。書き方は `CHATGPT.md`。
`cards/` は投稿用のカード画像・動画（Instagram に渡す公開URL用）。

編集の正本は Claude 側の `settings/pipeline`（このフォルダの中身を直接編集しても次の実行で上書きされます）。
