---
title: Debian Installation
description: Instructions to install Noflux on Debian GNU/Linux
url: docs/debian.html
---

- [Install the Debian Package Manually](#debian-package)
- [Install the Debian Package from the APT Repo](#apt-repo)
- [Configure Noflux](#configuration)

You must have Debian >= 8 or Ubuntu >= 16.04.

When using the Debian package, the Noflux daemon is supervised by systemd.

Make sure to [install and configure Postgresql]({{< ref "database.md" >}}) before installing Noflux.

<h2 id="debian-package">Install Noflux with the Debian package <a class="anchor" href="#debian-package" title="Permalink">¶</a></h2>

1. Download the Debian package from the [GitHub Releases page](https://github.com/fiatjaf/noflux/releases).
2. Install the Debian package: `dpkg -i noflux_2.0.13_amd64.deb`

<h2 id="apt-repo">Install Noflux from the APT Repository <a class="anchor" href="#apt-repo" title="Permalink">¶</a></h2>

You can configure APT to use Noflux repository.
To start, create a `noflux.list` file in the `/etc/apt/sources.list.d` directory.
You will need sudo access to make these changes:

Here is a basic template for `/etc/apt/sources.list.d/noflux.list`:

```
deb [trusted=yes] https://repo.noflux.app/apt/ * *
```

Or run this one-liner:

```bash
echo "deb [trusted=yes] https://repo.noflux.app/apt/ * *" | sudo tee /etc/apt/sources.list.d/noflux.list > /dev/null
```

Update the list of packages:

```bash
apt update
```

Then install the package:

```bash
apt install noflux
```

To upgrade Noflux, run `apt upgrade noflux`, and don't forget to run the database migrations.

<div class="warning">
The previous repository URL <code>https://apt.noflux.app/</code> is deprecated in favor of <code>https://repo.noflux.app/apt/</code>.
</div>

<h2 id="configuration">Configure Noflux <a class="anchor" href="#configuration" title="Permalink">¶</a></h2>

1. Define the environment variable `DATABASE_URL` in `/etc/noflux.conf`
2. Run the SQL migrations manually: `noflux -migrate -config-file /etc/noflux.conf`, or set the variable `RUN_MIGRATIONS=1` in `/etc/noflux.conf`
3. Create an admin user: `noflux -create-admin -config-file /etc/noflux.conf`
4. Restart the process: `systemctl restart noflux`
5. Check the process status: `systemctl status noflux`

The Debian package is available for multiple architectures: `amd64`, `arm64`, and `armhf`.
This way, it's very easy to install Noflux on a Raspberry Pi.

<p class="info">
Systemd reads the environment variables from the file <code>/etc/noflux.conf</code>.
You must restart the service to take the new values into consideration.
</p>

Make sure to take a look at the list of [configuration parameters]({{< relref configuration >}}) to customize your installation.
