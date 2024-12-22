---
title: Command Line Usage
description: List of available command line arguments for Noflux
url: docs/cli.html
---

<h2 id="config-dump">Show Interpreted Configuration Values <a class="anchor" href="#config-dump" title="Permalink">¶</a></h2>

```bash
noflux -config-dump
```

<h2 id="config-file">Use a Configuration File <a class="anchor" href="#config-file" title="Permalink">¶</a></h2>

```bash
noflux -config-file /etc/noflux.conf
```

or

```bash
noflux -c /etc/noflux.conf
```

<h2 id="create-admin">Create Admin User <a class="anchor" href="#create-admin" title="Permalink">¶</a></h2>

```bash
noflux -create-admin
Enter Username: root
Enter Password: ****
```

<h2 id="debug">Enable Debug Mode <a class="anchor" href="#debug" title="Permalink">¶</a></h2>

```bash
noflux -debug
[INFO] Debug mode enabled
[INFO] Starting Noflux...
```

<h2 id="export-feeds">Export feeds <a class="anchor" href="#export-feeds" title="Permalink">¶</a></h2>

```bash
noflux -export-user-feeds username > feeds.opml
```

<h2 id="flush-sessions">Flush All Sessions <a class="anchor" href="#flush-sessions" title="Permalink">¶</a></h2>

```bash
noflux -flush-sessions
Flushing all sessions (disconnect users)
```

<h2 id="healthcheck">Healthcheck <a class="anchor" href="#healthcheck" title="Permalink">¶</a></h2>

Perform a health check on the given endpoint. The value "auto" try to guess the health check endpoint.

```bash
noflux -healthcheck https://noflux.domain.tld/healthcheck
```

Return 0 as exit code if successful otherwise returns 1.

<h2 id="info">Show Build Information <a class="anchor" href="#info" title="Permalink">¶</a></h2>

```bash
noflux -info # or -i
Version: 2.0.15
Build Date: 2019-03-16T18:26:30-0700
Go Version: go1.12
Compiler: gc
Arch: amd64
OS: darwin
```

<h2 id="migrate">Run Database Migrations <a class="anchor" href="#migrate" title="Permalink">¶</a></h2>

```bash
export DATABASE_URL=replace_me

noflux -migrate
Current schema version: 0
Latest schema version: 12
Migrating to version: 1
Migrating to version: 2
Migrating to version: 3
Migrating to version: 4
Migrating to version: 5
Migrating to version: 6
Migrating to version: 7
Migrating to version: 8
Migrating to version: 9
Migrating to version: 10
Migrating to version: 11
Migrating to version: 12
```

<h2 id="refresh-feeds">Refresh feeds <a class="anchor" href="#refresh-feeds" title="Permalink">¶</a></h2>

```bash
noflux -refresh-feeds
```

<h2 id="reset-feed-errors">Reset All Feed Errors <a class="anchor" href="#reset-feed-errors" title="Permalink">¶</a></h2>

```bash
noflux -reset-feed-errors
```

<h2 id="reset-password">Reset User Password <a class="anchor" href="#reset-password" title="Permalink">¶</a></h2>

```bash
noflux -reset-password
Enter Username: myusername
Enter Password: ****
```

<h2 id="run-cleanup-tasks">Run Cleanup Tasks <a class="anchor" href="#run-cleanup-tasks" title="Permalink">¶</a></h2>

Delete old sessions and archives old entries.

```bash
noflux -run-cleanup-tasks
```

<h2 id="version">Show Application Version <a class="anchor" href="#version" title="Permalink">¶</a></h2>

```bash
noflux -version # or -v
2.0.15
```
