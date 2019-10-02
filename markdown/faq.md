---
title: IUS - FAQ
permalink: /faq
---

# Frequently Asked Questions

### Is IUS a Rackspace service or product?

No.  Rackspace is not obligated to provide support of any kind for IUS
packages.  Using IUS does not make you a Rackspace customer.

If you are a Rackspace customer, service level agreements (SLA) don't apply to
IUS packages.  Contact your account manager if you have further questions.

### What is the relationship between Rackspace and IUS?

IUS is sponsored by Rackspace, but is not a service or product of Rackspace.
It is similar to the relationship between Red Hat and EPEL.

### Can IUS add a package for {software}?

It depends.  IUS is not a general purpose repository.  It has the limited scope
of only providing newer versions of packages already in RHEL.  If the software
in question is not packaged in RHEL, then it is eligible to be submitted to the
[EPEL][epel] (Extra Packages for Enterprise Linux) repository, and is out of
scope for IUS.  If the software is packaged in RHEL (or EPEL) but is an older
version, it may be a good fit for IUS.  You can open a new package request on
our [wishlist][wishlist].

### How is IUS different from SCL?

IUS and [Software Collections][scl] (SCL) both seek to solve the problem of
providing optional newer versions of software for Enterprise Linux.  They
differ significantly in execution.

Most IUS packages are designed to [safely replace][safe-replacement] their
stock equivalent, but SCL packages are designed to be [parallel
installable][parallel-installable] with stock packages (and each other).  This
means that SCL packages must install to alternate paths such as `/opt/`,
`/etc/opt/`, and `/var/opt/`.  Most IUS packages can be used just like their
stock equivalents, but commands from SCL packages must be used through the
`scl` wrapper script.  Daemons from SCL packages are named differently as well.

IUS packages follow upstream releases, but SCL packages have [independent life
cycles][scl-life-cycle] that may be shorter or longer than the upstream
software.

### Should I use IUS so I can pass a security audit such as PCI?

Some security audits only use software versions to confirm security
vulnerabilities have been addressed.  This approach does not take into account
Red Hat's practice of [backporting of security fixes][backporting].  It is not
recommended to use IUS packages just to pass a security audit.

### How do I know when an IUS package is being retired?

Since IUS packages follow their respective upstream life cycles, they reach end
of life (EOL) before the operating system and are retired.  To be notified
about package retirements (and other important announcements), watch our
[announce][announce] repository on GitHub.

### Why do some IUS packages have a "u" suffix?

RHEL 5.6 (2011) added an alternate php53 package.  This name conflicted with
the existing php53 package that IUS was shipping.  To prevent overriding a
stock package, we renamed our package to php53u.  Later we Red Hat announced
SCL (2013), we were faced with several other naming collisions.  To avoid
confusion and possible yum mix ups, we started adding a "u" suffix to all our
package names.

Red Hat quickly changed their SCL naming scheme and started prefixing all their
SCL packages with "rh-".  All of the conflicting SCL packages are now EOL.
With this change, and Red Hat moving past SCL to [modularity][modularity],
suffixing our packages will likely never be necessary again.  In 2018 we
started created new packages without the "u" suffix.

### How long do updates have to wait in the testing repository before being promoted to the main repository?

Updates for our existing packages are first released in the [testing
repository][testing].  If no issues are reported after one week, the updated
packages will be promoted to the main repository.  We reserve the right to
promote package sooner if necessary.

This release policy does not not apply to new packages that have yet to be
added to the main repository.  When a new package is requested, the requester
must agree to test the package.  Once the requester confirms that everything
works as expected, the package is eligible to be added to the main repository.

### Why doesn't IUS have packages for RHEL 8?

RHEL 8 introduced [Application Streams][appstream] (also know as
[modularity][modularity]).  This gives Red Hat a way to provide optional newer
versions of software.  [EPEL][epel] plans to give package maintainers the
ability to offer additional streams that Red Hat doesn't offer.  If this goes
according to plan, IUS simply won't be necessary in RHEL 8 going forward.

### Why does yum fail with conflict errors when installing a non-IUS package?

This can happen if the package you want to install has dependencies that could
be satisfied by multiple IUS packages.  Yum's dependency resolution is not
always smart enough to pull in all the correct dependencies.  You can work
around this by explicitly requesting a few more package names to help the
transaction resolve successfully.

Alternatively, you can install [DNF][dnf], which has more sophisticated
dependency resolution capabilities and can determine the right thing to do.

### Why does composer fail to install with IUS enabled?

This is explained [above][yum].  You can explicitly request these package names
to help yum resolve the transaction.

- `yum install composer php72u-{cli,common,gd,intl,mbstring,pdo,process}`
- `yum install composer php73-{cli,common,gd,intl,mbstring,pdo,process}`

Alternatively, you can use [DNF][dnf].  If you already have some PHP packages
installed, it will resolve matching ones.  If you don't have any PHP packages
installed yet, it will resolve to the latest ones available to satisfy
composer's dependencies.  If you ask for any specific PHP package in your yum
command, DNF will resolve the rest of the dependencies to match.

- `dnf install composer`
- `dnf install composer php72u-common`
- `dnf install composer php73-common`

### I don't see php73 in the repos, where is it?

Traditionally in Red Hat and Fedora PHP packages, the php package contains the
PHP module for the Apache HTTPD Server, commonly known as mod\_php.  The PHP
language is packaged as php-common.  This naming is confusing, but Fedora has
[declined to change it][mod-php-rename].

IUS decided to fix this in our PHP packages to reduce user confusion.  We move
the mod\_php files into a subpackage such as mod\_php73.  When you want to use
our PHP packages, you must explicitly choose the PHP SAPI (server API) you
want, such as mod\_php73 or php73-fpm.

### Why can't I install mod\_php71u with httpd24u?

mod\_php compiles against the MMN (magic module number) of httpd.  This means
that if you build mod\_php against httpd 2.2, it can only install with httpd
2.2.  When we created httpd24u, [we decided to continue building our mod\_php
packages against stock httpd][mod-php-decision].  Building mod\_php for every
combination of php and httpd was far more complexity than we were willing to
maintain.  If you would like to use php71u with httpd24u, you must use
php71u-fpm.

### How can I report an issue with an IUS package?

If you think you've discovered a problem with an IUS package, please let us
know.  Locate the appropriate [package source][package-sources]  GitHub
repository and open an issue.  If you are familiar with RPM packaging and know
what the fix is, you can send a pull requests.  If the problem is with the
software and not the packaging, we can usually assist in reporting it upstream.
We also like to determine if Fedora is affected as well, and coordinate the fix
there as well.

### Can I become an IUS mirror?

For many years we relied on a network of mirrors to distribute our content.
Organizations would volunteer to mirror our content, and we would direct our
users to them via our mirrorlist API.  We referred to these as public mirrors.
Some organizations only wanted to mirror our content for their own use and not
serve it as part of the mirror network.  We referred to these as private
mirrors.

In 2019 we switched to using the [Rackspace CDN][cdn].  This means we no longer
need public mirrors.  If you would still like to mirror our content for your
own needs (private mirror), email us at [dev@ius.io](mailto:dev@ius.io) and we
will send you the rsync information so you can bypass the CDN and sync straight
from the source.


[epel]: https://fedoraproject.org/wiki/EPEL
[wishlist]: https://github.com/iusrepo/wishlist
[scl]: https://www.softwarecollections.org/en/
[safe-replacement]: /usage#safe-replacement-packages
[parallel-installable]: /usage#parallel-installable-packages
[scl-life-cycle]: https://access.redhat.com/support/policy/updates/rhscl
[backporting]: https://access.redhat.com/security/updates/backporting
[announce]: https://github.com/iusrepo/announce
[modularity]: https://docs.fedoraproject.org/en-US/modularity/
[testing]: /setup#testing
[appstream]: https://developers.redhat.com/blog/2018/11/15/rhel8-introducing-appstreams/
[dnf]: /usage#dnf
[yum]: #why-does-yum-fail-with-conflict-errors-when-installing-a-non-ius-package
[mod-php-rename]: https://bugzilla.redhat.com/show_bug.cgi?id=1290267
[mod-php-decision]: https://lists.launchpad.net/ius-community/msg01277.html
[package-sources]: https://github.com/search?q=org%3Aiusrepo+topic%3Arpm&s=updated
[cdn]: https://www.rackspace.com/en-us/cloud/cdn-content-delivery-network
