未完待续

```c
#add for chkconfig
#chkconfig:35 80 10
#description:i am god
#processname:shenyid

PID_FILE='/etc/shenyid.pid'

start () {
  if [ -f $PID_FILE ] 
    	then
          echo 'god_me is already running'
      else
          echo '123' > $PID_FILE
          echo 'start god_me'
  fi
}

stop () {
   rm $PID_FILE -f
   echo 'god_me is stoped'
}

# /home/god/bin/god_me
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



