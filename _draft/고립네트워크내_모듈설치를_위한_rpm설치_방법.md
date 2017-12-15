#### 0. 전제사항
1. virtualbox등
2.

#### 1. virtualbox 설치해 관련 디펜던시를 다운로드 받아 설치
2-1. yum을 통해 설치를 한뒤 cache에 다운로드된 rpm들을 모은다.

#### 2-2. 패키지 로컬 다운로드

아래 yum 다운로더를 설치한다.
```
# # (RHEL5)
# yum install yum-downloadonly
# #(RHEL6)
# yum install yum-plugin-downloadonly
```

설치를 시도한다.  
`의존성 문제가 발생한 패키지들의 리스트가 나열된다.`

```bash
[root@localhost ~]# rpm -ivh esl-erlang_19.0.3-centos-6_amd64.rpm
warning: esl-erlang_19.0.3-centos-6_amd64.rpm: Header V4 RSA/SHA1 Signature, key ID a14f4fca: NOKEY
error: Failed dependencies:
        libodbc.so.2()(64bit) is needed by esl-erlang-19.0.3-1.x86_64
        libwx_baseu-2.8.so.0()(64bit) is needed by esl-erlang-19.0.3-1.x86_64
        libwx_baseu-2.8.so.0(WXU_2.8)(64bit) is needed by esl-erlang-19.0.3-1.x86_64
        libwx_baseu_xml-2.8.so.0()(64bit) is needed by esl-erlang-19.0.3-1.x86_64
        libwx_gtk2u_adv-2.8.so.0()(64bit) is needed by esl-erlang-19.0.3-1.x86_64
        libwx_gtk2u_adv-2.8.so.0(WXU_2.8)(64bit) is needed by esl-erlang-19.0.3-1.x86_64
        libwx_gtk2u_aui-2.8.so.0()(64bit) is needed by esl-erlang-19.0.3-1.x86_64
        libwx_gtk2u_aui-2.8.so.0(WXU_2.8)(64bit) is needed by esl-erlang-19.0.3-1.x86_64
        libwx_gtk2u_aui-2.8.so.0(WXU_2.8.5)(64bit) is needed by esl-erlang-19.0.3-1.x86_64
        libwx_gtk2u_core-2.8.so.0()(64bit) is needed by esl-erlang-19.0.3-1.x86_64
        libwx_gtk2u_core-2.8.so.0(WXU_2.8)(64bit) is needed by esl-erlang-19.0.3-1.x86_64
        libwx_gtk2u_gl-2.8.so.0()(64bit) is needed by esl-erlang-19.0.3-1.x86_64
        libwx_gtk2u_gl-2.8.so.0(WXU_2.8)(64bit) is needed by esl-erlang-19.0.3-1.x86_64
        libwx_gtk2u_html-2.8.so.0()(64bit) is needed by esl-erlang-19.0.3-1.x86_64
        libwx_gtk2u_html-2.8.so.0(WXU_2.8)(64bit) is needed by esl-erlang-19.0.3-1.x86_64
        libwx_gtk2u_stc-2.8.so.0()(64bit) is needed by esl-erlang-19.0.3-1.x86_64
        libwx_gtk2u_stc-2.8.so.0(WXU_2.8)(64bit) is needed by esl-erlang-19.0.3-1.x86_64
        libwx_gtk2u_xrc-2.8.so.0()(64bit) is needed by esl-erlang-19.0.3-1.x86_64
        libwx_gtk2u_xrc-2.8.so.0(WXU_2.8)(64bit) is needed by esl-erlang-19.0.3-1.x86_64

```

아래 명령어로 패키지 다운로드를 시도한다.

```
yum install --downloadonly --downloaddir=<다운로드_DIR> <패키지명>
```

정상적으로 다운로드가 완료가 되면 아래와 같은 메시지를 볼 수 있다.

```
[root@tg-d-iwas-in1 ~]# yum install --downloadonly --downloaddir=/root libodbc.so.2
Loaded plugins: fastestmirror, security
Setting up Install Process
Loading mirror speeds from cached hostfile
 * base: mirror.oasis.onnetcorp.com
 * centosplus: mirror.oasis.onnetcorp.com
 * contrib: mirror.oasis.onnetcorp.com
 * extras: mirror.oasis.onnetcorp.com
 * fasttrack: mirror.oasis.onnetcorp.com
 * updates: mirror.oasis.onnetcorp.com

Resolving Dependencies
--> Running transaction check
---> Package unixODBC.i686 0:2.2.14-14.el6 will be installed
--> Processing Dependency: libreadline.so.6 for package: unixODBC-2.2.14-14.el6.i686
--> Processing Dependency: libltdl.so.7 for package: unixODBC-2.2.14-14.el6.i686
--> Running transaction check
---> Package libtool-ltdl.i686 0:2.2.6-15.5.el6 will be installed
---> Package readline.i686 0:6.0-4.el6 will be installed
--> Processing Dependency: libtinfo.so.5 for package: readline-6.0-4.el6.i686
--> Running transaction check
---> Package ncurses-libs.i686 0:5.7-4.20090207.el6 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

=========================================================================================================================================================================================================================================================================
 Package                                                          Arch                                                     Version                                                                   Repository                                                     Size
=========================================================================================================================================================================================================================================================================
Installing:
 unixODBC                                                         i686                                                     2.2.14-14.el6                                                             C6.6-base                                                     382 k
Installing for dependencies:
 libtool-ltdl                                                     i686                                                     2.2.6-15.5.el6                                                            C6.0-base                                                      45 k
 ncurses-libs                                                     i686                                                     5.7-4.20090207.el6                                                        base                                                          249 k
 readline                                                         i686                                                     6.0-4.el6                                                                 C6.3-base                                                     176 k

Transaction Summary
=========================================================================================================================================================================================================================================================================
Install       4 Package(s)

Total size: 852 k
Total download size: 176 k
Installed size: 2.2 M
Is this ok [y/N]: Is this ok [y/N]: y
Downloading Packages:
readline-6.0-4.el6.i686.rpm                                                                                                                                                                                                                       | 176 kB     00:00
exiting because --downloadonly specified
```

만약 실패시 아래와 같은 메시지를 볼 수 있는데,

```
[root@localhost ~]# yum install --downloadonly --downloaddir=/root  libwx_baseu_xml-2.8.so.0
Loaded plugins: fastestmirror, security
Setting up Install Process
Loading mirror speeds from cached hostfile
 * base: mirror.oasis.onnetcorp.com
 * centosplus: mirror.oasis.onnetcorp.com
 * contrib: mirror.oasis.onnetcorp.com
 * extras: mirror.oasis.onnetcorp.com
 * fasttrack: mirror.oasis.onnetcorp.com
 * updates: mirror.oasis.onnetcorp.com
No package libwx_baseu_xml-2.8.so.0 available.
Error: Nothing to do
```

이런 경우 실제로를 같은 패키지인데 yum Repository내의 패키지명 달라서 생기는 문제 일 수 있다.
이럴 경우 아래 사이트에서 해당 패키지명을 검색해보고 다른 이름의 패키지명을 검색해서 위 명령어를 다시 수행


[rpmfind.net](https://rpmfind.net/linux/RPM/index.html)

그런뒤

다운로드가 되면 아래 명령으로 설치를 시도해본다.

`rpm -ivh <패키지명>`  
`rpm -ivh libodbc.so.2`


rpm -ivh
libwx_baseu_xml-2.8.so.0
ncurses-libs

rpm -ivh esl-erlang_19.0.3-centos-6_amd64.rpm unixODBC-2.2.14-14.el6.i686.rpm libtool-ltdl-2.2.6-15.5.el6.x86_64.rpm  readline-6.0-4.el6.i686.rpm wxBase-2.8.12-1.el6.centos.x86_64.rpm

yum install --downloadonly --downloaddir=/root wxGTK-gl


yum install --downloadonly --downloaddir=/root rabbitmq-server-3.6.5-1.noarch.rpm
yum install  --downloadonly --downloaddir=/root erlang-compiler


- erlang-19.1-1.el6.x86_64.rpm
  - erlang-asn1
    - erlang-compiler
    - erlang-stdlib
    - erlang-crypto
    - erlang-erts
    - erlang-hipe
    - erlang-kernel
    - erlang-stdlib
    - erlang-syntax_tools
