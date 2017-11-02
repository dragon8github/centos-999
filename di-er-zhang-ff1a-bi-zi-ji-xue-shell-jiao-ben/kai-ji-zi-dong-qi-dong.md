我们做了一个丑陋的守护进程  
，那怎样让我们这个守护进程开机自启动、并且像服务那样运行呢？譬如我们常看到的：

> $ service mysqld start
>
> $ service httpd start

这样写看起来很有档次~~~~

---

在 /etc/init.d 下创建一个&lt;服务脚本&gt; shenyid

```php
#add for chkconfig
#chkconfig:35 80 10
#description:i am god
#processname:shenyid

/home/god/me
```

内容解析：

**80** 代表启动优先级，**10** 代表关闭优先级

**35** 指的是标准模式桌面模式会自动启动，一般也只需要开启35即可。其他等级代号  
如下：

* 0 – 关机
* 1 - 单用户模式 
* 2 - 多用户，但是没有NFS ，不能使用网络 
* 3 - 完全多用户模式\(标准模式）
* 4 - 保留 
* 5 - 桌面模式
* 6 - 重新启动 

`/home/god/me`是调用程序。事实上，除了上面（必填）注释之外。其他地方可以用来书写SHELL脚本代码。譬如 `echo 'i am god'`

---

# chkconfig：检查、设置系统的各种服务

--add &lt;服务名&gt;　增加所指定的系统服务；

--del &lt;服务名&gt;　 删除所指定的系统服务，不再由chkconfig指令管理；

--level   &lt;等级代号&gt; 　指定读系统服务要在哪一个执行等级中开启或关毕。

设置我们上面我们配置的服务脚本 **shenyid**

> $ chkconfig --add shenyid

然后查看我们的服务是否开启

> $ chkconfig

![](/assets/2c268585-f9b5-4b80-8c87-276476d57d2bimport.png)

---

# 启动我们的服务

> service shenyid start

于是按照逻辑，我们的服务就调用了 `/home/god/me`的程序（开启了一个线程）。

我们使用 `ps -ef | grep "god"`查看以下程序：

![](/assets/28ed1c1a-e552-4a73-b72f-fccf8361a61bimport.png)

# 如何关闭我们的服务从而停止我们的程序呢？

按照逻辑，命令是否应该这样书写：（用脚想都知道是不可能的！！！）

> service shenyid stop

可当我们这样输入之后，我们查看线程，却发现多了一个 /home/god/me 程序。

![](/assets/d4e5750b-a145-4c52-bc25-ca32122acfdeimport.png)

这是为什么呢？

事实上，无论是 start 还是 stop ，都对我们的服务脚本没有起到任何效果。仅仅是传递了参数进去。而我们的代码没有进行任何的逻辑区分。仅仅是无差别的运行了 /home/god/me 程序。并且还会重复运行！

* 我们应该如何获取参数呢？
* 如何停止或开启服务/程序呢？
* 如何防止重复运行呢？



