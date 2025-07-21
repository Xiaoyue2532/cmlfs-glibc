# libatomic-chimera

```shell
CC=/lfs/tools/bin/x86_64-pc-linux-gnu-gcc  \
CXX=/lfs/tools/bin/x86_64-pc-linux-gnu-g++ \
AR=/lfs/tools/bin/x86_64-pc-linux-gnu-ar \
RANLIB=/lfs/tools/bin/x86_64-pc-linux-gnu-ranlib \
make PREFIX="/lfs/tools" -j`nproc --all`

make PREFIX="/lfs/tools" install
```