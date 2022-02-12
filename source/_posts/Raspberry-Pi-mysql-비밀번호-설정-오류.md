---
title: Raspberry Pi mysql 비밀번호 설정 오류
date: 2022-02-12 11:26:17
tags:
  - Raspberry Pi
  - mysql
categories:
  - Raspberry Pi
---

## root 비밀번호 설정 오류

- https://kihyeon-hong.github.io/2021/11/15/Raspberry-Pi-mysql-%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0/
- 기존의 방식으로 root 비밀번호를 설정하는 과정에서 오류가 발생한다.

<p align="center"><img src="/images/RaspberryPi/mysql/mysqlError/mysqlError1.jpg"></p>

```bash
ERROR 1356 (HY000): View 'mysql.user' references invalid table(s) or column(s) or function(s) or definer/invoker of view lack rights to use them
```

- 이는 MariaDB-10.4+에서 user가 table이 아니라 view로 변경되어 발생하는 오류이다.

### 오류 수정

<p align="center"><img src="/images/RaspberryPi/mysql/mysqlError/mysqlError2.jpg"></p>

- 다음의 명령어로 root의 password hash 값이 변경되는 것을 확인할 수 있다.
- 이를 적용한다.

```bash
set password for root@'localhost' = PASSWORD('gachon654321');
flush privileges;
exit
```

### 변경 확인

```bash
sudo systemctl restart mariadb.service
mysql -u root -p
```

<p align="center"><img src="/images/RaspberryPi/mysql/mysqlError/mysqlError3.jpg"></p>

- 잘못된 비밀번호를 입력하면, 접속이 거부되며, 올바른 비밀번호로 접속이되는 것을 확인할 수 있다.
- 이때, 주의할 점은 sudo 명령어로 mysql 접속을 시도할 경우 잘못된 비밀번호를 입력하더라도 접속이 허용될 수 있다.
