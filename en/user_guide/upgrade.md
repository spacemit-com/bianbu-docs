---
sidebar_position: 3
---

# System Upgrade

Bianbu Desktop/NAS supports online upgrades.

## Choose the Subscription Version

Note: To upgrade from Bianbu 1.0.x to 2.0, you must first **update to 1.0.15 or later**, subscribe to 2.0, and continue the upgrade.

1. Open the **Software and Updates** application

    If you cannot open it, please confirm that you have upgraded to version 1.0.15 or later.

![Software and Updates](../static/6bc33876738265e409d2b802a0ee6238bfe384e2_2_690x388.jpeg)

2. Click the **Updates** tab, select the subscription (e.g., Bianbu 2.0) in **Subscribe**, and close it.

![Subscribe](../static/ba27b70fc486de4c26a592ea156dbe71b1df4a78.png)

## Upgrade

Note: Major version upgrades of Bianbu (e.g., from 1.0.15 to Bianbu 2.0.x) take a long time, approximately 2 hours, with multiple interactions in the last half hour. You can choose as needed (if unsure, select Next/Keep).

Note: Major version upgrades of Bianbu (e.g., from 1.0.15 to Bianbu 2.0.x) take a long time, approximately 2 hours. During the last half hour, there will be multiple interactions while configuring packages. You can choose as needed (if unsure, select Next/Keep). When asked whether to remove obsolete packages, select **Remove**.

If you encounter any issues during the upgrade, please refer to the [FAQs](../faqs.md#Update).

### Method 1: Open the Graphical Upgrade Interface via Command Line (Recommended)

Only for Bianbu Desktop.

```bash
do-release-upgrade -f DistUpgradeViewGtk3
```

### Method 2: Fully via Command Line

```bash
do-release-upgrade
```

Follow the prompts to complete the process, then restart.

### Method 3: Through the Software Updater

Only for Bianbu Desktop.

1. Connect the device to the internet;
2. Open the "Software Updater";
3. Wait for the update check to complete;
4. When a new version is found, click upgrade;
5. Follow the prompts to complete the process;
6. Restart.
