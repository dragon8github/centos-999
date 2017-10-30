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

如果用户已存在的情况：

![](/assets/cb5264ff-0fd5-48d0-91ba-bcf793afbd08import.png)

