# Save（現在の仕様）

> 根拠: `script.js`  
> ブラウザ `localStorage` に永続化される項目のみ。

## 保存キー一覧

| キー | 型（実際の値） | デフォルト | 用途 |
|------|---------------|-----------|------|
| `cube_difficulty` | 数値文字列（2/4/6/8） | `4`（Normal） | 最後に選択した LEVEL |
| `cube_extra_unlocked` | `"true"` / 未設定 | 未設定 = 未解放 | Extra モード解放フラグ |
| `cube_sound_enabled` | `"true"` / `"false"` | 未設定 = ON | サウンド設定 |
| `egebro_highscore_sz{SIZE}` | 数値文字列 | 未設定 = 0 | 難易度（SIZE）別ベストスコア |

### ハイスコアキーの例

- Normal: `egebro_highscore_sz4`
- Hard: `egebro_highscore_sz6`
- Extra: `egebro_highscore_sz8`

Tutorial（SIZE=2）ではハイスコアの読み書きを行わない。

## 更新タイミング

| キー | いつ書き込むか |
|------|---------------|
| `cube_difficulty` | LEVEL ボタン選択時 |
| `cube_extra_unlocked` | Hard 初クリア時 `"true"` |
| `cube_sound_enabled` | サウンドボタン toggl 時 |
| `egebro_highscore_sz{SIZE}` | プレイ中スコアが BEST 超過時、クリア時 `finalScore` 超過時 |

## 保存されないもの

以下はページを閉じると失われる（コード上、永続化処理なし）:

- 盤面・ブロック配置
- 残り時間・タイマー状態
- 一時停止状態
- 選択中ブロック
- 現在スコア（クリア前の進行中値）
- BGM の再生位置（OFF→ON 時は続きから再開を試みる実装あり）

## 参照

- ゲームルール（スコア）: [gameplay.md](gameplay.md)
