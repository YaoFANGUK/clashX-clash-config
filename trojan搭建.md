# Trojan-GO

#### 脚本特点

- 全自动配置伪装网站，网站位于/usr/share/nginx/html/目录，可自行修改替换。
- 全自动申请配置SSL证书用于https网站，使用的是let’s encrypt证书。
- SSL证书到期前会自动续期，免维护。
- 自动配置开放80、443端口。
- 自动配置好Trojan客户端文件及参数，下载即可使用。
- 不支持Cloudflare等CDN服务，建议不要使用CDN。

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

## 安装BBR

- Debian:
```shell
wget --no-check-certificate https://github.com/tcp-nanqinlang/general/releases/download/3.4.2.1/tcp_nanqinlang-fool-1.3.0.sh
bash tcp_nanqinlang-fool-1.3.0.sh
```

- CentOS:
```shell
wget --no-check-certificate https://raw.githubusercontent.com/tcp-nanqinlang/general/master/General/CentOS/bash/tcp_nanqinlang-1.3.2.sh
bash tcp_nanqinlang-1.3.2.sh
```

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


## acme.sh

配置网站自动续签https ssl证书

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









