# Cloudbreak Database

By default Cloudbreak uses it's built in PostgreSQL database to persist data. For production environment we suggest to use an external database, an RDS served by the cloud provider,
but in some cases would be useful to dump and restore built in databases. Cloudbreak deployer has some extra features to solve that problem.

First of all let's dig into deeper. Cloudbreak deployer uses Docker for the underlying infrastructure and uses Docker volume for storing data. There are two separated volumes, one for live data called `common` and one for database dumps called `cbreak_dump`. You can override default live data volume any time by extending your `Profile` with the variable below:

```
export COMMON_DB_VOL="my-live-data-volume"
```

To create database dumps you have to execute the following commands:

```
cbd db dump common cbdb
cbd db dump common uaadb
cbd db dump common periscopedb
```

You can list existing dumps by executing `cbd db list-dumps` command.

Next thing what you have to understand is each kind of database dump (cbdb, uaadb, periscopedb) has a link to the latest inside of `cbreak_dump` volume. During restore deployer restores the latest one. You can check which one is the latest:

```
docker run --rm -v cbreak_dump:/dump -it alpine ls -lsa /dump/cbdb/latest
```

> If you want to restore an older dump, you have to link an other as latest.

After you stopped all the related Cloudbreak containers with `cbd kill` command, you can remove existing volume:

```
docker volume rm common
```

Last step is to restore databases from dumps:

```
cbd db restore-volume-from-dump common cbdb
cbd db restore-volume-from-dump common uaadb
cbd db restore-volume-from-dump common periscopedb
```

You can save any of your dump to the host machine easily:

```
docker run --rm -v cbreak_dump:/dump -it alpine cat /dump/cbdb/latest/dump.sql > cbdb.sql
docker run --rm -v cbreak_dump:/dump -it alpine cat /dump/uaadb/latest/dump.sql > uaadb.sql
docker run --rm -v cbreak_dump:/dump -it alpine cat /dump/periscopedb/latest/dump.sql > periscopedb.sql
```