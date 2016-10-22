### WordPress Backup and Restore Procedures

The backup and restore procedures are very good automation targets.

#### Automation Constraints

1. URL name length is different than mysql user, database, password maximum length
2. Use `sudo -u www-data do-stuff` to maintain ownership under `apache2`'s `www-data` user.


#### WordPress Backup Procedure

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


#### WordPress Restore Procedure

1. Backup the bad database and files. Include `bad` in the backup filenames.
    - Use the `WordPress Backup Procedure`
2. Disable the site in apache2 
    1. `sudo a2dissite www.example.com`
    2. `sudo service apache2 reload`
3. Delete the database being overwritten in mysql - feel free to login and combine steps. These are added this way for atomicity."
    1. `$ sudo mysql -e "DROP DATABASE mydbname; \q"`
    2. `$ sudo mysql -e "CREATE DATABASE wwwthesketchycom; \q"`
    3. `$ sudo mysql mydbname < mydbname.bkp.sql`
    4. User grants stay intact when a database is dropped; no need to modify users 
4. Assess and restore the file backup to see which files will be restored.
    1. Typically the restore will be the entire `public_html` directory
    2. Delete the old directory that will be replaced.
    3. As `www-data`, restore the backup.
        1. `cd /var/www/websites`
        2. `rm -rf www.example.com`
            - use extra caution, write the command then go back and add the `-rf` flags.
        3. `sudo -u www-data tar -xzvf ~/www.thesketchy.com.bkp.YYYYMMDD.HHMM.tar.gz`
5. Re-enable the site:
    1. `sudo a2ensite www.example.com`
    2. `sudo service apache2 reload`
