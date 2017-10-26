安装c、c++编辑器

```py
# 这是c编译器
yum install gcc

# 这是c++编译器
yum install gcc-c++
```

进入/home/&lt;用户名：lee&gt;，新建一个.c文件夹： `vim fuck.c`

```c
#include <stdio.h>

int main () {
  printf("hello");
  return 0;
}
```

编译并输出一个可执行文件

```js
gcc fuck.c -o fuck
```

本地就生成一个可执行的文件fuck了

![](/assets/1235467687654465567.png)

```py
# 运行该文件，也可以使用绝对路径 /home/lee/fuck 来运行，这里使用相对路径 ./ 来运行
./fuck
```

执行该文件，输出hello

---

将fuck文件移动到/bin命令文件夹中去。这样我们在任意地方都可以访问到它了。再也不需要加入相对或绝对路径

```
mv /home/lee/fuck /bin/
```

这时候再从任意地方运行 fuck 命令，都可以打印出hello

![](/assets/ads864ijnxvccfuck.png)

![](/assets/adsszzczxcwqeqweqweq.png)

