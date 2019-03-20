---
layout: post
title: "CentOS에서 IP 설정 하는법"
tags: [CentOS, Linux, IP]
comments: true
---

CentOS에서 IP 설정하는 방법을 공부해 보았습니다.

---

## CentOS에서 IP 설정 방법

1. 명령어 cd /etc/sysconfig/network-scripts/ 실행 (network-scripts 디렉토리로 이동)

2. 명령어 ls로 파일 확인 (ifcfg-ens__찾기. 6버전에선 ifcfg-e___)
3. Vi or gedit 으로 위에서 찾은 파일 실행	

4. BOOTPROTO = NONE으로 수정, IPADDR, NETMASK, GATEWAY, DNS1 설정하기 
onboot = yes 해줘야 다시 재부팅 해도 자동으로 ipup이 된 상태가 됩니다.

5. Systemctl restart network 실행 (네트워크 재실행)

6. ip addr 실행 (IP 정보 출력)

 실행이 되지 않을시

  1)	ifup ens__ 실행 (네트워크 인터페이스 켜기)

  2)	VMware > 가상머신세팅 > 네트워크어댑터 > Bridged체크, 체크박스 체크

  3)	Ping 8.8.8.8 실행 (연결 확인차)

