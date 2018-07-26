---
title: "Tcpdump常用命令"
date: 2018-07-26T20:45:20+08:00
draft: false
---
#### 指定特定 `interface`:

```shell
$ tcpdump -i eth1
```


#### 指定 `ip`
```shell
$ tcpdump host 10.42.133.213
```

#### 指定端口:
```shell
$ tcpdump port 8080
$ tcpdump src port 8080
$ tcpdump des port 8080
```
#### 组合
```shell
$ tcpdump -i eh1 host 10.42.133.213 and port 8000
```

#### 参考：
- http://www.tcpdump.org/

