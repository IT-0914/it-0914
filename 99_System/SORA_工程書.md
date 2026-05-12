---
tags: [system, sora]
updated: 2026-05-12
version: v02
---

# SORA 工程書 v02

TAKUMIがObsidianに書いてGitHubにpushしたノートを、SORAが処理・整理・昇格させるための工程定義書です。

---

## フォルダ構成（確定版）

| フォルダ | 役割 | 管理者 |
|---|---|---|
| `00_Inbox` | 依頼メモ・タグ付き断片の入り口 | TAKUMI |
| `01_Daily` | デイリーノート専用（原本ログ） | TAKUMI |
| `05_Permanent` | TAKUMIの主張・再利用できる知識 | SORA（昇格）＋ TAKUMI（判断） |
| `10_Projects` | 進行中プロジェクト・タスク・成果物・メール下書き | SORA |
| `20_Resources` | 外部情報・参考資料・調査結果・整理済み知識 | SORA |
| `30_Archive` | 処理済みの元ノート | SORA |
| `99_System` | テンプレート・ルール・プロンプト | SORA |

---

## 処理フロー概要

```
① GitHubリポジトリ（IT-0914/it-0914）をpull
② 00_Inbox内の全ノートを走査
③ タグを検出
④ タグに対応するプロンプト（99_System/プロンプト/）を読み込む
⑤ ノートの内容 + プロンプトでタスクを実行
⑥ 結果を指定の出力先に書き込む
⑦ 元ノートに処理済みマークを追記
⑧ 処理済みノートを適切なフォルダに移動
⑨ GitHubにpush
```

---

## タグ別処理定義（確定版）

| タグ        | 使用プロンプト           | 出力先                                              | 元ノートの移動先                               |
| --------- | ----------------- | ------------------------------------------------ | -------------------------------------- |
| `#調査`     | `prompt_調査.md`    | 同ノートに追記                                          | `20_Resources`                         |
| `#タスク`    | `prompt_タスク.md`   | `10_Projects` に新ノート                              | `30_Archive`                           |
| `#実行`     | `prompt_実行_作成.md` | `10_Projects` に成果物                               | `30_Archive`                           |
| `#作成`     | `prompt_実行_作成.md` | `10_Projects` に成果物                               | `30_Archive`                           |
| `#整理`     | `prompt_整理.md`    | `20_Resources` に新ノート                             | `20_Resources`                         |
| `#メール`    | `prompt_メール.md`   | `10_Projects` に新ノート                              | `30_Archive`                           |
| `#週次レビュー` | （内蔵ロジック）          | `01_Daily` にWeekly Review + `05_Permanent` に昇格候補 | Daily Noteは移動しない（`reviewed: true` に更新） |

---

## #週次レビュー の詳細工程

1. `01_Daily` フォルダ内の `reviewed: false` のノートを全て取得する
2. 各ノートを横断して以下を抽出する：
   - 未完了タスク
   - 決定事項
   - 繰り返し出た論点
   - Permanent Note候補（TAKUMIの主張になりそうな気づき）
   - Projectへ転記すべき内容
3. `01_Daily/Weekly_Review_（週番号）.md` を新規作成して抽出結果を記述する
4. Permanent Note候補がある場合は `05_Permanent/（テーマ名）.md` を新規作成する
   - テンプレート：`99_System/テンプレート_Permanent.md` を使用
5. 処理したデイリーノートの `reviewed` プロパティを `true` に更新する

---

## 処理済みマークのフォーマット

元ノートの末尾に以下を追記する。

```markdown
---
## ✅ SORA処理完了
- 処理日時: YYYY-MM-DD HH:MM
- 使用タグ: #タグ名
- 出力先: [[リンク]]
- 処理内容: （1行サマリー）
```

---

## エラー処理

| ケース | 対応 |
|---|---|
| 複数タグが付いている | 優先順位順に処理（調査→整理→タスク→実行→作成→メール→週次レビュー） |
| ノートが空またはタグのみ | スキップして `30_Archive` に移動する |
| 処理に失敗した場合 | 元ノートに `#SORA_エラー` タグを追記して `00_Inbox` に残す |
| `reviewed: false` のDailyが存在しない | 週次レビューをスキップしてTAKUMIに報告する |

---

## 処理後のGit操作

全処理完了後、以下を実行してGitHubに反映する：

```bash
git add -A
git commit -m "SORA: （処理内容の要約）"
git push origin main
```
