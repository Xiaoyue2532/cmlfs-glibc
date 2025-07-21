## libstdc++ from gcc-15.1.1

```shell
mkdir build-libstdcxx && cd build-libstdcxx

# clang cannot build libstdcxx
../libstdc++-v3/configure \
    --host=x86_64-pc-linux-gnu \
    --build=$(../config.guess) \
    --prefix=/usr \
    --disable-multilib \
    --disable-nls \
    --disable-libstdcxx-pch \
    --with-gxx-include-dir=/tools/x86_64-pc-linux-gnu/include/c++/15.1.0 \
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

make && make DESTDIR=/lfs install

rm -v /lfs/usr/lib/lib{stdc++{,exp,fs},supc++}.la
```
