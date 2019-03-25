---
layout: post
title: "CentOS7에서 MariaDB binary 설치"
tags: [MariaDB,CentOS7,binary]
comments: true
---

CentOS7버전에서 MariaDB를 binary 형식으로 설치해보기

---

## 과정

	1. 	tar.gz 파일 다운로드(wget)

	2. 	Database 계정 생성

	3. 	DATA, LOG 디렉토리 생성

	4. 	tar파일 압축 해제

	5. 	심볼릭 링크 설정

	6. 	소유권 변경

	7. 	etc 디렉토리 아래 my.cnf 설정 해주기

	8. 	database 설치

	9. 	service 등록

	10.	MariaDB 실행


## 세부 과정

1. tar.gz 파일을 다운로드한다.

	주소 : https://downloads.mariadb.org/mariadb/

 참고. wget을 사용하려면 yum -y install wget 으로 wget먼저 설치 후 사용

2. OS 계정을 생성한다.

	~]# groupadd dba
	~]# useradd -g dba maria

3. DATA와 LOG 디렉토리를 생성해준다.
	~]# mkdir /DATA
	~]# mkdir /LOG

4. tar 파일 압축 해제

	~]# tar -zxvf mariadb-10.2.8-linux-x86_64.tar.gz -C /usr/local/

5. 심볼릭 링크 설정 >>> 알아보기 쉽게 하려고

	~]# cd /usr/local
	local]# mv mariadb-버전-linux-x86_64 mariadb-버전
	local]# ln -s mariadb-버전 mariadb
	local]# ll

6. 소유권 변경 >>> maria.dba에서 사용하려고

	~]# chown -R maria.dba /usr/local/mariadb-버전
	~]# chown -R maria.dba /usr/local/mariadb
	~]# chown -R maria.dba /DATA
	~]# chown -R maria.dba /LOG

7. etc 디렉토리 안에 my.cnf 생성 >>> 꼭 etc 디렉토리 안에 생성 안해도 된다.
	
	(초기 셋팅값)
	
	[mysqld] 
	user = maria 
	port = 3306 
	socket = /tmp/mysql.sock 
	basedir = /usr/local/mariadb 
	datadir = /DATA 
	transaction_isolation = REPEATABLE-READ 
	innodb_data_home_dir = /DATA 
	innodb_buffer_pool_size = 512M 
	innodb_log_file_size = 128M 
	log-error = /LOG/maria_error.log

8. 데이터베이스 설치

	~]$ /usr/local/mariadb/scripts/mysql_install_db --defaults-file=/etc/my.cnf --basedir=/usr/local/mariadb

9. 서비스 등록

	~]# cp /usr/local/mariadb/support-files/mysql.server /etc/init.d/maria 
	~]# vi /etc/init.d/maria 

	line 46, 47 basedir, datadir 수정
	
	basedir=/usr/local/mariadb 
	datadir=/DATA

10. 실행

	su – maria
	service maria start

	설치 되어있는 /bin 폴더로 이동

	./mysql -u 계정 -p
