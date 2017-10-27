# 什么是动态链接库？

其实我们早就接触过动态链接库

1、Windows上是dynamic   link   library \(DLL\),后缀？xxx.dll嘛！

2、UNIX或Linux上是Shared   Library .后缀是啥? xxx.so嘛！

为了好理解我们暂时不要拘泥于动态库的形式 ，我们就理解为**把其封装为类库，其他程序都可以动态调用就完事了。    **

---

# 把me.c编译成”dll”

无比简单的编译过程：

> $ gcc -shared me.c -o libme.so

编译 fuck 程序并且手动指定我的动态链接库在哪

> $ gcc -L /home/lee/ -l me fuck.c -o fuck

-L 动态链接库的文件夹位置

-l 动态链接库的库名 \(去除最前面的 lib 和 .so 就是库名\)

---

# 使用 ldd 命令：探测程序需要多少个依赖文件

> $ ldd fuck

![](/assets/asda566745yjb.png)

我们发现我们的 fuck 程序依赖四个文件，但 libme.so 文件无法找到。

其实Linux和windows一样，有个类似system32的系统库文件夹。各种公共类库都放于此

CentOS中有和windows很类似的两个存放公共库的文件夹

/lib：内核级

/usr/lib：用户系统级

/usr/lib64/：64位系统才有

我们将生产的so文件，放置在公共库的位置

> $ gcc -L /home/lee/ -l me fuck.c -o fuck

---

# 使用 ldconfig 重新更新缓存

> $ ldconfig

---

# 大功告成

这时候我们的 ./fuck 就又能正常运行了。哪怕当前目录中没有 me.c 和 me.h

![](/assets/1231253412834812544124381243.png)

---

修改我们的makefile

```
fuck:fuck.c libme.so
        gcc -L ./ -l me fuck.c -o fuck
libme.so:me.c
        gcc -shared me.c -o libme.so
install:
        cp ./libme.so /usr/lib
        ldconfig
```

先使用 `make` 命令编译我们的软件，再使用 `make install` 命令将 .so 文件移动到 /lib 中去

> $ make && make install

![](/assets/asdasdasd45456456525234234234234234234234.png)

