# ADR: ドキュメントを「現在の仕様」と「将来の構想」に分離する

- **日付:** 2026-07-04
- **ステータス:** 採用
- **対象:** Cube Puzzle プロジェクトのみ（mini-rpg 等には適用しない）

## コンテキスト

- ゲームロジックはほぼ `script.js` 1 ファイルに集約されている
- `README.md` にプレイヤー向け説明・localStorage 詳細・開発メモ・改善候補が混在
- AI や将来の自分が実装時に「今動いている仕様」と「まだのアイデア」を区別しづらい
- `CUBE_SPEC.md` は未作成。`GAME_SPEC.md` は本プロジェクトでは使わない

## 決定

ドキュメントを以下の 4 区分に分ける。

```
docs/
├── current/     … コード上確認できる実装仕様のみ
├── roadmap/     … 未実装の構想・改善案・マイルストーン
├── decisions/   … 設計判断の記録（本 ADR 含む）
└── archive/     … 将来、古い仕様を移す置き場（現時点は空）
```

### ルール

1. **`docs/current/` には未実装を書かない**
2. **判断に迷う内容は current に入れない** — roadmap または decisions へ
3. **既存ファイル（README.md 等）は削除しない** — 新構成へ内容を再配置するのみ
4. **既存コードは変更しない** — ドキュメント追加のみ
5. **事実の根拠はコード**（`script.js`, `index.html`, `style.css`, `sounds/`）

### current の分割方針

| ファイル | 担当 |
|----------|------|
| `gameplay.md` | ルール、スコア、難易度、盤面生成、クリア条件 |
| `ui.md` | 画面構成、HTML 要素、レイアウト、レスポンシブ |
| `audio.md` | 効果音・BGM・再生条件 |
| `save.md` | localStorage キーと更新タイミング |

### roadmap の分割方針

| ファイル | 担当 |
|----------|------|
| `ideas.md` | 改善案・構想の一覧 |
| `milestones.md` | 大きな達成段階 |
| `backlog.md` | タスク粒度の候補 |

## 理由

- AI が実装提案する際、current を SSOT（Single Source of Truth）にできる
- README の「今後の改善候補」を roadmap に移すことで、プレイヤー向け README の slim 化が後から可能
- コードと README の不一致（例: 開発用ボタン記載）を current では書かず backlog で管理できる

## 影響

- 新規: `docs/` 以下 8 ファイル + `archive/` 空ディレクトリ
- 変更なし: `README.md`, ソースコード
- 未作成のまま: `CUBE_SPEC.md`, `GAME_SPEC.md`

## 関連

- 実装仕様: [../current/](../current/)
- 構想: [../roadmap/](../roadmap/)
