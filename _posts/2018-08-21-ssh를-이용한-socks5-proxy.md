ssh를 이용한 socks5 proxy 설정
-------------

### 실행

```bash
sshpass -p<암호> ssh -D <IP or Domain Name>:<port> -f -N -C -q localhost
```

### 예제
```bash
sshpass -ppwstring ssh -D 192.168.0.1:1009 -f -N -C -q localhost
```