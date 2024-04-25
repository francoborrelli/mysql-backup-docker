# mysql-backup-docker

![MySQL](https://img.shields.io/badge/mysql-4479A1.svg?style=for-the-badge&logo=mysql&logoColor=white)
![MariaDB](https://img.shields.io/badge/MariaDB-003545?style=for-the-badge&logo=mariadb&logoColor=white)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white)

A background backup utility for MySQL and Mariadb. It allows uploading backups to AWS S3.

## 🐳 Docker compose example

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
    image: ghcr.io/francoborrelli/mysql-backup-docker:master
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
