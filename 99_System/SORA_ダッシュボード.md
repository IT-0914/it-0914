---
tags: [system, dashboard]
updated: 2026-05-12
---

# SORA ダッシュボード

TAKUMIとSORAの連携状況を一覧で確認するノート。

---

## SORAへの未処理依頼（Dataview）

```dataview
TABLE file.mtime AS "更新日", tags AS "タグ"
FROM "00_Inbox"
WHERE contains(tags, "調査") OR contains(tags, "タスク") OR contains(tags, "実行") OR contains(tags, "作成") OR contains(tags, "整理") OR contains(tags, "メール")
SORT file.mtime DESC
```

---

## 進行中のプロジェクト（Dataview）

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
| `#調査` | Web検索して要約・書き戻し |
| `#タスク` | タスクリストに分解 |
| `#実行` | 指示された作業をそのまま実行 |
| `#作成` | ファイル・資料を生成 |
| `#整理` | 知識ノートとして20_Resourcesに保存 |
| `#メール` | 返信メールの下書きを作成 |

---

## 使い方

1. `00_Inbox` に何でもメモを書く
2. 上のタグを1つ付ける
3. 5分待つ（Obsidian Gitが自動でpush）
4. SORAが処理して結果をpushして返す
5. Obsidianに自動で反映される
