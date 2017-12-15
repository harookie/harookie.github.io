## 기본 설정
- 방화벽 해제
- sudo 유저 설정  
  - 암호입력제거

```bash
[root@cent01 ~]# adduser harookie
[root@cent01 ~]# passwd harookie
... (생략)
[root@cent01 ~]# # sudo 유저 설정 
[root@cent01 ~]# cat >> /etc/sudoers << EOF
tangosvc        ALL=(ALL)       NOPASSWD: ALL
EOF
[root@cent01 ~]# # 네트워크 카드 활성화
[root@cent01 ~]# sed s/ONBOOT=no/ONBOOT=yes/ /etc/sysconfig/network-scripts/ifcfg-eth0 > /tmp/tmp.tmp
[root@cent01 ~]# mv /tmp/tmp.tmp /etc/sysconfig/network-scripts/ifcfg-eth0
mv: overwrite `/etc/sysconfig/network-scripts/ifcfg-eth0'? y
[root@cent01 ~]# sed s/ONBOOT=no/ONBOOT=yes/ /etc/sysconfig/network-scripts/ifcfg-eth1 > /tmp/tmp.tmp
[root@cent01 ~]# mv /tmp/tmp.tmp /etc/sysconfig/network-scripts/ifcfg-eth1
mv: overwrite `/etc/sysconfig/network-scripts/ifcfg-eth1'? y
[root@cent01 ~]# /etc/rc.d/init.d/network restart 
[root@cent01 ~]# 
[root@cent01 ~]# # 방화벽 해제
[root@cent01 ~]# /etc/init.d/iptables stop
[root@cent01 ~]# yum groupinstall -y "Development tools"
[root@cent01 ~]# yum install -y make kernel-devel gcc perl python-devel gcc-c++ openssl libaio bc flex dpkg-devel zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel libffi-devel expat-devel
 
Loaded plugins: fastestmirror, security
... (생략)
Complete!
[root@cent01 ~]# yum upgrade -y
[root@cent01 ~]# # 시스템 재시작
[root@cent01 ~]# reboot
```

## 게스트 확장 설치
호스트 PC의 소스를 바로 이용하기 위해 호스트OS-게스트OS간의 공유 폴더를 생성한다.  
이 기능을 활성화 하기 위해 VirtualBox의 GuestAdditions(게스트확장)을 설치해준다.   
또한 필요한 링크들도 적당한 디렉토리에 설정한다.

```bash
[tangosvc@cent01 ~]$ # CD 삽입
[tangosvc@cent01 ~]$ ll /dev/cd*
lrwxrwxrwx. 1 root root 3 Nov 28 10:01 /dev/cdrom -> sr0
[tangosvc@cent01 ~]$ sudo mount -r /dev/cdrom /media
[tangosvc@cent01 ~]$ ll /media
total 51395
dr-xr-xr-x. 2 root root     2048 Nov 22 01:51 32Bit
dr-xr-xr-x. 2 root root     2048 Nov 22 01:51 64Bit
-r-xr-xr-x. 1 root root  8109517 Nov 22 02:46 VBoxLinuxAdditions.run
... (생략)

[tangosvc@cent01 ~]$ sudo /media/VBoxLinuxAdditions.run --nox11
Verifying archive integrity... All good.
Uncompressing VirtualBox 5.1.10 Guest Additions for Linux...........
... (생략)
Could not find the X.Org or XFree86 Window System, skipping.
```
## 공유 폴더 생성
최초 위 작업을 수행한후 매 부팅시 마다 공유폴더가 생성되도록 `/etc/rc.local`파일에도 명령을 추가 해준다. 
```bash
[tangosvc@cent01 ~]$ sudo mkdir -p /home/tangosvc/Documents /home/tangosvc/download /home/tangosvc/DR/drparser /data
[tangosvc@cent01 ~]$ sudo mount -t vboxsf Documents /home/tangosvc/Documents
[tangosvc@cent01 ~]$ sudo mount -t vboxsf download /home/tangosvc/download
[tangosvc@cent01 ~]$ sudo mount -t vboxsf drparser /home/tangosvc/DR/drparser
[tangosvc@cent01 ~]$ sudo mount -t vboxsf data /data
[tangosvc@cent01 ~]$ su - root
Password:
[root@cent01 ~]# cat >> /etc/rc.local << EOF
/etc/init.d/iptables stop
mount -t vboxsf drparser    /home/tangosvc/DR/drparser
mount -t vboxsf data        /data
mount -t vboxsf download    /home/tangosvc/download
mount -t vboxsf Documents   /home/tangosvc/document
EOF
```