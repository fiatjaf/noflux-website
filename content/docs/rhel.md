---
title: RHEL Installation
description: Instructions to install Noflux on RHEL distros
url: docs/rhel.html
---

This document describes how to install Noflux on any RHEL compatible Linux distributions such as RedHat, CentOS, RockyLinux, or AlmaLinux.

When you use the RPM package, the Noflux daemon is supervised by systemd.

Make sure to [install and configure Postgresql]({{< ref "database.md" >}}) before installing Noflux.

- [Install the RPM Package Manually](#rpm-package)
- [Install the RPM Package from the YUM Repo](#rpm-repo)
- [Configure Noflux](#configuration)

<h2 id="rpm-package">RPM Package Installation <a class="anchor" href="#rpm-package" title="Permalink">¶</a></h2>

1. Download the RPM package from the [GitHub Releases page](https://github.com/fiatjaf/noflux/releases).
2. Install the RPM package: `rpm -ivh noflux-2.0.13-1.0.x86_64.rpm`

<h2 id="rpm-repo">How to Configure the RPM Repository <a class="anchor" href="#rpm-repo" title="Permalink">¶</a></h2>

Create the file `/etc/yum.repos.d/noflux.repo`:

```
[noflux]
name=Noflux Repository
baseurl=https://repo.noflux.app/yum/
enabled=1
gpgcheck=0
```

Then install the package:

```bash
dnf install -y noflux
```

<div class="warning">
The previous repository URL <code>https://rpm.noflux.app/x86_64/</code> is deprecated in favor of <code>https://repo.noflux.app/yum/</code>.
</div>


<h2 id="configuration">Configure Noflux <a class="anchor" href="#configuration" title="Permalink">¶</a></h2>

1. Define the environment variable `DATABASE_URL` if necessary
2. Run the SQL migrations: `noflux -migrate`, or set the variable `RUN_MIGRATIONS=1` in `/etc/noflux.conf`
3. Create an admin user: `noflux -create-admin`
4. Customize your configuration file `/etc/noflux.conf` if necessary
5. Enable the systemd service: `systemctl enable noflux`
6. Start the process with systemd: `systemctl start noflux`
7. Check the process status: `systemctl status noflux`

<p class="info">
Systemd reads the environment variables from the file <code>/etc/noflux.conf</code>.
You must restart the service to take the new values into consideration.
</p>

Make sure to take a look a the list of [configuration parameters]({{< relref configuration >}}) to customize your installation.
