# 仕様として決めておきたいこと。

* 自動運転ではアプリ操作者はその場に居なくても運転は継続されること、という前提とするか？
* 中継器は一度にWayPointセットを1組しか保持できない、という前提で良いか？
* 中継器は一度に1台のハードとしかペアリングしない、という前提で良いか？

## どこまでの機能をアプリで行えるようにしておくべきか？

* 一番最初に行なう「ハード～中継器のBLEペアリング」の作業。
  - この作業は、中継器（RaspberryPi）にモニタ/キーボード/マウスを接続して行なうもの、と考えて良いか？
  - それともアプリからこのペアリングも行えるようにしておくのか？
* 中継器とハードのペアリングが切断してしまい自動復元しない場合の対応。
  - この場合も中継器にモニタ/キーボード/マウスを接続して行なうもの、と考えて良いか？


# 位置測位について

## 測位方式（2018/06/10決定）

* 屋内でのRTKを試す。
  - レピータを設置。
  - 理屈では、RTKだけでは「半径がレピータと移動体の距離、中心がレピータである球」の球面上のどこに移動体があるのかは確定できない形となるハズ。精度が10cmであれば、球面の厚さ10cmのどこかという感じ。
  - そこまで特定できれば、後はカルマンフィルタなどを使うことでかなり絞り込めるのではないか？
  - ただし屋内ではGPS信号が乱反射してしまって、正しいGPS信号が受信できない可能性も大きい。
* 屋内ではBLEビーコンを利用した位置計測も候補。
  

## 測位方式候補

* RTK
* ＋カルマンフィルタ
* BLE：通常ビーコン
* BLE：高指向性ビーコン
* ＋NFC

## 確認ポイント

* どの程度の精度で計測できる必要があるのか？

### 「誤差が1mだとマズい、10cmくらいに抑えないと」という話だったと思うが、何故だっけ？

### 「絶対座標？を取得できないとダメ」という話があったと思うが、何故だっけ？

* 例えば走行エリアの四隅にアンテナ（BLEビーコンなど）を配置し、それとの相対座標？が分かれば問題ないのでは？
* 参考＞　[Bluetoothの受信強度を用いた位置推定システム](https://ipsj.ixsq.nii.ac.jp/ej/?action=repository_action_common_download&item_id=108819&item_no=1&attribute_id=1&file_no=1)
