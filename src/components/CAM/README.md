# CAM の方向性

## メインプロセッサ

### 点群生成

#### Level1

半径方向に切り込んで 1 回転し、開始点に戻ったら軸方向に切り込み再度回転を繰り返すシンプルなパス。

断面構成点を単純に半径方向切り込み量オフセット。  
法線方向オフセット及びオフセット時の断面再構成なし。
→ このため、立壁形状では想定寸法にならない

回転軸方向 分割数 = MAX(ストック長/工具直径, ストック長/切り込みピッチ, MAX(断面構成点))

#### Level2

未定

### CL データフォーマット

Fusion360 のフォーマットを一部使用する

| 種類     |                                            |
| -------- | ------------------------------------------ |
| 高速移動 | `onRapid5D(_x, _y, _z, _a, _b, _c)`        |
| 直線移動 | `onLinear5D(_x, _y, _z, _a, _b, _c, feed)` |
| ドゥエル | `onDwell(seconds)`                         |
| 最初     | `onOpen()`                                 |
| 最後     | `onEnd()`                                  |
| コメント | `onComment(message)`                       |

## ポストプロセッサ

CL データを NC ファイルに変換する。

### 実施すること

- マシンの座標系への座標変換
- G コードへの変換
- カスタム G コードの挿入（ヘッダー、フッター）

#### オプション

- 360 度ごとに回転角度リセット
