tango-i 서버 신규 패키지 설치 방법 정리
---

docker명령은 windows의 powershell에서 실행한다.

### tango-i 서버 정보
- centos 6.8

### docker desktop 설치
docker desktop을 설치한다.  
설치후 docker desktop을 실행하면 wsl을 통해 백그라운드 데몬으로 동작한다.  
때문에 이후 PC를 재부팅하면 다시 데몬을 실행해야한다.(옵션으로 시작시 실행 가능)

### centos 이미지 다운로드
centos6.8 이미지를 다운로드 한다.

```powershell
PS> docker pull centos:6.8
```
> 이미지 tag 정보: https://hub.docker.com/_/centos?tab=tags&page=1&name=6.8

### centos 이미지 실행

```
PS> docker run -i -t centos:6.8 /bin/bash
[root@012840c00ab2 /]#
```

이때 docker desktop 대쉬보드에서 exited (139)로 강제 종료되면  
```%userprofile%\.wslconfig``` 파일을 생성한뒤 재부팅 후 다시 시도한다.  
파일내의 내용은 아래와 같다.

```powershell
[wsl2]
kernelCommandLine = vsyscall=emulate
```

