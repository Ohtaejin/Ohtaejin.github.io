---
layout: post
title: "CentOS7에서 MariaDB Source Compile 설치"
tags: [MariaDB,CentOS7,SourceCompile]
comments: true
---

CentOS7버전에서 MariaDB를 Source Compile 형식으로 설치해보기

---



## Source compile 설치 과정

	1.	설치에 필요한 패키지 설치

	2.	MariaDB source file 다운로드

	3.	소스 압축 해제 및 compile 위한 디렉토리 생성

    4.	Compile

    5.	사용자 그룹 및 사용자 생성

    6.	디렉토리 생성 및 퍼미션 변경

    7.	시스템 테이블 생성

    8.	Mysqld startup script 설정

    9.	Library 등록

    10.	My.cnf 생성

    11.	MariaDB 실행


## 세부 과정

##### 1.	설치에 필요한 패키지 설치

	-yum install -y cmake make gcc gcc-c++ ncurses-devel libevent openssl openssl-devel gnutls-devel

##### 2.	MariaDB source file 다운로드

[바로가기](https://downloads.mariadb.org/) https://downloads.mariadb.org/

    wget 이용해 다운로드 받는다. 이때 wget을 설치하지 않았다면,

    yum -y install wget

    명령어를 이용해 wget를 먼저 설치한 후 진행한다.

##### 3.	소스 압축 해제 및 compile 위한 디렉토리 생성

    tar xvzf mariadb-버전.tar.gz
    cd mariadb-버전
    mkdir build_target
    cd build_target

##### 4.	Compile

    cmake .. -DWITH_READLINE=1
    -DWITH_SSL=bundled
    -DWITH_ZLIB=system
    -DDEFAULT_CHARSET=utf8
    -DDEFAULT_COLLATION=utf8_general_ci
    -DENABLED_LOCAL_INFILE=1
    -DWITH_EXTRA_CHARSETS=all
    -DWITH_ARIA_STORAGE_ENGINE=1
    -DWITH_XTRADB_STORAGE_ENGINE=1
    -DWITH_ARCHIVE_STORAGE_ENGINE=1 
    -DWITH_INNOBASE_STORAGE_ENGINE=1 
    -DWITH_PARTITION_STORAGE_ENGINE=1 
    -DWITH_BLACKHOLE_STORAGE_ENGINE=1 
    -DWITH_FEDERATEDX_STORAGE_ENGINE=1 
    -DWITH_PERFSCHEMA_STORAGE_ENGINE=1 
    -DCMAKE_INSTALL_PREFIX=/usr/local/mariadb 
    -DMYSQL_DATADIR=/usr/local/mariadb/data

    make && make install

##### 5.	사용자 그룹 및 사용자 생성

    groupadd mysql
    useradd -m -g mysql -d /usr/local/mariadb/data -s /bin/bash -c “MariaDB” mysql

##### 6.	디렉토리 생성 및 퍼미션 변경

    mkdir -p /usr/local/mariadb-버전/InnoDB/redoLogs
    mkdir -p /usr/local/mariadb-버전/InnoDB/undoLogs
    chown -R mysql /usr/local/mariadb-버전/data
    chown -R mysql /usr/local/mariadb-버전
    mkdir /usr/local/mariadb-버전/logs /usr/local/mariadb-버전/tmp
    chown mysql.mysql /usr/local/mariadb-버전/logs
    chown mysql.mysql /usr/local/mariadb-버전/tmp

##### 7.	시스템 테이블 생성

    cd /usr/local/mariadb/scripts
    ./mysql_install_db –basedir=/usr/local/mariadb –datadir=/usr/local/mariadb/data
    chown -R mysql:mysql /usr/local/mariadb/data

##### 8.	Mysqld startup script 설정

    cd /usr/local/mariadb/support-files
    cp mysql.server /etc/init.d/mysqld
    update-rc.d mysqld defaults

##### 9.	Library 등록

    echo “/usr/local/mariadb/lib” > /etc/ld.so.conf.d/mysql.conf
    ln -s /usr/local/mariadb-버전/lib /usr/local/mariadb-버전/lib64

##### 10. My.cnf 생성

    vi /etc/my.cnf

##### 11. MariaDB 실행

    /etc/init.d/mysqld start

