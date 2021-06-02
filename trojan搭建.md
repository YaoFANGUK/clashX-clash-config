# 最简单的Trojan一键脚本, 系统要求>=Centos7

最简单的Trojan一键脚本，效率高/速度快/延迟低，系统>=Centos7，完美支持tls1.3，个人体验速度和延迟都优于v2ray+ws+tls1.3，本次的centos版使用了官方编译的二进制文件，搭建非常快速和简单。脚本中集成了Trojan的Windows客户端，自动配置证书及启动脚本，安装完成直接下载客户端即可。



## 关于申请证书没有成果的处理

1、出现这个问题最可能的原因是你的同一个域名多次申请证书，导致let’s encrypt官方的限制，同一域名每周最多5次申请。



2、处理方法，更换二级域名，例如原来使用的域名是www.abc.com或abc.com或xyz.abc.com，那么现在你添加一个二级域名解析例如xxx.abc.com，安装时使用这个域名即可。



## 系统要求及脚本介绍

1、系统>=centos7，用centos8最好，内核可直接开启bbr不需升级。

2、域名解析到VPS并生效。

3、脚本自动续签https证书

4、自动配置伪装网站，位于/usr/share/nginx/html/目录下，可自行替换其中内容



## 使用一键脚本安装

```
curl -O https://raw.githubusercontent.com/atrandys/trojan/master/trojan_centos7.sh && chmod +x trojan_centos7.sh && ./trojan_centos7.sh
```

另外建议安装bbr，以下脚本安装，不赘述了

```
cd /usr/src && wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh

```

trojan服务端配置文件路径如下，如需修改内容，修改以下文件即可。

```
/usr/src/trojan/server.conf
```

修改完成后，重启trojan服务端即可，同时客户端的密码也要同步修改哦。

```shell
systemctl restart trojan
```



## **电脑上其他软件如何使用Trojan**

> 1、如果软件支持配置socks5，直接指向127.0.0.1：1080即可。
>
> 2、如果软件不支持配置socks5，可选择sstap/sockscap64/supercap等软件，曲线实现代理。



## **常见问题总结**

1、Trojan客户端打开无法运行，提示缺少找不到vcruntime140.dll或找不到msvcp140.dll。

> 原因缺少运行库，[点击下载链接](https://www.microsoft.com/en-us/download/details.aspx?id=48145)中的两个软件，一个是32位一个是64位，请全部安装即可。

2、如果遇到vcruntime140_1的错误，下载下面的文件放到C:\windows\system32目录下即可

[点击下载140_1.dll](https://github.com/atrandys/trojan/raw/master/vcruntime140_1.dll)

