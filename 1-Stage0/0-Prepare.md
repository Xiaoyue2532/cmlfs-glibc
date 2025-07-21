# LFS

## Environment

Ubuntu 25.10 Questing

## Preparation

```shell
sudo apt install \
    bison flex texinfo python-is-python3 \
    clang-19 llvm-19 lld-19 \
    build-essential cmake ninja-build \
    ccache pigz

# Fix llvm-15 links
ln -sv ../lib/llvm-19/bin/llvm-ar /usr/bin/llvm-ar
ln -sv ../lib/llvm-19/bin/llvm-as /usr/bin/llvm-as
ln -sv ../lib/llvm-19/bin/llvm-nm /usr/bin/llvm-nm
ln -sv ../lib/llvm-19/bin/llvm-objdump /usr/bin/llvm-objdump
ln -sv ../lib/llvm-19/bin/llvm-objcopy /usr/bin/llvm-objcopy
ln -sv ../lib/llvm-19/bin/llvm-ranlib /usr/bin/llvm-ranlib
ln -sv ../lib/llvm-19/bin/llvm-strip /usr/bin/llvm-strip
ln -sv ../lib/llvm-19/bin/llvm-readelf /usr/bin/llvm-readelf
ln -sv ../lib/llvm-19/bin/llvm-size /usr/bin/llvm-size
ln -s ../lib/llvm-19/bin/clang-19 /usr/bin/clang
ln -s ../lib/llvm-19/bin/clang-19 /usr/bin/clang++

# Create symbol links so that clang can use configuration file
ln -s ../lib/llvm-19/bin/clang-19 /usr/bin/x86_64-pc-linux-gnu-clang
ln -s ../lib/llvm-19/bin/clang-19 /usr/bin/x86_64-pc-linux-gnu-clang++
ln -s ../lib/llvm-19/bin/ld.lld /usr/bin/ld.lld

# Acquire clang use lld linker by default
cat > /usr/lib/llvm-19/bin/x86_64-pc-linux-gnu.cfg << EOF
-fuse-ld=lld
EOF

# Use ccache to boost building
mkdir /home/ubuntu/.bin
ln -s /usr/bin/ccache /home/ubuntu/.bin/x86_64-pc-linux-gnu-clang
ln -s /usr/bin/ccache /home/ubuntu/.bin/x86_64-pc-linux-gnu-clang++
export PATH=/home/ubuntu/.bin:$PATH

# Change Ownership
mkdir -p /lfs/tools
chown -R ubuntu:ubuntu /lfs
```