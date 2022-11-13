# V2Ray

## 服务端一键安装

<https://github.com/233boy/v2ray/wiki/V2Ray>一键安装脚本

```bash
bash <(curl -s -L https://git.io/v2ray.sh)
```

## 官方纯净安装

<https://github.com/v2fly/fhs-install-v2ray/blob/master/README.zh-Hans-CN.md>

安装可执行文件和 .dat 数据文件

```bash
bash <(curl -L https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh)
```

只更新 .dat 数据文件

```bash
bash <(curl -L https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-dat-release.sh)
```

卸载

```bash
bash <(curl -L https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh) --remove
```

## 客户端配置

```json
{
    "inbounds": [
        {
            "port": 1080, // 监听端口
            "protocol": "socks", // 入口协议为 SOCKS 5
            "sniffing": {
                "enabled": true,
                "destOverride": ["http", "tls"]
            },
            "settings": {
                "auth": "noauth"
            }
        }
    ],
    "outbounds": [
        {
            "protocol": "vmess", // 出口协议
            "settings": {
                "vnext": [
                    {
                        "address": "serveraddr.com",
                        "port": 16823, // 服务器端口
                        "users": [
                            {
                                "id": "b831381d-6324-4d53-ad4f-8cda48b30811",
                                "alterId": 0
                            }
                        ]
                    }
                ]
            }
        }
    ]
}
```

## 客户端链式代理配置

```json
{
    "outbounds": [
        {
            "protocol": "vmess",
            "settings": {
                "vnext": [
                    {
                        "address": "172.19.0.2",
                        "port": 40000,
                        "users": [
                            {
                                "id": "",
                                "alterId": 64
                            }
                        ]
                    }
                ]
            },
            "tag": "transit"
        },
        {
            "protocol": "vmess",
            "settings": {
                "vnext": [
                    {
                        "address": "172.19.0.3",
                        "port": 40000,
                        "users": [
                            {
                                "id": "",
                                "alterId": 64
                            }
                        ]
                    }
                ]
            },
            "tag": "final",
            "proxySettings": {
                "tag": "transit"
            }
        }
    ],
    "routing": {
        "domainStrategy": "IPOnDemand",
        "rules": [
            {
                "type": "field",
                "ip": [
                    "172.19.0.6"
                ],
                "outboundTag": "final"
            }
        ]
    }
}
```

## 服务端链式代理配置

transit server config

```json
{
    "inbounds": [
        {
            "port": 40000,
            "protocol": "vmess",
            "settings": {
                "clients": [
                    {
                        "id": "",
                        "alterId": 64
                    }
                ],
                "disableInsecureEncryption": true
            }
        }
    ],
    "outbounds": [
        {
            "protocol": "vmess",
            "settings": {
                "vnext": [
                    {
                        "address": "172.19.0.3",
                        "port": 40000,
                        "users": [
                            {
                                "id": "",
                                "alterId": 64
                            }
                        ]
                    }
                ]
            }
        }
    ]
}
```

final server config

```json
{
    "inbounds": [
        {
            "port": 3389,
            "protocol": "vmess",
            "settings": {
                "clients": [
                    {
                        "id": "",
                        "alterId": 64
                    }
                ],
                "disableInsecureEncryption": true
            }
        }
    ],
    "outbounds": [
        {
            "protocol": "freedom"
        }
    ]
}
```
