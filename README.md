# it-0914 Obsidian Vault

TAKUMI専用PKM（Personal Knowledge Management）Vault。
SORAとのAI連携ハブとして機能する。

## フォルダ構成

| フォルダ | 役割 |
|---|---|
| `00_Inbox` | すべてのメモの入り口。AIへの依頼タグを付けてここに投げる |
| `10_Projects` | 現在進行中のプロジェクトノート |
| `20_Resources` | 恒久的な知識・リンクで繋ぐメイン領域 |
| `30_Archive` | 完了・不要になったが残しておくノート |
| `99_System` | テンプレート・画像・システムノート |

## AIタグ（SORAへの依頼書）

| タグ | SORAの動作 |
|---|---|
| `#SORA_調査` | テーマをWeb検索し要約して書き戻す |
| `#SORA_タスク化` | タスクリストに変換しNotionやカレンダーに登録 |
| `#SORA_メール` | 返信メールの下書きを作成 |
| `#SORA_整理` | 要約・タグ付けして20_Resourcesへ移動 |
| `#SORA_テスト` | 動作確認用。内容を読んで要約を返す |
