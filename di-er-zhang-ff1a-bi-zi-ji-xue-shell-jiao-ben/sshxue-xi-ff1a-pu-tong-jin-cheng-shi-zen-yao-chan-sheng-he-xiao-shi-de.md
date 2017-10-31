# SSH

Secure Shell 的缩写。它是一个协议，既可以远程登录，也可以用这个协议传送文件。

有个软件叫做 OpenSSH .其中它包含了两个程序：

1. SSHD 服务进程。以守护进程的方式运行；
2. SSH 客户端。用以连接SSH服务。

---

# ps命令

重要参数如下：

* -e： 显示所有进程

* -f ：显示程序之间关系

* -u ：显示指定用户下的进程

常见的使用如下：

显示所有的进程 并显示命令行

> ps -ef

显示正在内存中的进程

> ps aux

显示指定名称的进程信息

> ps -ef \| grep &lt;你要查询的字符串，如httpd、mysqld&gt;

---

# 进程的产生和消失

1、写了一个 shell 观察进程执行的列表情况

2、用c语言超简单的写了个程序,为了模拟写了sleep函数。

打开两个“终端”，一个切换到god用户，一个切换到root用户。我们通过root用户来观察god用户。默认如下： ![](/assets/9624e640-1a28-48c2-a94a-7cfc1c40194eimport.png)在god中新建一个测试脚本test.sh：

```php
echo "start"
sleep 5
echo "end"
```

运行它，并且尽快切换到root的账号下查看它的情况。

![](/assets/cee618ed-7704-420a-a124-b1267f5773d0import.png)

等待god输出end之后。我们再查看一下：

![](/assets/0e09a307-2e46-48de-a485-11e316fb197dimport.png)

我们发现程序一旦结束，进程就消失了。

---

# 无名的Shell 与 有名的C

但我们发现。进程名中的名字，不包含任何test.sh，只有bash和sleep。这说明进程不会把程序名打印出来。

除非你运行的的是c语言。那么就会打印出你程序的名字。

创建一个me.c 并且编译执行

```c
#include <stdio.h>

int main()
{
    printf("start\n");
    sleep(5);
    printf("end\n");
}
```

![](/assets/0f686ee7-5c7b-4ada-a9b5-7e2608767d96import.png)

我们就可以在进程中看到me了。

