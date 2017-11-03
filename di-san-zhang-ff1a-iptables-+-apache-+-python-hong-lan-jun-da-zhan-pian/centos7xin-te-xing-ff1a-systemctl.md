centos中service命令与/etc/init.d的关系

service httpd start 其实是启动了存放在/etc/init.d目录下的脚本。

但是centos7的服务管理改规则了。  
CentOS 7继承了RHEL 7的新的特性，例如强大的systemctl，  
而systemctl的使用也使得以往系统服务的/etc/init.d的启动脚本的方式就此改变，  
也大幅提高了系统服务的运行效率。但服务的配置和以往也发生了极大的不同，  
说实在的，变的简单而易用了许多。

---

CentOS 7的服务 systemctl 脚本存放在：`/usr/lib/systemd/`

有系统（system）和用户（user）之分

需要开机不登陆就能运行的程序，存在系统服务里，即：`/usr/lib/systemd/system`目录下

每一个服务以.service结尾，文本内容一般会分为3部分：\[Unit\]、\[Service\]和\[Install\]。

譬如我们的httpd服务：

> $ yum install httpd
>
> $ cd /usr/lib/systemd/system
>
> $ ls \| grep httpd
>
> $ cat httpd.service

![](/assets/c4eba8b4-a2fe-47bf-9262-181b6f928d59import.png)

* \[Unit\]部分主要是对这个服务的说明，内容包括Description和After，Description用于描述服务，After用于描述服务类别;

* \[Service\]部分是服务的关键，是服务的一些具体运行参数的设置，这里Type=forking是后台运行的形式，PIDFile为存放PID的文件路径，ExecStart为服务的运行命令，ExecReload为重启命令，ExecStop为停止命令，PrivateTmp=True表示给服务分配独立的临时空间，注意：\[Service\]部分的启动、重启、停止命令全部要求使用绝对路径，使用相对路径则会报错;

* \[Install\]部分是服务安装的相关设置，可设置为多用户的服务脚本按照上面编写完成后，以754的权限保存在/usr/lib/systemd/system目录下，这时就可以利用systemctl进行测试了。

最后用以下命令将服务加入开机启动即可：

> $ systemctl enable httpd.service
>
> $ systemctl is-enabled httpd.service

![](/assets/9ba2cc15-c180-44da-ac20-187978283328import.png)

