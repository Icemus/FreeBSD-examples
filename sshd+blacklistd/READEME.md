
## 1. 配置sshd_config，启用Blacklist

### UseBlacklist参数介绍
```
#man sshd_config
      UseBlacklist
              Specifies whether sshd(8) attempts to send authentication success
              and failure messages to the blacklistd(8) daemon.  The default is
              no.  For forward compatibility with an upcoming blacklistd
              rename, the UseBlocklist alias can be used instead.
```
### 启用UseBlacklist
```
#vim /etc/ssh/sshd_config
UseBlacklist yes
```
### 重启sshd服务
```
#service sshd restart
```

## 2. 配置rc.conf，启用blacklistd服务。

### blacklistd默认配置
```
#cat /etc/defaults/rc.conf | grep blacklistd
blacklistd_enable="NO"          # Run blacklistd daemon (YES/NO).
blacklistd_flags=""             # Optional flags for blacklistd(8).
```
### blacklistd参数介绍
```
#man blacklistd
     -r      Re-read the firewall rules from the internal database, then
             remove and re-add them.  This helps for packet filters that do
             not retain state across reboots.
```
### 启用blacklistd服务
```
#vim /etc/rc.conf
blacklistd_enable="YES"
blacklistd_flags="-r"
```
### 重启blacklistd服务
```
#service blacklistd restart
```
### 查看blacklistd数据
```
#blacklistctl dump [-abdnrw]
```
