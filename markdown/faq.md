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

### Why doesn't IUS have packages for RHEL 8?

RHEL 8 introduced [Application Streams][appstream] (also know as
[modularity][modularity]).  This gives Red Hat a way to provide optional newer
versions of software.  [EPEL][epel] plans to give package maintainers the
ability to offer additional streams that Red Hat doesn't offer.  If this goes
according to plan, IUS simply won't be necessary in RHEL 8 going forward.

[epel]: https://fedoraproject.org/wiki/EPEL
[wishlist]: https://github.com/iusrepo/wishlist
[scl]: https://www.softwarecollections.org/en/
[safe-replacement]: /usage#safe-replacement-packages
[parallel-installable]: /usage#parallel-installable-packages
[scl-life-cycle]: https://access.redhat.com/support/policy/updates/rhscl
[backporting]: https://access.redhat.com/security/updates/backporting
[announce]: https://github.com/iusrepo/announce
[modularity]: https://docs.fedoraproject.org/en-US/modularity/
[appstream]: https://developers.redhat.com/blog/2018/11/15/rhel8-introducing-appstreams/
