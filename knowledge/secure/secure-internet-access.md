# Secure Internet Access

## Operations

- Git pull/push
- SSH
- Web request
- Telegram

## Resolvtions

### Client side v2ray multilayer proxy

<details>

  <summary>client config</summary>

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
              "tag": "one"
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
              "tag": "two",
              "proxySettings": {
                  "tag": "one"
              }
          },
          {
              "protocol": "vmess",
              "settings": {
                  "vnext": [
                      {
                          "address": "172.19.0.4",
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
              "tag": "three",
              "proxySettings": {
                  "tag": "two"
              }
          },
          {
              "protocol": "vmess",
              "settings": {
                  "vnext": [
                      {
                          "address": "172.19.0.5",
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
              "tag": "four",
              "proxySettings": {
                  "tag": "three"
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
                  "outboundTag": "four"
              }
          ]
      }
  }
  ```

</details>

### Server side v2ray multilayer proxy

<details>

  <summary>server config</summary>

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
  
</details>

<details>

  <summary>final server config</summary>

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

</details>

### V2ray + Tor

tor service Dockerfile

```docker
FROM ubuntu:latest

RUN apt update \
    && apt install tor -y

CMD ["/bin/tor"]
```

docker compose file

```yaml
version: "3"

services:
  one:
    image: "v2fly/v2fly-core"
    ports:
      - "443:443"
    volumes:
      - "./in_server.json:/etc/v2ray/config.json"
    networks:
      sia:
        ipv4_address: "172.19.0.2"

  two:
    build: "."
    volumes:
      - "./rc:/etc/tor/torrc"
    networks:
      sia:
        ipv4_address: "172.19.0.3"

networks:
  sia:
    ipam:
      config:
        - subnet: "172.19.0.0/16"
```

rc file

```text
SOCKSPort 172.19.0.3:9100
ExcludeNodes {cn},{hk},{mo},{kp},{ir},{sy},{pk},{cu},{vn}
StrictNodes 1
```

server config

```json
{
    "inbounds": [
        {
            "port": 443,
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
                        "address": "",
                        "port": 3389,
                        "users": [
                            {
                                "id": "",
                                "alterId": 64
                            }
                        ]
                    }
                ]
            },
            "proxySettings": {
                "tag": "tor"
            }
        },
        {
            "protocol": "socks",
            "settings": {
                "servers": [
                    {
                        "address": "172.19.0.3",
                        "port": 9100
                    }
                ]
            },
            "tag": "tor"
        }
    ]
}
```

client config

```json
{
    "outbounds": [
        {
            "protocol": "vmess",
            "settings": {
                "vnext": [
                    {
                        "address": "",
                        "port": 3389,
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
                        "address": "",
                        "port": 3389,
                        "users": [
                            {
                                "id": "",
                                "alterId": 64
                            }
                        ]
                    }
                ]
            },
            "tag": "proxy",
            "proxySettings": {
                "tag": "transit"
            }
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
                "outboundTag": "proxy"
            }
        ]
    }
}
```
