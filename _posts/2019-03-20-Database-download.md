---
layout: post
title: "CentOS7에서 MariaDB,MySQL,PerconaDB 설치"
tags: [MariaDB,MySQL,PerconaDB]
comments: true
---

CentOS7버전에서 MariaDB, MySQL, PerconaDB를 설치하는 방법

---

## MariaDB yum install

참고 사이트

[MariaDB.com](https://mariadb.com/kb/en/library/yum/)
https://mariadb.com/kb/en/library/yum/

- curl -sS https://downloads.mariadb.com/MariaDB/mariadb_repo_setup | sudo bash
mariadb 패키지 저장소 설치 스크립트 사용. 다운로드를 받을 수 있는 환경 구축.

- sudo yum install MariaDB-server MariaDB-client
yum을 이용해서 MariaDB 설치

- rpm – qa | grep MariaDB
설치가 제대로 되었나 확인.(common, server, client)

- /etc/init.d/mysql start
mariadb 설치시 replaced가 mysql로 되어서 mysql을 실행시킴

## MySQL yum install

참고 사이트

[mysql.com](https://dev.mysql.com/doc/mysql-yum-repo-quick-guide/en/#repo-qg-yum-installing)
https://dev.mysql.com/doc/mysql-yum-repo-quick-guide/en/#repo-qg-yum-installing

- rpm -ivh https://dev.mysql.com/get/mysql80-community-release-el7-2.noarch.rpm
MySQL 다운로드를 받을 수 있는 환경 구축.

- yum install -y mysql-community-server
mysql 설치

- rpm – qa | grep mysql
설치가 제대로 되었나 확인.

- systemctl start mysqld.service
mysql 실행

## Percona yum install

참고 사이트

[percona.com](https://www.percona.com/doc/percona-server/5.7/installation/yum_repo.html)
https://www.percona.com/doc/percona-server/5.7/installation/yum_repo.html

- yum install https://repo.percona.com/yum/percona-release-latest.noarch.rpm
perconadb 다운로드 받을 수 있는 환경 구축

- yum install Percona-Server-server-57
PerconaDB 설치

- systemctl mysql start
PerconaDB 실행
