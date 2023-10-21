# Варианты inbound

В данном примере мы рассмотрим все варианты inbound доступные в xray-core&#x20;

{% hint style="info" %}
Рекомендуется изменить и настроить указанные в примерах порты, SNI и другие данные под себя
{% endhint %}

## VLESS

### VLESS **TCP** REALITY

```json
 {
            "tag": "VLESS TCP REALITY",
            "listen": "0.0.0.0",
            "port": 2040,
            "protocol": "vless",
            "settings": {
                "clients": [],
                "decryption": "none"
            },
            "streamSettings": {
                "network": "tcp",
                "tcpSettings": {},
                "security": "reality",
                "realitySettings": {
                    "show": false,
                    "dest": "tradingview.com:443",
                    "xver": 0,
                    "serverNames": [
                        "tradingview.com"
                    ],
                    "privateKey": "CGT_YQt0HWMfX7XcvZhdzChag8401evaHVWs3KaPw0U",
                    "shortIds": [
                        "",
                        "6ba85179e30d4fc2"
                    ]
                }
            },
            "sniffing": {
                "enabled": true,
                "destOverride": [
                    "http",
                    "tls"
                ]
            }
        },
```

### VLESS GRPC REALITY

```json
{
            "tag": "VLESS GRPC REALITY",
            "listen": "0.0.0.0",
            "port": 2041,
            "protocol": "vless",
            "settings": {
                "clients": [],
                "decryption": "none"
            },
            "streamSettings": {
                "network": "grpc",
                "grpcSettings": {
                    "serviceName": "xyz"
                },
                "security": "reality",
                "realitySettings": {
                    "show": false,
                    "dest": "discordapp.com:443",
                    "xver": 0,
                    "serverNames": [
                        "cdn.discordapp.com",
                        "discordapp.com"
                    ],
                    "privateKey": "MMX7m0Mj3faUstoEm5NBdegeXkHG6ZB78xzBv2n3ZUA",
                    "shortIds": [
                        "",
                        "6ba85179e30d4fc2"
                    ]
                }
            },
            "sniffing": {
                "enabled": true,
                "destOverride": [
                    "http",
                    "tls"
                ]
            }
        },
```

### VLESS H2 REALITY

```json
       {
            "tag": "VLESS H2 REALITY",
            "listen": "0.0.0.0",
            "port": 2042,
            "protocol": "vless",
            "settings": {
              "clients": [],
              "decryption": "none"
            },
            "streamSettings": {
              "network": "h2",
              "security": "reality",
              "realitySettings": {
                "show": true,
                "dest": "web.dev:443",
                "xver": 0,
                "serverNames": [
                  "web.dev"
                ],
                "privatekey": "OPNgJisoHtWNEW9TbX0dFOmnKnxaVDRfffYMCKTdhGs",
                "shortIds": [
                  "fb8bb9e825f65563"
                ]
              }
            },
            "sniffing": {
              "enabled": true,
              "destOverride": [
                "http",
                "tls"
              ]
            }
          },
```

### VLESS TCP Tls

```json
         {
              "tag": "VLESS TCP Tls",
              "listen": "0.0.0.0",
              "port": 2043,
              "protocol": "vless",
              "settings": {
                  "clients": [],
                  "decryption": "none"
              },
              "streamSettings": {
                  "network": "tcp",
                  "security": "tls",
                  "tlsSettings": {
                      "serverName": "SERVER_NAME",
                      "certificates": [
                          {
                              "ocspStapling": 3600,
                              "certificateFile": "/var/lib/marzban/certs/fullchain.pem",
                              "keyFile": "/var/lib/marzban/certs/key.pem"
                          }
                      ],
                      "minVersion": "1.2",
                      "cipherSuites": "TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305_SHA256:TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256:TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384:TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384:TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256:TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256"
                  }
              }
          },
```

### VLESS TCP NO TLS

```json
      {
          "tag": "VLESS TCP NO TLS",
          "listen": "0.0.0.0",
          "port": 2044,
          "protocol": "vless",
          "settings": {
              "clients": [],
              "decryption": "none"
          },
          "streamSettings": {
              "network": "tcp"
          }
      },
```

### VLESS TCP Header

```json
      {
        "tag": "VLESS TCP Header",
        "listen": "0.0.0.0",
        "port": 2045,
        "protocol": "vless",
        "settings": {
            "clients": [],
            "decryption": "none"
        },
        "streamSettings": {
            "network": "tcp",
            "tcpSettings": {
                "header": {
                    "type": "http",
                    "request": {
                        "method": "GET",
                        "path": [
                            "/"
                        ],
                        "headers": {
                            "Host": [
                                "google.com"
                            ]
                        }
                    },
                    "response": {}
                }
            },
            "security": "none"
        },
        "sniffing": {
            "enabled": true,
            "destOverride": [
                "http",
                "tls"
            ]
        }
    },
```

### VLESS WS Tls

```json
    {
        "tag": "VLESS WS Tls",
        "listen": "0.0.0.0",
        "port": 2046,
        "protocol": "vless",
        "settings": {
            "clients": [],
            "decryption": "none"
        },
        "streamSettings": {
            "network": "ws",
            "wsSettings": {
                "path": "/"
            }
             ,
             "security": "tls",
             "tlsSettings": {
                 "serverName": "SERVER_NAME",
                 "certificates": [
                     {
                         "ocspStapling": 3600,
                         "certificateFile": "/var/lib/marzban/certs/fullchain.pem",
                         "keyFile": "/var/lib/marzban/certs/key.pem"
                     }
                 ],
                 "minVersion": "1.2",
                 "cipherSuites": "TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305_SHA256:TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256:TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384:TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384:TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256:TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256"
             }
        }
    },
```

### VLESS WS

```json
   {
            "tag": "VLESS WS",
            "listen": "0.0.0.0",
            "port": 2047,
            "protocol": "vless",
            "settings": {
                "clients": [],
                "decryption": "none"
            },
            "streamSettings": {
                "network": "ws",
                "security": "none",
                "wsSettings": {
                    "path": "/"
                }
            },
            "sniffing": {
                "enabled": true,
                "destOverride": [
                    "http",
                    "tls"
                ]
            }
        },
```

### VLESS WS Header

```json
        {
            "tag": "VLESS WS Header",
            "listen": "0.0.0.0",
            "port": 2048,
            "protocol": "vless",
            "settings": {
                "clients": [],
                "decryption": "none"
            },
            "streamSettings": {
                "network": "ws",
                "security": "none",
                "wsSettings": {
                    "path": "/",
                    "headers": {
                        "Host": "google.com"
                    }
                }
            },
            "sniffing": {
                "enabled": true,
                "destOverride": [
                    "http",
                    "tls"
                ]
            }
        },
```

### VLESS GRPC

```json
        {
            "tag": "VLESS GRPC",
            "listen": "0.0.0.0",
            "port": 2049,
            "protocol": "vless",
            "settings": {
                "clients": [],
                "decryption": "none"
            },
            "streamSettings": {
                "network": "grpc",
                "grpcSettings": {
                    "serviceName": "/"
                }
                 ,
                 "security": "tls",
                 "tlsSettings": {
                     "serverName": "SERVER_NAME",
                     "certificates": [
                         {
                             "ocspStapling": 3600,
                             "certificateFile": "/var/lib/marzban/certs/fullchain.pem",
                             "keyFile": "/var/lib/marzban/certs/key.pem"
                         }
                     ],
                     "minVersion": "1.2",
                     "cipherSuites": "TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305_SHA256:TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256:TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384:TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384:TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256:TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256"
                 }
            }
        },
```

## VMESS

### VMESS TCP TLS

```json
        {
            "tag": "VMESS TCP TLS",
            "listen": "0.0.0.0",
            "port": 2050,
            "protocol": "vmess",
            "settings": {
                "clients": []
            },
            "streamSettings": {
                "network": "tcp",
                "security": "tls",
                "tlsSettings": {
                    "serverName": "SERVER_NAME",
                    "certificates": [
                        {
                            "ocspStapling": 3600,
                            "certificateFile": "/var/lib/marzban/certs/fullchain.pem",
                            "keyFile": "/var/lib/marzban/certs/key.pem"
                        }
                    ],
                    "minVersion": "1.2",
                    "cipherSuites": "TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305_SHA256:TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256:TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384:TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384:TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256:TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256"
                }
            }
        },
```

### VMESS TCP

```json
        {
            "tag": "VMESS TCP",
            "listen": "0.0.0.0",
            "port": 2051,
            "protocol": "vmess",
            "settings": {
                "clients": []
            },
            "streamSettings": {
                "network": "tcp"
                }
        },
```

### VMess TCP Header

```json
    {
        "tag": "VMess TCP Header",
        "listen": "0.0.0.0",
        "port": 2052,
        "protocol": "vmess",
        "settings": {
            "clients": []
        },
        "streamSettings": {
            "network": "tcp",
            "tcpSettings": {
                "header": {
                    "type": "http",
                    "request": {
                        "method": "GET",
                        "path": [
                            "/"
                        ],
                        "headers": {
                            "Host": [
                                "google.com"
                            ]
                        }
                    },
                    "response": {}
                }
            },
            "security": "none"
        },
        "sniffing": {
            "enabled": true,
            "destOverride": [
                "http",
                "tls"
            ]
        }
    },
```

### Vmess WS TLS

```json
    {
        "tag": "Vmess WS TLS",
        "listen": "0.0.0.0",
        "port": 2053,
        "protocol": "vmess",
        "settings": {
            "clients": []
        },
        "streamSettings": {
            "network": "ws",
            "wsSettings": {
                "path": "/"
            }
             ,
             "security": "tls",
             "tlsSettings": {
                 "serverName": "SERVER_NAME",
                 "certificates": [
                     {
                         "ocspStapling": 3600,
                         "certificateFile": "/var/lib/marzban/certs/fullchain.pem",
                         "keyFile": "/var/lib/marzban/certs/key.pem"
                     }
                 ],
                 "minVersion": "1.2",
                 "cipherSuites": "TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305_SHA256:TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256:TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384:TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384:TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256:TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256"
             }
        }
    },
```

### Vmess WS

```json
    {
        "tag": "Vmess WS",
        "listen": "0.0.0.0",
        "port": 2054,
        "protocol": "vmess",
        "settings": {
            "clients": []
        },
        "streamSettings": {
            "network": "ws",
            "security": "none",
            "wsSettings": {
                "path": "/"
            }
        },
        "sniffing": {
            "enabled": true,
            "destOverride": [
                "http",
                "tls"
            ]
        }
    },
```

### Vmess WS Header

```json
    {
        "tag": "Vmess WS Header",
        "listen": "0.0.0.0",
        "port": 2055,
        "protocol": "vmess",
        "settings": {
            "clients": []
        },
        "streamSettings": {
            "network": "ws",
            "security": "none",
            "wsSettings": {
                "path": "/",
                "headers": {
                    "Host": "google.com"
                }
            }
        },
        "sniffing": {
            "enabled": true,
            "destOverride": [
                "http",
                "tls"
            ]
        }
    },
```

### VMESS GRPC

```json
    {
        "tag": "VMESS GRPC",
        "listen": "0.0.0.0",
        "port": 2056,
        "protocol": "vmess",
        "settings": {
            "clients": []
        },
        "streamSettings": {
            "network": "grpc",
            "grpcSettings": {
                "serviceName": "/"
            }
             ,
             "security": "tls",
             "tlsSettings": {
                 "serverName": "SERVER_NAME",
                 "certificates": [
                     {
                         "ocspStapling": 3600,
                         "certificateFile": "/var/lib/marzban/certs/fullchain.pem",
                         "keyFile": "/var/lib/marzban/certs/key.pem"
                     }
                 ],
                 "minVersion": "1.2",
                 "cipherSuites": "TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305_SHA256:TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256:TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384:TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384:TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256:TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256"
             }
        }
    },
```

## TROJAN

### TROJAN TCP TLS

```json
    {
        "tag": "TROJAN TCP TLS",
        "listen": "0.0.0.0",
        "port": 2057,
        "protocol": "trojan",
        "settings": {
            "clients": []
        },
        "streamSettings": {
            "network": "tcp",
            "security": "tls",
            "tlsSettings": {
                "serverName": "SERVER_NAME",
                "certificates": [
                    {
                        "ocspStapling": 3600,
                        "certificateFile": "/var/lib/marzban/certs/fullchain.pem",
                        "keyFile": "/var/lib/marzban/certs/key.pem"
                    }
                ],
                "minVersion": "1.2",
                "cipherSuites": "TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305_SHA256:TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256:TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384:TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384:TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256:TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256"
            }
        }
    },
```

### TROJAN WS TLS

```json
    {
        "tag": "TROJAN WS TLS",
        "listen": "0.0.0.0",
        "port": 2058,
        "protocol": "trojan",
        "settings": {
            "clients": []
        },
        "streamSettings": {
            "network": "ws",
            "wsSettings": {
                "path": "/"
            }
             ,
             "security": "tls",
             "tlsSettings": {
                 "serverName": "SERVER_NAME",
                 "certificates": [
                     {
                         "ocspStapling": 3600,
                         "certificateFile": "/var/lib/marzban/certs/fullchain.pem",
                         "keyFile": "/var/lib/marzban/certs/key.pem"
                     }
                 ],
                 "minVersion": "1.2",
                 "cipherSuites": "TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305_SHA256:TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256:TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384:TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384:TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256:TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256"
             }
        }
    },
```

### TROJAN GRPC TLS

```json
    {
        "tag": "TROJAN GRPC TLS",
        "listen": "0.0.0.0",
        "port": 2059,
        "protocol": "trojan",
        "settings": {
            "clients": []
        },
        "streamSettings": {
            "network": "grpc",
            "grpcSettings": {
                "serviceName": "/"
            }
             ,
             "security": "tls",
             "tlsSettings": {
                 "serverName": "SERVER_NAME",
                 "certificates": [
                     {
                         "ocspStapling": 3600,
                         "certificateFile": "/var/lib/marzban/certs/fullchain.pem",
                         "keyFile": "/var/lib/marzban/certs/key.pem"
                     }
                 ],
                 "minVersion": "1.2",
                 "cipherSuites": "TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305_SHA256:TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256:TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384:TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384:TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256:TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256"
             }
        }
    },
```

## SHADOWSOCKS

```json
    {
        "tag": "SHADOWSOCKS",
        "listen": "0.0.0.0",
        "port": 2060,
        "protocol": "shadowsocks",
        "settings": {
            "clients": [],
            "network": "tcp,udp"
        }
    }
```

## WIREGUARD

```json
{
  "tag": "warp",
  "protocol": "wireguard",
  "settings": {
    "secretKey": "Your_Secret_Key",
    "DNS": "1.1.1.1",
    "address": ["172.16.0.2/32", "2606:4700:110:8756:9135:af04:3778:40d9/128"],
    "peers": [
      {
        "publicKey": "bmXOC+F1FxEMF9dyiK2H5/1SUtzH0JuVo51h2wPfgyo=",
        "endpoint": "engage.cloudflareclient.com:2408"
      }
    ]
  }
}
```
