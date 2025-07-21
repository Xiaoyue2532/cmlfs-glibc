## libstdc++ from gcc-15.1.1

```shell
cd build-gcc

make \
    all-target-libstdc++-v3

make \
    DESTDIR=/lfs/tools \
    install-strip-target-libstdc++-v3
```
