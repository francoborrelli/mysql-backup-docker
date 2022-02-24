# mysql-backup-docker

A background backup utility for MySQL and AWS S3

Docker compose example

```yml
version: '3'

services:
  db:
    image: mariadb:latest
    restart: always
    environment:
      MYSQL_DATABASE: database
      MYSQL_USER: test
      MYSQL_PASSWORD: test-pwd

  backup:
    image: registry.gitlab.com/gral/backups/mysql-backup-docker
    restart: always
    environment:
      MYSQL_DATABASE: database
      MYSQL_HOST: db
      MYSQL_PORT: 3306
      MYSQL_PASSWORD: test-pwd
      MYSQL_USER: test
      AWS_ACCESS_KEY_ID: xxxxxxxx
      AWS_SECRET_ACCESS_KEY: xxxxxxxx
      BUCKET: bucket
      PREFIX: db
      MAIL_FROM: mail@example.com
      MAIL_USER: mail@example.com
      MAIL_HOST: mail.example.com
      MAIL_PORT: 587
      MAIL_PASSWORD: mail_pass
      MAIL_TO: mail@example.com
    volumes:
      - database_backup:/backups

volumes:
  database_backup:
    driver: local
```
