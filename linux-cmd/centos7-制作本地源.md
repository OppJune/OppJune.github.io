#### 制作本地源

以安装ceph所需本地源为例，局域网内可使用该源

```shell
# 由于使用ceph-ansible进行安装时，会自动配置防火墙，关闭httpd的80端口。
# 因此建议使用集群外服务器上搭建的本地源，或每台服务器均搭建本地源
# 本地源仅给本机使用时，不需要安装httpd服务


### 10.20.2.94(非ceph集群服务器) 上执行
# 无外网需使用rpm安装
yum install httpd createrepo -y
# httpd服务目录在/var/www/html/,ceph-rpm目录下是准备好的rpm包
createrepo /var/www/html/ceph-rpm
# 启动httpd服务
systemctl start httpd

### node01节点执行
# 添加源
vim /etc/yum.repos.d/ceph.repo
vim /etc/yum.repos.d/extra.repo
# ceph.reph
[Ceph-local]
name=Cephlocal packages
baseurl=http://10.20.2.94/ceph-rpm
enabled=1
gpgcheck=0
priority=1
# extra.repo
[Extra]
name=extra packages
baseurl=http://10.20.2.94/ceph-rpm
enabled=1
gpgcheck=0
# 增加其他节点的源
scp node01:/etc/yum.repos.d/ceph.repo node02:/etc/yum.repos.d/ceph.repo
scp node01:/etc/yum.repos.d/ceph.repo node03:/etc/yum.repos.d/ceph.repo
scp node01:/etc/yum.repos.d/extra.repo node02:/etc/yum.repos.d/extra.repo
scp node01:/etc/yum.repos.d/extra.repo node03:/etc/yum.repos.d/extra.repo

### 集群每个节点均需要执行，注意10.20.2.94的80端口需开放
yum clean all
rm -rf /var/cache/yum
yum makecache

yum install ceph ceph-radosgw
ceph -v
```
