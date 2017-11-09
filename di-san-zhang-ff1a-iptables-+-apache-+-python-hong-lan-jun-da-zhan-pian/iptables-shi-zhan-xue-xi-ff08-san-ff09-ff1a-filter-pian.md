# 最简单的禁止访问：一律红灯

> $ iptables -P INPUT DROP

* -P 代表默认策略；
* DROP 标准行为，代表直接拒收（类似直接挂电话）。

# ![](/assets/吖吖zzzzc6453534534534import.png)

---

# 思考题

如果我们想重新开通外部对80端口的访问，执行了`iptables -t filter -A INPUT -p tcp --dport 80 -j ACCEPT`

但依然不能放行，这是为什么 ? ？？

其实我们可以通过 `iptables-save` 查看iptables配置规则。在这里，第一个 DROP 已经执行了阻塞，后面再ACCEPT都没用了。

所以要这么干：`iptables -I INPUT -p tcp --dport 80 -j ACCEPT`

（PS：最好保存规则：`iptables-save > /etc/sysconfig/iptables`这样子下次重启就自动读取了。）

![](/assets/87要图dfgdfgdfgimport.png)

事实上，我们也可以使用 -D （删除） / -R （替换） DROP 的选项都是可以实现的。

> $ iptables -t filter -D INPUT -p tcp --dport 80 -j DROP

![](/assets/asdasdxzzcvxcbvbvcbcimport.png)

---

# 禁止 80 端口

> $ iptables -t filter -A INPUT -p tcp --dport 80 -j DROP

* -t 就是默认表 filter ；
* -p 使用什么传输协议，如 TCP / UDP / ICMP ；
* --dport 目标端口。

如果还是可以访问 80 端口，就把 -A 换成 - I 原因同上面的思考题。

---

# 规则管理

* -A &lt;rule&gt;：追加，在当前链的最后新增一个规则；
*  -I &lt;rule \| num&gt;：插入，把当前链第N条插入，默认在首部插入；
* -R &lt;rule \| num&gt;：替换，第几条规则格式，如` iptables -R 3 <rule>`；
* -D &lt;rule \| num&gt;：删除，明确指定删除第几条规则，如删除第二条规则`iptables -D INPUT 2`。

---

# -j &lt;Action&gt;

* DROP：直接丢弃；
* REJECT：明示拒绝；
* ACCEPT：接受。

---

# 保存规则 ：iptables-save

当服务器重启之后，我们之前所配置的规则就统统失效了。所以常用的规则应该保存到配置文件中。

> $ which iptables-save
>
> $ iptables-save &gt; /etc/sysconfig/iptables
>
> $ cat /etc/sysconfig/iptables

# ![](/assets/asads65545234234234import.png)

---

# 禁止指定 IP 进入网站

上面的做法是，禁止一切事物请求80端口 那如果我们只要 禁止某个IP该如何？

> $ iptables -I INPUT -p tcp -s 这里写上IP --dport 80 -j ACCEPT

-s 代表来源。可以写IP 还可以封IP段。请自行搜索写法

