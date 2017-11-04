# 学习新工具 netstat

* 显示与IP、TCP、UDP和ICMP协议相关的统计数据，一般用于检验本机各端口的网络连接情况；
* 提供TCP连接，TCP和UDP监听，进程内存管理的相关报告。

### 常见参数：

* -a或–all 显示所有连线中的Socket；
* -t或–tcp 显示TCP传输协议的连线状况； 
* -u或–udp 显示UDP传输协议的连线状况；
* -l或–listening 显示监听中的服务器的Socket； 
* -n或–numeric 直接使用IP地址，而不通过域名服务器； 
* -p或–programs 显示正在使用Socket的程序识别码和程序名称。

### 常见的一些命令：

显示tcp模式运行状况：

> $ netstat -ant
>
> $ netstat -ant \| greep 80

显示正在通讯IP：

> $ netstat -ant\| grep ESTABLISHED netstat -antp

# Tcp状态

1、LISTENING：服务启动后首先处于侦听状态；

2、ESTABLISHED：建立连接。表示两台机器正在通信；

3、CLOSE\_WAIT： 对方主动关闭连接或者网络异常导致连接中 ；

4、TIME\_WAIT： 我方主动调用close\(\)断开连接，收到对方确认后状态变为TIME\_WAIT。

