# binutils-2.44

```shell
../configure \
    --prefix=/lfs/tools \
    --with-sysroot=/lfs \
    --target=x86_64-pc-linux-gnu \
    --enable-default-hash-style=gnu \
    --enable-gprofng=no \
    --enable-new-dtags \
    --disable-werror \
    --disable-nls \
    CC=x86_64-pc-linux-gnu-clang \
    CXX=x86_64-pc-linux-gnu-clang++ \
    OBJDUMP=llvm-objdump \
    OBJCOPY=llvm-objcopy \
    READELF=llvm-readelf \
    RANLIB=llvm-ranlib \
    STRIP=llvm-strip \
    SIZE=llvm-size \
    NM=llvm-nm \
    AR=llvm-ar \
    AS=llvm-as \
    LD=ld.lld
```