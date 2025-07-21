# gcc-15.1.1

## Prepare source

```shell
wget https://ipv6.mirrors.ustc.edu.cn/gnu/mpfr/mpfr-4.2.2.tar.bz2 && \
    tar -xf mpfr-4.2.2.tar.bz2 && \
    rm mpfr-4.2.2.tar.bz2 && \
    ln -sf mpfr-4.2.2 mpfr

wget https://ipv6.mirrors.ustc.edu.cn/gnu/mpc/mpc-1.3.1.tar.gz && \
    tar -xf mpc-1.3.1.tar.gz && \
    rm mpc-1.3.1.tar.gz && \
    ln -sf mpc-1.3.1 mpc

wget https://ipv6.mirrors.ustc.edu.cn/gnu/gmp/gmp-6.3.0.tar.bz2 && \
    tar -xf gmp-6.3.0.tar.bz2 && \
    rm gmp-6.3.0.tar.bz2 && \
    ln -sf gmp-6.3.0 gmp

sed -e '/m64=/s/lib64/lib/' \ -i.orig gcc/config/i386/t-linux64
```

## Build

```shell
mkdir build-gcc && cd build-gcc

../configure \
    --prefix="" \
    --exec-prefix="" \
    --sbindir=/bin \
    --libexecdir=/lib \
    --datarootdir=/_tmp \
    --target="x86_64-pc-linux-gnu" \
    --disable-bootstrap \
    --enable-checking=release \
    --disable-multilib \
    --disable-fixed-point \
    --enable-languages=c,c++ \
    --disable-rpath \
    --disable-nls \
    --disable-gnu-indirect-function \
    --disable-initfini-array \
    --disable-gnu-unique-object \
    --disable-linker-build-id \
    --disable-libsanitizer \
    --disable-libssp \
    --enable-default-ssp \
    --enable-link-serialization=1 \
    --enable-host-pie \
    --enable-host-bind-now \
    --enable-default-pie \
    --disable-cet \
    --disable-werror \
    --disable-symvers \
    --disable-libstdcxx-pch \
    --enable-clocale=generic \
    --with-build-sysroot="/lfs/tools" \
    --with-sysroot=/ \
    --with-pic \
    --with-linker-hash-style="sysv" \
    --with-arch=x86-64 \
    --with-tune=generic

mkdir -p /lfs/tools/usr/include

make \
    all-gcc

CFLAGS='-pipe -g0 -O0' \
    CXXFLAGS='-pipe -g0 -O0' \
    LDFLAGS=-Wl,-s \
    make \
    enable_shared=no \
    all-target-libgcc

make \
  DESTDIR="/lfs/tools" \
  install-strip-gcc \
  install-strip-target-libgcc
```