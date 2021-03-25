# XRayR
A Xray backend framework that can easily support many panels.

一个基于Xray的后端框架，支持V2ay,Trojan,Shadowsocks协议，极易扩展，支持多面板对接

Find the source code here: [XrayR-project/XrayR](https://github.com/XrayR-project/XrayR)

# 面板节点设置

[教程](https://github.com/XrayR-project/XrayR/blob/master/README.md)

# 一键安装

```
bash <(curl -Ls https://raw.githubusercontent.com/XrayR-project/XrayR-release/master/install.sh)
```
# Docker 安装

```
docker pull crackair/xrayr:latest && docker run --restart=always --name xrayr -d -v ${PATH_TO_CONFIG}/config.yml:/etc/XrayR/config.yml --network=host crackair/xrayr:latest
```

# Docker compose 安装
0. 安装docker-compose: 
```
curl -fsSL https://get.docker.com | bash -s docker
curl -L "https://github.com/docker/compose/releases/download/1.26.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```
1. `git clone https://github.com/XrayR-project/XrayR-release`
2. `cd XrayR-release`
3. 编辑config。
配置文件基本格式如下，Nodes下可以同时添加多个面板，多个节点配置信息，只需添加相同格式的Nodes item即可。
4. 启动docker：`docker-compose up -d`
```
Log:
  Level: debug # Log level: none, error, warning, info, debug 
  AccessPath: # ./access.Log
  ErrorPath: # ./error.log
Nodes:
  -
    PanelType: "SSpanel" # Panel type: SSpanel
    ApiConfig:
      ApiHost: "http://127.0.0.1:667"
      ApiKey: "123"
      NodeID: 41
      NodeType: V2ray # Node type: V2ray, Shadowsocks, Trojan
      EnableVless: false # Enable Vless for V2ray Type, Prefer remote configuration
      EnableXTLS: false # Enable XTLS for V2ray and Trojan， Prefer remote configuration
    ControllerConfig:
      ListenIP: 0.0.0.0 # IP address you want to listen
      UpdatePeriodic: 60 # Time to update the nodeinfo, how many sec.
      CertConfig:
        CertMode: dns # Option about how to get certificate: none, file, http, dns. Choose "none" will forcedly disable the tls config.
        CertDomain: "node1.test.com" # Domain to cert
        CertFile: ./cert/node1.test.com.cert # Provided if the CertMode is file
        KeyFile: ./cert/node1.test.com.key
        Provider: alidns # DNS cert provider, Get the full support list here: https://go-acme.github.io/lego/dns/
        Email: test@me.com
        DNSEnv: # DNS ENV option used by DNS provider
          ALICLOUD_ACCESS_KEY: aaa
          ALICLOUD_SECRET_KEY: bbb
```

## Docker compose升级
在docker-compose.yml目录下执行：
```
docker-compose pull
docker-compose up -d
```
