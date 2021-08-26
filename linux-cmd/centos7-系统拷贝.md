## 系统拷贝

清理磁盘

```shell
# 删除分区
fdisk /dev/sdg
# 删除文件系统
wipefs -a /dev/sdg
# dd清理
dd if=/dev/zero of=/dev/sdg bs=1M count=10
```

拷贝系统

```shell
dd if=/dev/sdh of=/dev/sdg bs=1M
```

进入单用户模式

```shell
centos界面，按“e”
浏览到最后，找到“ro”，替换为“rw init=/sysroot/bin/sh”
ctrl+x
```

修复xfs

```shell
xfs_repair -L /dev/centos/root
xfs_repair /dev/centos/root
exit || reboot
```



## 系统故障

### 问题

/dev/centos/root not exist

/dev/centos/swap not exist

/dev/mapper/centos-root not exist

### 未解决

```shell
# 方法一
# 运行 lvm vgscan 后报错segement fault
lvm vgscan
lvm vgchange -ay 
exit
```



<br /><br />

------

<script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>
<span id="busuanzi_container_page_pv">本文阅读量<span id="busuanzi_value_site_pv"></span>次</span>

<br />

*@Author OppJune*

[BACK](../README.md)../README.md)