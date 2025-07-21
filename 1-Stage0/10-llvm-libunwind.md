# llvm-libunwind

```shell
mkdir build-unwind && cd build-unwind

cmake \
    -G Ninja \
    -Wno-dev \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX="/lfs/tools" \
    -DCMAKE_INSTALL_OLDINCLUDEDIR="/lfs/tools/include" \
    -DCMAKE_C_COMPILER="/lfs/tools/bin/x86_64-pc-linux-gnu-gcc" \
    -DCMAKE_CXX_COMPILER="/lfs/tools/bin/x86_64-pc-linux-gnu-g++" \
    -DCMAKE_AR="/lfs/tools/bin/x86_64-pc-linux-gnu-ar" \
    -DCMAKE_NM="/lfs/tools/bin/x86_64-pc-linux-gnu-nm" \
    -DCMAKE_RANLIB="/lfs/tools/bin/x86_64-pc-linux-gnu-ranlib" \
    -DLIBUNWIND_INSTALL_HEADERS=ON \
    -DLIBUNWIND_ENABLE_CROSS_UNWINDING=ON \
    -DLIBUNWIND_ENABLE_STATIC=OFF \
    -DLIBUNWIND_HIDE_SYMBOLS=ON \
    ../libunwind
```