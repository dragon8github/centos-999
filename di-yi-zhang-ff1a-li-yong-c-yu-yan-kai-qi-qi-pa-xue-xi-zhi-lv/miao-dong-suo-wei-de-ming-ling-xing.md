安装c、c++编辑器

```py
# 这是c编译器
yum install gcc

# 这是c++编译器
yum install gcc-c++
```

进入/root，新建一个.c文件夹： `vim fuck.c`

```c
#include <stdio.h>

int main () {
  printf('hello');
  return 0;
}
```



