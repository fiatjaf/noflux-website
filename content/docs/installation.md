---
title: Installation Instructions
description: Instructions to install Noflux on your own server
url: docs/installation.html
---

Installing Noflux is straightforward if you have some basic system administration knowledge.

- [Packages](#packages)
- [Database Configuration]({{< ref "database.md" >}})
- [Manual Installation]({{< ref "binary.md" >}})
- [Debian/Ubuntu/Raspbian Package Installation]({{< ref "debian.md" >}})
- [RPM Package Installation]({{< ref "rhel.md" >}})
- [Alpine Linux Installation]({{< ref "alpine.md" >}})
- [Docker Installation]({{< ref "docker.md" >}})

<h2 id="packages">Packages <a class="anchor" href="#packages" title="Permalink">¶</a></h2>

Platform       |  Type               |  Repository URL
---------------|---------------------|---------------------------------------------------------------------
Debian/Ubuntu  |  Upstream (Binary)  |  https://github.com/fiatjaf/noflux/tree/master/packaging/debian
RHEL/Fedora    |  Upstream (Binary)  |  https://github.com/fiatjaf/noflux/tree/master/packaging/rpm
Alpine Linux   |  Community (Source) |  https://git.alpinelinux.org/aports/tree/community/noflux
Arch Linux     |  Community (Source) |  https://archlinux.org/packages/extra/x86_64/noflux/
Debian         |  Community (Binary) |  https://packages.debian.org/trixie/noflux
FreeBSD Port   |  Community (Source) |  https://svnweb.freebsd.org/ports/head/www/noflux/
Nix            |  Community (Source) |  https://github.com/NixOS/nixpkgs/tree/master/pkgs/servers/noflux
Ubuntu         |  Community (Binary) |  https://packages.ubuntu.com/noble/noflux

You can download precompiled binaries and packages from the [GitHub Releases page](https://github.com/fiatjaf/noflux/releases). You could also [build the application from the source code]({{< ref "development.md" >}}).
