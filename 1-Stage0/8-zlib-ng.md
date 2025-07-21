# zlib-ng

```shell
CC=/lfs/tools/bin/x86_64-pc-linux-gnu-gcc \
CXX=/lfs/tools/bin/x86_64-pc-linux-gnu-g++ \
./configure \
    --prefix=/lfs/tools \
    --libdir=/lfs/tools/lib \
    --zlib-compat

make -j`nproc --all` && make install

ln -sv libz.so.1.3.0.zlib-ng /lfs/tools/lib/libz.so.1.3.0
```