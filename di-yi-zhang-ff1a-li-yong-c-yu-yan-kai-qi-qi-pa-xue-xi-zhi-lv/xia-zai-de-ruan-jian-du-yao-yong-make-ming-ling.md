上节课我们用最简单的方法写了个C程序，那么如果把一些方法放到外部调用呢？  
譬如我有个外部函数库，有个显示我年龄的方法，规范的做法是：

1、定义一个 me.h 头文件

```c
int get_age();
```

2、定义一个me.c 文件

```c
int get_age()
{
   return 18;
}
```

3、修改一下 fuck.c 文件

```c
#include <stdio.h>
#include "me.h"
int main () {
  int age = get_age();
  printf("my age is %d", age);
  return 0;
}
```

多个文件一起编译

```c
$ gcc fuck.c me.c -o fuck
```

这时就纳闷了

如果有多个依赖多个文件每次编译起来岂不是很麻烦？

为啥我们下载了好多开源软件（如PHP）没让我们执行什么gcc命令呢？

有没有一键编译的做法呢？譬如都是输入 make  就自动编译了呢？

---

下载和安装make

```
 $ yum install make
```

Makefile最简单写法

```
目标文件名:依赖文件

<tab> 你的命令
```

创建makefile

```
fuck:fuck.c me.c
        gcc fuck.c me.c -o fuck
```

使用make命令调用makefile

```
$ make
```

我们发现自动执行了 `gcc fuck.c me.c -o fuck`，fuck又文件出来啦~。

![](/assets/123133546和规范房GV成本vcnccbnc.png)

