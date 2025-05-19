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


# 2. Xray安装

#### 2.1 脚本特点

系统支持：Ubuntu，Debian，CentOS，推荐使用 Ubuntu 22，谨慎使用 CentOS，脚本可能无法正常运行！


#### 2.2 安装Xray

```
bash <(wget -qO- -o- https://raw.githubusercontent.com/YaoFANGUK/clashX-clash-config/main/vless.sh)
```

#### 2.3 管理Xray

安装完成后，输入 xray 就能看到管理面板

#### 2.4 无法使用

- 步骤1

测试端口是否能连接上：<a href="https://tcp.ping.pe/">https://tcp.ping.pe/</a>

写上你的 VPS IP 跟端口；内容为 ip:端口，示例：1.1.1.1:443，然后点击 Go；或者直接回车

如果显示 successful；证明端口能连接；如果显示 failed；那是无法连接上端口。

> 提醒，你可以使用 xray ip 查看 VPS IP。

- 步骤2

关闭防火墙，执行如下命令：

```shell
systemctl stop firewalld; systemctl disable firewalld; ufw disable
```

关闭防火墙之后再测试一下端口是否通，如果不通，你可能还有外部防火墙没关，必须要能连接上端口才能正常使用。如果能连接上端口，那就继续


# 3. iptables配置

#### 3.1 iptables 开放所有端口

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

#### 3.2 保存规则

```shell
iptables-save
```

安装 iptables-persistent

```shell
sudo apt-get install iptables-persistent
```

#### 3.3 持久化规则

```shell
sudo netfilter-persistent save
sudo netfilter-persistent reload
```

查看所有规则：
```shell
sudo iptables -L --line-numbers
```
根据编号删除规则(以INPUT 编号3为例)：
```shell
sudo iptables -D INPUT 3
```


