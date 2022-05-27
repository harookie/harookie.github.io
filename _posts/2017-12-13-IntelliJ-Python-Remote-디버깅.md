---
layout: post
title: IntelliJ Python Remote 디버깅
---

# 문서 수정 사항
- 작동여부확인
- 내용보충

### 개요

실제 프로젝트를 수행할경우, 대부분의 경우 프로그램을 작성하는 PC의 환경과
실제 운용/테스트 환경이 다른경우가 대부분이다.
OS, DB, 파일시스템등 데스크탑에서 작성할때는 문제 없이 동작하던 모듈이 서버에만 올라가면
오동작할때 `print`등을 사용해 변수를 찍는 방법과, pdb를 이용한 방법을 사용할수 있다.
하지만, 두 경우 모두 여의치 않을때 Intellij의 리모트 디버깅을 사용하면 좀더 쉽게 디버깅을 진행할수 있다.

원격 디버깅의 간단한 흐름은 아래와 같다.

1. PC의 Intellij에서 python debug server 시작
1. AP 서버의 client 클라이언트 수행, 디버깅 서버 접속
1. remote 디버깅 시작

### Prerequirement

설명에 등장하는, 서버나, 프로그램들의 이름이 헷갈릴 가능성이 있어 용어를 정의.

- AP 서버 : 디버깅을 수행하려는 서버
- PC : IntelliJ을 실행하는 데스크탑 PC
- 디버깅 클라이언트 : AP서버에서 실행되는 디버깅 대상 프로세스
- 디버깅 서버 : PC의 IntelliJ에서 실행되는 디버깅을 위해 실행되는 서버 프로그램

#### pydevd-pycharm 설치

스크립트에서 호출되어 remote 디버깅을 수행하는 파이썬 라이브러리이다.  
pip 혹은 소스로 AP 서버에 설치한다.  

해당 라이브러리는 아래중에 선택해 설치한다.

1. pip를 이용해 설치 
1. intellij python plugin 제공 파일 설치 
   -  위치 : `C:\Users\<username>\AppData\Roaming\JetBrains\IntelliJIdea<versrion>\plugins\python\pydevd-pycharm.egg`
   - `python -m easy_install pydevd-pycharm.egg`
1. [pypi.org/project/pydevd-pycharm]에서 다운로드후 설치

root계정이 아닌경우 --user 옵션을 주어 user계정 아래 모듈이 설치되도록 한다.  

#### 클라이언트 코드 추가

Remote 디버깅을 하려면, 약간의 추가적인 코드가 필요하다.
기존 스크립트에 추가 혹은, 스크립트를 호출하는 별도의 클라이언트 코드 둬도 된다.
핵심 코드는 `pydevd.settrace()`를 호출, 디버깅 서버에 접속하는 코드를 추가해주는 것이다.

```python
# filename : test_remote.py
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

```bash
> test_remote.py --debug_ip=<ip> --debug_port=<port>
```

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

![pic_debugging]

[pypi.org/project/pydevd-pycharm]: https://pypi.org/project/pydevd-pycharm/
[debug configuration]: ./_img/2017-12-13-IntelliJ-Python-Remote-디버깅/001.png
[run debugging]: _img/2017-12-13-IntelliJ-Python-Remote-디버깅/002.png
[run client script]: ../_img/2017-12-13-IntelliJ-Python-Remote-디버깅/003.png
[pic_debugging]: /_img/2017-12-13-IntelliJ-Python-Remote-디버깅/004.png
