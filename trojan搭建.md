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
curl -O https://raw.githubusercontent.com/YaoFANGUK/clashX-clash-config/main/trojan.sh && chmod +x trojan.sh && ./trojan.sh
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

## 使用acme.sh脚本配置网站自动续签https ssl证书

1. 下载acme.sh并安装
```shell
curl https://get.acme.sh | sh
```

2. 刷新环境变量
```shell
source /root/.bashrc
```

3. 修改默认CA为 LetsEncrypt
```shell
acme.sh --set-default-ca --server letsencrypt
```

4. 为示例域名www.sbdj.com申请ssl证书
```shell
acme.sh --issue -d www.sbdj.com --webroot /usr/share/nginx/html/
```

5. 安装证书到指定位置
```shell
acme.sh --install-cert -d abc.com --key-file /usr/local/nginx/abc.com.key --fullchain-file /usr/local/nginx/abc.com.crt
```

6. 配置trojan证书位置

```shell
vim /etc/trojan-go/config.json
```


7. 查看自动续签任务
```shell
crontab -l
```









