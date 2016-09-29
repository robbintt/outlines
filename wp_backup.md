### Basic Backup Protocol for WordPress Sites

A simple reference.


#### Components

This is the same pattern for any modern web application framework.

1. MySQL Database
2. Project Directory


#### Backing up the MySQL Database

1. Get the following from the `wp-config.pyp`:
    - Database Name
    - Username
    - Password

2. `mysqldump {Database Name} > ~/backups/mywpsite.bkp.yyyymmdd.sql -u <Username> -p
    - Enter password at the prompt 


#### Backing up the Project Directory

`tar -czvf ~/backups/myproject.bkp.yyyymmdd.tar.gz /my/project/root/directory/`
