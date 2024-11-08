---
sidebar_position: 9
---

# FAQs

## Login

### What to do if a regular user forgets their password?

If a regular user forgets their password, it can be changed by the root user. Here are the specific steps.

1. Boot into the login screen, as shown below

   ![](static/tmps6urhcyi.PNG)

2. Press the Ctrl + Alt + F3 key combination (make sure to lock Fn first) to enter the tty3 terminal, as shown below

   ![](static/tmpw7385ih6.PNG)

3. Enter the username `root` and password, the default password is `bianbu`, as shown below

   ![](static/tmphgeanjg5.PNG)

4. Run `export LANG=en_US.UTF-8` to temporarily change the terminal language to avoid garbled text

5. Run `passwd username` to change the user's password, for example, for the user `bianbu`, as shown below

   ![](static/tmpst8dy3yi.PNG)

6. Press the Ctrl + Alt + F1 key combination to switch back to the login screen and log in with the new password.
