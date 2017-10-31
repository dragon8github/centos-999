# su：用户的切换和指使

切换到 god 用户

> $ su god

切换到 god 用户，并且进入用户目录（通常是/home/god）

> $ su - god

以 god 用户的身份去执行命令。当然作用也是在god用户的空间中。

> $ su - god -c 'echo "i am god" &gt; test.txt '

![](/assets/0abcb564-dce0-4663-82a4-69a18be43e1dimport.png)

---

# 需求

为了安全，该软件在运行时不推荐使用ROOT账户运行。所以我们会有个初始化shell脚本，来创建用户和初始化文件。

1. 判断用户是否存在\(譬如叫god\),没有则创建；
2. 创建后设置密码为123；
3. 把一些程序文件拷贝过去，并且除了ROOT外，只能god用户运行\(最好是ROOT也不能方便的运行\)。

 test.sh 代码：

```php
USER_COUNT=`cat /etc/passwd | grep '^god:' -c`
USER_NAME='god'

# 添加用户
# 如果用户已存在那么会报错。将报错扔进/dev/null中，来禁止报错输出。
useradd $USER_NAME 2>/dev/null

# $? 显示最后命令的退出状态。0表示没有错误，其它任何值表明有错误(或执行不成功)
if [ $? -eq 0 ]
    then
        # 使用 passwd 修改密码需要提示和确认，使用 --stdin 标准输入（键盘)强迫设置
        echo '123' | passwd $USER_NAME --stdin
        echo 'done'
    else
        echo 'god is exist'

    # 如果不存在/home/god/bin文件夹。那么创建它
    if [ ! -d /home/god/bin ]
      then
          su - god -c 'mkdir bin'
          echo 'bin is created'
    fi

    # 在文件夹中新建 me 文件。并且插入文本 “echo i am god”
    su - god -c 'echo "echo i am god" > bin/me'
    # 为 me 文件添加可执行权限
    su - god -c 'chmod +x bin/me'
fi
```



