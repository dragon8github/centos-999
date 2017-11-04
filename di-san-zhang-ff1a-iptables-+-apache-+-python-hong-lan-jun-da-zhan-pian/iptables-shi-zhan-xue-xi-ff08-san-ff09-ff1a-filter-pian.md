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
* -R num：Replays替换/修改第几条规则 格式：iptables -R 3 ………… 
* -D num：删除，明确指定删除第几条规则。

---

# -j &lt;Action&gt;

* DROP：直接丢弃；
* REJECT：明示拒绝；
* ACCEPT：接受。



