## 用户系统

### 常用命令

```shell
# 创建新用户
adduser <username>
# 更改用户密码
passwd <username>
# 将用户添加到wheel用户组里，因为wheel用户组拥有sudo的权限
usermod -aG wheel <username>

# 新建用户组
groupadd test

# 用户列表文件
cat /etc/passwd
cut -d : -f 1 /etc/passwd
# 用户组列表文件
cat /etc/group

# 查看某一用户
w 用户名
# 查看登录用户
who am i
# 查看用户登录历史记录
last
# 查看当前用户的用户组
groups
id
# 查看特定用户的用户组
groups <username>
id <username>

# 其他用户对/testdir目录可进行读写执行
chmod o=rwx /testdir
# 修改文件用户权限
chmod -R 0760 /testdir # -R参数，将读写权限传递给子文件夹
# 增加用户到指定用户组
usermod -a -G 指定文件夹的组名 要分配的用户名

# r=4，w=2，x=1  因此rwx=4+2+1=7
```





### 登录用户出现‘’-bash-4.2$‘’问题

今天在linux服务器上创建的用户，登录后发现此用户的CRT的终端提示符显示的是-bash-4.2# 而不是user@主机名 + 路径的显示方式，以往一直用的脚本也不能执行起来；
原因是在用useradd添加普通用户时，有时会丢失家目录下的环境变量文件，丢失文件如下：
1、.bash_profile
2、.bashrc
以上这些文件是每个用户都必备的文件。

```shell
# 从主默认文件/etc/skel/下重新拷贝一份配置信息到此用户家目录下
cp /etc/skel/.bashrc  /home/user/
cp /etc/skel/.bash_profile   /home/user
# 注销并重新登录此用户后便可以恢复正常了！！
```



<br /><br />

------

<script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>
<span id="busuanzi_container_page_pv">本文阅读量<span id="busuanzi_value_page_pv"></span>次</span>

<br />

*@Author OppJune*

[BACK](../README.md)../README.md)