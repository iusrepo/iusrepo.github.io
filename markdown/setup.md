---
title: IUS - Setup
permalink: /setup
---

# Setup

To enable the IUS repository on your system, install the **ius-release**
package.  This package contains the IUS repository configuration and public
package signing keys.  Many IUS packages have dependencies from the
[EPEL][epel] repository, so install the **epel-release** package as well.

### RHEL/CentOS 6

```
yum install \
https://repo.ius.io/ius-release-el6.rpm \
https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm
```

### RHEL/CentOS 7

```
yum install \
https://repo.ius.io/ius-release-el7.rpm \
https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
```

[epel]: https://fedoraproject.org/wiki/EPEL
