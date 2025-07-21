# Glibc-2.41 from azanella/clang

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

make && make DESTDIR=/lfs install

sed '/RTLDLIST=/s@/usr@@g' -i /lfs/usr/bin/ldd

echo 'int main(){}' | /lfs/tools/bin/x86_64-pc-linux-gnu-gcc -x c - -v -Wl,--verbose &> dummy.log
llvm-readelf -l a.out | grep ': /lib'
# [Requesting program interpreter: /lib64/ld-linux-x86-64.so.2]

grep -E -o "/lfs/lib.*/S?crt[1in].*succeeded" dummy.log
# /lfs/lib/Scrt1.o succeeded
# /lfs/lib/crti.o succeeded
# /lfs/lib/crtn.o succeeded

grep -B3 "^ /lfs/usr/include" dummy.log
# #include <...> search starts here:
#  /lfs/tools/lib/gcc/x86_64-pc-linux-gnu/15.1.1/include
#  /lfs/tools/lib/gcc/x86_64-pc-linux-gnu/15.1.1/include-fixed
#  /lfs/usr/include

grep 'SEARCH.*/usr/lib' dummy.log |sed 's|; |\n|g'
# SEARCH_DIR("=/lfs/tools/x86_64-pc-linux-gnu/lib64")
# SEARCH_DIR("=/lfs/tools/lib64")
# SEARCH_DIR("=/usr/local/lib64")
# SEARCH_DIR("=/lib64")
# SEARCH_DIR("=/usr/lib64")
# SEARCH_DIR("=/lfs/tools/x86_64-pc-linux-gnu/lib")
# SEARCH_DIR("=/lfs/tools/lib")
# SEARCH_DIR("=/usr/local/lib")
# SEARCH_DIR("=/lib")
# SEARCH_DIR("=/usr/lib");

grep "/lib.*/libc.so.6 " dummy.log
# attempt to open /lfs/usr/lib/libc.so.6 succeeded

grep found dummy.log
# found ld-linux-x86-64.so.2 at /lfs/usr/lib/ld-linux-x86-64.so.2
```