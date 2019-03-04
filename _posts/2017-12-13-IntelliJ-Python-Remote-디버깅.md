IntelliJ Python Remote 디버깅
----------------------------

### 개요

실제 프로젝트를 수행할경우, 대부분의 경우 프로그램을 작성하는 PC의 환경과
실제 운용/테스트 환경이 다른경우가 대부분이다.
OS, DB, 파일시스템등 데스크탑에서 작성할때는 문제 없이 동작하던 모듈이 서버에만 올라가면
오동작할때 `print`등을 사용해 변수를 찍는 방법과, pdb를 이용한 방법을 사용할수 있다.
하지만, 두 경우 모두 여의치 않을때 Intellij의 리모트 디버깅을 사용하면 좀더 쉽게 디버깅을 진행할수 있다.

원격 디버깅의 간단한 흐름은 아래와 같다.

1. PC의 Intellij에서 디버깅 서버 시작
1. AP 서버의 client 클라이언트 수행, 디버깅 서버 접속
1. remote 디버깅 시작

### Prerequirement

설명에 등장하는, 서버나, 프로그램들의 이름이 헷갈릴 가능성이 있어 용어를 정의.

- AP 서버 : 디버깅을 수행하려는 서버
- PC : IntelliJ을 실행하는 데스크탑 PC
- 디버깅 클라이언트 : AP서버에서 실행되는 디버깅 코드가 삽입된 대상 스크립트를 수행한 프로세스
- 디버깅 서버 : IntelliJ에서 실행되는 디버깅을 위해 실행되는 서버 프로그램

#### pydevd 설치

스크립트에서 호출되어 remote 디버깅을 수행하는 파이썬 라이브러리이다.  
pip 혹은 소스로 PC와 AP 서버에 모두 설치한다.  
소스의 경우 [여기]에서 다운로드 받으면 된다.  
root계정이 아닌경우 --user 옵션을 주어 user계정 아래 모듈이 설치되도록 한다.  
설치 직후 'import pydevd'를 수행하면 아래와 warning이 발생하는데, 지시와 같이 명령을 수행하면 사라진다.

```bash
$ cd ~
$ python $PYDEVD_DOWNLOAD_PATH/setup.py build
$ python $PYDEVD_DOWNLOAD_PATH/setup.py install --user
$ python
Python 2.7.12 (default, Dec 20 2016, 21:15:56)
[GCC 4.4.7 20120313 (Red Hat 4.4.7-17)] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> import pydevd
warning: Debugger speedups using cython not found. Run '"/usr/local/bin/python2.7" "setup_cython.py" build_ext --inplace' to build.
>>>
$ "/usr/local/bin/python2.7" "setup_cython.py" build_ext --inplace
running build_ext
copying build/lib.linux-x86_64-2.7/_pydevd_bundle/pydevd_cython.so -> _pydevd_bundle
$
```

#### 클라이언트 코드 추가

Remote 디버깅을 하려면, 약간의 추가적인 코드가 필요하다.
기존 스크립트에 추가 혹은, 스크립트를 호출하는 별도의 클라이언트 코드 둬도 된다.
핵심 코드는 `pydevd.settrace()`를 호출, 디버깅 서버에 접속하는 코드를 추가해주는 것이다.

```python
import pydevd
import argparse


def main():
    var01 = 01
    var02 = 02
    print 'here'


if __name__ == "__main__":
    argParser = argparse.ArgumentParser(description='Remote Debugging Test')
    argParser.add_argument('--debug_ip', metavar='DEBUG_IP')
    argParser.add_argument('--debug_port', metavar='DEBUG_PORT', default=5678, type=int)
    args = argParser.parse_args()

    if args.debug_ip:
        pydevd.settrace(host=args.debug_ip, port=args.debug_port, stdoutToServer=True, stderrToServer=True)

    main()
```

> test_remote.py

#### Intellij Remote 디버깅 Configuration 추가

IntelliJ의 **Run \| Edit Configurations \| Python Remote Debug**에서 신규 항목을 추가한 뒤, 아래와 같이 설정한다.

- local host name : PC의 IP
- Port : 디버깅 서버 port
- Path mapping : PC의 프로젝트 root와 AP 서버의 프로젝트 root를 설정한다. 설정한 디렉토리 하위는 동일해야, 디버깅이 정상 동작한다.

![debug configuration]

### 디버깅

#### 디버깅 서버 실행

실행하려는 디버깅 항목을 선택하고, 벌레 모양을 클릭하여 디버깅을 시작  
`Wait for process connection...` 이라는 메시지와 함께 클라이언트의 접속을 대기한다.

![run debugging]

#### 디버깅 클라이언트 실행

AP 서버에서 클라이언트 스크립트 실행

![run client script]

#### 디버깅 시작

![debugging]

[여기]: https://pypi.python.org/pypi/pydevd
[debug configuration]: /user_images/2017-12-13-IntelliJ-Python-Remote-디버깅/001.png
[run debugging]: /user_images/2017-12-13-IntelliJ-Python-Remote-디버깅/002.png
[run client script]: /user_images/2017-12-13-IntelliJ-Python-Remote-디버깅/003.png
[debugging]: /user_images/2017-12-13-IntelliJ-Python-Remote-디버깅/004.png