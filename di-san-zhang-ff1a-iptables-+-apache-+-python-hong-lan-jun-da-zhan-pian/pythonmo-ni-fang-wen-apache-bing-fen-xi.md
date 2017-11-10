正常事实上，大部分非善意的访问都是通过工具来访问我们的网站的。

```py
import urllib2

def gotoUrl():
    url = 'http://192.168.14.121/index.htm'
    response = urllib2.urlopen(url)
    html = response.read()
    print html

for x in range(1, 5):
    gotoUrl()
```

调用示例，由于我们删除了第一行的解释器代码 `#!/usr/bin/python` ，所以需要手动指定解释器：

> $ /usr/bin/python ./test.py
>
> 或者
>
> $ python ./test.py

# ![](/assets/37377b6c-91ac-4b5e-ad6e-0cddd7eb405bimport.png)

# 注意

请确保 [http://192.168.14.121/index.htm](http://192.168.14.121/index.htm) 是你的虚拟机eth0网卡的ip。且可以正常访问。

---

# Apache 日志

> $ httpd -V
>
> 找到 HTTPD\_ROOT + /logs/access\_log 就是我们的 Apache 日志了。譬如笔者的目录在 /etc/httpd/logs/access\_log
>
> $ cat /etc/httpd/logs/access\_log

刚刚我们使用python访问了httpd。所以可以清晰的看到访问记录。

![](/assets/12321612831283123123import.png)

虽然我们虽然我们透过日志可以清晰的看出python行为。但真实的黑客并没有那么傻。肯定会使用某种方式伪装。

