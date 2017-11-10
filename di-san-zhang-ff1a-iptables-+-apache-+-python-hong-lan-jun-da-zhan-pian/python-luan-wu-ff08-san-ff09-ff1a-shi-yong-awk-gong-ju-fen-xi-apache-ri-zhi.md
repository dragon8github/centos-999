当我们使用python模拟 一次请求若干次时。往往造成类似 DDOS 的迹象，所以我们需要通过 Apache 日志分析出几点：

1. 那个IP访问次数最多；
2. 把这个IP取出来；
3. 发邮件给管理员提醒。

---

# ln：创建文件链接

课程中的日志在  
/etc/httpd/logs/access\_log

首先，每次都要打下这么长的路径 好麻烦！

ln -s 源文件名  目标文件名

加入-s参数 的叫做软连接（好比windows中桌面的快捷方式）

譬如，我想把Apache日志文件放置在根目录下方便访问：

> $ cd /
>
> $ ln -s /etc/httpd/logs/access\_log httpdlog

![](/assets/cd2b9319-7bd4-4ae1-837a-54be988c6db0import.png)

---

# awk：宇宙最强的文本分析工具

![](/assets/8279159f-dc67-47a6-b8b0-20defb92f5b0import.png)

把文件逐行的读入，以空格为默认分隔符将每行切片，切开的部分再进行各种分析处理。

按行读取文件\(管道内容\)后，按空格自动分割。$1代表第一段内容，-F 指定分隔符（其实默认就是按空格分割）

> $ cat httpdlog \| awk '{print $1}'
>
> $ cat -F ' ' httpdlog \| awk '{print $1}'

---

# Sort 命令

![](/assets/2be39449-d20d-4748-879b-03f8397c81c6import.png)

排序，默认按ascii排序。

> $ sort &lt;文件&gt;

常用参数：

* -n 按数字形式排序 
* -r 倒排序

如 sort -nr 文件名 按数字排序 并且按倒排序。

往往我们是配合cat、awk、sort一起使用，而并不单独使用sort。

---

# Uniq 命令

![](/assets/cb22efb6-0726-4b93-ab8e-cf4cd9759c99import.png)

去除排序过的文件中的重复行，因此uniq经常和sort合用，所有的重复行必须是相邻的。

常用参数：

* -c或--count 在每列旁边显示该行重复出现的次数
* -d或--repeated 仅显示重复出现的行列



