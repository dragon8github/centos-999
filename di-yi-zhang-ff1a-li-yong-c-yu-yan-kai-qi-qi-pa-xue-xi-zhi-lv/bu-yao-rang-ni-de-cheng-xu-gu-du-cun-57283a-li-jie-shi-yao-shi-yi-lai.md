# 什么是动态链接库？

其实我们早就接触过动态链接库

1、Windows上是dynamic   link   library \(DLL\),后缀？xxx.dll嘛！

2、UNIX或Linux上是Shared   Library .后缀是啥? xxx.so嘛！

为了好理解我们暂时不要拘泥于动态库的形式 ，我们就理解为**把其封装为类库，其他程序都可以动态调用就完事了。**



# 把me.c编译成”dll”

无比简单的编译过程：

> $ gcc -shared me.c -o libme.so

手动指定我的动态链接库在哪

> $ gcc –L /home/lee/ -l me fuck.c -o fuck

-L 动态链接库的文件夹位置   

-l 动态链接库的库名 \(去除最前面的 lib 和 .so 就是库名\)

---

# 使用 ldd 命令：探测程序需要多少个依赖文件

> $ ldd fuck

![](/assets/asda566745yjb.png)



