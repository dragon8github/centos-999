# iptables：Linux核心网络安全的重要工具。

中文名：IP信息包过滤系统。通过一定的配置便能成为操作系统的防火墙（不仅仅是防火墙\)。

既然它名称有个tables说明和表有关，iptables中的四张表：

1. filter表 —— 实现包过滤；
2. nat表 —— 网络地址转换；
3. mangle表 —— 包重构\(修改\)；
4. raw表 —— 数据跟踪处理

看到这我们似乎已经觉得很难了，接下来我们将开始颠覆式简化学习。

---

# 查看 iptables 是否存在

Centos中他是自带的。在6.x系列中。可以用 `service iptables start` 来启动。

> $ service iptables start

如果不存在，可以使用yum安装并配置一下：

> $ yum install iptables
>
> $ yum install iptables-services -y
>
> $ cp /usr/libexec/iptables/iptables.init /etc/init.d/iptables
>
> $ service iptables start

![](/assets/0ed9d991-ec0d-41eb-8a6e-f19cf4655cb7import.png)

我们通过查看 `/etc/init.d/iptables` 脚本文件，发现它实际上是启动了

---

# 配置文件

默认的iptables 配置文件在 `/etc/sysconfig/iptables`为了方便学习，我们备份一下。然后清空这里面的内容然后重启。开始一步步学习。

由于配置文件内容被清空，实际上此时和没有iptables没什么区别。

---

# 两个重要的概念：input 和 output

![](/assets/05f4f25a-de27-4f27-ba36-7dd21c833e8fimport.png)

这个叫做：input

譬如我们用SSH连接服务器、访问网站等，都是把数据包发给服务器，然后等待服务器响应。

![](/assets/9d4a564f-0d2e-484a-bf2f-3bee2393d709import.png)这个叫做：output

服务器给我们响应，或者服务器主动向外发送数据这个过程就好比是output。懂了这两个概念，我们仿佛一下子入门了。

譬如我们要禁止别人访问我们的服务器 ，只要禁止INPUT就可以。

---

# 速装 apache 服务

为了更好的理解和贴合我们的web级。我们来快速装一个apache服务，速度的搭建一个静态网站。

> $ yum install httpd



