transmission-daemon 간편 사용법
==============================

-항목 추가 사항
  - **부팅시 자동 시작하는지 확인**
  - ui 설정 확인

1. 설치
```bash
$ sudo apt install transmission-daemon -y
$ sudo vim /etc/transmission-daemon/settings.json
$ service transmission-daemon restart
```
transmission-daemon 설치

```bash
$ service transmission-daemon stop
```
`/etc/transmission-daemon/settings.json` 파일 수정시 데몬을 멈춰야 수정이 가능

```json
"rpc-whitelist": "127.0.0.1",
"rpc-whitelist-enabled": false,
"rpc-password": "password",
"rpc-password": "camell",
"download-dir": "/data/samba",
"download-queue-size": 2,
```
