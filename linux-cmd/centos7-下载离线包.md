### 下载rpm

```shell
yum install --downloadonly --downloaddir=/home <package-name>
```

### 强制安装

```shell
rpm -ivh  *.rpm --force --nodeps
```



### 下载package

```shell
pip download -d /tmp/offline_packages <package>
pip download -d /tmp/offline_packages -r requirements.txt
```

### 安装package

```shell
pip install --no-index --find-links="/tmp/tranferred_packages" <package>
pip install --no-index --find-links="/tmp/tranferred_packages" -r requirements.txt
```





------

*@Author OppJune*

[BACK](../README.md)