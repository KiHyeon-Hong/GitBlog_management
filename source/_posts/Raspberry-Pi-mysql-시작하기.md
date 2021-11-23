---
title: Raspberry Pi mysql 시작하기
date: 2021-11-15 21:32:12
tags:
  - Raspberry Pi
  - mysql
categories:
  - Raspberry Pi
---

## mysql 설치

```bash
$ sudo apt-get install mariadb-server
```

### mysql 설정

```bash
$ cd /etc/mysql/mariadb.conf.d
$ sudo cp 50-server.cnf server.cnf.backup
$ sudo vi 50-server.cnf
```

- bind-address = 127.0.0.1를 주석처리 한다.

```bash
# bind-address = 127.0.0.1
```

### mysql 시작하기

```bash
$ sudo systemctl restart mariadb.service
$ cd -
$ sudo mysqladmin -u root password 'gachon654321'
```

```bash
$ sudo mysql -u root -p
Enter password: *
MariaDB > set password for root@localhost = password('gachon654321');
MariaDB > use mysql;
MariaDB > update user set authentication_string=password(''), plugin='mysql_native_password' where user='root';
MariaDB > flush privileges;
MariaDB > exit
$ mysql -u root -p
Enter password: *
MariaDB >
```

## mysql 테스트

- 추후 진행할 9축센서 데이터를 이용한 충격감지 알고리즘 개발을 위한 데이터베이스 생성

```sql
create database 9axisdb;
use 9axisdb;
```

```sql
create table ShockData(time datetime(3), shocklevel int, shockdirection int, azimuthshockdirection int, shockvalue float, degree int, azimuth int, code int, message varchar(256));

create table Log(time datetime(3), log varchar(256));

desc ShockData;
desc Log;
```
