未完待续。。。

```py
import urlib2

def gotoUrl():
    url = 'http://192.168.128.128/index.htm'
    response = urlib2.urlopen(url)
    html = response.read()
    print html

for x in range(1, 5):
    gotoUrl()
```



