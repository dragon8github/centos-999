# 需求

有时我们的软件需要自动根据到网上去获取当前版本是否要更新。

如果需要更新则自动下载一些必要的文件。

---

# Curl：命令行下的浏览器

用GET的方式直接访问网页：

> $ curl [http://www.baidu.com](http://www.baidu.com)

curl很牛逼的地方是还能模拟POST提交：

> $  curl -d "password=123" http://www.jtthink.com/test/update.php -s

---



