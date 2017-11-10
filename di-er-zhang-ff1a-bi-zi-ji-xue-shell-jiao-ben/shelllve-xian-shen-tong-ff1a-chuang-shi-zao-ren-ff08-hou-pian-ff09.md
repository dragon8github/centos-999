# grep：最强大的文本搜索工具

能使用正则表达式搜索文本，并把匹配的行打印出来。

这也是日常维护和系统部署时，用的最多的一个命令。

* grep &lt;你要检索的字符串&gt;  &lt;文件名&gt;
* grep &lt;正则&gt;  &lt;文件名&gt;
* cat &lt;文件名&gt; \| grep &lt;你要检索的字符串&gt;
* ls \| grep &lt;你要检索的字符串&gt;

常用参数

* -c：只输出匹配行的计数。
* -I：不区分大 小写\(只适用于单字符\)。
* -h：查询多文件时不显示文件名。
* -l：查询多文件时只输出包含匹配字符的文件名。
* -n：显示匹配行及 行号。

---

# 判断用户是否存在

添加一个用户

> **$ useradd jtthink**

使用grep命令搜索 "jtthink"

> **$ grep "jtthink" /etc/shadow**
>
> jtthink:!!:17469:0:99999:7:::
>
> **$ grep "jtthink" /etc/passwd**
>
> jtthink:x:1001:1001::/home/jtthink:/bin/bash

---

# 回顾需求

1. 判断用户是否存在\(譬如叫god\),没有则创建；

2. 创建后设置密码为123；

```php
USER_COUNT=`cat /etc/passwd | grep '^god:' -c`
USER_NAME='god'

# 添加用户
useradd $USER_NAME

# $? 显示最后命令的退出状态。0表示没有错误，其它任何值表明有错误(或执行不成功)
if [ $? -eq 0 ]
  then
      # 使用passwd 修改密码需要提示和确认，使用 --stdin 标准输入（键盘)强迫设置
      echo '123' | passwd $USER_NAME --stdin
      echo 'done'
  else
      echo 'error'
fi
```

![](/assets/edcbb753-d131-44a6-a05d-ff4a6fc3412eimport.png)

如果用户已存在的情况如图所示：

![](/assets/cb5264ff-0fd5-48d0-91ba-bcf793afbd08import.png)

---

可以看到，如果用户存储的情况，会报出错误信息：‘useradd：用户“god”已存在  
’

我们已经使用 `if [ $? -eq 0 ]` 使程序尽可能避免出错了。但我们还希望连错误提示也屏蔽掉。

# /dev/null ： UNIX中的黑洞

/dev/null 代表一个空设备。好比是个垃圾像、回收站、黑洞。

所谓黑洞，就是任何内容输入"&gt;"、“&gt;&gt;”都会被吸收而无效化。

> **$ useradd god**
>
> useradd：用户“god”已存在
>
> **$  useradd god 2&gt; /dev/null**
>
> （没有任何错误提示）

这里的2指的是错误提示，如果是1，那么就是正常的输出。譬如：

> **$ echo 123 1&gt; abc.txt**
>
> **$ cat abc.txt**
>
> 123

那如果一个正常输出的命令，我传入一个2（错误提示）呢？我们可以试试，其实是没有任何输出的

> **$ echo 123 2&gt; abc.txt**
>
> **$ cat abc.txt**
>
> （没有任何内容，因为命令没有任何报错提示）

如果我们希望无论错误还是正确的输出都被忽略的话。还可以采用这种语法：

> $ echo 123 1&gt; /dev/null 2&gt;&1

这里的2&gt;&1的意思是，让2&gt;参照第一个参数（/dev/null）的配置即可。是一种缩写啦。其实等同于这样:

> $ echo 123 1&gt;/dev/null 2&gt;/dev/null

---

根据“黑洞”的知识点，我们可以修改代码，使其不报错：

```php
USER_COUNT=`cat /etc/passwd | grep '^god:' -c`
USER_NAME='god'

# 添加用户
useradd $USER_NAME 2>/dev/null

# $?显示最后命令的退出状态。0表示没有错误，其它任何值表明有错误(或执行不成功)
if [ $? -eq 0 ]
  then
      # 使用passwd 修改密码需要提示和确认，使用 --stdin 标准输入（键盘)强迫设置
      echo '123' | passwd $USER_NAME --stdin
      echo 'done'
  else
      echo 'error'
fi
```

这里的error只是god用户存在而输出我们的调试信息罢了。没什么影响。

![](/assets/0174322a-fa77-434e-b77d-2a0b0cdc472fimport.png)

