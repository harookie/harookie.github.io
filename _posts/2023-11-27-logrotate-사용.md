
logrotate는 자체적으로 로그의 로테이트가 불가한 프로그램의 로그를 원하는대로
로테이트 할수 있도록 해주는 유틸리티

자원사용량 수집을 위해 생성하는 로그의 사이즈와 갯수를 조절하기 위해 사용했던 실제 사용 예제에 대한 기록임.

### 실행 방식
- logrotate.d를 이용한 데몬에의한 수행방법
  - 이글에서는 사용하지 않음
- logrotate명령어를 수행때마다 즉시 수행하는 방법
  - 이글에서 사용하는 방법

### 설정 파일설정
```
# 대상이 되는 파일리스트
# 다수 파일을 나열 가능
/home/harookie/log/iostat/iostat.log
/home/harookie/log/inotifywait/inotifywait.log
/home/harookie/log/iotop/iotop.log

{
# 유지할 로그 파일의 갯수
rotate 96

# 시간/사이즈 등으로 분할 조건 부여가능
# hourly는 시간마다 생성
#size 100k
hourly
# 로그파일을 발견하지 못해도 에러처리 하지 않음
missingok
notifempty
# 로테이트 파일의 이름에 날짜가 들어가도록 생성
dateext
dateformat -%Y%m%d%H
#dateyesterday

# 파일 로테이트 하기전 수행할 명령어
# 아래설정은 파일명을 수정할수 있도록 한 프로세스를 kill하는 명령어들
prerotate
    #kill -9 `ps -ef | grep inotifywait  | grep -v grep | awk '{print $2}'`
    kill -9 `ps -ef | grep iostat | grep -v grep | awk '{print $2}'`
    sudo kill -9 `ps -ef | grep iotop | grep -v grep | awk '{print $2}'`
endscript
# 파일 로트이트 후 수행할 명령어
# 아래설정은 kill했던 프로세스들을 새로 시작하는 명령어들
postrotate
    #inotifywait -m  -e create,delete --format "%T %e %f" --timefmt "%Y-%m-%d %H:%M:%S" /home/nmsplus/DATA/alarm >> /home/nmsplus/user/harookie/inotifywait/inotifywait.log 2>&1 &
    iostat -txkdz -p ALL 5 >> /home/nmsplus/user/harookie/iostat/iostat.log 2>&1 &
    sudo iotop -P -o -a -k -t -q -d 60 >> /home/nmsplus/user/harookie/iotop/iotop.log 2>&1 &
endscript
}
```

### logrotate 실행
설정파일명과 상태 저장을 위한 .state 파일 path 지정해 수행함. 지속적인 수행이 아니라 1회성으로 수행됨
따라서 주기적으로 변경할 경우 crontab 등록 필요
`logrotate -f /home/nmsplus/user/harookie/logrotate.conf --state /home/nmsplus/user/harookie/logrotate.state`

### crontab 등록
```
0 * * * * /usr/sbin/logrotate -f /home/nmsplus/user/harookie/logrotate.conf --state /home/nmsplus/user/harookie/logrotate.state
```