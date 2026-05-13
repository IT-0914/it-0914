---
tags: [system, dashboard]
updated: 2026-05-13
version: v05.1
---

# SORA | INTEGRATED COGNITIVE OS

> [!abstract] **IDENTITY: SENIOR STRATEGY CONSULTANT & PM**
> 「判断を前に進める」ための統合ダッシュボード。
> 平日 08:00 - 20:00 の 2時間おきに自律サイクルが稼働中。

---

## 🧭 QUICK NAVIGATION
| [00_INBOX](00_Inbox) | [01_DAILY](01_Daily) | [10_PROJECTS](10_Projects) | [20_RESOURCES](20_Resources) | [99_SYSTEM](99_System) |
|:---:|:---:|:---:|:---:|:---:|
| 思考の起点 | 日々の記録 | 実行計画 | 整理された知識 | 運用・設定 |

---

## ⚡️ ACTIVE ISSUES (PENDING)
`00_Inbox` 内の未処理タグを自動抽出します。

```dataview
TABLE file.mtime AS "LAST_UPDATED", tags AS "TAGS"
FROM "00_Inbox"
WHERE contains(tags, "調査") OR contains(tags, "タスク") OR contains(tags, "実行") OR contains(tags, "作成") OR contains(tags, "整理") OR contains(tags, "メール") OR contains(tags, "指示") OR contains(tags, "緊急")
WHERE !contains(file.name, "Template")
SORT file.mtime DESC
```

---

## 📈 STRATEGIC PROJECTS
現在進行中の主要プロジェクトの進捗状況。

```dataview
TABLE status AS "STATUS", priority AS "PRIORITY", file.mtime AS "LAST_UPDATED"
FROM "10_Projects"
WHERE status != "完了" AND status != "Archive"
SORT priority ASC, file.mtime DESC
```

---

## 🛠 SORA COMMANDS (TAGS)
| ICON | TAG | COMMAND | OUTPUT |
|:---:|---|---|---|
| 🔍 | `#調査` | EVENT REPORT SPECIALIST | `20_Resources` |
| 📋 | `#タスク` | PROJECT DECOMPOSITION | `10_Projects` |
| 🛠 | `#実行` | PRACTICAL EXECUTION | `10_Projects` |
| 🎨 | `#作成` | ASSET GENERATION | `10_Projects` |
| 💎 | `#整理` | KNOWLEDGE STRUCTURING | `20_Resources` |
| 📧 | `#メール` | EXECUTIVE COMMUNICATION | `00_Inbox` |
| ⚡️ | `#指示` | CUSTOM PROMPT EXECUTION | OPTIMIZED |
| 🚨 | `#緊急` | INCIDENT RESPONSE | `10_Projects` |
| 📊 | `#週次レビュー` | STRATEGIC REVIEW | `20_Resources` |

---

## 📅 AUTOMATION SCHEDULE
- **08:00 AM**: `MORNING_ROUTINE` (DAILY_NOTE_GEN + TAG_PROCESS)
- **10:00 AM - 06:00 PM**: `ACTIVE_CYCLE` (TAG_PROCESS_EVERY_2H)
- **08:00 PM**: `EVENING_ROUTINE` (LOG_ENTRY + TAG_PROCESS)

---
[SYSTEM_RULES](99_System/運用ルール.md) | [SORA_SKILL](obsidian-sora-workflow) | [RELOAD_DASHBOARD](SORA_ダッシュボード.md)
