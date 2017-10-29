# 需求

譬如某一天我们做了一个很屌的软件。 有时我们的软件需要用户依赖一些其他软件，如果没有则要自动去下载。

1、写一个shell脚本；

2、判断当前目录是否存在d.zip, 如果不存在则从网上下载，并存储为d.zip；

3、判断当前目录是否存在 licence 文件，如果不存在则从网上下载 conf.txt, 读取第一行，保存为licence文件名。

---

# Wget：使用率最高的Linux下载工具

使用非常简单。

wget 命令后加上网址即可将内容下载到当前目录，并以网址最后一个/后的字符串作为文件名。

> #### ** $ wget **[http://www.jtthink.com/test/d.rar](http://www.jtthink.com/test/d.rar)
>
> d.rar
>
> #### **$ wget **[http://www.jtthink.com/test/d.rar?a=123](http://www.jtthink.com/test/d.rar?a=123)
>
> d.rar?a=123

wget -O 你喜欢的文件名、指定目录

> #### **$ wget -O fuck.zip wget **[http://www.jtthink.com/test/d.rar](http://www.jtthink.com/test/d.rar)
>
> fuck.zip

---

# Sed：最强大的文件处理工具

主要是以行为单位进行处理，可以将数据行进行替换、删除、新增、选取等特定工作。**不学sed不能称之为会Linux**

读取文件并显示第x行：

* sed -n ‘1p’ 文件名  ;
* 1p代表第一行,2p代表第二行，依次类推  ;
* sed -n ‘1,2p’ 文件名，读取第1到第2行  ;
* sed -n ‘$p’ 文件名 读取最后一行。

---

test.sh：

```php
RAR_FILE='http://www.jtthink.com/test/d.rar'
CONF_FILE='http://www.jtthink.com/test/conf.txt'
ZIP_FILE='d.zip'

# 如果d.zip不存在，那么下载它
if [ ! -f $ZIP_FILE ]
    then
        wget -O $ZIP_FILE $RAR_FILE
        echo 'd.zip is downloaded'
fi

# 如果文件不存在，那么下载它并且读取第一段文本
# 然后再新建licence文件，最后往licence文件中插入该段文本
if [ ! -f 'licence' ]
    then 
        wget $CONF_FILE
        sed -n '1p' conf.txt >licence
        echo 'licence created'
fi

# conf.txt文件完成任务后，深藏功与名的离开了人世
rm -f conf.txt
echo 'init done'
```



