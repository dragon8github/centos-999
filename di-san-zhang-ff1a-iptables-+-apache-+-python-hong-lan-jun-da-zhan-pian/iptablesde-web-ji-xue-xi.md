# 速装 Apache 服务

![](/assets/8335fafd-1c9a-43e7-b380-8be82760ff88import.png)

为了更好的理解和贴合我们的web级。我们来快速装一个 apache 服务，迅速搭建一个静态网站。

> $ yum install httpd

可以通过rpm命令来查询相关的安装包信息

```
rpm -qal httpd
```

#### centos7.x 中是使用 systemctl 命令来控制的

将 httpd 加入开机启动的服务中：

> $ systemctl start httpd.service

或者依然可以使用CentOS 6.5的chkconfig命令。会自动转播

> $ chkconfig httpd
>
> 注意：正在将请求转发到“systemctl is-enabled httpd.service”。
>
> enabled

查看 httpd 服务是否开启

> $ systemctl is-enabled httpd.service

![](/assets/43c7a4e3-00c4-4251-af4e-83786632e76fimport.png)

查看 httpd 的服务情况

> $ systemctl status httpd.service

![](/assets/b22699b9-f3b8-4328-b162-231f40480273import.png)

---

# 找到 httpd 的配置文件

其中 `/etc/httpd/conf/httpd.conf`  文件夹就是httpd的配置文件。我是如何找到的呢？

> $ rpm -qal httpd \| grep ".conf"

或者可以使用：

```
$ httpd -V
```

根据输出的 `HTTPD_ROOT`和 `SERVER_CONFIG_FILE`就可以确定httpd.conf的路径了。

![](/assets/b5565ae4-27ab-4aa2-9cf7-31edcae93adaimport.png)

---

# 网站根目录

进入应该可以找到 `DocumentRoot "/var/www/html"`说明我们的默认站点默认路径就在这里。

> cat /etc/httpd/conf/httpd.conf \| grep -i DocumentRoot

![](/assets/7088f7ce-329c-4f2c-a600-0c4e9c070a8bimport.png)

---

# 网站端口

接下来查看一下端口\(虽然我知道默认肯定是80\)。

```
$ cat /etc/httpd/conf/httpd.conf | grep  -i listen
```

![](/assets/da0da257-0897-4cb9-9a21-1857342057ebimport.png)

---

# 新建一个测试页面

> $ cd /var/www/html
>
> $ echo 'hello httpd' &gt; index.htm

随后，我们通过ifconfig，查看eth0配置。得到虚拟机的ip地址（如192.168.128.128）。在外部利用[http://ip/index.htm](http://ip/index.htm) 就可以看到网站内容：

```
http://192.168.128.128/index.htm
```

![](/assets/asdas2312123import.png)

---

# 这说明了什么？

1、我们通过input向80端口的httpd软件发起了请求；

2、httpd这个软件通过output返回给我们响应。

