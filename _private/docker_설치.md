G1. 버전
    - centos : 7.6
1. docker desktop 설치
    - [Docker Desktop][Docker Desktop Download]을 다운받아 설치 GUI 설치
1. 도커 이미지 설치 및 설정
    ```shell
    $ # docker CLI 설치
    $ brew install docker
    $ # centos 이미지 다운로드 및 실행
    $ # CentOS systemctl permit 오류없이 실행
    $ # /sbin/init 실행후 "docker exec" 명령을 통해 bash를 실행한다.
    $ docker run --privileged -d -p 22 --name centos centos:centos7.6.1810 /sbin/init
    $ docker exec -it centos bash
    ```
1. 도커 컨테이너내 설정    
    HOST_IP를 GW라는 변수로 설정한다.
    ```shell
    $ # 개발툴 설치 및 초기 설정
    $ yum update -y && yum install -y initscripts sudo vim net-tools ntsysv openssh-server openssh-clients openssh-askpass && yum clean all
    $ yum groupinstall -y 'Development Tools'
    $ # 로케일 설정
    $ localedef -v -c -i en_US -f UTF-8 en_US.UTF-8 && echo -e "LANG=en_US.utf-8\nLC_ALL=en_US.utf-8" >> /etc/environment
    $ # 시간 맞추기
    $ ln -sf /usr/share/zoneinfo/Asia/Seoul /etc/localtime
    $ # ssh 설정, no password 접속 설정
    $ cd ~ && ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa && cd .ssh && cat id_rsa.pub >> authorized_keys && mkdir /var/run/sshd
    $ sed -i 's/^#Port 22$/Port 22/g' /etc/ssh/sshd_config
    $ # 다른 host에서 컨테이너에 접속하기 위한 설정
    $ CONTAINER_IP=`ifconfig eth0 | grep inet | awk '{print $2}'`
    $ NETMASK=`ifconfig eth0 | grep inet | awk '{print $4}'`
    $ echo "route add -net $CONTAINER_IP netmask $NETMASK gw $GW" 
    $ route add -net 172.17.0.0 netmask 255.255.0.0 gw 192.168.26.57
    route add -net 172.17.0.2 netmask 255.255.0.0 gw 192.168.65.0
    
    $ systemctl restart sshd.service
    ```

1. 도커 실행
$ docker rm centos

$ # centos 버전확인
$ cat /etc/system-release


/sbin/init



[Docker Desktop Download]: https://www.docker.com/products/docker-desktop


cat /etc/ssh/sshd_config | grep Port
cp /etc/ssh/sshd_config ~/sshd_config

sed 's/^#Port 22$/Port 22/' /etc/ssh/sshd_config > /etc/ssh/sshd_config
head /etc/ssh/sshd_config

cp ~/sshd_config /etc/ssh/sshd_config 