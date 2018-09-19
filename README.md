# v2ray 一键部署 heroku [![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy?template=https://github.com/wangyi2005/v2ray-heroku) [![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy?template=https://github.com/pqguanyinli/v2ray-heroku-openshift)
V2ray-Core 3.9

1.服务端部署后，应 open app ，显示 Bad Request，表示部署成功。

2.客户端应使用websocket+tls传输协议。Vmess协议的 users id 应当换成自己的UUID，"alterId": 64
# v2ray 部署在 openshift starter
openshift: 内存设置为256M，每 project 可配置 4 Pods。

Docker 镜像：pqguanyinli/v2ray-openshift:latest，pqguanyinli/v2ray-openshift:core版本号

环境变量： CONFIG_JSON（配置）、CERT_PEM（证书）、KEY_PEM（私钥）

用notepad++将上述变量中 \r\n 替换为\\\n，变成一行，导入容器。

客户端： android Actinium、windows v2ray 可用同一个服务端。

具体配置: 见 issues。

CONFIG_JSON 配置内容
```
{
  "log": {
    "loglevel": "warning"
  },
  "inbound": {
    "protocol": "vmess",
    "port": 8080,
    "settings": {
      "clients": [
        {
          "id": "uuid换成你自己的",
          "alterId": 64,
          "security": "加密方式自己选"
        }
      ]
    },
    "streamSettings": {
      "network": "ws"
    }
  },
  "inboundDetour": [],
  "outbound": {
    "protocol": "freedom",
   "settings": {}
  }
}
```
openshift搭建v2ray图文教程：

https://docs.google.com/document/d/17lLmEk3pp-IyNqqdtE100_0gpBwIetj71kwYzRrh4a4/edit?usp=sharing

youtube教程：https://www.youtube.com/watch?v=wdnWsEnMxac&t=96s
