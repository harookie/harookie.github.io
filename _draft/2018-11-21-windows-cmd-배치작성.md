windows cmd 배치작성 snippet
--------------------------

### 이더넷 설정 관련

#### 이더넷 enable/disable

```sh
> rem 인터페이스 목록 확인
> netsh interface show interface

관리 상태      상태           종류             인터페이스 이름
-------------------------------------------------------------------------
사용             연결됨            전용               로컬 영역 연결
사용             연결됨            전용               로컬 영역 연결 2

> rem 인터페이스 끄기
> netsh interface set interface "로컬 영역 연결" disable
> rem 인터페이스 켜기
> netsh interface set interface "로컬 영역 연결" enable
```

#### 연결 관리

```sh
> rem 연결 해제
> ipconfig /release
> rem 연결 갱신
> ipconfig /renew
```

#### 연결 공유

### 기타

#### 프로그램 수행

```text
> rem 명령어 형식
> rem start "설명(프로그램명)" "수행 명령어"
> rem start "chrome" "URL"
> start "KakaoTalk" "C:\Program Files (x86)\Kakao\KakaoTalk\KakaoTalk.exe"
> start "Outlook" "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Microsoft > Office\Microsoft Office Outlook 2007"
> start "NateOnBiz" "C:\Program Files (x86)\NATEON BIZ\Bin\NateOnBiz.exe"
> start "synergy" "C:\Program Files\Synergy\synergy.exe"
> start "chrome" "http://monaco.mobigen.com"
```