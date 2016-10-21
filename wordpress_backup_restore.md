### WordPress Backup and Restore Procedures

The backup and restore procedures are very good automation targets.

#### Automation Constraints

1. URL name length is different than mysql user, database, password maximum length
2. Use `sudo -u www-data do-stuff` to maintain ownership under `apache2`'s `www-data` user.


#### WordPress Backup

This backup methodology is generic across projects and databases. The written protocol is specific for `apache2`, `MySQL`, and `WordPress`.

1. Backup the database
    1. `$ sudo mysql -e "show databases; \q"`
    2. `$ sudo mysqldump mydbname > ~/mydbname.dump.sql`
2. Back up www project root directory, e.g. `/var/www/websites/www.example.com`
    1. Back up the whole wordpress install - it can be used as a complete snapshot
      - The wordpress install is a specific version and is tiny anyways
    2. `$ cd /var/www/websites/`
    3. Prune any big logs in `logs`: `access.log`, `error.log`
    4. `$ tar -czvf ~/www.example.com.bad.YYYYMMDD.HHMM.tar.gz www.example.com`
    5. Move the backups from ~ to the appropriate archival location


#### WordPress Restore

1. Backup the bad database and files. Include `bad` in the backup filenames.

1. Disable the site in apache2 `sudo a2dissite www.example.com`
2. Delete the database being overwritten in mysql
    - 
3. Assess the file backup to see which files will be restored.
3. Delete project directory in `/var/www/websites` or the `wp-content` directory depending on the file backup
