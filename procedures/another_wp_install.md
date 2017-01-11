
### Another method for installing WordPress

1. Get the WordPress files
    1. `cd /var/www/websites`
    2. `sudo -u www-data mkdir -p ./public_html/logs`
    3. `sudo -u www-data touch ./public_html/logs/error.log ./public_html/logs/access.log`
    4. `cd public_html`
    5. `sudo -u www-data wp core download`
2. INSERT CUSTOM WP CONTENT STEP
    - remove original wp-content
    - download `wp-base` git repo from taui source, use submodules for 3rd party themes/plugins
        - consider hosting stable mirrors of these 3rd party things and upgrading manually
        - this would be quite possible by simply hosting my own submodules and leaving the 3rd party sources as non upstream
3. Generate the database, user, and password for this WordPress instance
    1. Login to MySQL as the root user: `$ sudo mysql -u root`
        - No password required on MySQL 5.7 (or enter password at prompt on 5.5)
        - note that you must use root system privs to login to root mysql on 5.7
    2. `create database {Database Name};`
    3. `create user '{User}'@'localhost' IDENTIFIED BY '{Password}'`
        - Does the next step create the user automatically if you don't do this?
    4. `GRANT ALL PRIVILEGES ON '{db}'.* To '{user}'@'localhost' IDENTIFIED BY '{passwd}';`
    5. view your changes: `mysql> select user, host, password from mysql.user;`
    6. `mysql> FLUSH PRIVILEGES;` then `mysql> quit;`
4. Set the `wp-config.php` salts and database info according to the MySQL information.
    - `sudo -u www-data cp wp-config-example.php wp-config.php`
    - `sudo -u www-data vim wp-config.php`
    - `DB_NAME`
    - `DB_USER`
    - `DB_PASSWORD`
    - `DB_HOST`
    - `$table_prefix`
    - [Authentication Unique Keys and Salts](https://api.wordpress.org/secret-key/1.1/salt/)
5. Use wp-cli for first time install
    - `sudo -u www-data wp core install --url=www.example.com --title=Example --admin_user=ex-admin --admin_password=123xyz --admin_email=admin@ex.com
    - if installed in a subdirectory `www.example.com/subdir` then `wp option update siteurl http://www.example.com/subdir`

#### Future

1. HOW DOES THIS WORK? `wp db create` - create a new database using the `wp-config.php`
    - not needed with my manual steps, but would i benefit from it?
2. How about sane default settings from wp-cli?
    - correct url rewrite rule
    - traceback pingback settings in 'reading' or whatever
    - remove tagline!!
3. Enumerate even more sane defaults
4. Create step 2. This will need to:
    1. install the custom `wp-base`
    2. enable theme and plugins for `wp-base`
