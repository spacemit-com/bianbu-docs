---
sidebar_position: 1
---

# 系统和Web后台登录

## 系统登录

- 系统管理员账户：`root`
- 密码：`bianbu`

串口查看NAS设备 IP 地址 `HOST_IP`：

```Bash
ifconfig
```

或者直接接入NAS 设备的WiFi热点。Bianbu NAS固件 v1.0.6版本之后支持。

- 热点名称：`BianbuAP`

- 热点密码：`12345678`

- HOST_IP：`10.0.0.1`

### SSH 登录

```Bash
ssh root@HOST_IP
```

## Web后台登录

- web管理员帐号：`admin`
- 密码：`openmediavault`

NAS设备上电上网之后，浏览器输入 `http://HOST_IP` 登录 Web 后台。
