---
sidebar_position: 3
---

# 系统升级

Bianbu Desktop/NAS 支持在线升级。

## 选择订阅的版本

提示：Bianbu 1.0.x 升级到2.0，需先**更新到1.0.15之后**，订阅2.0并继续升级。

1. 打开**软件和更新**应用

   如无法打开，请确认已升级到1.0.15或更高版本。

![软件和更新](../static/6bc33876738265e409d2b802a0ee6238bfe384e2_2_690x388.jpeg)

2. 点击**更新**标签页，**订阅**中选择（如Bianbu2.0），并关闭

![订阅](../static/ba27b70fc486de4c26a592ea156dbe71b1df4a78.png)

## 升级

提示：Bianbu 大版本升级（如1.0.15 升级到Bianbu 2.0.x）耗时较久，预计2小时，其中最后半小时内会有多次交互，可按需选择（如不清楚，可选择Next/保留）。

### 方式1：通过命令行打开图形化升级界面（推荐）

仅限 Bianbu Desktop。

```bash
do-release-upgrade -f DistUpgradeViewGtk3
```

### 方式2：完全通过命令行

```bash
do-release-upgrade
```

根据提示逐步完成，然后重启。

### 方式3：通过软件更新器

仅限 Bianbu Desktop。

1. 设备联网；
2. 打开“软件更新器”；
3. 等待检查更新完成；
4. 发现新版本，点击升级；
5. 根据提示逐步完成；
6. 重启。
