#### 磁盘挂载

扩大centos系统盘

```shell
# 查看所有磁盘
fdisk -l
fdisk /dev/sda # 未分区磁盘位置
# n 新建分区
# p 创建主分区
# w 保存分区
mkfs.xfs /dev/sda1 # 格式化，仿佛不用这一步

# 创建物理卷
pvcreate /dev/sda1
# 查看物理卷
pvdisplay
# 将新分区 /dev/sda1 加入根目录分区centos中
vgextend centos /dev/sda1
# 查看卷组信息
vgdisplay
# 增加centos大小，增加100G
lvresize -L +100G /dev/mapper/centos-root
# 重新识别centos大小
xfs_growfs /dev/mapper/centos-root
```
磁盘挂载

```shell
# 查看所有磁盘
fdisk -l
fdisk /dev/sda # 未分区磁盘位置
n -> p -> 1 -> enter -> enter -> w
# n：添加一个分区
# P：主分区
# 两个回车指是开始和结束的磁盘大小；
# w：写入磁盘

mkfs.ext4 /dev/sda1 # 格式化磁盘
mkdir /mydata
mount /dev/sda1 /mydata # 挂载
df -h
```

