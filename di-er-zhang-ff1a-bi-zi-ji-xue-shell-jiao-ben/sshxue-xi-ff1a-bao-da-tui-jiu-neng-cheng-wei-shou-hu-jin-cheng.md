# 什么是守护进程？

我们先来聊聊普通进程和守护进程的区别。譬如我们开启一个会话，运行一个脚本/程序。从而产生了一个进程。

但一旦我们关闭结束这个会话。脚本/程序就会停止。进程就会消失！

守护进程指的就是，哪怕会话结束。它所产生的进程依然存在。如何实现呢？我们往下看。

---

先来证明一下，普通进程关闭会话就会结束进程的特点。

新建 me.c 文件：

```c
#include <stdio.h>
#include <unistd.h>

int main () {
    int pid;
    while (1) {
  
    }
    return 0;
}
```

![](/assets/24e9558c-cea8-46e1-9396-0dcee7abdf63import.png)

除非在 god 会话中主动 CTRL + C 中止。否则 god 会话是无法继续使用的。（当然如果你使用 CTRL+C 的话。代表程序中止，进程也会结束）。

此时我们试着将god会话直接关闭。再次查看时，发现进程已消失了~

![](/assets/8de25a3d-a730-4eb6-b169-52745000bae0import.png)

---

我们通过编写一个C语言程序来实现守护进程。原理特别简单，就是让使本进程成为“首领进程”。

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main() {
    int pid;
    pid = fork();
    if (pid > 0) exit(0);
    setsid();
    while (1) {

    }
    return 0;
}
```

编译并且运行一下。我们发现god会话依然是可用的。![](/assets/92d26da8-266a-4d4c-888a-de573915811aimport.png)现在我们关闭xshell的god会话。我们发现me进程依然是存活着。（sshd消失了，说明我真的关闭了一个会话）![](/assets/3542a708-7ac4-40cf-833a-66477b671718import.png)）



