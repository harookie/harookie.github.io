windows cmd 배치작성
-------------------

### 예제

```text
rem 이더넷 재설정
ipconfig /release
ipconfig /renew

rem 프로그램 기동
rem start "프로그램명" "수행 명령어"
start "KakaoTalk" "C:\Program Files (x86)\Kakao\KakaoTalk\KakaoTalk.exe"
start "Outlook" "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Microsoft Office\Microsoft Office Outlook 2007"
start "NateOnBiz" "C:\Program Files (x86)\NATEON BIZ\Bin\NateOnBiz.exe"
start "synergy" "C:\Program Files\Synergy\synergy.exe"
start "chrome" "http://monaco.mobigen.com"
```