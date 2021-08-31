## 1. Clash 各版本下载地址
- <a href="https://github.com/Dreamacro/clash/releases/tag/premium"> Clash Premium 命令行版 </a>: (兼容 Windows、macOS、Linux、OpenWRT 等多种平台）
- <a href="https://install.appcenter.ms/users/clashx/apps/clashx-pro/distribution_groups/public"> Clash Premium 图形用户界面版</a>:（ClashX Pro，兼容 macOS）
- <a href="https://github.com/Fndroid/clash_for_windows_pkg/releases"> Clash Premium 图形用户界面版</a>: **【推荐，mac/windows亲测成功】**（Clash for Windows，兼容 Windows、macOS）

## 2. 设置配置文件 (以clash for windows为例)

#### 2.1 选中`Profiles`标签，新建配置文件

<img src="https://s3.ax1x.com/2020/11/21/D1CE6O.png" height="500">
<img src="https://s3.ax1x.com/2020/11/21/D1CrcT.png" height="500">

#### 2.2 编辑配置文件

<img src="https://s3.ax1x.com/2020/11/21/D1CRE9.md.png" height="500">

> 如果点击没有反应请先桌面新建.yml格式的文件，然后右键选择“记事本”打开方式

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
    port: 443
    password: <节点1密码>
  - name: <节点2>
    type: trojan
    server: <节点2服务器域名>
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

  gfw:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/gfw.txt"
    path: ./ruleset/gfw.yaml
    interval: 86400

  greatfire:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/greatfire.txt"
    path: ./ruleset/greatfire.yaml
    interval: 86400

  tld-not-cn:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/tld-not-cn.txt"
    path: ./ruleset/tld-not-cn.yaml
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

rules:
  - PROCESS-NAME,v2ray,DIRECT
  - PROCESS-NAME,Surge%203,DIRECT
  - PROCESS-NAME,ss-local,DIRECT
  - PROCESS-NAME,privoxy,DIRECT
  - PROCESS-NAME,trojan,DIRECT
  - PROCESS-NAME,trojan-go,DIRECT
  - PROCESS-NAME,naive,DIRECT
  - PROCESS-NAME,Thunder,DIRECT
  - PROCESS-NAME,DownloadService,DIRECT
  - PROCESS-NAME,qBittorrent,DIRECT
  - PROCESS-NAME,Transmission,DIRECT
  - PROCESS-NAME,fdm,DIRECT
  - PROCESS-NAME,aria2c,DIRECT
  - PROCESS-NAME,Folx,DIRECT
  - PROCESS-NAME,NetTransport,DIRECT
  - PROCESS-NAME,uTorrent,DIRECT
  - PROCESS-NAME,WebTorrent,DIRECT
  - DOMAIN,clash.razord.top,DIRECT
  - DOMAIN,yacd.haishan.me,DIRECT
  - RULE-SET,reject,REJECT
  - RULE-SET,icloud,DIRECT
  - RULE-SET,apple,DIRECT
  - RULE-SET,google,DIRECT
  - RULE-SET,proxy,PROXY
  - RULE-SET,direct,DIRECT
  - GEOIP,,DIRECT
  - GEOIP,CN,DIRECT
  - MATCH,PROXY

```

- 修改<>括号里面的内容为自己的节点信息

<img src="https://s3.ax1x.com/2020/11/21/D1Poin.png" height="500">

#### 2.3 双击配置文件以生效

<img src="https://s3.ax1x.com/2020/11/21/D1C7uD.png" height="500">

<img src="https://s3.ax1x.com/2020/11/21/D1iVdH.md.png" height="500">

#### 2.4 开启代理

<img src="https://s3.ax1x.com/2020/11/21/D1inJI.md.png" height="500">
