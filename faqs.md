---
sidebar_position: 5
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
