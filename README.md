## 1. 设置配置文件 (以clash for windows为例)

#### 1.1 选中`Profiles`标签，新建配置文件



<img src="https://s3.ax1x.com/2020/11/21/D1CrcT.png" height="500">

#### 1.2 编辑配置文件

<img src="https://s3.ax1x.com/2020/11/21/D1CRE9.md.png" height="500">

> 如果点击没有反应请先桌面新建.yml格式的文件，然后右键选择“记事本”为**默认**打开方式

- 复制配置文件如下：

```yaml
mixed-port: 7890
allow-lan: false
log-level: info
external-controller: '127.0.0.1:9090'
secret: ''
ipv6: false

# 代理设置
proxies:
  - name: <节点1>
    type: trojan
    server: <节点1服务器域名>
    skip-cert-verify: true  # 关闭证书验证
    port: 443
    password: <节点1密码>
  - name: <节点2>
    type: trojan
    server: <节点2服务器域名>
    skip-cert-verify: true  # 关闭证书验证
    port: 443
    password: <节点2密码>
proxy-groups:
  - name: PROXY
    type: select
    proxies:
      - <节点1>
      - <节点2>

rule-providers:
  reject:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/reject.txt"
    path: ./ruleset/reject.yaml
    interval: 86400

  icloud:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/icloud.txt"
    path: ./ruleset/icloud.yaml
    interval: 86400

  apple:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/apple.txt"
    path: ./ruleset/apple.yaml
    interval: 86400

  google:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/google.txt"
    path: ./ruleset/google.yaml
    interval: 86400

  proxy:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/proxy.txt"
    path: ./ruleset/proxy.yaml
    interval: 86400

  direct:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/direct.txt"
    path: ./ruleset/direct.yaml
    interval: 86400

  private:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/private.txt"
    path: ./ruleset/private.yaml
    interval: 86400

  gfw:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/gfw.txt"
    path: ./ruleset/gfw.yaml
    interval: 86400

  tld-not-cn:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/tld-not-cn.txt"
    path: ./ruleset/tld-not-cn.yaml
    interval: 86400

  telegramcidr:
    type: http
    behavior: ipcidr
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/telegramcidr.txt"
    path: ./ruleset/telegramcidr.yaml
    interval: 86400

  cncidr:
    type: http
    behavior: ipcidr
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/cncidr.txt"
    path: ./ruleset/cncidr.yaml
    interval: 86400

  lancidr:
    type: http
    behavior: ipcidr
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/lancidr.txt"
    path: ./ruleset/lancidr.yaml
    interval: 86400

  applications:
    type: http
    behavior: classical
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/applications.txt"
    path: ./ruleset/applications.yaml
    interval: 86400

# 白名单模式-终端用（流量使用多）
#rules:
#  - RULE-SET,applications,DIRECT
#  - DOMAIN,clash.razord.top,DIRECT
#  - DOMAIN,yacd.haishan.me,DIRECT
#  - RULE-SET,private,DIRECT
#  - RULE-SET,reject,REJECT
#  - RULE-SET,icloud,DIRECT
#  - RULE-SET,apple,DIRECT
#  - RULE-SET,google,DIRECT
#  - RULE-SET,proxy,PROXY
#  - RULE-SET,direct,DIRECT
#  - RULE-SET,lancidr,DIRECT
#  - RULE-SET,cncidr,DIRECT
#  - RULE-SET,telegramcidr,PROXY
#  - GEOIP,LAN,DIRECT
#  - GEOIP,CN,DIRECT
#  - MATCH,PROXY

# 黑名单模式-软路由用（流量使用少）
rules:
  - RULE-SET,applications,DIRECT
  - DOMAIN,clash.razord.top,DIRECT
  - DOMAIN,yacd.haishan.me,DIRECT
  - RULE-SET,private,DIRECT
  - RULE-SET,reject,REJECT
  - RULE-SET,tld-not-cn,PROXY
  - RULE-SET,gfw,PROXY
  - RULE-SET,telegramcidr,PROXY
  - MATCH,DIRECT


```

- 修改<>括号里面的内容为自己的节点信息

<img src="https://s3.ax1x.com/2020/11/21/D1Poin.png" height="500">

#### 1.3 双击配置文件以生效

<img src="https://s3.ax1x.com/2020/11/21/D1C7uD.png" height="500">

<img src="https://s3.ax1x.com/2020/11/21/D1iVdH.md.png" height="500">

#### 1.4 开启代理

<img src="https://s3.ax1x.com/2020/11/21/D1inJI.md.png" height="500">



## 2. Linux配置Clash 

#### 2.1 Clash 下载

在 Clash release 页面下载相应的版本，对于 Ubuntu 一般使用 clash-linux-amd64 版本：

```shell
wget https://github.com/Dreamacro/clash/releases/download/v1.14.0/clash-linux-amd64-v1.14.0.gz
```

> 如果直接 wget 速度较慢的话，可以本地下载完成后，使用 SFTP 上传到 Linux 服务器。

然后使用 gunzip 命令解压，并重命名为 clash：

```shell
gunzip clash-linux-amd64-v1.14.0.gz
mv clash-linux-amd64-v1.14.0 clash
```
为 clash 添加可执行权限：

```
chmod u+x clash
```

Clash 运行时需要 Country.mmdb 文件，当第一次启动 Clash 时（使用 ./clash 命令） 会自动下载（会下载至 /home/XXX/.config/clash 文件夹下）。自动下载可能会因网络原因较慢，可以访问该<a herf="https://github.com/Dreamacro/maxmind-geoip/releases">链接</a>手动下载。

>  Country.mmdb 文件利用 GeoIP2 服务能识别互联网用户的地点位置，以供规则分流时使用。


#### 2.2 Clash as a daemon

将 Clash 转变为系统服务，从而使得 Clash 实现常驻后台运行、开机自启动等。

> 普通用户需要 sudo 权限。

##### 配置 systemd 服务

Linux 系统使用 systemd 作为启动服务器管理机制，首先把 Clash 可执行文件拷贝到 ```/usr/local/bin``` 目录，相关配置拷贝到 ```/etc/clash``` 目录。

```shell
sudo mkdir /etc/clash
sudo cp clash /usr/local/bin
sudo cp config.yaml /etc/clash/
sudo cp Country.mmdb /etc/clash/
```


创建 systemd 服务配置文件 ```sudo vim /etc/systemd/system/clash.service```：

```
[Unit]
Description=Clash daemon, A rule-based proxy in Go.
After=network.target

[Service]
Type=simple
Restart=always
ExecStart=/usr/local/bin/clash -d /etc/clash

[Install]
WantedBy=multi-user.target
```

##### 使用 systemctl

使用以下命令，让 Clash 开机自启动：

```shell
sudo systemctl enable clash
```

然后开启 Clash：

```shell 
sudo systemctl start clash
```


查看 Clash 日志：

```shell
sudo systemctl status clash
sudo journalctl -xe
```

##### 使用代理

利用 Export 命令使用代理
Clash 运行后，其在后台监听某一端口。Ubuntu 下使用代理，需要 export 命令。根据 config 配置文可以查看到件Clash 代理端口（订阅转换后，端口为7890），设置系统代理命令为：

```shell
export https_proxy=http://127.0.0.1:7890 http_proxy=http://127.0.0.1:7890 all_proxy=socks5://127.0.0.1:7890
```


可以将该命令添加到 .bashrc 中，登陆后该用户自动开启代理。

取消系统代理：

```shell
unset  http_proxy  https_proxy  all_proxy
```

> 一般下载数据集时，记得取消代理。

