# PostgreSQL

## Installation

```
brew install postgresql
```

>To migrate existing data from a previous major version of PostgreSQL run: 
>
>```
>brew postgresql-upgrade-database
>```
>
>Restart postgresql after an upgrade! 

### Start/Stop/Restart 

Manually 

```
pg_ctl -D /usr/local/var/postgres start
pg_ctl -D /usr/local/var/postgres stop
```

Via Homebrew

```
brew services start postgresql
brew services stop postgresql
brew services reststart postgresql
```

### Admin softwares
 
- [pgAdmin 4](https://www.pgadmin.org/download/pgadmin-4-macos/)
- [Postico](https://eggerapps.at/postico/)

## Commands

Credits: 

- [@ibraheem4/postgres-brew.md](https://gist.github.com/ibraheem4/ce5ccd3e4d7a65589ce84f2a3b7c23a3)

### Create user

```
createuser --interactive --pwprompt
```

### Create database

```
createdb <database_name>
```
>createdb mydatabasename

### List databases

```
psql -U postgres -l
```

### Show tables in database

```
psql -U postgres -d <database_name>
```
> psql -U postgres -d mydatabasename

### Drop database

```
dropdb <database_name>
```
>dropdb mydatabasename

### Re-create database

```
dropdb <database_name> && createdb <database_name>
```
> dropdb mydatabasename && createdb mydatabasename

### List all users

```
# Log into postgres
psql -d postgres

# Type:
\du
# or
\du+
```

### Quit psql

```
\q
```

### Backup

```
pg_dump mydatabasename > path/to/backupname
```

### Restore 

```
psql mydatabasename < path/to/backupname
```

## Troubleshooting

### Server not connected

Stop server on Brew and manually and restart via Brew.

### Upgrade issue

Last postgres upgrade (10 to 11) got me an empty database, so the solution for this was stopping all brew postgres services

```
brew services stop postgresql
brew services stop postgresql@10

brew postgresql-upgrade-database
```
and run

```
pg_upgrade -v \                                    
    -d /usr/local/var/postgresql@10 \
    -D /usr/local/var/postgres \
    -b /usr/local/Cellar/postgresql@10/10.10/bin/ \
    -B /usr/local/Cellar/postgresql/11.5_1/bin/
```
> -v to enable verbose internal logging
> 
> -d the old database cluster configuration directory
> 
> -D the new database cluster configuration directory
> 
> -b the old PostgreSQL executable directory
> 
> -B the new PostgreSQL executable directory
