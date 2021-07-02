---
title: IUS - Setup
permalink: /setup
---

# Setup

To enable the IUS repository on your system, install the **ius-release**
package.  This package contains the IUS repository configuration and public
package signing keys.  Many IUS packages have dependencies from the
[EPEL][epel] repository, so install the **epel-release** package as well.

### RHEL/CentOS 7

```
yum install \
https://repo.ius.io/ius-release-el7.rpm \
https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
```

### Testing

IUS packages are first made available in the ius-testing repository before
being promoted to the main repository.  When you install ius-release, the
ius-testing repository is disabled by default.  Enable it if you would like to
participate in testing new IUS packages.

```
yum install yum-utils
yum-config-manager --enable ius-testing
```

[epel]: https://fedoraproject.org/wiki/EPEL
