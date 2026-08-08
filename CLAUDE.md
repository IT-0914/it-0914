# このリポジトリについて

これは **Obsidian Vault そのもの**です。ソフトウェアのソースコードではありません。
PC / iPhone / iPad の Obsidian が Obsidian Sync で同期され、PC 上の obsidian-git
プラグインだけがこの GitHub リポジトリと read/write します。

## ディレクトリ構造

| パス | 用途 |
|---|---|
| `00_Inbox` | 思考の起点。依頼の投入場所。元ノートはここから動かさない |
| `01_Daily` | デイリーノート（自動生成） |
| `02_Memo` | 短いメモ |
| `05_Permanent` | 永続ノート |
| `10_Projects` | 実行計画・プロジェクト管理 |
| `20_Resources` | 整理された知識・調査レポート |
| `30_Archive` | 完了済み |
| `99_System` | プロンプト・テンプレート・運用ルール |

タグ運用と各タグの出力先は `README.md` を参照。

## 編集ルール

- **触らないこと**: `.obsidian/`、`.smart-env/`、`copilot/copilot-conversations/`。
  これらは Obsidian とプラグインが管理する領域で、手で書き換えると壊れる。
- ノートは Markdown。フロントマターがある場合は既存のキー構成を崩さない。
- ファイル名・見出しは日本語のまま扱う。リネームすると Obsidian の
  内部リンク（`[[...]]`）が切れるので、リネーム時は参照元も必ず追従させる。
- 既存ノートを作り直すのではなく、追記・部分編集を優先する。
  Vault の内容はユーザーの一次記録であり、失われると復元できない。

## ブランチと反映経路

作業ブランチへ push すると `.github/workflows/auto-merge-claude.yml` が
`main` へ自動マージする。`main` に入ると PC の obsidian-git が pull し、
Obsidian Sync 経由で全端末の Vault に反映される。

コミットメッセージは obsidian-git の `vault backup: {{date}}` と区別できるよう、
何を変更したかを日本語で簡潔に書く。
