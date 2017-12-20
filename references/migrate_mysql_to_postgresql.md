# Migrating from MySQL to PostgreSQL

There are a number of guides for this.


## MediaWiki-Vagrant Test Environment

This environment was setup.

The git/gerrit user given was `anonymous` during `setup.sh`.


## MediaWiki specific migration

Note that the postgres backend is volunteer supported.

- [Official Page](https://www.mediawiki.org/wiki/Manual:PostgreSQL)
  - [Specific section, seems out of date](https://www.mediawiki.org/wiki/Manual:PostgreSQL#From_MySQL_to_PostgreSQL)
  - The [perl script](https://phabricator.wikimedia.org/source/mediawiki/browse/master/maintenance/postgres/mediawiki_mysql2postgres.pl) seems to proscribe (in its header notes) just spinning up a postgres database and attaching it to a working mediawiki instance then importing a mediawiki backup created with `maintenance/dumpBackup.php`.


### MediaWiki Test Environment

This env probably starts with a MySQL database, so it will need reconfigured

- [Official howto](https://www.mediawiki.org/wiki/MediaWiki-Vagrant) 

### Configuring for PostgreSQL

todo...


## Postgres Wiki

- [wiki.postgres.org: high level planning](https://wiki.postgresql.org/wiki/How_to_make_a_proper_migration_from_MySQL_to_PostgreSQL)
- [wiki.postgres.org: general converting guide](https://wiki.postgresql.org/wiki/Converting_from_other_Databases_to_PostgreSQL)

## Specific Tooling: `pgloader`

- [pgloader github project](https://github.com/dimitri/pgloader)
- [pgloader howto](https://pgloader.io/howto/mysql.html)
