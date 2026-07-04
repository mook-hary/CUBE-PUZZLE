# UI（現在の仕様）

> 根拠: `index.html` / `style.css` / `script.js`  
> HTML に存在する要素のみ画面仕様として記載。

## 画面構成

```
#game-screen-wrapper
└── #game-body-box          … 16:9 のゲーム枠
    ├── #start-overlay      … タイトル
    ├── #pause-overlay      … 一時停止
    ├── #clear-overlay      … クリア / TIME UP 結果
    └── #game-container     … プレイ画面
        ├── #utility-buttons
        ├── #ui-panel
        ├── #stage-area
        └── #screen-fade    … 画面フェード
```

## タイトル画面（`#start-overlay`）

| 要素 | id | 動作 |
|------|-----|------|
| Tutorial | `diff-tutorial-btn` | Tutorial 開始 |
| Normal | `diff-normal-btn` | 難易度 4 を選択 |
| Hard | `diff-hard-btn` | 難易度 6 を選択 |
| Extra | `diff-extra-btn` | 難易度 8（解放後のみ表示） |
| START | `actual-start-btn` | 選択中 LEVEL で開始 |

起動時: Normal が `active`。前回の難易度は `cube_difficulty` から復元。

## プレイ画面

### 左パネル（`#ui-panel`）

| 表示 | id | 内容 |
|------|-----|------|
| SCORE | `score` | 現在スコア（Tutorial は `-`） |
| BEST | `best-score` | 難易度別ベスト |
| ステータス | `status` | 操作ガイド・エラー |
| 残りブロック | `count` | アクティブブロック数 |
| タイマー | `timer-text` / `timer-bar` | 残り時間または「チュートリアル」（Normal 120秒 / Hard 170秒 / Extra 200秒） |
| 回転説明 | `rotate-hint` | 「180° ROTATE」 |
| ⇦ 左 | `rot-left-btn` | 180° 回転（X 軸） |
| ⇨ 右 | `rot-right-btn` | 180° 回転（Z 軸） |
| ⇧ 上 | `rot-up-btn` | 180° 回転（中心対称） |
| ⇩ 下 | `rot-down-btn` | 180° 回転（Y 軸） |
| PAUSE | `pause-btn` | 一時停止 |
| RESET | `reset-btn` | 同条件で再生成 |

### 右上（`#utility-buttons`）

| 要素 | id | 動作 |
|------|-----|------|
| 🔊 / 🔇 | `sound-toggle-btn` | サウンド ON/OFF（`cube_sound_enabled` に保存） |

### 3D ステージ（`#stage-area`）

- `#viewport`: `perspective: 1400px`
- `#stage`: `transform-style: preserve-3d`、ブロック（`.cube` / `.face`）を子要素として配置
- 選択中ブロック: `.selected`（黄色枠・半透明）

## 一時停止（`#pause-overlay`）

| ボタン | id | 動作 |
|--------|-----|------|
| CONTINUE | `resume-btn` | 再開 |
| 🏠 TITLE | `to-title-btn` | タイトルへ（盤面リセット） |

表示中: タイマー停止、BGM 一時停止。

## 結果画面（`#clear-overlay`）

クリア・TIME UP 共通。TIME UP 時は `.clear-card.timeup-result`（赤テーマ）。

| 表示 | id |
|------|-----|
| タイトル | `h2`（CLEAR! / TIME UP） |
| メッセージ | `clear-message` |
| スコア | `clear-score` |
| TIME BONUS | `clear-time-bonus` |
| CLEAR BONUS | `clear-clear-bonus` |
| ランク | `clear-rank` |
| NEW RECORD | `clear-new-record` |
| Extra 解放 | `clear-extra-unlock` |

| ボタン | id | 動作 |
|--------|-----|------|
| CONTINUE | `clear-retry-btn` | 再プレイ |
| 🏠 TITLE | `clear-title-btn` | タイトルへ |
| SHARE | `clear-share-btn` | 結果共有 |

## レイアウト・レスポンシブ（`style.css`）

| 条件 | 挙動 |
|------|------|
| 幅 ≥ 960px | `#game-body-box` 800×450px |
| 幅 < 960px | 16:9 を vmin/vmax でフィット |
| モバイル縦持ち | `#game-screen-wrapper` を 90° 回転（横画面レイアウト相当） |

ブロックの画面上サイズ（`getCubeSizeByDevice`）:

| SIZE | PC（幅≥960） | モバイル |
|------|-------------|----------|
| 2 | 80px | 65px |
| 4 | 56px | 46px |
| 6 | 40px | 35px |
| 8 | 30px | 26px |

## モバイル起動時（`script.js`）

- iOS **以外** かつ幅 < 960px: フルスクリーン要求・横向きロックを試行（拒否されても続行）
- ゲーム開始時: タイトルフェード → ステージイントロアニメーション（0° → 60°/-45°）

## OGP（`index.html`）

- タイトル: CUBE PUZZLE
- URL: `https://mook-hary.github.io/CUBE-PUZZLE/`
- 画像: `assets/ogp.png`

## 参照

- ゲームルール: [gameplay.md](gameplay.md)
