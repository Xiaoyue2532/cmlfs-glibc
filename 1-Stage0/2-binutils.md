# binutils-2.44

```shell
mkdir build && cd build

../configure \
    --prefix="" \
    --exec-prefix="" \
    --sbindir=/bin \
    --libexecdir=/lib \
    --datarootdir=/_tmp \
    --target=x86_64-pc-linux-gnu \
    --disable-bootstrap \
    --disable-multilib \
    --enable-relro \
    --disable-default-execstack \
    --enable-default-hash-style="sysv" \
    --disable-initfini-array \
    --disable-werror \
    --disable-nls \
    --disable-rpath \
    --with-pic \
    --with-mmap \
    --with-sysroot=/ \
    --with-build-sysroot="/lfs/tools"

make \
    all-binutils \
    all-gas \
    all-ld

make \
    DESTDIR=/lfs/tools \
    install-strip-binutils \
    install-strip-gas \
    install-strip-ld
```