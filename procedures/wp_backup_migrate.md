### Basic Backup or Migration Protocols for WordPress Sites

A protocol for backing up and/or migrating a Wordpress site.


### Future

1. Integrate Install Needs section into ansible for ubuntu 16.04 systems.


### Backup

#### Components

This is the same pattern for any modern web application framework.

1. MySQL Database
2. Project Directory


#### Backing up the MySQL Database

1. Get the following from the `wp-config.pyp`:
    - Database Name
    - Username
    - Password

2. `mysqldump {Database Name} > ~/backups/mywpsite.bkp.yyyymmdd.sql -u {Username} -p
    - Enter password at the prompt 


#### Backing up the Project Directory

`tar -czvf ~/backups/myproject.bkp.yyyymmdd.tar.gz /my/project/root/directory/`


### Migration

Do these in order.

1. Back up the site and copy the `tar.gz` and the `sql` files to the new location

2. Rebuilding the project
    1. Unzip the `tar.gz` file into `/var/www/websites` 
        - The full path should be `/var/www/websites/www.example.com/www/{wordpress root}`
    2. Change the permissions of this path: `chown -R www-data:www-data {path}`
        - If you wish to traverse symlinks, use `-H` flag.
    3. Make a symlink at `/var/www/www.example.com` to `/var/www/websites/www.example.com`
        - Saves tons of work later if you need to redirect to another location

3. Set up the MySQL user, database, password on the new location
    1. Login to MySQL as the root user: `$ mysql -u root -p`
        - enter password at prompt
    2. `create database {Database Name};`
    3. `create user '{User}'@'localhost' IDENTIFIED BY '{Password}'`
        - Does the next step create the user automatically if you don't do this?
    4. `grant usage on '{database}'.* to '{User}'@'localhost' identified by '{Password}';`
    5. view your changes: `mysql> select user, host, password from mysql.user;`
    6. `mysql> FLUSH PRIVILEGES;` then `mysql> quit;`
    7. Ensure the `wp-config.php` has the same Database Name, Username, Password
    8. Move the `sql` file to the wordpress root directory
    9. `$ wp-cli.phar db import mywpsite.bkp.yyyymmdd.sql`
        - [wp db import](http://wp-cli.org/commands/db/import/)
        - You need wp-cli.phar on your path if it is not already
        - Alternatively put a copy in local directory or specify `/path/to/wp-cli.phar`
    10. If your WordPress site URL has changed
        1. Update the database with wp-cli
            - `wp-cli.phar option update home 'http://www.example.com'`
            - `wp-cli.phar option update siteurl 'http://www.example.com'`
        2. If you have urls in your posts, pages, etc.
            - `wp-cli.phar search-replace 'example.dev' 'example.com' --skip-columns=guid`

4. Configure and restart apache2
    1. Use a template!
        - Generally I just copy another site that follows the same pattern
        - Then search and replace your new website name
    2. Store in `/etc/apache2/sites-available/{mywebsitename}.conf`
    3. Make sure your apache logs exist in `{projectdirectory}/logs/`
        - For more info, check the path in your apache config file
        - `access.log`, `error.log`
    4. `a2ensite {mywebsitename}` then `apache2 restart`

5. If you have errors, fix this configuration as you fix the error.
6. [WP Codex - Changing The Site URL](https://codex.wordpress.org/Changing_The_Site_URL)


### WordPress Requirements

WordPress requires a great many packages and configuration settings. Here are some packages that were installed manually on a Ubuntu 14.04 server in the past.

1. `apt-get install postfix`
    - This is important so WordPress can send mail (doesn't need a real outbound address)
    - This needs configured more completely to try to evade spam filters
    - [DigitalOcean WordPress Email Reference](https://www.digitalocean.com/community/questions/wordpress-won-t-send-contact-form-emails)
    - FUTURE: There are alternatives like going through a gmail acount with wp-smtp plugin
    - FUTURE: [WordPress Contact Form 7 Spam Reference](http://kb.cf7skins.com/contact-form-7-email-issues/#spam) - Apparently there are some nice tricks to avoid being treated as spam?
2. Set up apache2 Virtual Hosts
3. Set up mysql root user
4. Set up php5 modules for apache2
5. Set up mod-rewrite for apache2
6. More...
7. Fix the php upload file sizes
8. Directory/File permission fixers (files vs dirs, see snips) for annoying hosts.
9. Other snips from my snips git repo
