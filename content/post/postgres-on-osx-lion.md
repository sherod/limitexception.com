+++
author = "Steven Herod"
date = 2012-05-25T00:00:00Z
description = ""
draft = false
slug = "postgres-on-osx-lion"
title = "Postgres on OSX Lion"

+++


Recently I was doing some work with RoR and needed to reset my password for the postgres that ships with OSX (9.1 it seems).

This turned into a challenge finding a simple set of instructions!

Editing the hba file

```
sudo vi /Library/PostgreSQL/9.1/data/pg_hba.conf
```

File should be modified so that the first line changes ‘md5’ to ‘trust’ to avoid it prompting for the current password.

```
# "local" is for Unix domain socket connections only
local all all trust  #was 'md5'
```

Then you need to Postgres:

```
$ sudo su - postgres
$ cd /Library/PostgreSQL/9.1/bin
$./pg_ctl restart -m fast -D /Library/PostgreSQL/9.1/data
```

Then you need to reconnect with the psql client and change the password:

```
./psql
```

And from the psql client, run the following statement:

```
WARNING: psql version 9.0, server version 9.1.
Some psql features might not work.
Type "help" for help.

postgres=# ALTER USER postgres with password 'yourpassword';
```

