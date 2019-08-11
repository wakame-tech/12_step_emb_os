# emb_os

## 環境構築
~~方針を変えて ubuntu Docker container on Vagrant VM on Windows 10 Pro でビルド＆書き込み環境を構築したい~~
macOS用のドライバ見つかったのでMBPで進めます

## USBtoSerial driver for macOS 見つかった!
[これ](https://www.ftdichip.com/Drivers/VCP.htm) の `Mac OS X 10.9 and above`　で `64bit` なやつ

## デバイスが認識されているか
```
$ ls /dev/cu*
/dev/cu.Bluetooth-Incoming-Port  /dev/cu.usbserial-FTRVI7J0
```

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

## シリアル接続
```
sudo cu -l /dev/tty.usbserial-FTRVI7J0
Connected.
Hello World!
Hello World!
Hello World!
Hello World!
Hello World!
```

🎉🎉🎉

# note
## section3
割り込みベクタの長さが本では `0x000100` だが リンカがエラー出すので `0x000120` にした.

#### ld.scr(抜粋)
```
MEMORY 
{
    romall(rx)  : o = 0x000000, l = 0x080000 /* 512KB */
    vectors(r)  : o = 0x000000, l = 0x000120 /* top of ROM */
    rom(rx)     : o = 0x000120, l = 0x07ff00

    ramall(rwx) : o = 0xffbf20, l = 0x004000 /* 16KB */
    data(rwx)   : o = 0xfffc20, l = 0x000300
    stack(rw)   : o = 0xffff00, l = 0x000000 /* end of RAM */
}
```

## section4
- 本では `cu` でファイル転送する場合 `load` のあとに `~C` と書いてあるがmacOSの場合は `~+`


## 参考文献
- [1stステップ 開発環境の作成](http://ishikuro.hateblo.jp/entry/20120812/1344750799)
- [【学習メモ#1st】12ステップで作る組込みOS自作入門](https://www.slideshare.net/sandai/12step-1-14296356)
- [12ステップで作る 組込みOS自作入門の開発環境をDockerで構築(gcc7系)](https://qiita.com/kjmatu/items/f9d25f38b3ccad180bae)
- [Windows環境でDockerコンテナにUSBウェブカメラを認識させてみる](https://www.unitrust.co.jp/7117)