# MAPWAY 操作系统的诞生

## 设置编译工具链

交叉编译工具链 是用来编译目标二进制代码的工具。我们选取 [i686-elf](https://wiki.osdev.org/ELF) 作为二进制可执行文件的格式.

使用 linux 开发环境，本身就具备了一个 32 位的 ELF 编译工具，但是这个工具链是为 linux 目标而存在的和我们今天的目标有点不兼容。

设置交叉编译工具，第一步需要安装依赖包

···
sudo apt-get install build-essential bison flex libgmp3-dev libmpc-dev libmpfr-dev texinfo libcloog-isl-dev libisl-dev qemu grub-common xorriso nasm grub-pc-bin
···
