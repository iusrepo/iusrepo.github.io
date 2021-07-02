---
title: IUS - Usage
permalink: /usage
---

# Usage

## Safe Replacement Packages

Most IUS packages are safe replacement packages.  This is a term we use to
describe packages with the following properties.

* Replaces the functionality of a stock package.
* Uses a different name than the stock package to prevent unintended upgrades.
* [Provide][provides] the stock package name to satisfy the dependencies of
  other packages.
* [Conflict][conflicts] with the stock package.
* Must not [obsolete][obsoletes] any stock packages.

### Basic Installation

Safe replacement packages completely replace their stock equivalents, and
cannot be installed at the same time.  If the stock equivalent of an IUS
package is **not** already installed, then you can just install the IUS package
like any other package.

```
yum install mariadb103-server
```

### Yum Shell

If the stock equivalent of an IUS package is already installed, you must
uninstall it first.  If other packages depend on the installed stock package,
you can perform the removal and installation in a single transaction.  The
native way to do this is via [`yum shell`][yum-shell].

```
yum shell
> erase php-common php-fpm
> install php73-common php73-fpm
> run
```

### Yum Swap

You can also use the `yum swap` command, which serves as a simpler alternative
to `yum shell`.

_Note: yum swap is only available in RHEL/CentOS 7._

```
yum swap haproxy haproxy20
```

### DNF

[DNF][dnf] (also known as [yum4][yum4]) has an [`--allowerasing`][allowerasing]
flag to erase conflicting packages in the same transaction.  This suites our
needs perfectly since safe replacement packages conflict with their stock
equivalents.

_Note: dnf is only available in RHEL/CentOS 7._

```
yum install dnf
dnf --allowerasing install git222-core
```

## Parallel Installable Packages


IUS also maintains some parallel installable packages.  This is a term we use
to describe packages with the following properties.

* Uses a different name than the stock package so it can be installed at the
  same time as the stock package.
* Files from the package must use different names than files from stock
  packages to avoid file conflicts.
* Must not [provide][provides] the stock package name.
* Must not [conflict][conflicts] with the stock package.
* Must not [obsolete][obsoletes] any stock packages.

The [EPEL][epel] repository also contains parallel installable packages.  These
packages can be installed just like any other package.  The only special
consideration needed is that commands and file paths will be different.

[obsoletes]: https://rpm.org/user_doc/dependencies.html#obsoletes
[provides]: https://rpm.org/user_doc/dependencies.html#provides
[conflicts]: https://rpm.org/user_doc/dependencies.html#conflicts
[yum-shell]: https://linux.die.net/man/8/yum-shell
[dnf]: https://dnf.readthedocs.io
[yum4]: https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/7.9_release_notes/technology_previews#technology-preview_system-and-subscription-management
[allowerasing]: https://dnf.readthedocs.io/en/latest/cli_vs_yum.html#packages-replacement-without-yum-swap
[epel]: https://fedoraproject.org/wiki/EPEL
