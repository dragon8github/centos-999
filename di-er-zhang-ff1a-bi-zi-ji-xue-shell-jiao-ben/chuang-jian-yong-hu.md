# 需求

为了安全，该软件在运行时不推荐使用ROOT账户运行。所以我们会有个初始化shell脚本，来创建用户和初始化文件。

1. 判断用户是否存在\(譬如叫god\),没有则创建；
2. 创建后设置密码为123；
3. 把一些程序文件拷贝过去，并且除了root外，只能god用户运行\(最好是root也不能方便的运行\)。

---

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

