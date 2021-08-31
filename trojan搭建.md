# Trojan-GO

#### 安装依赖

- CentOS

```
yum install -y curl
```

- Debian/Ubuntu

```
sudo apt install -y curl
```

#### 安装Trojan-GO

```
bash <(curl -sL https://raw.githubusercontent.com/YaoFANGUK/clashX-clash-config/main/trojan.sh)
```

<img src="https://z3.ax1x.com/2021/08/31/hUix41.png">



根据自己的需求选择安装 trojan-go 或trojan-go+WS（+WS 版本能使用 CDN 中转，如果你需要 CDN 中转请选择“2”，trojan-go+WS 需要设置 WS 路径。一般默认选择“1”就好了）



#### Trojan配置文件

位于以下目录：

```
/etc/trojan-go/config.json
```



>  重启trojan服务
>
> ```
> systemctl restart trojan
> ```





## BBR安装

```
cd /usr/src && wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh

```

trojan服务端配置文件路径如下，如需修改内容，修改以下文件即可。

```
/usr/src/trojan/server.conf
```

