# uboot-ssd20x
sigmstar SSD201/SSD202 uboot

# 安装依赖
ubuntu 16.04.7 64位系统

````sh
sudo apt-get install subversion build-essential libncurses5-dev zlib1g-dev gawk git ccache \
		gettext libssl-dev xsltproc libxml-parser-perl \
		gengetopt default-jre-headless ocaml-nox sharutils texinfo
sudo dpkg --add-architecture i386
sudo apt-get update
sudo apt-get install zlib1g:i386 libstdc++6:i386 libc6:i386 libc6-dev-i386
````

# 下载代码
1. 下载主工程代码
```
git clone https://github.com/wireless-tag-com/uboot-ssd20x.git
```

# 安装toolchian

1. 下载toolchain
链接：https://pan.baidu.com/s/1SUk1a-drbWo1tkHQzCgchg 
提取码：1o3d 

2.  解压缩toolchain

```
sudo tar wt-gcc-arm-8.2-2018.08-x86_64-arm-linux-gnueabihf.tag.gz -xvf -C /opt/
```

3. 设置环境变量，修改 ~/.profile文件, 将下面这行添加到文件末尾
```
PATH="/opt/gcc-arm-8.2-2018.08-x86_64-arm-linux-gnueabihf/bin:$PATH"
```

手动生效环境变量
```
source ~/.profile
```

测试交叉工具链
```
arm-linux-gnueabihf-gcc --version
```


# 编译

1. 生成机型配置文件

```
declare -x ARCH="arm"
declare -x CROSS_COMPILE="arm-linux-gnueabihf-"
make qmsd_spinand_defconfig
```

| 机型名 | 说明            |
| ------ | --------------- |
| qmsd_nor_defconfig | NOR FLASH |
| qmsd_spinand_defconfig | SPI NAND FLASH|

2. 编译

```
make clean; make -j4 && make
```

3. 编译产物

| 文件名                   | 说明                 |
| ------------------------ | -------------------- |
| u-boot.xz.img.bin    | NOR FLASH            |
| u-boot_spinand.xz.img.bin      | SPI NAND FLASH |


