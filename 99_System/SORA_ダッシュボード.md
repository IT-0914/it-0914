---
tags: [system, dashboard]
---

# SORA ダッシュボード

TAKUMIとSORAの連携状況を一覧で確認するノート。

---

## SORAへの依頼一覧（Dataview）

### 未処理の依頼

```dataview
TABLE file.mtime AS "更新日", tags AS "タグ"
FROM "00_Inbox"
WHERE contains(tags, "SORA_調査") OR contains(tags, "SORA_タスク化") OR contains(tags, "SORA_メール") OR contains(tags, "SORA_作成") OR contains(tags, "SORA_整理")
SORT file.mtime DESC
```

### 進行中のプロジェクト

```dataview
TABLE file.mtime AS "更新日", status AS "ステータス"
FROM "10_Projects"
WHERE status != "完了"
SORT file.mtime DESC
```

---

## SORAタグ早見表

| タグ | SORAがやること |
|---|---|
| `#SORA_調査` | テーマをWeb検索して要約・書き戻し |
| `#SORA_タスク化` | 内容をタスクリストに変換 |
| `#SORA_作成` | ファイル・資料・メールなどを生成 |
| `#SORA_メール` | 返信メールの下書きを作成 |
| `#SORA_整理` | 要約・タグ付けして20_Resourcesへ移動 |

---

## 使い方

1. `00_Inbox` に何でもメモを書く
2. 上のタグを1つ付ける
3. GitHubにpushする（Obsidian Gitなら自動）
4. SORAが処理して結果をpushして返す
5. Obsidianでpullすると結果が反映される
