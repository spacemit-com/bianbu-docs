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

### Bianbu 1.0 apt update时报错 invalid: EXPKEYSIG 0C1C275F85F3A22A Bianbu Repo Signing Key

详细报错如下，

```shell
W: GPG error: https://archive.bianbu.xyz/bianbu-ports mantic-porting InRelease: The following signatures were invalid: EXPKEYSIG 0C1C275F85F3A22A Bianbu Repo Signing Key <bianbu@spacemit.com>

E: The repository 'https://archive.bianbu.xyz/bianbu-ports mantic-porting InRelease' is not signed.
```

由于Bianbu 1.0 源的签名已于2024年11月27日过期，故需修改/etc/apt/sources.list和/etc/apt/sources.list.d/bianbu.list文件，追加`[trusted=yes]`。

/etc/apt/sources.list

```shell
deb [trusted=yes] https://archive.spacemit.com/bianbu-ports/ mantic/snapshots/<version> main multiverse restricted universe
deb [trusted=yes] https://archive.spacemit.com/bianbu-ports/ mantic-security/snapshots/<version> main multiverse restricted universe
```

/etc/apt/sources.list.d/bianbu.list

```shell
deb [trusted=yes] https://archive.spacemit.com/bianbu-ports/ mantic-spacemit/snapshots/<version> main multiverse restricted universe
deb [trusted=yes] https://archive.spacemit.com/bianbu-ports/ mantic-porting/snapshots/<version> main multiverse restricted universe
deb [trusted=yes] https://archive.spacemit.com/bianbu-ports/ mantic-customization/snapshots/<version> main multiverse restricted universe
```
