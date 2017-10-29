未完待续

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



