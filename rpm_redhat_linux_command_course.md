# RPM / Red Hat Linux Command-Line Course
## University Computer Science Edition
### Beginner → Intermediate → Advanced Package Management

> **Purpose**
>
> This course teaches RPM-based Linux package management from beginner to advanced level.
>
> It is designed for university computer science students using distributions such as:
>
> - Red Hat Enterprise Linux (RHEL)
> - Fedora
> - Rocky Linux
> - AlmaLinux
> - CentOS Stream
>
> The main package-management tools covered are:
>
> ```text
> rpm
> dnf
> yum
> repoquery
> rpmdev tools
> rpmbuild
> ```
>
> **Important:** `rpm` is the low-level package manager. Modern Red Hat-family systems normally use **DNF** as the high-level package manager because DNF handles repositories, dependency resolution, updates, and package transactions.
>
> The historical `yum` command is still encountered frequently. On modern systems it is commonly a compatibility interface around DNF.

---

# Table of Contents

1. [RPM Ecosystem Overview](#1-rpm-ecosystem-overview)
2. [RPM vs DNF vs YUM](#2-rpm-vs-dnf-vs-yum)
3. [RPM Package Files](#3-rpm-package-files)
4. [First RPM Commands](#4-first-rpm-commands)
5. [Querying Installed Packages](#5-querying-installed-packages)
6. [Querying RPM Package Files](#6-querying-rpm-package-files)
7. [Installing RPM Packages](#7-installing-rpm-packages)
8. [Updating RPM Packages](#8-updating-rpm-packages)
9. [Removing RPM Packages](#9-removing-rpm-packages)
10. [RPM Package Verification](#10-rpm-package-verification)
11. [RPM Package Database](#11-rpm-package-database)
12. [Finding Which Package Owns a File](#12-finding-which-package-owns-a-file)
13. [Listing Files Installed by a Package](#13-listing-files-installed-by-a-package)
14. [Package Information and Metadata](#14-package-information-and-metadata)
15. [Dependencies](#15-dependencies)
16. [DNF Fundamentals](#16-dnf-fundamentals)
17. [Installing Software with DNF](#17-installing-software-with-dnf)
18. [Removing Software with DNF](#18-removing-software-with-dnf)
19. [Updating the System](#19-updating-the-system)
20. [Searching Packages](#20-searching-packages)
21. [DNF Package Information](#21-dnf-package-information)
22. [Repository Management](#22-repository-management)
23. [Repository Files](#23-repository-files)
24. [DNF Cache](#24-dnf-cache)
25. [Package Groups](#25-package-groups)
26. [DNF History](#26-dnf-history)
27. [Dependency Troubleshooting](#27-dependency-troubleshooting)
28. [RPM Scriptlets](#28-rpm-scriptlets)
29. [RPM File Verification](#29-rpm-file-verification)
30. [RPM Signatures and GPG Keys](#30-rpm-signatures-and-gpg-keys)
31. [Architecture](#31-architecture)
32. [Source RPMs](#32-source-rpms)
33. [Building RPM Packages](#33-building-rpm-packages)
34. [RPM SPEC Files](#34-rpm-spec-files)
35. [RPM Build Directory](#35-rpm-build-directory)
36. [Creating a Simple RPM](#36-creating-a-simple-rpm)
37. [RPM Macros](#37-rpm-macros)
38. [RPM Query Formats](#38-rpm-query-formats)
39. [Advanced RPM Queries](#39-advanced-rpm-queries)
40. [DNF Plugins and Useful Tools](#40-dnf-plugins-and-useful-tools)
41. [Package Download Without Installation](#41-package-download-without-installation)
42. [Local RPM Installation with DNF](#42-local-rpm-installation-with-dnf)
43. [Offline Package Management](#43-offline-package-management)
44. [Repository Mirroring Concepts](#44-repository-mirroring-concepts)
45. [Package Management Security](#45-package-management-security)
46. [Troubleshooting Package Problems](#46-troubleshooting-package-problems)
47. [Useful RPM/DNF Command Combinations](#47-useful-rpmdnf-command-combinations)
48. [University Laboratory Exercises](#48-university-laboratory-exercises)
49. [12-Week Teaching Progression](#49-12-week-teaching-progression)
50. [RPM/DNF Cheat Sheet](#50-rpmdnf-cheat-sheet)

---

# 1. RPM Ecosystem Overview

RPM stands for:

```text
RPM Package Manager
```

Historically, RPM was associated with:

```text
Red Hat Package Manager
```

Today, RPM is the package format and low-level package-management technology used by many Linux distributions.

A simplified architecture is:

```text
User
  │
  ▼
DNF
  │
  ├── repositories
  ├── dependency resolution
  ├── package downloads
  └── transaction management
  │
  ▼
RPM
  │
  ├── install files
  ├── remove files
  ├── maintain package database
  ├── verify files
  └── execute package scripts
  │
  ▼
Linux filesystem
```

This distinction is extremely important.

---

# 2. RPM vs DNF vs YUM

## rpm

Low-level package manager.

Example:

```bash
rpm -qa
```

It can:

```text
install packages
remove packages
query packages
verify packages
inspect metadata
```

However, RPM itself does not provide the complete repository/dependency-resolution workflow expected from a modern package manager.

---

## dnf

High-level package manager.

Example:

```bash
sudo dnf install nginx
```

DNF can:

```text
search repositories
resolve dependencies
download packages
install packages
remove packages
upgrade packages
manage repositories
maintain transactions
```

---

## yum

Historical high-level package manager:

```bash
yum install nginx
```

On modern Red Hat-family distributions, `yum` is commonly implemented through DNF compatibility.

Students should recognize both:

```bash
yum
dnf
```

but should generally learn:

```bash
dnf
```

as the modern interface.

---

# 3. RPM Package Files

RPM packages normally have:

```text
.rpm
```

extension.

Example:

```text
example-1.2.3-4.x86_64.rpm
```

Conceptually:

```text
example
  │
  ├── package name
  ├── version
  ├── release
  └── architecture
```

A package contains more than just executable files.

It can contain:

```text
programs
libraries
configuration files
documentation
licenses
man pages
systemd units
users/groups
package scripts
metadata
dependencies
```

---

# 4. First RPM Commands

Check RPM version:

```bash
rpm --version
```

Show help:

```bash
rpm --help
```

Manual:

```bash
man rpm
```

List installed packages:

```bash
rpm -qa
```

Search installed packages:

```bash
rpm -qa | grep nginx
```

---

# 5. Querying Installed Packages

## List all installed packages

```bash
rpm -qa
```

Count:

```bash
rpm -qa | wc -l
```

---

## Search installed packages

```bash
rpm -qa | grep python
```

---

## Exact package query

```bash
rpm -q bash
```

Possible output:

```text
bash-5.x.x-x.el9.x86_64
```

---

## Package information

```bash
rpm -qi bash
```

Information includes:

```text
Name
Version
Release
Architecture
Install Date
Packager
Vendor
Summary
Description
```

---

# 6. Querying RPM Package Files

Suppose:

```text
example.rpm
```

Information:

```bash
rpm -qip example.rpm
```

List files:

```bash
rpm -qlp example.rpm
```

Dependencies:

```bash
rpm -qpR example.rpm
```

Scripts:

```bash
rpm -qp --scripts example.rpm
```

Package name:

```bash
rpm -qp --queryformat '%{NAME}\n' example.rpm
```

The `p` means:

```text
query the package file
```

rather than an installed package.

---

# 7. Installing RPM Packages

Basic installation:

```bash
sudo rpm -ivh package.rpm
```

Options:

```text
-i    install
-v    verbose
-h    progress hash marks
```

Example:

```bash
sudo rpm -ivh example-1.0-1.x86_64.rpm
```

Modern best practice for a local RPM with dependencies is often:

```bash
sudo dnf install ./example-1.0-1.x86_64.rpm
```

DNF can resolve dependencies from configured repositories.

---

# 8. Updating RPM Packages

RPM:

```bash
sudo rpm -Uvh package.rpm
```

`-U` means upgrade.

If the package is not installed, RPM may install it as part of the upgrade operation.

DNF:

```bash
sudo dnf upgrade package
```

Or:

```bash
sudo dnf update package
```

On modern DNF systems, `upgrade` and `update` are generally aliases or closely related operations.

---

# 9. Removing RPM Packages

Query package name:

```bash
rpm -q package
```

Remove:

```bash
sudo rpm -e package
```

`-e` means erase.

Using DNF:

```bash
sudo dnf remove package
```

DNF is usually preferable because it can understand dependency relationships and remove packages through a managed transaction.

---

# 10. RPM Package Verification

Verify installed files:

```bash
rpm -V package
```

or:

```bash
rpm --verify package
```

RPM can compare installed files against package metadata.

Possible attributes include:

```text
size
permissions
ownership
MD5/digest
device
link
user
group
modification time
```

Example:

```bash
rpm -V bash
```

No output generally means no detected differences for the files RPM verifies.

---

# 11. RPM Package Database

RPM maintains a package database.

Query it:

```bash
rpm -qa
```

Database location on modern RPM systems is commonly under:

```text
/var/lib/rpm/
```

Do not manually modify the RPM database files.

If the database appears corrupted, RPM provides database-related maintenance operations, but students should first make backups and understand the consequences.

---

# 12. Finding Which Package Owns a File

This is one of the most useful RPM skills.

For an installed file:

```bash
rpm -qf /usr/bin/bash
```

Meaning:

```text
-q    query
-f    file
```

Example:

```bash
rpm -qf /usr/bin/ls
```

This answers:

> Which installed RPM package owns this file?

---

# 13. Listing Files Installed by a Package

```bash
rpm -ql bash
```

This can reveal:

```text
executables
configuration files
documentation
libraries
man pages
```

Example:

```bash
rpm -ql openssl
```

---

# 14. Package Information and Metadata

Installed package:

```bash
rpm -qi package
```

Package file:

```bash
rpm -qip package.rpm
```

Useful metadata:

```text
NAME
VERSION
RELEASE
ARCH
SUMMARY
DESCRIPTION
LICENSE
URL
PACKAGER
VENDOR
BUILD HOST
INSTALL DATE
```

---

# 15. Dependencies

Package dependencies are relationships between packages and capabilities.

Query dependencies of installed package:

```bash
rpm -qR package
```

For a package file:

```bash
rpm -qpR package.rpm
```

Example:

```bash
rpm -qR bash
```

The result may contain shared libraries and capabilities such as:

```text
libc.so.6
libtinfo.so.6
```

---

## Why dependencies matter

Suppose:

```text
Application A
    │
    ├── Library B
    │      │
    │      └── Library C
    │
    └── Library D
```

Installing A requires:

```text
B
C
D
```

DNF automatically resolves this dependency graph when possible.

---

# 16. DNF Fundamentals

Check:

```bash
dnf --version
```

Help:

```bash
dnf --help
```

List installed packages:

```bash
dnf list installed
```

List available packages:

```bash
dnf list available
```

List updates:

```bash
dnf list updates
```

---

# 17. Installing Software with DNF

Install:

```bash
sudo dnf install package
```

Multiple:

```bash
sudo dnf install git gcc make
```

Assume yes:

```bash
sudo dnf install -y git
```

Dry-run-style preview:

```bash
sudo dnf install package --assumeno
```

The exact behavior of command options can vary by DNF version, so students should always check:

```bash
dnf --help
```

---

# 18. Removing Software with DNF

```bash
sudo dnf remove package
```

Remove multiple:

```bash
sudo dnf remove package1 package2
```

Before confirming a removal transaction, inspect the packages DNF proposes to remove.

Never blindly accept a large transaction on an important system.

---

# 19. Updating the System

Check available updates:

```bash
dnf check-update
```

Upgrade all packages:

```bash
sudo dnf upgrade
```

Upgrade a specific package:

```bash
sudo dnf upgrade bash
```

Automatic confirmation:

```bash
sudo dnf upgrade -y
```

On production systems, system updates should be planned and tested rather than blindly automated.

---

# 20. Searching Packages

Search package names/descriptions:

```bash
dnf search nginx
```

Search specifically by package name:

```bash
dnf list '*nginx*'
```

Installed:

```bash
dnf list installed
```

Available:

```bash
dnf list available
```

---

# 21. DNF Package Information

```bash
dnf info nginx
```

Installed package information:

```bash
dnf info installed nginx
```

Available versions:

```bash
dnf list --showduplicates nginx
```

This is useful when studying version selection and package repositories.

---

# 22. Repository Management

List repositories:

```bash
dnf repolist
```

Detailed:

```bash
dnf repolist all
```

Repository information:

```bash
dnf repoinfo
```

Repositories provide:

```text
package metadata
package files
signatures
dependency information
```

---

# 23. Repository Files

Repository definitions are commonly stored under:

```text
/etc/yum.repos.d/
```

List:

```bash
ls -l /etc/yum.repos.d/
```

Inspect:

```bash
cat /etc/yum.repos.d/example.repo
```

A `.repo` file commonly contains:

```ini
[repository-id]
name=Repository Name
baseurl=https://example.com/repository/
enabled=1
gpgcheck=1
gpgkey=https://example.com/key
```

Repository configuration varies between distributions and releases.

---

# 24. DNF Cache

DNF maintains metadata and package caches.

Clean metadata:

```bash
sudo dnf clean metadata
```

Clean all cached data:

```bash
sudo dnf clean all
```

Rebuild metadata:

```bash
sudo dnf makecache
```

Cache location commonly includes:

```text
/var/cache/dnf/
```

---

# 25. Package Groups

List groups:

```bash
dnf group list
```

Group information:

```bash
dnf group info "Development Tools"
```

Install a group:

```bash
sudo dnf group install "Development Tools"
```

Remove:

```bash
sudo dnf group remove "Development Tools"
```

Package groups are convenient for installing collections of related development tools.

---

# 26. DNF History

DNF records transactions.

List:

```bash
dnf history
```

Show a transaction:

```bash
dnf history info ID
```

Example:

```bash
dnf history info 12
```

Undo a transaction when appropriate:

```bash
sudo dnf history undo 12
```

Redo:

```bash
sudo dnf history redo 12
```

> Transaction rollback is not magic. Some changes may have external effects, configuration changes, database migrations, or dependencies that cannot be perfectly reversed.

---

# 27. Dependency Troubleshooting

Check dependencies of an installed package:

```bash
rpm -qR package
```

Check dependencies of a local RPM:

```bash
rpm -qpR package.rpm
```

DNF can resolve dependencies:

```bash
sudo dnf install ./package.rpm
```

Find providers:

```bash
dnf provides '/usr/bin/example'
```

Or:

```bash
dnf provides '*/libexample.so'
```

This answers:

> Which repository package provides this file?

---

# 28. RPM Scriptlets

RPM packages can contain scripts that execute during package transactions.

Inspect:

```bash
rpm -qp --scripts package.rpm
```

For an installed package:

```bash
rpm -q --scripts package
```

Scripts may run at stages such as:

```text
pre-install
post-install
pre-uninstall
post-uninstall
pre-trans
post-trans
```

These scripts can:

```text
create users
update caches
register services
create configuration
restart services
```

Because package scripts execute with administrative privileges during installation, package provenance and signatures are important security considerations.

---

# 29. RPM File Verification

Basic:

```bash
rpm -V package
```

Verbose verification:

```bash
rpm -Vv package
```

Verify all installed packages:

```bash
rpm -Va
```

This can produce a large amount of output.

Students should learn the meaning of verification symbols from:

```bash
man rpm
```

---

# 30. RPM Signatures and GPG Keys

RPM packages can be cryptographically signed.

Check package signature/header information:

```bash
rpm -K package.rpm
```

Equivalent long form:

```bash
rpm --checksig package.rpm
```

DNF repository configuration can enforce signature checking:

```ini
gpgcheck=1
```

Import a trusted GPG key:

```bash
sudo rpm --import /path/to/RPM-GPG-KEY
```

Never import an unknown key merely to make an installation work.

The security chain is:

```text
Trusted repository
        ↓
Package
        ↓
Cryptographic signature
        ↓
Verification
        ↓
Installation
```

---

# 31. Architecture

Common architectures:

```text
x86_64
aarch64
ppc64le
s390x
```

Current architecture:

```bash
uname -m
```

RPM architecture:

```bash
rpm --eval '%{_arch}'
```

Query package architecture:

```bash
rpm -q --qf '%{NAME} %{ARCH}\n' package
```

Architecture matters because compiled binaries and libraries are not generally interchangeable across CPU architectures.

---

# 32. Source RPMs

Source packages are commonly identified as:

```text
.src.rpm
```

They contain source code and packaging instructions rather than a normal compiled binary package.

A source RPM can be inspected with:

```bash
rpm -qpl package.src.rpm
```

Extract source package contents:

```bash
rpm2cpio package.src.rpm | cpio -idmv
```

Source RPM workflows are important for:

```text
distribution packaging
reproducible builds
software maintenance
patching
auditing
```

---

# 33. Building RPM Packages

The standard RPM build tool is:

```bash
rpmbuild
```

Check:

```bash
rpmbuild --version
```

Install development tools where appropriate:

```bash
sudo dnf install rpm-build rpmdevtools
```

Create a standard RPM build tree:

```bash
rpmdev-setuptree
```

This normally creates:

```text
~/rpmbuild/
├── BUILD
├── BUILDROOT
├── RPMS
├── SOURCES
├── SPECS
└── SRPMS
```

---

# 34. RPM SPEC Files

RPM packages are normally described by a `.spec` file.

Typical sections:

```text
Name
Version
Release
Summary
License
URL
Source
BuildRequires
Requires
%description
%prep
%build
%install
%files
%changelog
```

Example skeleton:

```spec
Name:           hello-linux
Version:        1.0
Release:        1%{?dist}
Summary:        Simple Linux example
License:        MIT
Source0:        %{name}-%{version}.tar.gz

%description
A simple example RPM package.

%prep
%setup -q

%build
make

%install
mkdir -p %{buildroot}%{_bindir}
install -m 0755 hello %{buildroot}%{_bindir}/hello

%files
%{_bindir}/hello

%changelog
* Mon Jan 01 2026 Student <student@example.com> - 1.0-1
- Initial package
```

The exact build instructions depend on the software being packaged.

---

# 35. RPM Build Directory

Standard layout:

```text
~/rpmbuild/
├── BUILD/
├── BUILDROOT/
├── RPMS/
├── SOURCES/
├── SPECS/
└── SRPMS/
```

Purpose:

```text
BUILD       temporary build directory
BUILDROOT   staged installation tree
RPMS        resulting binary RPMs
SOURCES     source archives/patches
SPECS       spec files
SRPMS       source RPMs
```

---

# 36. Creating a Simple RPM

Install tools:

```bash
sudo dnf install rpm-build rpmdevtools gcc make
```

Set up:

```bash
rpmdev-setuptree
```

Create source:

```bash
mkdir -p ~/rpmbuild/SOURCES/hello-linux-1.0
```

Example source:

```bash
cat > ~/rpmbuild/SOURCES/hello-linux-1.0/hello <<'EOF'
#!/bin/bash
echo "Hello from an RPM package"
EOF
```

Make executable:

```bash
chmod +x ~/rpmbuild/SOURCES/hello-linux-1.0/hello
```

Create archive:

```bash
cd ~/rpmbuild/SOURCES
tar -czf hello-linux-1.0.tar.gz hello-linux-1.0
```

Create spec:

```bash
nano ~/rpmbuild/SPECS/hello-linux.spec
```

Build:

```bash
rpmbuild -ba ~/rpmbuild/SPECS/hello-linux.spec
```

Results normally appear under:

```text
~/rpmbuild/RPMS/
~/rpmbuild/SRPMS/
```

---

# 37. RPM Macros

RPM uses macros such as:

```text
%{_bindir}
%{_libdir}
%{_sysconfdir}
%{_datadir}
%{_mandir}
%{buildroot}
```

Inspect:

```bash
rpm --showrc
```

Print one macro:

```bash
rpm --eval '%{_bindir}'
```

Example:

```bash
rpm --eval '%{_libdir}'
```

Macros make spec files more portable between distributions and architectures.

---

# 38. RPM Query Formats

RPM provides powerful query formatting.

Example:

```bash
rpm -q --qf '%{NAME}\n' bash
```

Show name/version/release:

```bash
rpm -q --qf '%{NAME}-%{VERSION}-%{RELEASE}\n' bash
```

Show architecture:

```bash
rpm -q --qf '%{NAME} %{ARCH}\n' bash
```

Multiple fields:

```bash
rpm -q --qf 'Name: %{NAME}\nVersion: %{VERSION}\nArch: %{ARCH}\n' bash
```

This is extremely useful for scripting.

---

# 39. Advanced RPM Queries

Find packages by architecture:

```bash
rpm -qa --qf '%{NAME} %{ARCH}\n' | sort
```

List packages alphabetically:

```bash
rpm -qa --qf '%{NAME}\n' | sort
```

Find package names and versions:

```bash
rpm -qa --qf '%{NAME}-%{VERSION}-%{RELEASE}.%{ARCH}\n'
```

Find packages installed most recently:

```bash
rpm -qa --last
```

---

# 40. DNF Plugins and Useful Tools

Useful package-management tools may include:

```text
dnf-plugins-core
rpmdevtools
createrepo_c
dnf-utils
```

The exact package names vary by distribution and release.

Install DNF plugins where available:

```bash
sudo dnf install dnf-plugins-core
```

Useful commands can include:

```bash
dnf config-manager
dnf download
dnf builddep
```

Check your installed version:

```bash
dnf --help
```

---

# 41. Package Download Without Installation

With DNF plugins where supported:

```bash
dnf download package
```

Download dependencies:

```bash
dnf download --resolve package
```

Download source package:

```bash
dnf download --source package
```

This is useful for:

```text
offline installation
package inspection
testing
building
dependency analysis
```

---

# 42. Local RPM Installation with DNF

Given:

```text
package.rpm
```

Install:

```bash
sudo dnf install ./package.rpm
```

The `./` helps distinguish a local path from a repository package name.

DNF can resolve dependencies using enabled repositories.

Compare:

```bash
sudo rpm -ivh package.rpm
```

with:

```bash
sudo dnf install ./package.rpm
```

For most modern administration tasks, the DNF approach is more convenient.

---

# 43. Offline Package Management

Offline environments can use downloaded RPM packages.

Download:

```bash
dnf download --resolve package
```

Transfer packages:

```bash
scp *.rpm student@offline-host:/tmp/
```

On target:

```bash
sudo dnf install /tmp/*.rpm
```

Offline repositories can also be built using repository metadata tools.

---

# 44. Repository Mirroring Concepts

A repository generally contains:

```text
RPM packages
+
repository metadata
+
checksums
+
signatures
```

`createrepo_c` can create repository metadata.

Install:

```bash
sudo dnf install createrepo_c
```

Create metadata:

```bash
createrepo_c /path/to/repository
```

A simple repository might look like:

```text
repo/
├── package1.rpm
├── package2.rpm
├── package3.rpm
└── repodata/
```

Repository administration is an advanced systems-administration topic.

---

# 45. Package Management Security

Students should understand these principles.

## Principle 1 — Source matters

Prefer trusted repositories.

Avoid random RPM files from unknown websites.

---

## Principle 2 — Verify signatures

```bash
rpm -K package.rpm
```

---

## Principle 3 — Understand scripts

```bash
rpm -qp --scripts package.rpm
```

---

## Principle 4 — Understand dependencies

```bash
rpm -qpR package.rpm
```

---

## Principle 5 — Review transactions

Before accepting:

```bash
sudo dnf install ...
```

inspect:

```text
packages installed
packages removed
packages upgraded
repositories used
disk space changes
```

---

# 46. Troubleshooting Package Problems

## Problem: package not found

Try:

```bash
dnf search package
```

Then:

```bash
dnf repolist
```

---

## Problem: package exists but wrong version

Try:

```bash
dnf list --showduplicates package
```

---

## Problem: dependency missing

Try:

```bash
dnf provides '*/missing-file'
```

or inspect:

```bash
rpm -qpR package.rpm
```

---

## Problem: local RPM fails

Instead of:

```bash
sudo rpm -ivh package.rpm
```

try:

```bash
sudo dnf install ./package.rpm
```

---

## Problem: repository metadata appears stale

Try:

```bash
sudo dnf clean metadata
sudo dnf makecache
```

---

## Problem: transaction history

Inspect:

```bash
dnf history
```

Then:

```bash
dnf history info ID
```

---

## Problem: file changed unexpectedly

Verify:

```bash
rpm -V package
```

---

# 47. Useful RPM/DNF Command Combinations

## Find package owning a command

```bash
command -v bash
```

Then:

```bash
rpm -qf "$(command -v bash)"
```

---

## Find package providing a command

If the command is not installed:

```bash
dnf provides '*/command-name'
```

---

## List installed packages sorted by name

```bash
rpm -qa --qf '%{NAME}\n' | sort
```

---

## List package sizes

```bash
rpm -qa --qf '%{SIZE} %{NAME}\n' | sort -n
```

---

## Find recently installed packages

```bash
rpm -qa --last | head -20
```

---

## Inspect local RPM

```bash
rpm -qip package.rpm
rpm -qpl package.rpm
rpm -qpR package.rpm
rpm -qp --scripts package.rpm
rpm -K package.rpm
```

---

## Compare RPM package and installed package

Installed:

```bash
rpm -qi package
```

File:

```bash
rpm -qip package.rpm
```

---

# 48. University Laboratory Exercises

## Lab 1 — RPM Fundamentals

Check:

```bash
rpm --version
dnf --version
```

Answer:

1. What is RPM?
2. What is DNF?
3. Why are both needed?

---

## Lab 2 — Installed Package Investigation

Choose:

```bash
bash
```

Run:

```bash
rpm -q bash
rpm -qi bash
rpm -ql bash
rpm -qR bash
rpm -qf /usr/bin/bash
```

Write a report explaining each result.

---

## Lab 3 — Package Database

Run:

```bash
rpm -qa | wc -l
```

Then:

```bash
rpm -qa | sort | head -20
```

Questions:

1. Approximately how many RPM packages are installed?
2. Why does Linux use many separate packages?
3. What is the advantage of modular packages?

---

## Lab 4 — DNF Repository Investigation

Run:

```bash
dnf repolist
```

Then:

```bash
dnf repolist all
```

Identify:

```text
enabled repositories
disabled repositories
repository IDs
repository names
```

---

## Lab 5 — Package Search

Search for a compiler:

```bash
dnf search gcc
```

Inspect:

```bash
dnf info gcc
```

Determine:

```text
version
architecture
repository
summary
description
```

---

## Lab 6 — Dependency Investigation

Choose an installed package:

```bash
rpm -qR bash
```

Identify several dependencies.

For each dependency, explain whether it is:

```text
shared library
package capability
configuration requirement
command
filesystem capability
```

---

## Lab 7 — Local RPM Inspection

Download a package without installing it.

Then:

```bash
rpm -qip package.rpm
rpm -qpl package.rpm
rpm -qpR package.rpm
rpm -qp --scripts package.rpm
rpm -K package.rpm
```

Write a report describing the package before installation.

---

## Lab 8 — Package Verification

Choose:

```bash
rpm -V bash
```

Explain why a clean verification normally produces no output.

Then investigate what the verification command checks.

---

## Lab 9 — DNF Transaction History

Run:

```bash
dnf history
```

Select a transaction:

```bash
dnf history info ID
```

Document:

```text
transaction ID
date
packages installed
packages removed
packages upgraded
```

---

## Lab 10 — Build an RPM

Install:

```bash
sudo dnf install rpm-build rpmdevtools gcc make
```

Create:

```bash
rpmdev-setuptree
```

Build a tiny "Hello Linux" RPM.

Students should submit:

```text
.spec file
source archive
binary RPM
source RPM
installation test
verification output
```

---

## Lab 11 — Package Ownership

Choose system files:

```bash
/usr/bin/bash
/usr/bin/ls
/usr/bin/grep
```

Run:

```bash
rpm -qf /usr/bin/bash
rpm -qf /usr/bin/ls
rpm -qf /usr/bin/grep
```

Explain why knowing package ownership is useful for troubleshooting.

---

## Lab 12 — Troubleshooting Scenario

Given an unknown package problem:

```text
Application cannot start because a library appears to be missing.
```

Students should investigate using:

```bash
command -v application
rpm -qf "$(command -v application)"
rpm -qR package
ldd "$(command -v application)"
dnf provides '*/library-name'
journalctl
```

The goal is not to memorize commands.

The goal is to develop a systematic diagnostic method.

---

# 49. 12-Week Teaching Progression

## Week 1 — Linux Package Management Concepts

Topics:

```text
software packages
repositories
RPM
DNF
YUM
dependencies
package metadata
```

---

## Week 2 — RPM Queries

Learn:

```bash
rpm -qa
rpm -q
rpm -qi
rpm -ql
rpm -qf
rpm -qR
```

---

## Week 3 — RPM Installation and Removal

Learn:

```bash
rpm -i
rpm -U
rpm -e
```

Compare with:

```bash
dnf install
dnf upgrade
dnf remove
```

---

## Week 4 — Package Files

Learn:

```bash
rpm -qip
rpm -qpl
rpm -qpR
rpm -qp --scripts
rpm -K
```

---

## Week 5 — DNF

Learn:

```bash
dnf install
dnf remove
dnf upgrade
dnf search
dnf info
dnf list
```

---

## Week 6 — Repositories

Learn:

```bash
dnf repolist
/etc/yum.repos.d/
repository metadata
GPG keys
```

---

## Week 7 — Dependencies

Learn:

```bash
dnf provides
rpm -qR
rpm -qpR
```

Study dependency graphs.

---

## Week 8 — Transactions

Learn:

```bash
dnf history
dnf history info
dnf history undo
```

Study transaction safety.

---

## Week 9 — Security

Learn:

```bash
rpm -K
rpm --import
GPG
repository trust
package signatures
```

---

## Week 10 — RPM Building

Learn:

```bash
rpmbuild
rpmdev-setuptree
SPEC files
BUILD
BUILDROOT
SOURCES
SPECS
RPMS
SRPMS
```

---

## Week 11 — Advanced Packaging

Learn:

```text
RPM macros
scriptlets
BuildRequires
Requires
package metadata
source RPMs
repository creation
```

---

## Week 12 — Final Project

Build a small RPM package and provide:

```text
source code
SPEC file
RPM package
SRPM package
repository metadata
installation instructions
verification report
dependency analysis
security/signature discussion
```

---

# 50. RPM/DNF Cheat Sheet

## RPM

```bash
rpm -qa
rpm -q PACKAGE
rpm -qi PACKAGE
rpm -ql PACKAGE
rpm -qR PACKAGE
rpm -qf FILE
rpm -V PACKAGE
rpm -ivh PACKAGE.rpm
rpm -Uvh PACKAGE.rpm
rpm -e PACKAGE
```

## Local RPM

```bash
rpm -qip PACKAGE.rpm
rpm -qpl PACKAGE.rpm
rpm -qpR PACKAGE.rpm
rpm -qp --scripts PACKAGE.rpm
rpm -K PACKAGE.rpm
```

## DNF

```bash
dnf search PACKAGE
dnf info PACKAGE
dnf list installed
dnf list available
dnf list --showduplicates PACKAGE
dnf install PACKAGE
dnf remove PACKAGE
dnf upgrade
dnf check-update
dnf repolist
dnf history
dnf history info ID
dnf provides '*/FILE'
```

## Repository

```bash
dnf repolist
dnf repolist all
sudo dnf clean metadata
sudo dnf clean all
sudo dnf makecache
```

## Package building

```bash
rpmdev-setuptree
rpmbuild -ba package.spec
rpmbuild -bb package.spec
rpmbuild -bs package.spec
```

## Package inspection

```bash
rpm -qi PACKAGE
rpm -ql PACKAGE
rpm -qR PACKAGE
rpm -qf FILE
rpm -Va
rpm -qa --last
```

---

# Final Mental Model

The most important concept is the distinction between the **package format**, the **low-level package manager**, and the **high-level package manager**.

```text
                    Linux Distribution
                           │
                           ▼
                    Repository System
                           │
                           ▼
                         DNF
                           │
          ┌────────────────┼────────────────┐
          │                │                │
       Search          Dependencies     Transactions
          │                │                │
          └────────────────┼────────────────┘
                           ▼
                          RPM
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
      Install            Query             Verify
        │                  │                  │
        └──────────────────┼──────────────────┘
                           ▼
                     RPM Database
                           │
                           ▼
                    Linux Filesystem
```

A student should eventually be able to answer:

```text
What package owns this file?
What files does this package install?
What dependencies does it have?
Which repository provides it?
Which version is installed?
Which versions are available?
Is the package signature trusted?
Have any installed files changed?
What happened during the last package transaction?
How do I build my own RPM?
How do I create a repository?
How do I diagnose a dependency problem?
```

The key commands are:

```bash
rpm
dnf
yum
repoquery
rpmbuild
rpmdev-setuptree
```

The key conceptual progression is:

```text
RPM file
   ↓
RPM metadata
   ↓
Installed package
   ↓
Dependencies
   ↓
Repositories
   ↓
DNF transactions
   ↓
Package security
   ↓
RPM building
   ↓
Repository administration
```

The objective is not simply to memorize:

```bash
rpm -q
dnf install
```

The real computer-science objective is to understand **how an operating system represents, distributes, installs, verifies, updates, and removes software**.
