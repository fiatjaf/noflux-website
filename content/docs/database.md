---
title: Database Configuration
description: Instructions to configure Postgresql for Noflux
url: docs/database.html
---

- [Postgresql Installation](#installation)
- [Postgresql Configuration](#configuration)
- [Database Connection Parameters](#dsn)

This document describes how to configure PostgreSQL for Noflux.

<h2 id="installation">Database Installation <a class="anchor" href="#installation" title="Permalink">¶</a></h2>

The first step is to install PostgreSQL with your package manager.

For example, on Debian it's simple as typing this command:

```bash
sudo apt install postgresql postgresql-contrib
```

<h2 id="configuration">Database Configuration <a class="anchor" href="#configuration" title="Permalink">¶</a></h2>

Here an example from the command line:

```
# Switch to the postgres user
$ sudo -u postgres -i

# Create a database user for Noflux
$ createuser -P noflux
Enter password for new role: ******
Enter it again: ******

# Create a database for noflux that belongs to our user
$ createdb -O noflux noflux

# Create the extension hstore as superuser
$ psql noflux -c 'create extension hstore'
CREATE EXTENSION
```

### Enabling HSTORE extension for Postgresql

Creating Postgresql extensions requires the `SUPERUSER` privilege.
Several solutions are available:

1) Give `SUPERUSER` privileges to the noflux user only during the schema migration:

```sql
ALTER USER noflux WITH SUPERUSER;
-- Run the migrations (noflux -migrate)
ALTER USER noflux WITH NOSUPERUSER;
```

2) You could [create the hstore extension](https://www.postgresql.org/docs/current/static/sql-createextension.html) with another user that have the ``SUPERUSER`` privileges before running the migrations.

```
sudo -u postgres psql $NOFLUX_DATABASE
> CREATE EXTENSION hstore;
```

Note that if you use Debian or Ubuntu, you might have to install the `postgresql-contrib` package to activate the `HSTORE` extension.

Recent versions of Noflux non longer uses the `HSTORE` extension but it still required to run the SQL migrations.

<h2 id="dsn">Database Connection Parameters <a class="anchor" href="#dsn" title="Permalink">¶</a></h2>

Noflux uses the Golang library [pq](https://github.com/lib/pq) to communicate with PostgreSQL.
The list of connection parameters are available on [this page](https://pkg.go.dev/github.com/lib/pq?utm_source=godoc#hdr-Connection_String_Parameters).

The default value for `DATABASE_URL` is `user=postgres password=postgres dbname=noflux sslmode=disable`.

You could also use the URL format `postgres://postgres:postgres@localhost/noflux?sslmode=disable`.

<div class="warning">
Password that contains special characters like ^ might be rejected. <a href="https://go-review.googlesource.com/c/go/+/87038">Golang v1.10 is now validating the password</a> and will return this error: <code>net/url: invalid userinfo</code>.
To avoid this issue, do not use the URL format for <code>DATABASE_URL</code>, or make sure the password is URL encoded.
</div>
