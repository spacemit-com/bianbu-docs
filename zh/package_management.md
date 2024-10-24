---
sidebar_position: 4
---

# 软件包管理

**软件包**

Bianbu 软件包遵循 Debian 软件包规范，使用 apt 管理。

**软件源**

软件源，即 Bianbu 软件包源：

- Bianbu 1.0: [http://archive.spacemit.com/bianbu-ports/](http://archive.spacemit.com/bianbu-ports/)
- Bianbu 2.0: [http://archive.spacemit.com/bianbu/](http://archive.spacemit.com/bianbu/)

## 更新软件源

```shell
apt-get update
```

## 安装或更新软件包

例如安装或更新软件包 `hello`：

```shell
apt-get install hello
```

## 卸载软件包

例如卸载 `hello`：

```shell
apt-get remove hello
```

如需删除相关的配置文件：

```shell
apt-get purge hello
```
