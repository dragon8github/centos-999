# 上帝降临

> $ mkdir /home/lee/god && vim /home/lee/god/god.c

```js
#include <stdio.h>

int main (int argc, char* argv[]) {
    int i;
    if (argc == 2) {
      if (strcmp(argv[1], "-version") == 0) {
        printf("god version is 1.0\n");
      } else {
        printf("%s\n", argv[1]);
      }
    }
    return 0;
}
```

创建make && makefile：

> $ vim /home/lee/god/makefile

```c
god: god.c
        gcc god.c -o god
```

测试一下是否一切正常：

> **$ make **
>
> gcc god.c -o god
>
> **$ ./god -version**
>
> god version is 1.0
>
> **$ ./god fuck**
>
> fuck

# C 语言里面的字符比较函数：strcmp

```c
// strcompare
int strcmp(const char *s1, const char *s2)
```

* 若s1 == s2，则返回零；
* 若s1 &gt; s2，则返回正数；
* 若s1 &lt; s2，则返回负数；
* 字符串大小的比较是以 ASCII 码表上的顺序来决定。

---

# 抛砖引玉的使用which

which 命令可以根据字符串查找软件存储的环境变量位置。

> **$ which echo**
>
> /usr/bin/echo

如上，我们得知echo命令（程序）存放位置在 /usr/bin/echo 中。

那这时候我们输入一个不存在环境变量的命令会如何呢？譬如 god：

> $ which god
>
> /usr/bin/which: no god in \(/usr/local/bin:/usr/local/sbin:/usr/bin:/usr/sbin:/bin:/sbin:/home/lee/.local/bin:/home/lee/bin\)

每个人配置不一样，输出的结果也不一样。总之我们得到了一个环境变量位置的列表。

我们可以把god放置在任意一个位置\(如/usr/bin\)。就可以在全局访问了。

---



