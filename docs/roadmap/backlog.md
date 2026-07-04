# Backlog（構想・タスク候補）

> 優先度未設定。実装済みかどうかは [../current/](../current/) で確認すること。

## 高優先（ドキュメント・整合性）

| ID | 内容 | 備考 |
|----|------|------|
| DOC-01 | README 更新: タイトル CUBE PUZZLE、`docs/` リンク | README 現状は「CUBE dev」 |
| DOC-02 | 公開 URL の確定と README / OGP の統一 | README: egeblo-dev / OGP: CUBE-PUZZLE |
| DOC-03 | `docs/archive/` へ旧 README 節の移管方針 | 削除はせず archive へ |

## 中優先（コード整理 — 構想）

| ID | 内容 | 備考 |
|----|------|------|
| REF-01 | `script.js` 分割 | README §7 より |
| REF-02 | `egebro_highscore_*` キー rename + 移行 | 既存ユーザー影響あり |
| REF-03 | 未使用 `soundBank.countdown` の整理 | ロードなし |
| REF-04 | `timeup-share-btn` リスナー | HTML に要素なし |

## 中優先（UI ギャップ — 構想）

| ID | 内容 | 現状 |
|----|------|------|
| UI-01 | `#extra-unlock-overlay` を index.html に追加 | CSS/JS のみ |
| UI-02 | `clear-test-btn` の扱い決定 | JS ハンドラのみ、README に記載 |
| UI-03 | 開発用 UI の本番非表示 | 方針未決 |

## 低優先（機能拡張 — 構想）

| ID | 内容 |
|----|------|
| FEAT-01 | 盤面途中保存 |
| FEAT-02 | ドラッグ視点操作 |
| FEAT-03 | ライセンス追加 |

## 完了済み（参考）

| ID | 内容 |
|----|------|
| DOC-00 | docs ディレクトリ構成の作成（2026-07-04） |
