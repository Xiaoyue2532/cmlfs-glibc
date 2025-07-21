# linux-6.12.39 headers

```shell
mkdir build && cd build

make -f ../Makefile mrproper && make -f ../Makefile headers

find usr/include -type f ! -name '*.h' -delete

cp -rv usr/include /lfs/usr
```