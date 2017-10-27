# 设置临时变量

```py
# 赋值
myname=shenyi

# 打印
echo $myname 

# 删除
unset myname
```

![](/assets/sadfuyciaskdufkcajxcauoyafukchunmei.png)

# 上帝之手无所不及

修改god.c代码。加入新的头文件&lt;stdlib.h&gt;。

`getenv` 获取UNIX中的变量；`putenv` 设置UNIX中的变量。

```c
#include <stdio.h>
#include <stdlib.h>

int main (int argc, char* argv[]) {
    int i;
    char *result=getenv("PATH");
    printf("PATH is %s\n", result);

    putenv("myname=lee");    
    char *name=getenv("myname");
    printf("my name is %s\n", name);
      
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

上例中，我们分别获取并打印了全局变量$PATH和临时变量$myname，并且$myname还是通过 C 语言代码来设置的。

![](/assets/wq4q8we8s7d8a7sd8a7sd8a7s8d7asd87zx8z8z78v78v7.png)

