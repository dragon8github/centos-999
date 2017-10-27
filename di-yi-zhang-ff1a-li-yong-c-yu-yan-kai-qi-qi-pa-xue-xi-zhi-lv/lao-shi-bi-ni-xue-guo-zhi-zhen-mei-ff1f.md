# C里面的字符串

C 木有string 。不像java 直接定义一个String完事

![](/assets/C啊实打实大大212334435678hkhjkhjkhjkhjkhjkhjkhjkh.png)



譬如我们要输出一个字符\(单字符\)

```c
// 注意是单引号
char a = 'a'; 

// %c 代表 单字符, 字符串则是 %s, 十进制无符号整形是 %d, 输出指针是 %p
printf("is %c", a);
```



# 那我就是要用字符串呢？

c 提供了字符数组

```c
#include <stdio.h>

int main () {
    char *ch = “shenyi”;
    for(i=0; i < 6; i++)
    {
        printf("is %c \n", *ch);
        ch++;
    }
    return 0;
}
```




