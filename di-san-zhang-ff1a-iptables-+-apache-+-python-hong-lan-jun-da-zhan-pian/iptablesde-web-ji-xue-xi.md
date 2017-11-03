# 速装 apache 服务

![](/assets/8335fafd-1c9a-43e7-b380-8be82760ff88import.png)

为了更好的理解和贴合我们的web级。我们来快速装一个 apache 服务，迅速搭建一个静态网站。

> $ yum install httpd

可以通过rpm命令来查询相关的安装包信息

```
rpm -qal httpd
```

centos7 中是使用 systemctl 命令来控制的：

> $ systemctl start httpd-service
>
> $ systemctl status httpd-service

![](/assets/b22699b9-f3b8-4328-b162-231f40480273import.png)

将 httpd 加入自动启动的服务中：

> $ systemctl start httpd-service
>
> $ systemctl is-enabled httpd-service
>
> enabled

![](/assets/43c7a4e3-00c4-4251-af4e-83786632e76fimport.png)

其中 `/etc/httpd/conf/httpd.conf`  文件夹就是httpd的配置文件。我是如何找到的呢？

> $ rpm -qal httpd \| grep ".conf"

或者可以使用：

```
$ httpd -V
```

根据输出的 HTTPD\_ROOT 和 SERVER\_CONFIG\_FILE 就可以确定httpd.conf的路径了

![](/assets/b5565ae4-27ab-4aa2-9cf7-31edcae93adaimport.png)

进入应该可以找到 `DocumentRoot "/var/www/html"`说明我们的默认站点默认路径就在这里。

> cat /etc/httpd/conf/httpd.conf \| grep -i DocumentRoot

![](/assets/7088f7ce-329c-4f2c-a600-0c4e9c070a8bimport.png)

接下来查看一下端口\(虽然我知道默认肯定是80\)

```
$ cat /etc/httpd/conf/httpd.conf | grep  -i listen
```

![](/assets/da0da257-0897-4cb9-9a21-1857342057ebimport.png)

---



