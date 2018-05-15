# myTracks と Exiftool による後付けジオタギング

## TL;DR

1. iPhone 上で myTracks を動かして GPS 記録を収集する
2. GPS のついてないカメラで写真を撮影する
3. ExifTool を使って 1. と 2. のデータを合成し、GPS 位置情報付きの JPEG ファイルを得る





## iPhone 側の準備

### GPS ロガーソフトウェアの準備

ExifTool が対応する GPS ログファイルの形式を出力できれば何でも構わないが、筆者の環境では myTracks を使って gpx ファイルを出力する方法がうまくいった。

[myTracks - the GPS solution for all your Apple devices](http://www.mytracks4mac.info/)

### GPS 記録の収集開始

## カメラ側の準備

### 時計を合わせる

後で時刻によるマッチングをとるので、カメラ側の時計を正確に合わせる必要がある。iPhone 側は勝手に合っているので、特に気にしなくて大丈夫。




ジオタギング（Geotagging）

[ExifTool by Phil Harvey](https://sno.phy.queensu.ca/~phil/exiftool/)

