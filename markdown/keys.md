---
title: IUS - Keys
permalink: /keys
---

# Package Signing Keys

All IUS packages are signed with a GPG signature.  By default, yum will verify
these signatures and refuse to install any packages that are not signed or have
bad signatures.  These signatures ensure that the packages you install are what
was produced by the IUS Project and have not been altered (accidentally or
maliciously) by any mirror or website that is providing the packages.

### RHEL/CentOS 7

- id: `rsa4096/4B274DF2 2018-12-17`
- fingerprint: `C958 7A09 A11F D706 4F0C A0F4 E558 0725 4B27 4DF2`
- [full key](https://repo.ius.io/RPM-GPG-KEY-IUS-7)

### RHEL/CentOS 6

- id: `rsa4096/74271A83 2018-12-17`
- fingerprint: `D304 C903 A324 3DEB A120 1973 6440 05F5 7427 1A83`
- [full key](https://repo.ius.io/RPM-GPG-KEY-IUS-6)

### Legacy Key

- id: `dsa1024/9CD4953F 2009-09-01`
- fingerprint: `8B84 6E3A B3FE 6462 74E8 670F DA22 1CDF 9CD4 953F`
- [full key](https://dl.ius.io/pub/IUS-COMMUNITY-GPG-KEY)

