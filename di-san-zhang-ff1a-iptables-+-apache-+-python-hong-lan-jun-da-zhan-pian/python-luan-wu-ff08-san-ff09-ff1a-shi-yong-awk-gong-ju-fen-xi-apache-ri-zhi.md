当我们使用python模拟 一次请求若干次时。往往造成类似 DDOS 的迹象，所以我们需要通过 Apache 日志分析出几点：

1. 那个IP访问次数最多；
2. 把这个IP取出来；
3. 发邮件给管理员提醒。

---

# 创建链接的工具 ln

课程中的日志在/etc/httpd/logs/access\_log首先，每次都要打下这么长的路径 好麻烦！

ln -s 源文件名  目标文件名

加入-s参数 的叫做软连接（好比windows中桌面的快捷方式）

譬如，我想把Apache日志文件放置在根目录下方便访问：

> $ cd /
>
> $ ln -s /etc/httpd/logs/access\_log httpdlog

![](/assets/cd2b9319-7bd4-4ae1-837a-54be988c6db0import.png)

---

# awk：宇宙最强的文本分析工具

把文件逐行的读入，以空格为默认分隔符将每行切片，切开的部分再进行各种分析处理。

---

未完待续....

