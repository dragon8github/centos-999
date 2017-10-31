# SSH

Secure Shell 的缩写。它是一个协议，既可以远程登录，也可以用这个协议传送文件。

有个软件叫做 OpenSSH .其中它包含了两个程序：

1. SSHD 服务进程。以守护进程的方式运行；
2. SSH 客户端。用以连接SSH服务。

# 什么是进程？什么是守护进程？

ps命令重要参数如下：

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

# 普通进程

我们观察一下 god 来了解什么是进程。

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

