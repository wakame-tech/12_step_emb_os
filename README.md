# emb_os

# 環境構築
## ツールインストール
```
curl -O https://ftp.gnu.org/gnu/binutils/binutils-2.19.1.tar.bz2
curl -O https://ftp.gnu.org/gnu/gmp/gmp-5.0.5.tar.bz2
curl -O https://ftp.gnu.org/gnu/gcc/gcc-4.7.1/gcc-4.7.1.tar.bz2
curl -O http://repository.timesys.com/buildsources/m/mpc/mpc-0.9/mpc-0.9.tar.gz
curl -O https://www.mpfr.org/mpfr-3.1.1/mpfr-3.1.1.tar.gz
```

## binutils
```bash
./configure --target=h8300-elf --disable-nls --disable-werror
make
sudo make install
```

## gmp
```bash
./configure --prefix=/usr/local/gmp
make
make check
sudo make install
```

## mpfr
```bash
./configure --prefix=/usr/local/mpfr --with-gmp=/usr/local/gmp
make
make check
sudo make install
```

## mpc
```bash
./configure --prefix=/usr/local/mpc \
  --with-gmp=/usr/local/gmp \
  --with-mpfr=/usr/local/mpfr \
make
make check
sudo make install
```

## gcc
パッチを当ててから

```bash
./configure \
 --target=h8300-elf \
 --disable-nls \
 --disable-threads \
 --disable-shared \
 --enable-languages=c \
 --disable-werror
```

## h8write
```
curl -O http://mes.osdn.jp/h8/h8write.c
gcc -Wall -o h8write h8write.c
```

## PL2303 Serial driver
High Sierra は対応していない？
[mac-osx-pl2303](https://github.com/bjarnoldus/mac-osx-pl2303)

# 参考文献
- [1stステップ 開発環境の作成](http://ishikuro.hateblo.jp/entry/20120812/1344750799)
- [【学習メモ#1st】12ステップで作る組込みOS自作入門](https://www.slideshare.net/sandai/12step-1-14296356)