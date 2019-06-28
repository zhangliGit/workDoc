### linux开启对端口

```
# 开启8888端口
sbin/iptables -I INPUT -p tcp --dport 8888 -j ACCEPT

# 重启端口服务
service network restart
```
