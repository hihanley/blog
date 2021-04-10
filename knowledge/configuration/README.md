# 各种配置

## PowerShell窗口设置

```
字体 Lucida Console 14
窗口大小 120 50
窗口位置 0 0
颜色 屏幕背景 黑色 不透明度 85%
```

## Java编码配置

`JAVA_TOOL_OPTIONS -Dfile.encoding=UTF-8`

## v2ray服务端配置

<details>
  <summary>config.json</summary>
  
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
  
</details>
