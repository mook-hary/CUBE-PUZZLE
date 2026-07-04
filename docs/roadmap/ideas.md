# Ideas（構想・改善案）

> 未実装。実装済み仕様は [../current/](../current/) を参照。

## ドキュメント・プロジェクト整理

- README を **CUBE PUZZLE** 名義に更新し、`docs/` への索引を追加
- `CUBE_SPEC.md` を新設する場合は `docs/current/` へのリンク集に留め、二重管理を避ける
- 公開 URL の一本化（README: `egeblo-dev` / OGP: `CUBE-PUZZLE` の不一致解消）

## コード構造

- `script.js`（約 2,600 行）の機能別分割（ゲームロジック / 音声 / UI / 保存）
- 未使用コードの整理
- 命名の統一（共有テキスト「CUBE dev」↔ HTML タイトル「CUBE PUZZLE」など）

## 永続化

- localStorage キー名の統一（`egebro_highscore_*` → プロジェクト名に合わせる）
- 既存ユーザーデータの移行処理
- **盤面の途中保存**（現状はページ離脱で全リセット）

## 操作・UX

- **ドラッグでの視点操作**（現状は回転ボタンのみ）
- モバイル向け操作感の改善

## 開発・デバッグ

- クリアテスト用 UI の整理（`script.js` に `clear-test-btn` ハンドラあり、`index.html` には未配置 — README にはボタン存在と記載）
- Extra 解放オーバーレイ HTML の追加（`style.css` / `script.js` に `#extra-unlock-overlay` 参照あり、`index.html` には未配置）
- 本番公開時の開発用 UI 非表示方針の決定

## その他

- ライセンス表記の追加（README 現状「未設定」）
- 共有ハッシュタグ・文言の見直し（`#CUBEdev` 等）

## 出典

主に [README.md](../../README.md) §7「今後の改善候補」と、コード調査で見つかった実装ギャップ。
