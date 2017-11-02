未完待续

```c
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



