---
layout: post
title: "CentOS7에서 MariaDB package 설치"
tags: [MariaDB,rpm,package]
comments: true
---

CentOS7버전에서 MariaDB를 package 형식으로 설치해보기

---

## MariaDB 설치 방식

- yum 방식
- package 방식
- binary 방식
- source 방식

각각의 특징은 binary와 source 방식의 설치도 해본 뒤 작성.


### Package 방식

 - https://downloads.mariadb.org/mariadb/ 접속해서 필요한 버전의 mariadb 다운로드 받기.
 이때 common, client, server는 필수로 받아야 한다. 이 세 파일만 있어도 mariadb를 설치 및 실행이 가능하다.

-  vmware 상의 폴더에 drag&drop 시킨다.

-  설치 파일이 제대로 옮겨졌나 확인.

![확인](https://user-images.githubusercontent.com/22653307/54742006-7864de00-4c03-11e9-825e-33a98e3802b3.JPG)


 - 파일이 있는 디렉토리로 이동하여, 설치를 진행하면 된다.
 
 명령어 : rpm -ivh --force --nodeps  MariaDB-*

![설치](https://user-images.githubusercontent.com/22653307/54742002-7569ed80-4c03-11e9-880b-d360348e7851.JPG)

- chkconfig mysql on 입력 >>> 서비스를 상시 가동시킨다.

- mysql 입력 >>> 실행