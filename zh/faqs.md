---
sidebar_position: 9
---

# 常见问题

## 登录

### 普通用户忘记密码怎么解决？

普通用户忘记密码，可以通过root用户修改。以下是具体步骤。

1. 开机进入登录界面，如下图

   ![](static/tmps6urhcyi.PNG)

2. 按下键盘Ctrl + Alt + F3组合键（注意要先lock Fn），进入tty3终端，如下图

   ![](static/tmpw7385ih6.PNG)

3. 输入用户名`root`和密码，默认密码是`bianbu`，如下图

   ![](static/tmphgeanjg5.PNG)

4. 运行`export LANG=en_US.UTF-8`，临时修改终端语言，避免乱码

5. 运行`passwd 用户名`修改该用户密码，例如用户`bianbu`，如下图

   ![](static/tmpst8dy3yi.PNG)

6. 按下键盘Ctrl + Alt + F1组合键，切回登录界面，使用新密码登录即可。

## 更新

### Bianbu 1.0 apt update时报错

`invalid: EXPKEYSIG 0C1C275F85F3A22A Bianbu Repo Signing Key`

**原因：** 由于Bianbu 1.0已EOL，先已停止更新和维护，强烈建议用户更新到Bianbu V2.0使用。

**更新方法**

可以参考进迭时空论坛链接：https://forum.spacemit.com/t/topic/250

#### 1. 通过命令行打开图形化升级界面（推荐）

> 注：仅限 Bianbu Desktop版本。

```shell
do-release-upgrade -f DistUpgradeViewGtk3
```

#### 2. 完全通过命令行

根据提示逐步完成，然后重启

```shell
do-release-upgrade
```

#### 3. 通过软件更新器

> 注：仅限 Bianbu Desktop。

* 设备联网；

* 打开“软件更新器”；

* 等待检查更新完成；

* 发现新版本，点击升级；

* 根据提示逐步完成；

* 重启。
