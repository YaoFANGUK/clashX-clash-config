# 1. Trojan-GO

#### 1.1 脚本特点

- 全自动配置伪装网站，网站位于/usr/share/nginx/html/目录，可自行修改替换。
- 全自动申请配置SSL证书用于https网站，使用的是let’s encrypt证书。
- SSL证书到期前会自动续期，免维护。
- 自动配置开放80、443端口。
- 自动配置好Trojan客户端文件及参数，下载即可使用。
- 不支持Cloudflare等CDN服务，建议不要使用CDN。

#### 1.2 安装依赖

- CentOS

```
yum install -y curl
```

- Debian/Ubuntu

```
sudo apt install -y curl
```

#### 1.3 安装Trojan-GO

```
bash <(curl -sL https://raw.githubusercontent.com/YaoFANGUK/clashX-clash-config/main/trojan.sh)
```

#### 1.4 Trojan配置文件

位于以下目录：

```
/etc/trojan-go/config.json
```

>  重启trojan服务
>
> ```
> systemctl restart trojan
> ```

# 2. iptables配置

#### 2.1 iptables 开放所有端口

```shell
sudo iptables -P INPUT ACCEPT
sudo iptables -P FORWARD ACCEPT
sudo iptables -P OUTPUT ACCEPT
sudo iptables -F
```

> [Oracle CLoud] Oracle自带的镜像默认设置了Iptable规则，关闭它
> ```shell 
> sudo apt-get purge netfilter-persistent && sudo reboot
> ```

> [Oracle CLoud] 删除oracle-cloud-agent，防止甲骨文监控
> ```shell
> snap remove oracle-cloud-agent
> ```

#### 2.2 保存规则

```shell
iptables-save
```

安装 iptables-persistent

```shell
sudo apt-get install iptables-persistent
```

#### 2.3 持久化规则

```shell
sudo netfilter-persistent save
sudo netfilter-persistent reload
```








