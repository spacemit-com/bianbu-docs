---
sidebar_position: 2
---

# Installation and Upgrade

## Installation

Bianbu firmware can be flashed using Titan Flasher, via fastboot commands, or by writing to an SD card with the system booting from the SD card.

### Flashing with Titan Flasher

Firmware in `.zip` format is suitable for Titan Flasher.

Refer to the "[Firmware Update Tool](https://developer.spacemit.com/documentation?token=B9JCwRM7RiBapHku6NfcPCstnqh)" for detailed steps.

### Flashing with Fastboot

Unzip the `.zip` firmware file and flash it with fastboot.

#### Prerequisites

1. Connect the device to the PC using a USB cable.
2. Ensure fastboot is installed on the computer.

#### Flashing Steps

1. Unzip the firmware.
2. Download the [flash-all.zip](https://archive.spacemit.com/image/k1/flash-all.zip) script and unzip it in the firmware directory.
3. Enter fastboot mode:

    ```bash
    reboot fastboot
    ```

   Wait for the device to reboot into fastboot mode.

4. Run the flash-all script and wait for the flashing to complete.
   - On a Linux PC, make the `flash-all.sh` executable before running it.
   - On a Windows PC, run `flash-all.bat`.
5. Once flashing is complete, power off the device and reboot to enter the system.

### Writing to SD Card and Booting

Firmware ending with `img.zip` is for SD cards. Use `dd` command or [balenaEtcher](https://etcher.balena.io/) to write to the SD card. Note, this method is not suitable for eMMC.

#### Steps

1. Write the firmware to the SD card.
2. Insert the SD card into the device.
3. Power on the device to boot.

## Upgrade

Bianbu Desktop/NAS supports online upgrades.

### Via Command Line

Run the following command:

```bash
sudo do-release-upgrade
```

Follow the prompts to complete the process and then restart the device.

### Via Software Updater (Bianbu Desktop Only)

1. Ensure the device is connected to the internet.
2. Open the "Software Updater."
3. Wait for updates to be checked.
4. If a new version is found, click to upgrade and follow the prompts.
5. Restart the device once the upgrade is complete.

These methods enable effective installation and upgrading of the Bianbu system.
