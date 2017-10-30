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

1、首先判断本地的 version 文件，读取;

2、用curl访问远程conf.txt,然后取第二行本地的 版本和远程版本进行比较，如果版本小则;

3、模拟post访问update.php，并获取需要下载的地址;

4、使用wget下载下来。

test.sh：

```php
REMOTE_VER=`curl http://www.jtthink.com/test/conf.txt -s | sed -n '2p'`

# 定义函数
function download () {
        # 获取服务器最新资源的下载地址
        # 注意神坑：``的等号两边不能有空格。千万不要手贱！
        # 这里的$1就是传递进来参数的"password=123"
        GET_UPDATE=`curl -d $1 http://www.jtthink.com/test/update.php -s`
        # 根据下载地址获取最新的资源到本地
        wget $GET_UPDATE
        # 将最新的版本信息写入version文件（这里写死了）
        echo 2 > version
}

# 如果 version 文件不存在 或者 当前版本低于服务器最新版本
if [ ! -f version ] || [ `cat version` != $REMOTE_VER ]
    then
        # 更新下载最新的版本
        download "password=123"
fi
```

![](/assets/5d3ddff7-5632-411e-a245-0adaa896a82eimport.png)

