# 需求

有时我们的软件需要自动根据到网上去获取当前版本是否要更新。

如果需要更新则自动下载一些必要的文件。

---

# Curl：命令行下的浏览器

用GET的方式直接访问网页：

> $ curl [http://www.baidu.com](http://www.baidu.com)

curl很牛逼的地方是还能模拟POST提交：

> \# 注意，由于某些场景 curl 会出现统计信息。于是我们需要加入一个参数 -s\(静默，表示不输入任何额外统计信息\)。
>
> $  curl -d "password=123" [http://www.jtthink.com/test/update.php](http://www.jtthink.com/test/update.php) -s

---

# 数字比对大小

* gt  ： 是大于的意思（large than）;  
* lt   ： 是小于（less than）;
* eq ： 是等于（equal）;        
* ne ： 是不等于（not equal）;
* ge ： 是大于等于（large equal）;
* le  ： 是小于等于（less equal）。

---

# 解题思路

1、首先判断本地的version文件，读取;

2、用curl访问远程conf.txt,然后取第二行本地的 版本和远程版本进行比较，如果版本小则;

3、模拟post访问update.php，并获取需要下载的地址;

4、使用wget下载下来。

新建脚本文件 test.sh：

```php
LOCAL_VER=`cat version`
REMOTE_VER=`curl http://www.jtthink.com/test/conf.txt -s | sed -n '2p'`

if [ $LOCAL_VER -lt $REMOTE_VER ]
   then
   GET_UPDATE = `curl -d "password=123" http://www.jtthink.com/test/update.php -s`
   wget $GET_UPDATE
   echo "2" > version
fi
```

未完待续...

