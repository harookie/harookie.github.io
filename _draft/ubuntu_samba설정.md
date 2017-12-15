
## TODO List

```
harookie@miTul-homelinux:~$ sudo apt-get install samba -y
```
samba를 간단하게 설치해 준다.

```
harookie@miTul-homelinux:~$ sudo mkdir /data
harookie@miTul-homelinux:~$ cd /data
harookie@miTul-homelinux:/data$ sudo mkdir samba
harookie@miTul-homelinux:/data$ sudo addgroup family
harookie@miTul-homelinux:/data$ sudo usermod -a -G family harookie
harookie@miTul-homelinux:/data$ sudo usermod -a -G family gpflatm
harookie@miTul-homelinux:/data$ sudo chgrp family samba
harookie@miTul-homelinux:/data$ sudo chmod g+w samba
```
공용으로 사용할 디렉토리와 개인용으로 사용할
공용그룹을 만들어 함께쓸 디렉토리에는 해당 그룹에 권한 부여

```
harookie@miTul-homelinux:/data$ sudo vi /etc/samba/smb.conf
harookie@miTul-homelinux:~$ sudo vim /etc/samba/smb.conf
harookie@miTul-homelinux:~$ sudo service smbd restart
```

```
harookie@miTul-homelinux:/data$ sudo smbpasswd -a harookie
New SMB password:
Retype new SMB password:
Added user harookie.
harookie@miTul-homelinux:/data$ sudo smbpasswd -a gpflatm
New SMB password:
Retype new SMB password:
Added user gpflatm.
harookie@miTul-homelinux:/data$
```
신규 계정을 추가해준다.

## TEST
```
[samba]
comment = common samba directory
path = /data/samba
valid users = harookie,gpflatm
writable = yes
public = yes
create mask = 0644
directory mask = 0755
```
