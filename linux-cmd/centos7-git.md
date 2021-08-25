## Git升级

```shell
# git版本 https://mirrors.edge.kernel.org/pub/software/scm/git/

yum remove git -y
yum -y install curl-devel expat-devel gettext-devel openssl-devel zlib-devel asciidoc
yum -y install gcc perl-ExtUtils-MakeMaker
cd /usr/local/src/
wget https://www.kernel.org/pub/software/scm/git/git-2.29.3.tar.xz
tar -vxf git-2.29.3.tar.xz
cd git-2.29.3
make prefix=/usr/local/git all
make prefix=/usr/local/git install
echo "export PATH=$PATH:/usr/local/git/bin" >> /etc/profile
source /etc/profile
git --version

# 注意：如果还是原来的版本，也不一定是安装失败了，首先检查一下Git的安装路径，可能有多个路径，是不是原来的Git版本没有删除，或者设置环境变量时添加了错误的路径。

# 查看Git的可执行文件位置，可能有多个路径
whereis git

# 再删除一遍
yum remove git -y
```



## Git操作



### 克隆操作

```shell
# 拉取代码
git clone http://10.20.5.5:10080/ehualu/Lakestor.git
git clone http://192.168.1.28/storage/storConsole.git --depth 0
```



### 分支操作

```shell
# 查看所有分支
git branch -a
# 切换分支到feature-shell-v1
git checkout feature-shell-v1
# 查看当前分支，包含本地所有分支
git branch
# 更新远程分支索引
git fetch

# 合并feature_osd_update分支到master
git checkout master
git merge feature_osd_update
git push # ?
```



### 提交操作

```shell
# 查看修改内容
git status
# 查看具体修改内容
git diff <filename>
# 增加所有修改内容，若非全部，一个一个添加文件
git add .
# 增加备注
git commit -m "1.脚本增加权限;2.更新ceph.spec.in"
# 更新本地分支到最新版本
git pull origin feature-shell-v1
# 本地更新推送至远程分支
git push
# ntpdate cn.pool.ntp.org
```



### 还原操作

```shell
# 只修改了文件，未进行git操作
# 还原指定文件
git checkout aaa.html
# 还原本地所有修改
git checkout .

# 修改了文件，提交到暂存区(git add 已操作)
git log
# 回退到当前版本
git reset HEAD
git checkout aaa.html

# 还原最近一次提交的修改
git revert HEAD
# 还原指定版本的修改
git revert commit-id

# 修改文件，提交到仓库区(git commit -m "" 已操作)
git log
git reset HEAD^
git checkout -- aaa.html

# revert和reset的区别：reset是将head往后退而revert执行后head继续前行
```





------

*@Author OppJune*

[BACK](../README.md)