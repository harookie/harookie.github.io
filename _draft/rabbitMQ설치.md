## 패키지 설치
#### erlang   
- wget https://packages.erlang-solutions.com/erlang-solutions-1.0-1.noarch.rpm
- rpm -Uvh erlang-solutions-1.0-1.noarch.rpm
- yum install erlang
#### socat
- wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm
- rpm -i epel-release-latest-6.noarch.rpm
- yum install socat
#### RabbitMQ   
- wget https://github.com/rabbitmq/rabbitmq-server/releases/download/rabbitmq_v3_6_5/rabbitmq-server-3.6.5-1.noarch.rpm
- rpm --import https://github.com/rabbitmq/rabbitmq-server/releases/download/rabbitmq_v3_6_5/rabbitmq-server-3.6.5-1.noarch.rpm.asc
- yum install rabbitmq-server-3.6.5-1.noarch.rpm
```bash
[harookie@cent01 ~]$ wget https://packages.erlang-solutions.com/erlang-solutions-1.0-1.noarch.rpm https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm https://github.com/rabbitmq/rabbitmq-server/releases/download/rabbitmq_v3_6_5/rabbitmq-server-3.6.5-1.noarch.rpm
--2016-11-30 14:23:25--  https://packages.erlang-solutions.com/erlang-solutions-1.0-1.noarch.rpm
Resolving packages.erlang-solutions.com... 31.172.186.53
Connecting to packages.erlang-solutions.com|31.172.186.53|:443...
... (생략)
[harookie@cent01 ~]$ sudo rpm -Uvh erlang-solutions-1.0-1.noarch.rpm && sudo rpm -i epel-release-latest-6.noarch.rpm && sudo rpm --import https://github.com/rabbitmq/rabbitmq-server/releases/download/rabbitmq_v3_6_5/rabbitmq-server-3.6.5-1.noarch.rpm.asc
[harookie@cent01 ~]$ sudo yum install -y erlang socat rabbitmq-server-3.6.5-1.noarch.rpm
[harookie@cent01 ~]$ rm epel-release-latest-6.noarch.rpm erlang-solutions-1.0-1.noarch.rpm rabbitmq-server-3.6.5-1.noarch.rpm
```

## 서비스 등록
```
[harookie@cent01 ~]$ su - root
Password:
[root@cent01 ~]# chkconfig --level 2345 rabbitmq-server on
[root@cent01 ~]# # rabbitmq pw 변경
[root@cent01 ~]# passwd rabbitmq
Changing password for user rabbitmq.
New password:
BAD PASSWORD: it is based on a dictionary word
BAD PASSWORD: is too simple
Retype new password:
passwd: all authentication tokens updated successfully.
[root@cent01 ~]# # rabbitmq plugin 설정 디렉토리의 소유변경
[root@cent01 ~]# chown rabbitmq:rabbitmq /etc/rabbitmq
[tangosvc@cent01 etc]$ su - rabbitmq
Password:
-bash-4.1$ echo export PS1=\"[\\u@\\h \\W]\\$ \" >> ~/.bash_profile
-bash-4.1$ source ~/.bash_profile
[rabbitmq@cent01 ~]$ # 관리용 UI 플러그인
[rabbitmq@cent01 ~]$ rabbitmq-plugins enable rabbitmq_management
The following plugins have been enabled:
  mochiweb
  webmachine
  rabbitmq_web_dispatch
  amqp_client
  rabbitmq_management_agent
  rabbitmq_management

Applying plugin configuration to rabbit@cent01... started 6 plugins.
[rabbitmq@cent01 ~]$ # 브로커 내부 user추가 및 설정
[rabbitmq@cent01 ~]$ rabbitmqctl add_user rabbitmq rabbitmq
Creating user "rabbitmq" ...
[rabbitmq@cent01 ~]$ rabbitmqctl set_user_tags rabbitmq administrator
Setting tags for user "rabbitmq" to [administrator] ...
[rabbitmq@cent01 ~]$ rabbitmqctl add_vhost /tango-i
Creating vhost "/tango-i" ...
[rabbitmq@cent01 ~]$ rabbitmqctl set_permissions -p /tango-i rabbitmq ".*" ".*" ".*"
Setting permissions for user "rabbitmq" in vhost "/tango-i" ...
[rabbitmq@cent01 ~]$
```
> python 사용시 pika 모듈이 필요함

<br>

## 기타
- `http://<host>:15672`을 통해 WEB UI 접근이 가능 
- 사용포트
    - 4369 (epmd), 25672 (Erlang distribution)
    - 5672, 5671 (AMQP 0-9-1 without and with TLS)
    - 15672 (if management plugin is enabled)
    - 61613, 61614 (if STOMP is enabled)
    - 1883, 8883 (if MQTT is enabled)