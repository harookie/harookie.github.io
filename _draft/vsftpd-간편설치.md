```bash
harookie@miTul-homelinux:~$ sudo apt install vsftpd -y
```

`/etc/vsftpd.conf`

```
xferlog_file=/var/log/vsftpd.log
write_enable=YES
```

```bash
$ service vsftpd restart
```
설정 활성화
