## DevOps

After a MariaDB crash, like one always does, I found myself with an old backup of the DB. I realised it could have been caused by the fact that I mounted a new Image with a new version for MariaDB, and that I need to improve the pracrices of first testing in Dev / QA against copies of current DB's, the impact of upgrades, for instance.

But then I also realised, that I did not know what the previous version no was, and that I need to track versions of Images, & NR nodes I am using, and to do package upgrades consciously, by tracking waht is in place, like a CMDB for all components, against a version.

So, here goes a list of things I want to use:

1. Check the version of **MariaDB**, running in a docker container.
  ```
  docker exec  dbr_mariadb_1 sh -c "mysql --version"
  ```
