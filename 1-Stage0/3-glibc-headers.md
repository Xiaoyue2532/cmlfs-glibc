# glibc-headers

build libgcc-static need glibc headers and kernel headers

```shell
ln -sfv ../lib/ld-linux-x86-64.so.2 /lfs/lib64
ln -sfv ../lib/ld-linux-x86-64.so.2 /lfs/lib64/ld-lsb-x86-64.so.3

patch -Np1 -i ../glibc-2.41-fhs-1.patch
mkdir build && cd build

echo "rootsbindir=/usr/sbin" > configparms

# Add --disable-werror
../configure \
    --prefix=/usr \
    --host=x86_64-pc-linux-gnu \
    --build=$(../scripts/config.guess) \
    --enable-kernel=5.4 \
    --disable-werror \
    --disable-nscd \
    libc_cv_slibdir=/usr/lib \
    CC=/lfs/tools/bin/x86_64-pc-linux-gnu-gcc

make && make DESTDIR=/home/ubuntu/mussel/sources/glibc/glibc-2.41/build/_install install

cp -rv /home/ubuntu/mussel/sources/glibc/glibc-2.41/build/_install/usr/include /lfs/tools/
```