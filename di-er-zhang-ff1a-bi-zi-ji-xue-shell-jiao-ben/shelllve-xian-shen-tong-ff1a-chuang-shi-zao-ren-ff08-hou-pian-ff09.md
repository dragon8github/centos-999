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



