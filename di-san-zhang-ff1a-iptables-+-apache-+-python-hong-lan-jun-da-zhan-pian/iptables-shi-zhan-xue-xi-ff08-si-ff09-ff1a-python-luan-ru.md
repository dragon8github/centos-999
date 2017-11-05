# Python的作用

1、很多shell脚本处理不了或者处理不方便的事情python可以干

2、python代码简单，配置简单。各种开源库多

3、效率高。性价比高

---

# 下载和安装Python 2.7x 版本

下载地址：[https://www.python.org/downloads/release/python-2711/](https://www.python.org/downloads/release/python-2711/)

![](/assets/asdadasdasd2312312312312import.png)我们选择XZ压缩版本的包进行下载：

> $ wget [https://www.python.org/ftp/python/2.7.11/Python-2.7.11.tar.xz](https://www.python.org/ftp/python/2.7.11/Python-2.7.11.tgz)

---

# Linux中的压缩

#### Xz压缩

xz 是一个使用 LZMA压缩算法的无损数据压缩文件格式 \(压缩率很高\)。

* -z 强制压缩；
* -d 解压缩.xz结尾的压缩文件。

#### tar 压缩

* tar zcvf xxx.tar.gz 文件夹或文件 \(打包\) ；
* tar zxvf xx.tar.gz 解压。

后缀如果没有 .gz 则代表没有 使用 gzip 压缩 则把参数的 z 去掉。

---

# Configure 这是什么？

其实就是一个shell脚本，用来生成makefile. 然而这个脚本又是通过 autoconf 这个软件来生成的.

由于比较复杂而且我们没有研究的必要性，所以我们果断选择跳过。

官方提供了安装方法

> $ ./configure

编译，需要等待点时间

> $ make

所谓安装，大致就是移动文件到某些特定的位置，你懂得。

> $ Make install



