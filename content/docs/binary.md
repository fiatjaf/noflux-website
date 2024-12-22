---
title: Manual Binary Installation
description: Instructions to install Noflux binary manually
url: docs/binary_installation.html
---

This document describes how to install the Noflux binary on your Linux server.

Make sure to [install and configure PostgreSQL]({{< ref "database.md" >}}) before installing Noflux.

You can download precompiled binaries from the [GitHub Releases page](https://github.com/fiatjaf/noflux/releases). You could also [build the application from the source code]({{< ref "development.md" >}}).

1. Copy the precompiled binary somewhere on your server, for example in `/usr/local/bin`
2. Make the file executable: `chmod +x noflux`
3. Define the environment variable `DATABASE_URL` if necessary
4. Run the SQL migrations: `noflux -migrate`
5. Create an admin user: `noflux -create-admin`
6. Start the application: `noflux`

<p class="info">
It's recommended to configure a process manager like systemd or supervisord to supervise the Noflux daemon.
</p>

Make sure to take a look a the list of [configuration parameters]({{< relref configuration >}}) to customize your installation.
