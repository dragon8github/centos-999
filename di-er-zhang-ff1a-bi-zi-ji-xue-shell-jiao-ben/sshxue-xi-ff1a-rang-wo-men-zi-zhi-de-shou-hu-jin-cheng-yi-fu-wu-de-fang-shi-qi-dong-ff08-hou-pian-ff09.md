# 结束进程：杀杀杀

![](/assets/237a27c6-df5b-4ed6-99d9-773728bf8568import.png)

# pgrep：通过程序的名字来查询进程的工具

* 重要参数：  -l 列出程序名和进程ID

> $ pgrep &lt;进程名&gt;
>
> $ pgrep god -l

# pkill：根据进程名杀掉符合条件的所有进程









---

本节课我们不再使用 /home/god/me 程序来启动和测试我们的服务。我们使用简单的输出代码来替代。

以下代码展示了:

1. 如何定义和使用函数;
2. 如何接收传入的参数（以 xxoo 和 ooxx为例）， 获取方式依然是熟悉的$1;
3. 通过文件的形式防止重复执行服务;
4. 杀死（关闭）程序。

![](/assets/d6a525a9-7304-4493-9202-400922ce7fedimport.png)

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
   rm $PID_FILE -f
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
>
> $ service shenyid ooxx



