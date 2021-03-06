# やりたいこと

1. 実家を訪ねる時に、私が最近撮った写真を実家のテレビに映して、近況報告をスムーズにしたい
2. 遠い親戚を訪ねる時に、親戚宅のテレビを用いて、来られなかった人と繋ぐためのテレカンファレンスをしたい
3. 友人宅で家呑みする時に、私が契約しているdアニメストアなどのコンテンツを友人宅のテレビに映して一緒に観たい
4. ビジネスホテル宿泊の時に、備え付けのテレビをノートPCのセカンドディスプレイとして使いたい
5. 以上を実現する道具を、なるべく小型軽量にして持ち運びたい
6. 高齢者や幼児が転倒するリスクを低めるため、現地展開するケーブルは少なくしたい

なお、タブレットやノートPCの画面でも近いことは可能なものの、

* 老眼の人は近くのものを見るのが苦手
* 複数人で同時に見るのに適していない

ことから、あくまで大画面に映したいと思っている。

# 道具セット

執筆時点（2018/05）での道具セットは以下。

![tv_projection_tool_01](tv_projection_tool_01.jpg)

## ワイヤレスディスプレイアダプタ Anycast M9 Plus

Chromecast、AirPlay、Miracastなど複数の方式に対応した、ワイヤレスディスプレイアダプタ。

https://www.amazon.co.jp/dp/B078P1Q8SC/

## USB ACアダプター 1ポート 2A対応

ワイヤレスディスプレイアダプタの電源として。ワイヤレスディスプレイアダプタAnycastのマニュアルによれば2A対応が必要とのことで、そのようなものをダイソーで購入。

## USB延長ケーブル 3m

ワイヤレスディスプレイアダプタの電源が近くにあるとは限らないので、延長できるようにした。このケーブルは、現地で不要なら使わないことが望ましい。

## モバイルポーチ

以上を収納するためのポーチ。無印良品で購入。たぶん、本来の目的はペンケースだと思われる。

## （追加）HDMI切替器 2ポート

テレビのHDMI入力端子が凹型の場所にあり、ワイヤレスディスプレイアダプタを挿せないことがあったため、急遽購入。本来はHDMI延長ケーブルで良いため、御役御免の予定。

# トラブルシューティング

## HDMI端子周辺の形状と干渉

テレビのHDMI入力端子が凹型の場所にあり、ワイヤレスディスプレイアダプタを挿せないことがあった。

解決には短いHDMI延長ケーブルが適している。

## iPhoneの熱暴走

テレカンファレンスのため、iPhoneを充電しながらLINEビデオ通話を動かしAirPlay出力したところ、10分程度でiPhoneが過熱して使えなくなってしまった。充電をやめると少し持つようになったが、やはり時間が経つと過熱する。

解決に向けて、冷却を考えつつ固定する方法を考える必要がある。

## AirPlay切断

iPhoneの写真を（写真アプリやGoogleフォトアプリを用いて）映していたところ、何度かAirPlayが切断された。

切断の原因は不明だが、

* ワイヤレスディスプレイアダプタ用のUSB ACアダプターが今ひとつな可能性を考えて、別のものに換えて様子を見たい
* AnycastのWi-Fiは2.GGHz帯にしか対応していないので、将来的には別のワイヤレスディスプレイアダプタも試したい

## Miracastできない

Windows PCのワイヤレスディスプレイとしての接続は、一度は成功したことがあるが、今は接続できない。

原因はよく分らないが、

* 接続試行中にはディスプレイ側の表示が「Waiting for connection」から「Connection in progress」に変化したので、何らかの接続はできているようだ
* 接続試行中のPCで `ipconfig` を実施したところ、IPアドレスとして 192.168.137.1 が設定されていたので、DHCP関係の通信は問題ないと思われる
* 接続試行中のPCでWiresharkを用いたパケットキャプチャを試みたが、原因の究明に役立ちそうな情報は取得できていない
* 以下の記事は参考になるかも知れないので、これから確認したい
  https://answers.microsoft.com/ja-jp/windows/forum/windows_10-hardware/windows/28eb21ce-9e11-469e-be64-99865b8b3433

## モバイルルーターとの相性

ワイヤレスディスプレイアダプタAnycastは、自身がWi-Fiアクセスポイントになる方式のため、モバイルルーターとは相性がよくない。各端末は、モバイルルーターとAnycastに同時には接続できないので、テレカンファレンスなどの際には差し支えることがある。

4G回線に接続されたiPhoneでは、Anycastとインターネット接続の同時利用が可能だった。