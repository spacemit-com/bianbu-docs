---
sidebar_position: 4
---

# Package Management

**Software Packages**

Bianbu software packages follow the Debian package standards and are managed using `apt`.

**Software Sources**

The software sources for Bianbu packages are:

- Bianbu 1.0: [http://archive.spacemit.com/bianbu-ports/](http://archive.spacemit.com/bianbu-ports/)
- Bianbu 2.0: [http://archive.spacemit.com/bianbu/](http://archive.spacemit.com/bianbu/)

## Update Software Sources

Use the following command to update the package list:

```shell
apt-get update
```

## Install or Update a Package

For example, to install or update the package `hello`, use:

```shell
apt-get install hello
```

## Remove a Package

To uninstall a package, for example, `hello`, use:

```shell
apt-get remove hello
```

If you also want to remove related configuration files, use:

```shell
apt-get purge hello
```
