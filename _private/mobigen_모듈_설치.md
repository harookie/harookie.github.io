mobigen 모듈 설치
---------------

- vdi내 파일 받아서
- 모비젠 파일 서버에 올리기

```
1. Mobigen Server Setup 
ID : mobigen
PW : mobigen.
  => svn export svn://svn.mobigen.com/MobigenServerSetup/trunk MobigenServerSetup  

위에 서버에 접속이 안될시 SKT 내부서버에 PORT 포워딩서버로 실행
  => svn export svn://150.23.15.96:58080/MobigenServerSetup/trunk MobigenServerSetup


2. SF 모듈 설치
ID : mobigen
PW : mobigen.

$HOME/bin/sf_checkout.sh 
1번과 마찬가지로 접속이 안될시 SKT 내부서버에 PORT 포워딩서버로 스크립트 수정후 실행

#svn co svn://svn.mobigen.com/SFI_pyc/trunk/Mobigen $HOME/mlib/Mobigen
svn co svn://150.23.15.96:58080/SFI_pyc/trunk/Mobigen $HOME/mlib/Mobigen


3. 프로젝트 폴더 생성
$HOME/bin/init_project.sh 프로젝트명

```


[https://github.com/mobigen/MSF_V2]


[WoodmanCastingX.com
[DPFanatics.com 
	SINematica.com
FantASStic DP