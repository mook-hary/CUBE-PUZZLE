# Project Structure

> **Purpose:** Define what each folder and key file **is for** — not how it is implemented.  
> **Audience:** Humans and AI agents working on Cube Puzzle.

---

## プロジェクト全体構成

```
cube-puzzle/
├── assets/              # 画像リソース
├── sounds/              # 音声ファイル
├── docs/                # ドキュメント一式
│   ├── current/         # 現在の仕様（実装済み）
│   ├── roadmap/         # 将来の構想
│   ├── decisions/       # 設計判断の記録
│   ├── archive/         # 過去仕様の退避先
│   ├── AI_RULES.md
│   ├── DOCUMENT_PRIORITY.md
│   ├── AI_WORKFLOW.md
│   ├── AI_TASK_TEMPLATE.md
│   └── PROJECT_STRUCTURE.md   # このファイル
├── index.html           # 画面構造（HTML）
├── script.js            # ゲームロジック・UI 制御（JS）
├── style.css            # レイアウト・見た目（CSS）
├── README.md            # 人間向け入口
└── CUBE_SPEC.md         # ゲーム仕様（統合参照用）
```

ビルド成果物・`node_modules`・テスト用ディレクトリは **現状なし**（静的ファイルのみ）。

---

## ルート — アプリケーション

| パス | 役割 |
|------|------|
| `index.html` | ページ構造。タイトル・ゲーム画面・オーバーレイなど DOM の定義 |
| `script.js` | ゲーム処理・イベント・音声制御・永続化の実行コード |
| `style.css` | レイアウト、3D 表示、UI コンポーネントのスタイル |

---

## ルート — ドキュメント・仕様

| パス | 役割 |
|------|------|
| `README.md` | **人間向け**プロジェクト入口。概要・遊び方・開発のはじめ方 |
| `CUBE_SPEC.md` | **ゲーム仕様**の統合参照用（単一ファイルで仕様を見たいとき）。詳細は `docs/current/` と整合させる |

---

## `assets/`

**画像などの静的リソース**

| 例 | 用途 |
|----|------|
| `ogp.png` | SNS 共有・OGP 用画像 |

ゲーム内スプライトは現状 CSS / 絵文字テキスト中心。画像を増やす場合はここに置く。

---

## `sounds/`

**音声ファイル（mp3）**

BGM・効果音・ファンファーレなど。コードから相対パス `sounds/` で参照する。

---

## `docs/`

**プロジェクトのドキュメント置き場**

実装コードは置かない。仕様・ルール・構想・判断記録のみ。

### `docs/current/`

**現在の仕様（実装済みのみ）**

| ファイル | 担当領域 |
|----------|----------|
| `gameplay.md` | ルール、スコア、難易度 |
| `ui.md` | 画面・HTML 要素・レイアウト |
| `audio.md` | 音声ファイルと再生条件 |
| `save.md` | localStorage と永続化 |

AI の実装 SSOT は **コード → `current/`**（[DOCUMENT_PRIORITY.md](DOCUMENT_PRIORITY.md) 参照）。

### `docs/roadmap/`

**将来の構想・未実装のアイデア**

| ファイル | 担当領域 |
|----------|----------|
| `ideas.md` | 改善案・構想一覧 |
| `milestones.md` | 大きな達成段階 |
| `backlog.md` | タスク候補 |

依頼がない限り AI はここを **実装しない**。

### `docs/decisions/`

**設計判断（ADR）**

なぜその構成・方針にしたかを記録。仕様そのものではない。

### `docs/archive/`

**過去仕様・廃止ドキュメントの退避先**

現行参照には使わない。削除せず移動する。

### `docs/` 直下 — AI 運用

| ファイル | 役割 |
|----------|------|
| [AI_RULES.md](AI_RULES.md) | AI が**絶対に守る**ルール（最優先） |
| [DOCUMENT_PRIORITY.md](DOCUMENT_PRIORITY.md) | AI が**何をどの順で読むか** |
| [AI_WORKFLOW.md](AI_WORKFLOW.md) | AI が**どう作業を進めるか** |
| [AI_TASK_TEMPLATE.md](AI_TASK_TEMPLATE.md) | 人間が AI に依頼するときの**標準テンプレート** |
| [PROJECT_STRUCTURE.md](PROJECT_STRUCTURE.md) | **フォルダとファイルの役割**（このファイル） |

### `docs/` 直下 — その他

| ファイル | 役割（想定） |
|----------|-------------|
| `CHANGELOG.md` | 変更履歴（未使用の場合は将来用プレースホルダ） |
| `DESIGN.md` | デザイン方針メモ（未使用の場合は将来用プレースホルダ） |
| `TODO.md` | 作業メモ（未使用の場合は将来用プレースホルダ） |

---

## AI 向けルール

AI は以下を守ること（詳細は [AI_RULES.md](AI_RULES.md)）。

| ルール | 意味 |
|--------|------|
| **役割に合わない場所へファイルを追加しない** | 例: 仕様を `script.js` に長文コメントしない / 音声を `assets/` に混ぜない |
| **同じ内容を複数ファイルへ重複記載しない** | 実装済み仕様は `docs/current/` を SSOT。`CUBE_SPEC.md` は統合ビュー |
| **新しいディレクトリを勝手に作らない** | `src/`、`lib/` 等は依頼がない限り作らない |
| **役割が分からない場合は提案に留める** | 置き場所に迷ったら実装前に確認 |

---

## Related

- AI constitution: [AI_RULES.md](AI_RULES.md)
- Read order: [DOCUMENT_PRIORITY.md](DOCUMENT_PRIORITY.md)
- Human entry: [../README.md](../README.md)
