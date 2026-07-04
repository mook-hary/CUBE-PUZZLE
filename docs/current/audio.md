# Audio（現在の仕様）

> 根拠: `script.js` / `sounds/`  
> 実装されている音声ファイルと再生条件のみ記載。

## 方式

| 種別 | API | 備考 |
|------|-----|------|
| 効果音・ファンファーレ | Web Audio API | `AudioContext` + `fetch` で mp3 をデコード |
| BGM | HTMLAudioElement | 3 曲からランダム、ループ、音量 0.20 |
| カウントダウン beep | Web Audio API（オシレーター） | mp3 ファイルは使わない |

## 設定

- **ON/OFF:** `cube_sound_enabled`（未設定または `"true"` で ON、`"false"` で OFF）
- **UI:** `#sound-toggle-btn`（🔊 / 🔇）
- OFF 時: BGM 一時停止、ファンファーレ停止（AudioContext は suspend しない — iOS 復帰対策）

## 効果音ファイル

| ファイル | soundBank キー | 再生タイミング |
|----------|----------------|----------------|
| `select_1.mp3` | `select` | ブロック選択、各種ボタン、共有 |
| `clear_1.mp3` | `clear` | ペア消去、クリア確定 |
| `error_1.mp3` | `error` | 選択不可ブロック |
| `timeup_1.mp3` | `timeup` | 時間切れ |
| `start_1.mp3` | `start` | ゲーム開始 |
| `clear_fanfare.mp3` | `clearFanfare` | クリア 500ms 後 |
| `extra_unlock_fanfare.mp3` | `extraUnlockFanfare` | Hard 初クリア 500ms 後 |
| `unlock_key.mp3` | `keyUnlock` | Extra 解放後、タイトル/再プレイ遷移時 |

`soundBank.countdown` は定義のみ。ロード処理なし（プログラム生成 beep を使用）。

## BGM

| ファイル |
|----------|
| `sounds/bgm_1.mp3` |
| `sounds/bgm_2.mp3` |
| `sounds/bgm_3.mp3` |

- ゲーム開始時にランダム選択
- RESET / クリア後再開時も再抽選または再開
- 開始時フェードインあり（`fadeInBGMVolume`）

## カウントダウン beep

| 残り秒 | 音 |
|--------|-----|
| 5〜3 | 単発 beep（1200Hz、0.15s） |
| 2〜1 | 連続 beep（1600Hz、2回） |

## ライフサイクル

| イベント | BGM |
|----------|-----|
| PAUSE | 一時停止 |
| RESUME | 再開 |
| タブ非表示（`visibilitychange`） | 一時停止 |
| タブ表示（ゲーム中・非 PAUSE・非 game over） | 再開 |
| クリア確定 | 一時停止 → ファンファーレ |
| タイトル復帰 | 停止（currentTime リセット） |

## 参照

- 保存キー: [save.md](save.md)
