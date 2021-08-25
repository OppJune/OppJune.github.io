## Kernel 升级

原kernel：3.10.0-957.el7.x86_64



### 小版本升级

```shell
目标：3.10.0-1062.18.1.el7.x86_64

# 查看当前和可升级版本
yum list kernel
# 升级
yum update kernel -y # 也可不加kernel，全部升级
reboot
uname -a

# 遇到问题
Existing mon, trying to rejoin cluster...
# 解决
docker cp monnode2:/opt/ceph-container/bin/start_mon.sh .
vim start_mon.sh
# 注释此行，直接将v2v1复制为2，代表是走V2协议， 以指定IP方式加入集群
#v2v1=$(ceph-conf -c /etc/ceph/${CLUSTER}.conf 'mon host' | tr ',' '\n' | grep -c ${MON_IP})
v2v1=2
docker cp start_mon.sh monnode2:/opt/ceph-container/bin/start_mon.sh
```



### 大版本升级

**1 查看系统内核版本**

```shell
[root@vvuv0394 ~]# cat /etc/redhat-release 
CentOS Linux release 7.2.1511 (Core) 
[root@vvuv0394 ~]# uname -r
3.10.0-327.el7.x86_64
```

**2 在升级内核之前，先升级软件包（非必要）**

```shell
yum update -y
```

**3 升级内核**

添加第三方yum源进行下载安装。
Centos 7 YUM源：http://www.elrepo.org/elrepo-release-7.0-2.el7.elrepo.noarch.rpm

先导入elrepo的key，然后安装elrepo的yum源：

```shell
rpm -import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-2.el7.elrepo.noarch.rpm
```

仓库启用后，列出可用的内核相关包：

```shell
yum --disablerepo="*" --enablerepo="elrepo-kernel" list available
```

安装最新稳定内核

```shell
yum -y --enablerepo=elrepo-kernel install kernel-ml
```

**4 修改默认内核版本**

查看系统上所有可用内核

```shell
# sudo awk -F\' '$1=="menuentry " {print i++ " : " $2}' /etc/grub2.cfg
0 : CentOS Linux (4.15.6-1.el7.elrepo.x86_64) 7 (Core)
1 : CentOS Linux (3.10.0-514.26.2.el7.x86_64) 7 (Core)
2 : CentOS Linux (3.10.0-327.el7.x86_64) 7 (Core)
3 : CentOS Linux (0-rescue-f9d400c5e1e8c3a8209e990d887d4ac1) 7 (Core)
```

设置第0个为默认内核

```shell
grub2-set-default 0
```

重新创建内核配置

```shell
grub2-mkconfig -o /boot/grub2/grub.cfg
```

**5 重启验证**

```shell
# reboot
# uname -r
4.15.6-1.el7.elrepo.x86_64
```

