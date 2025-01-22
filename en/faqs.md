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

## Update

### Bianbu 1.0 apt update error

`invalid: EXPKEYSIG 0C1C275F85F3A22A Bianbu Repo Signing Key`

This is due to Bianbu V1.0 is EOL， please upgrade to V2.0.

#### 1. Reflashing

This option is best for users who don’t need to keep any data and prefer a fresh installation of the new firmware.

- Use the SpacemiT's fashing tool, Titan Flasher, to flash the complete system image. You can download the image here:
https://archive.spacemit.com/image/k1/version/bianbu/
- Please refer to Fashing Guide in our community platform for detailed instructions on using the this tool:
https://developer.spacemit.com/documentation?token=O6wlwlXcoiBZUikVNh2cczhin5d

#### 2. Graphical Upgrade Interface with Command Line / Terminal (Recommended)

> Note:This method is only available for Bianbu Desktop users.

To upgrade via the command line and access the graphical upgrade interface, run the following command:

```shell
do-release-upgrade -f DistUpgradeViewGtk3
```

#### 3. Full Command Line / Terminal Upgrade

Follow the prompts step by step to complete the upgrade, then restart the system.

To start the upgrade, run the command:

```shell
do-release-upgrade
```

#### 4. Upgrade via Software Updater

Note: This method is only available for Bianbu Desktop users.

- Ensure your device is connected to the internet
- Open the "Software Updater" application
- Wait while the updater checks for available updates
- Click "Upgrade" if a new version is found
- Follow the on-screen prompts to finish the upgrade
- Restart your device once the upgrade is complete

**Notes:**

- It may take up to 2 hours for the major version upgrades (e.g., from 1.0.15 to Bianbu 2.0.x)
- If you are running a version older than V1.0.15, the upgrade process will first update your system to V1.0.15. After that, and you’ll need to repeat the process to upgrade to V2.0.

### Possible Issues During Bianbu 2.0.x Upgrade

#### Prompt: `Please install all available updates for your release before upgrading`

Reason: Some installed package versions do not match the versions in the software source.

Solution:

1. Run `sudo apt upgrade` to reinstall the versions from the source.

2. Re-run `do-release-upgrade -f DistUpgradeViewGtk3`.

If the prompt `Please install all available updates for your release before upgrading` still appears, run `apt list --upgradable` to check for available updates. The possible package list and handling methods are as follows:

| Package Name                 | Handling Method                                      |
| :--------------------------- | :--------------------------------------------------- |
| thunderbird-local-zh-cn      | Temporarily uninstall with `sudo apt remove thunderbird-local-zh-cn` |
| thunderbird-local-zh-cn-hans | Temporarily uninstall with `sudo apt remove thunderbird-local-zh-cn-hans` |

## Feedback

If you still have issues, you can provide feedback through any of the following channels:

1. [Submit issues on Gitee](https://gitee.com/bianbu/bianbu-docs/issues)
2. [Developer Forum](https://forum.spacemit.com/)
3. [Submit a ticket](https://ticket.spacemit.com/projects/main/issues/new)
