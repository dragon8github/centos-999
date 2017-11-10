事实上，大部分非善意的访问都是通过工具来访问我们的网站的。

```py
import urllib2

def gotoUrl():
    url = 'http://192.168.128.128/index.htm'
    response = urlib2.urlopen(url)
    html = response.read()
    print html

for x in range(1, 5):
    gotoUrl()
```

# Apache 日志

> $ httpd -V
>
> 找到 HTTPD\_ROOT + /logs/access\_log 就是我们的 Apache 日志了。譬如笔者的目录在 /etc/httpd/logs/access\_log 
>
> $ cat /etc/httpd/logs/access\_log





