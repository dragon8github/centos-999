# 最简单的禁止访问：一竿子打死

> $ iptables -P INPUT DROP

* -P 代表默认策略；
* DROP 标准行为，代表直接拒收（类似直接挂电话）。

---

# 禁止80端口

> $ iptables -t filter -A INPUT -p tcp --dport 80 -j DROP

* -t 就是默认表 filter ；
* -p 使用什么传输协议，如 TCP / UDP / ICMP ；
* --dport 目标端口。

---

# 规则管理

* -A：追加，在当前链的最后新增一个规则；
* -I num : 插入，把当前规则插入为第几条；
* -R num：替换 / 修改第几条规则 格式：iptables -R 3 &lt;...&gt;；
* -D num：删除，明确指定删除第几条规则。

---

# -j &lt;Action&gt;

* DROP：直接丢弃；
* REJECT：明示拒绝；
* ACCEPT：接受。

---

# 保存规则 ：iptables-save

当服务器重启之后，我们之前所配置的规则就统统失效了。所以常用的规则应该保存到配置文件中。

> $ whiuch iptables-save
>
> $ iptables-save &gt; /etc/sysconfig/iptables
>
> $ cat /etc/sysconfig/iptables

![](/assets/asads65545234234234import.png)如果我们想重新开通外部对80端口的访问。并且执行了`iptables -t filter -A INPUT -p tcp --dport 80 -j ACCEPT` 

但依然不能放行，这是为什么 ? 其实我们可以通过 /etc/sysconfig/iptables 配置规则看出端倪。

在这里，第一个 DROP 已经执行了阻塞，后面再ACCEPT都没用了。

所以要这么干：`iptables -I INPUT -p tcp --dport 80 -j ACCEPT`

然后再一次保存规则：`iptables-save > /etc/sysconfig/iptables`

这时候就可以恢复正常访问了。

![](/assets/87要图dfgdfgdfgimport.png)

