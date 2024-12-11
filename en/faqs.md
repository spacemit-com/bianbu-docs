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

### Bianbu 1.0 apt update error: invalid: EXPKEYSIG 0C1C275F85F3A22A Bianbu Repo Signing Key

The detailed error is as follows,

```shell
W: GPG error: https://archive.bianbu.xyz/bianbu-ports mantic-porting InRelease: The following signatures were invalid: EXPKEYSIG 0C1C275F85F3A22A Bianbu Repo Signing Key <bianbu@spacemit.com>

E: The repository 'https://archive.bianbu.xyz/bianbu-ports mantic-porting InRelease' is not signed.
```

Since the signature of the Bianbu 1.0 source expired on November 27, 2024, you need to modify the /etc/apt/sources.list and /etc/apt/sources.list.d/bianbu.list files and add `[trusted=yes]`.

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

Delete the previous package index cache

```shell
sudo rm -r /var/lib/apt/lists
```

At this point, you can run `apt update` normally. Warnings can be ignored.
