---
title: IUS - About
permalink: /about
---

# About

IUS is a yum repository that provides newer versions of select software for
RHEL and CentOS.  It started as an internal experiment at
[Rackspace][rackspace] before being transitioned into a community project.  The
packages we offer enable our users to combine a stable base operating system
with a faster moving application stack.  Our packages are designed to be used
on an individual opt-in basis, so the repository can be enabled and not
override other unrelated packages on your system.

### Stability Versus Features

The 10 year lifecycle of Red Hat Enterprise Linux is impressive, but it is only
possible by prioritizing stability and security over new features.  The nature
of the distribution leads many stock packages getting far behind their
respective upstream projects.  Red Hat routinely [backports][backports]
security and bug fixes, but is limited in adding new features in order to
maintain compatibility.  Major version upgrades are typically not possible.

This results in a high quality, secure, and stable operating system.  However,
the older package versions can sometimes be frustrating to users when they want
to use features from newer versions.  There are times when users are willing to
sacrifice some of that stability in order to gain access to those features.

### Safe Replacement

Our packages use different names than their stock equivalents.  Using the same
name would implicitly obsolete the stock package.  The goal of IUS is to avoid
this.

IUS primarily offers safe replacement packages.  This means that our packages
both provide and conflict with their stock equivalents, but don't obsolete
them.  In some cases we will also provide parallel-installable packages.
Unlike safe replacement packages, parallel-installable packages can be
installed at the same time as their stock equivalents.  This is necessary in
situations when replacing the stock package would break other parts of the
system.

This unique approach ensures that a stock package will never be unexpectedly
replaced by an IUS package just because the repository is enabled.  Only
packages you explicitly request (and their dependencies) will be installed.

### Inline With Upstream Stable

Our packages track the latest upstream versions from their respective upstream
projects.  They are named in accordance with what the upstream considers a
"major version" or a "branch".  Not all project follow [semantic
versioning][semver], so this may be the first segment of the version (i.e. `2`)
or the first and second segments (i.e. `2.4`).  As expected, they will only be
updated to the latest version of that major version branch.  They will never be
updated to the next major version.

There is an inherent risk with this approach.  New upstream versions may
introduce bugs that users of stock packages will never have to deal with.  IUS
users are implicitly agreeing to forfeit a small part of their system stability
in order to get the new features they desire.

To help mitigate this risk, new IUS packages are first made available in the
ius-testing repository before being promoted to the main repository.  When you
install [ius-release][setup], the ius-testing repository is disabled by
default.  You can enable it in non-production environments to help identify any
potential issues early.  Report any issues you find on [GitHub][issues].

### History

IUS started as an internal experiment at [Rackspace][rackspace] in 2006.
Rackspace customers would regularly request newer versions of PHP and MySQL.
These newer version were packaged elsewhere, but in repositories that would
obsolete other stock packages besides what was needed.  Rackspace engineers
decided to solve this problem for their customers by creating packages with
different names than the stock packages.  Because the package names were
different, a system could enable the repository and have no changes take place
other than the requested replacement.  This naming scheme also allowed multiple
major versions of packages to exist in the same repository, rather than
requiring multiple repositories.  All upgrades were on an individual, opt-in
basis.  This gave customers the flexibility and control they were looking for.

In 2009 the project was transitioned into a community project.  Issues and new
package requests were initially tracked on [Launchpad][launchpad], but in 2013
we switched to [GitHub][github].  Package builds were handled on a private
Rackspace build farm until 2019, when we switched to [Cirrus CI][cirrus].  For
many years we relied on a network of mirrors to distribute our content, but in
2019 we switched to a [Rackspace CDN][cdn].

[rackspace]: https://www.rackspace.com
[backports]: https://access.redhat.com/security/updates/backporting
[semver]: https://semver.org
[setup]: /setup
[issues]: https://github.com/search?q=org%3Aiusrepo+topic%3Arpm
[launchpad]: https://launchpad.net/ius
[github]: https://github.com/iusrepo
[cirrus]: https://cirrus-ci.com/github/iusrepo
[cdn]: https://www.rackspace.com/en-us/cloud/cdn-content-delivery-network
