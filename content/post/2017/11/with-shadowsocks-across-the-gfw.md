---
title: "Shadowsocks科学上网"
date: 2017-11-24T23:34:18+08:00
draft: false
---

---
#### shadowsocks是什么
  shadowsocks是一款基于socks5的代理，在国内被广泛用于科学上网
  
---

### 准备工作
  要使用shadowsocks科学上网，首先你得有一台位于墙外边的服务器，这里推荐[搬瓦工](https://bandwagonhost.com/aff.php?aff=7877)的
VPS，由于搬瓦工已经被墙，上不去的同学可以访问[国内官方地址](https://bwh1.net/index.php)。关于购买以及其他事宜，以后我会专门写一篇来介绍

---

### shadowsocks服务器端配置
第一步: 先安装 shadowsocks
```bash
pip install shadowsocks 
```

第二步: 生成`/etc/shadowsocks.json`内容如下
```json
{
    "server":"my_server_ip",
    "server_port":8388,
    "password":"barfoo!",
    "timeout":600,
    "method":"aes-256-cfb"
}
```
每个字段的含义：

  - server: 主机的ip
  - server_port: shadowsocks监听的端口
  - password: 用于加密的密码
  - timeout: 连接过期时间
  - method: 加密算法，加密算法建议先用 `aes-256-cfb`，想更换加密算法的可以参考[官网](https://shadowsocks.org/en/spec/Stream-Ciphers.html)

第三步：启动
```bash
ssserver -c /etc/shadowsocks.json start
```
shadowsocks服务器端起来之后，可以先用客户端连接下，看一看是否已经可以科学上网，确认无误后，进行下一步

第四部：设置开机自启

使用systemd来管理，添加 `/etc/systemd/system/shadowsocks.service`内容如下
```
[Unit]
Description=Shadowsocks Server
After=network.target

[Service]
Type=simple
User=root
ExecStart=/usr/local/bin/ssserver -c /etc/shadowsocks.json

[Install]
WantedBy=multi-user.target
```

注意把 `/usr/local/bin/ssserver`替换成你系统中`ssserver`的绝对路径

最后:
```bash
sudo systemctl enable /etc/systemd/system/shadowsocks.service
```

以上就是 `shadowsocks` 的服务器端配置
