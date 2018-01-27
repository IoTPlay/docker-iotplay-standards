## General MariaDB Help and HowTo's

#### Initiation of Database for Dabar
- Fix login of initial database, [mariadb](https://mariadb.com/kb/en/library/configuring-mariadb-for-remote-client-access/):
  - The my.cnf file must actually by `mariadb.cnf`, in the folder /etc/mysql, on the docker instance.
  - add bind_address=0.0.0.0 to mariadb.cnf
  - Login to DB server:
      - if on Docker `docker exec -it -containerid- sh`,
      - `mysql -uroot -pWhatisthePassword01 dabar`
      - `SELECT User, Host FROM mysql.user WHERE Host <> 'localhost';`
      - `GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'WhatisthePassword01' WITH GRANT OPTION;`
      - `flush privileges;`

  - Check if port `3306` is running: from db command line: `SHOW GLOBAL VARIABLES LIKE 'PORT'; ` or from Linux: `netstat -tlnp`

  - with NodeRed connected to the mariadb via a 'link', the host field on nodered is the container name `dbr_mariadb_1`
  - To check GRANTS: `show grants for 'root'@'%' ;`

#### HowTo's
- Checking the version, log into the client, or just do an SQL call. `SELECT VERSION() ; `
- Which my.cnf is my mariadb using?: `mysqld --verbose --help | grep -A 1 "Default options"`
- Create a mysql backup read-only user [blog bencane](http://bencane.com/2011/12/12/creating-a-read-only-backup-user-for-mysqldump/)

##### User Mgt from Command Line
- Display users: `SELECT User,Host FROM mysql.user;`
- Delete a user: `DROP USER 'root'@'localhost';`
- Create a user: `CREATE USER 'root'@'%' IDENTIFIED BY '-password-';`
- Grant all privileges: `GRANT ALL PRIVILEGES ON *.* TO 'root'@'%';`
- Clean up: `FLUSH PRIVILEGES;`

##### MariaDB from docker

- Problems with stopping the container
  > docker stop --time=30 mariadbtest
    docker kill mariadbtest  