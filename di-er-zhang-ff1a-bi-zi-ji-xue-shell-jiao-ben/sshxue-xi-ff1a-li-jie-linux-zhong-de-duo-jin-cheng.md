# 什么是父进程？

Linux 开机后就会运行第一个进程/sbin/init  
 。

我们通过 `ps -ef` 会发现，进程是一级一级派生的。  
最终的源头就是  init （长老进程\)

每个新进程产生，需要有个父进程，来带领子进程运行。（这个子进程还可能再运行一个子进程\)。

这一长串的玩意儿可以成为进程组，其中还有首领进程。

`ps -ef`   
我们会发现，除了进程有PID，还有个PPID （父进程ID）

> ps --pid  &lt;pid&gt;
>
> ps --pid &lt;ppid&gt;

# 开始玩一下多线程

我们加入新的头文件 &lt;unistd.h&gt;  使用 fork\(\);即可开启多线程了。然后重新编译一下` gcc me.c -o me`

```c
#include <stdio.h>
#include <unistd.h>

int main() {
    fork();
    printf("start \n");
    sleep(20);
    printf("end \n");
    return 0;
}
```

启动 ./me 然后观察一下进程。我们会发现进程变成了两个。而 ./me 也输出了两个 start 

![](/assets/2f6d0edc-06e0-4bdb-8a5d-ece472149d51import.png)

