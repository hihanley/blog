# V2Ray

## V2Ray Server Config

```json
{
    "inbounds": [
        {
            "listen": "0.0.0.0",
            "port": 1080,
            "protocol": "http",
            "settings": {
                "timeout": 0,
                "allowTransparent": false
            },
            "tag": "http"
        },
        {
            "listen": "0.0.0.0",
            "port": 1081,
            "protocol": "socks",
            "settings": {
                "auth": "noauth",
                "ip": "${本机IP}",
                "udp": true
            },
            "tag": "socks"
        }
    ],
    "outbounds": [
        {
            "protocol": "vmess",
            "settings": {
                "vnext": [
                    {
                        "address": "${SERVER}",
                        "port": 1080,
                        "users": [
                            {
                                "id": "${UUID}",
                                "alterId": 64
                            }
                        ]
                    }
                ]
            },
            "tag": "proxy"
        },
        {
            "protocol": "freedom",
            "tag": "direct"
        }
    ],
    "routing": {
        "domainStrategy": "IPOnDemand",
        "rules": [
            {
                "type": "field",
                "ip": [
                    "geoip:private"
                ],
                "outboundTag": "direct"
            },
            {
                "type": "field",
                "inboundTag": "http",
                "outboundTag": "proxy"
            },
            {
                "type": "field",
                "inboundTag": "socks",
                "outboundTag": "proxy"
            }
        ]
    }
}
```
