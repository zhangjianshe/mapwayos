# MAPWAY 操作系统的诞生

## 设置编译工具链

交叉编译工具链 是用来编译目标二进制代码的工具。我们选取 [i686-elf](https://wiki.osdev.org/ELF) 作为二进制可执行文件的格式.

使用 linux 开发环境，本身就具备了一个 32 位的 ELF 编译工具，但是这个工具链是为 linux 目标而存在的和我们今天的目标有点不兼容。

### 设置交叉编译工具，第一步需要安装依赖包

```shell
sudo apt-get install build-essential bison flex libgmp3-dev libmpc-dev libmpfr-dev texinfo libcloog-isl-dev libisl-dev qemu grub-common xorriso nasm grub-pc-bin

```

### 准备一些变量和目录

```shell
    export MAPWAY_PREFIX="$HOME/opt/cross"
    export MAPWAY_TARGET=i686-elf
    export PATH="$PREFIX/bin:$PATH"
    mkdir ~/src
```

~/src 目录是我们将要安装编译工具的目录

安装二进制工具包

```shell
cd ~/src
wget https://ftp.gnu.org/gnu/binutils/binutils-2.31.1.tar.xz
tar -xf binutils-2.31.1.tar.xz
rm binutils-2.31.1.tar.xz
mkdir build-binutils
cd build-binutils/
../binutils-2.31.1/configure --target=$TARGET --prefix="$PREFIX" \
--with-sysroot --disable-nls --disable-werror
make
make install
```

安装 gcc 编译器

```shell
    cd ~/src
wget https://ftp.gnu.org/gnu/gcc/gcc-8.2.0/gcc-8.2.0.tar.xz
tar -xf gcc-8.2.0.tar.xz
rm gcc-8.2.0.tar.xz
mkdir build-gcc
cd build-gcc
../gcc-8.2.0/configure --target=$TARGET --prefix="$PREFIX" \
--disable-nls --enable-languages=c,c++ --without-headers
make all-gcc
make all-target-libgcc
make install-gcc
make install-target-libgcc
```

输出编译器的路径
export PATH=$HOME/opt/cross/bin:$PATH

### 系统启动和链接
