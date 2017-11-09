# iptables：Linux 核心网络安全的重要工具。

中文名：IP信息包过滤系统。通过一定的配置便能成为操作系统的防火墙（不仅仅是防火墙\)。

![](/assets/阿打算的11212121import.png)

既然它名称有个tables说明和表有关，iptables中的四张表：

1. filter表 —— 实现包过滤；
2. nat表 —— 网络地址转换；
3. mangle表 —— 包重构\(修改\)；
4. raw表 —— 数据跟踪处理。

看到这我们似乎已经觉得很难了，接下来我们将开始颠覆式简化学习。

---

# 两个重要的概念：input 和 output

![](/assets/05f4f25a-de27-4f27-ba36-7dd21c833e8fimport.png)

这个叫做：input

譬如我们用SSH连接服务器、访问网站等，都是把数据包发给服务器，然后等待服务器响应。

![](/assets/9d4a564f-0d2e-484a-bf2f-3bee2393d709import.png)这个叫做：output

服务器给我们响应，或者服务器主动向外发送数据这个过程就好比是output。懂了这两个概念，我们仿佛一下子入门了。

譬如我们要禁止别人访问我们的服务器 ，只要禁止INPUT就可以。

---

# 查看 iptables 是否存在

Centos中他是自带的。在6.x系列中。可以用 `service iptables start` 来启动。

> $ service iptables start

如果是 7.x 系列则不存在，需要手动安装一下：

> $ yum install iptables
>
> $ yum install iptables-services -y

**开启 iptables 服务：**

> $ systemctl start iptables.service

**设置开机启动服务：**

> $ systemctl enable iptables.service

![](/assets/0ed9d991-ec0d-41eb-8a6e-f19cf4655cb7import.png)

**检查是否开机启动服务：**

> $ chkconfig iptables
>
> 注意：正在将请求转发到“systemctl is-enabled iptables.service”。
>
> enabled

---

# 配置文件 与 清空配置

默认的iptables 配置文件在 `/etc/sysconfig/iptables`为了方便学习，我们备份一下。

> $ cp iptables iptables.bak

然后清空这里面的内容然后重启。开始一步步学习。由于配置文件内容被清空，实际上此时和没有 iptables 没什么区别。

> $ iptables -F
>
> $ iptables -X
>
> $ iptables -Z

存储配置并重启

> $ iptables-save /etc/sysconfig/iptables
>
> $ systemctl restart iptables

---

# 个人经验

1. 如果直接使用 iptables 命令， 如 `iptables -F` 就会立即生效，不需要 `systemctl restart iptables`；
2. 如果直接对`/etc/sysconfig/iptables`配置文件进行修改，就必须使用 `systemctl restart iptables` 来重启服务使重新读取配置生效；
3. 使用 `iptables -L -n` 可以查看情况；
4. 使用 `iptables-save > /etc/sysconfig/iptables` 用来保存当前配置。

---

传送门：

> [http://blog.csdn.net/l1028386804/article/details/50779761](http://blog.csdn.net/l1028386804/article/details/50779761)



