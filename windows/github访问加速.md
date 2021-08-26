## GitHub访问加速

提供CDN加速方法

> 通过修改系统hosts文件的办法，绕过国内dns解析，直接访问GitHub的CDN节点，从而达到github访问加速的目的。不需要海外的服务器辅助。



### 查询域名IP

通过网站查询github核心域名解析地址。直接打开下面三个网址即可看到对应的ip地址。

**GitHub的三个核心域名**

<https://github.com.ipaddress.com>

<https://github.com.ipaddress.com/assets-cdn.github.com>

<https://fastly.net.ipaddress.com/github.global.ssl.fastly.net>



### 修改hosts文件

文件地址：`C:\Windows\System32\drivers\etc\hosts`

在末尾加上ip和域名，注意需要使用管理员权限打开文件才能修改。

 ![1629940963077](github\1.png)



### 刷新DNS解析缓存

win+r 打开运行，输入cmd后回车，打开命令提示符工具

刷新dns解析缓存：`ipfongif /flushdns`

 ![1629941239992](github\2.png)



<br /><br />

------

<script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>
<span id="busuanzi_container_page_pv">本文阅读量<span id="busuanzi_value_site_pv"></span>次</span>

<br />

*@Author OppJune*

[BACK](../README.md)