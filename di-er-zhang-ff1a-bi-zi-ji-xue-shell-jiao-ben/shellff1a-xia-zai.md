未完待续

```php
RAR_FILE='http://www.jtthink.com/test/d.rar'
CONF_FILE='http://www.jtthink.com/test/conf.txt'
ZIP_FILE='d.zip'

if [ ! -f $ZIP_FILE ]
    then
        wget -O $ZIP_FILE $RAR_FILE
        echo 'd.zip is downloaded'
fi

if [ ! -f 'licence' ]
    then 
        wget $CONF_FILE
        sed -n '1p' conf.txt >licence
        echo 'licence created'
fi

rm -f conf.txt
echo 'init done'
```



