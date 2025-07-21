# libgcc-shared from gcc-15.1.1

```shell
make -C x86_64-pc-linux-gnu/libgcc distclean

make \
    enable_shared=yes \
    all-target=libgcc

make \
    DESTDIR=/lfs/tools \
    install-strip-target-libgcc
```