# 模拟一个功能

我们经常在网上下载一些软件。安装和配置好后需要我们配置一些环境变量，否则无法使用。

1、程序在运行时，默认要生成一个god.log文件，用于后面记录日志

2、那么生成在哪呢？于是我们要求用户必须设置一个永久环境变量 譬如叫做GOD\_PATH

---

1、/etc/profile 全局环境变量脚本文件，好比windows的系统环境变量。任何用户都可以访问到

2、我们在最后面加上一句话 ：

> GOD\_PATH=/god
>
> export GOD\_PATH

\(export用于设置环境变量，并传导到全局\)

3、重新读取文件，使其最新内容生效。

> $ source /etc/profile

source 命令是内建命令。用于在bash环境下读取和立即执行某文件中的命令

---

大功告成，这样一来所有的用户都可以读取到 $GOD\_PATH 这个变量了。

接下来回到 C 语言，利用 GOD\_PATH 输出日志。

本demo中用到了新的库 &lt;string.h&gt; 。显然是操作字符串的库。如何把字符串相加，用到3个函数：

* strcpy ：复制字符串；
* strcat ：连接字符串；
* strlen ：获取串长度。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

void makelogfile();

int main (int argc, char *argv[]) {
    makelogfile();
    int i;
    if (argc == 2) {
        if (strcmp(argv[1], "-version") == 0) {
            printf("god version is 1.0\n"); 
        } else {
            printf("%s\n",argv[1]);
        }
    }
	return 0;
}

void makelogfile () {
    // 获取 GO_PATH 全局变量
    char *god_path = getenv("GOD_PATH");
    if (god_path == NULL){
	    printf("can not find GOD_PATH");
	    return;
	} else {
        // 创建文件夹
        mkdir(god_path);
        // 定义日志文件名
        char *god_file_name = "/godlog.log";
        // 定义一个字符数组
        char god_file_path[strlen(god_path) + strlen(god_file_name)];
        // 复制（/god）
        strcpy(god_file_path, god_path);
        // 拼接 (/god/godlog.log)
        strcat(god_file_path, god_file_name);
        // 读取文件（暂不写入）
        FILE *fp = fopen(god_file_path,"w");
        // 关闭文件
        fclose(fp);
        printf("god log file make");
    }
}

```



