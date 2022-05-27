# 문서 수정 사항
- 작동여부확인
- 내용보충


### 설치전에
- 중간에 `<username>`은 개인의 windows id로 변경해야함.
- 빌드툴의 경우 2015버전을 기준으로 작성되었으나, 실제 설치한 빌드툴 버전에 맞춰 변경 필요함.
- 이외의 프로그램/패키지들도 실제로 다운로드 받은 버전에 맞춰 path등의 변경 해야함.

### 필요 프로그램/패키지 다운로드
- Visual Studio용 빌드 도구(https://visualstudio.microsoft.com/ko/downloads)
    - 모든 다운로드 > Tools for Visual Studio 2019 > Visual Studio 2019용 Build Tools
    - 인터넷 접속 불가일 경우 이전 버전(https://visualstudio.microsoft.com/ko/vs/older-downloads)에서 풀버전을 다운로드 받아 설치
        - 재배포 가능 패키지 및 빌드 도구 > Microsoft Build Tools 2015 업데이트 3
- Perl, Strawberry Perl (https://strawberryperl.com)
- NASM(https://www.nasm.us)
- OpenSSL(https://www.openssl.org/source) 안정버전

### 설치전 설정
- path 환경변수 경로 추가
    - `C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\bin`
    - `C:\Users\<username>\AppData\Local\bin\NASM`

### 설치
시작 메뉴에서 `Visual C++ 2015 x86 x64 Cross Build Tools Command Prompt`를 **관리자 권한**으로 실행 아래 명령어들을 수행한다.
첫줄의 

```
> cd <압축해제 폴더>\openssl-1.1.1j
> perl Configure VC-WIN64A
> nmake
> nmake test
> nmake install
```

`NMAKE : fatal error U1045: spawn failed : Permission denied'`와 같은 에러를 발생할경우 windows의 보안 설정을 잠시
끈뒤 재진행, 완료 후 반드시 다시 켜기

- 설정 > Windows 보안 > 바이러스 및 위협 방지 > 바이러스 및 위협 방지 설정 > 설정 관리내의 
    - 실시간 보호
    - 클라우드 전송 보호
    - 자동 샘플 전송
    - 변조 보호


### 설치 확인
`C:\Program Files\OpenSSL\bin`에서 정상 설치 여부 확인



### python 설치시 ssl 에러 처리
openssl의 실행 경로를 환경변수 `PATH`에 추가한다.

환경변수는 아래에서 변경가능함.

`설정 > 시스템 > 정보 > 고급 시스템 설정 > 환경 변수 > 사용자 변수 > PATH`


### 아나콘다 설치시
아나콘다내의 `C:\Users\<<user>>\anaconda3\Library\bin`를 `PATH`에 추가한다.
해당 경로에 openssl 실행파일을 찾을수 있다.

### 일반 python
링크: </_private/python_pip_설치시_ssl_에러_처리.md>

[링크](/_private/python_pip_설치시_ssl_에러_처리.md)
