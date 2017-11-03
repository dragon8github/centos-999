# 结束进程：杀杀杀

![](/assets/237a27c6-df5b-4ed6-99d9-773728bf8568import.png)

# pgrep：通过程序的名字来查询进程的工具

* 重要参数：-l 列出程序名和进程ID

> $ pgrep &lt;进程名 \| 表达式&gt;

使用示例：

> $ pgrep ^me$ -l

![](/assets/9e4c0bfa-5b5c-4221-8ac0-a06ac5133fd5import.png)

# pkill：根据进程名杀掉符合条件的所有进程

> $ pkill ^me$

![](/assets/93a45d7f-3e79-4a11-b6a3-6b119d7eca6fimport.png)

---

完整代码示例，以下代码展示了:

1. 如何定义和使用函数;
2. 如何接收传入的参数（xxoo代表开启 、ooxx代表关闭）， 获取方式依然是熟悉的$1;
3. 通过文件的形式防止重复执行服务;
4. 杀死（关闭）程序。

![](/assets/d2ac6e56-c212-406d-a796-af80ff61ad6eimport.png)

```php
#add for chkconfig
#chkconfig:35 80 10
#description:i am god
#processname:shenyid

# 只是一个防止重复执行的媒介文件而已
PID_FILE='/etc/shenyid.pid'

start () {
  # 防止重复执行
  if [ -f $PID_FILE ] 
        then
          echo 'god_me is already running'
      else
          # 生成文件来防止重复执行
          echo '123' > $PID_FILE
          # 启动我们的核心程序
          /home/god/me
          # 输出提示信息
          echo 'start god_me'
  fi
}

stop () {
   # 删除文件，既删除重复执行的标识
   rm $PID_FILE -f
   # 删除我们的进程
   pkill ^me$
   # 输出提示信息
   echo 'god_me is stoped'
}

case $1 in
   xxoo)
      start
   ;;
   ooxx)
      stop
   ;;
   *)
      echo 'unknown'
   ;;
esac
```

调用示例：

> $ service shenyid xxoo

根据我们的逻辑，输入xxoo参数就是&lt;开启&gt;的意思，并且调用了`/home/god/me`程序，然后再添加`'/etc/shenyid.pid'`文件来防止重复，然后我们查看一下进程。发现 /home/god/me 程序已经启动了：

![](/assets/ff6e4e3a-3164-4f67-b93a-e4a9974a4631import.png)

> $ service shenyid ooxx

根据我们的逻辑，输入xxoo参数就是&lt;关闭&gt;的意思，并且杀死了/home/god/me程序，然后再删除'/etc/shenyid.pid'文件，然后我们查看一下进程。发现 /home/god/me 程序已经消失了。

![](/assets/33228c2d-c046-4c8a-88b2-60cf7023a665import.png)

