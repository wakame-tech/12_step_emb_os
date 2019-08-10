# emb_os

## 環境構築
方針を変えて ubuntu Docker container on Vagrant VM on Windows 10 Pro でビルド＆書き込み環境を構築したい

## USBtoSerial driver for macOS 見つかった!
[これ](https://www.ftdichip.com/Drivers/VCP.htm) の `Mac OS X 10.9 and above`　で `64bit` なやつ

## コンパイル & イメージ作成 & フラッシュROM書き込み
```
$ make
$ make image
$ sudo make write
../../tools/h8write/h8write -3069 -f20 kzload.mot /dev/cu.usbserial-FTRVI7J0
H8/3069F is ready!  2002/5/20 Yukio Mituiwa.
writing
WARNING:This Line dosen't start with"S".
Address Size seems wrong
WARNING:This Line dosen't start with"S".
Address Size seems wrong
.....
EEPROM Writing is successed.
```

## 参考文献
- [1stステップ 開発環境の作成](http://ishikuro.hateblo.jp/entry/20120812/1344750799)
- [【学習メモ#1st】12ステップで作る組込みOS自作入門](https://www.slideshare.net/sandai/12step-1-14296356)
- [12ステップで作る 組込みOS自作入門の開発環境をDockerで構築(gcc7系)](https://qiita.com/kjmatu/items/f9d25f38b3ccad180bae)
- [Windows環境でDockerコンテナにUSBウェブカメラを認識させてみる](https://www.unitrust.co.jp/7117)