# useradd：创建用户

首先我们执行which useradd 发现这是/usr/sbin 下面的工具。 那么 /bin 和 /usr/sbin 的区别在哪呢？

* /bin 包含了老大和小弟均可使用的工具 ；
* /usr \(unix software source\)代表安装的应用软件目录；
* /usr/bin 代表安装的软件（应用）中，一般情况下老大和小弟都可以使用。我们安装一些软件，默认就会在此；
* /usr/sbin代表安装的软件（应用）中，老大专门使用的工具。

> $ useradd jtthink

就会创建一个用户，并且会在Home目录下创建一个文件夹叫jtthink。

> $ userdel -r jtthink

删除用户，如果不加-r仅仅会删除用户，不会删除相关的文件，譬如/Home/jtthink。

---

# passwd：设置密码

> $ passwd jtthink

修改 &lt;jtthink&gt; 这个用户的密码。输入两次密码后一切ok。

---

> **$ cat /etc/shadow**
>
> jtthink:x:501:501::/home/jtthink:/bin/bash

0、用冒号分割;

1、第一位是用户名;

2、第二位是密码（看不到，加密了\);

3、第三位是用户ID（数字），普通用户都从500开始;

4、第四位是用户组ID（数字）;

5、第五位是备注;

6、第六位是用户主目录;

7、第七位是用户默认的shell。

---

# groupadd：创建用户组

创建用户组：

> $ groupadd &lt;组名&gt;

查看群组：

> $ cat /etc/group

新建的用户默认为创建同名用户组， 当这个组只有一个用户时你又执行了删除操作， 那么这个组也没了。

---

# 禁止用户shell登录

基本使用：

> usermod -s /sbin/nologin &lt;用户名&gt;

创建时也可以：

> useradd -s /sbin/nologin &lt;用户名&gt;



