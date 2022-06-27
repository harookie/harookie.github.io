### WSL 디렉토리 탐색기에서 열기
```
$ explorer.exe .
```

### 외장디스크 마운트 하기
```
sudo mount -t drvfs D: /mnt/d
```

### WSL 디스크 사이즈 압축
WSL2가 사용하는 가상 디스크의 사이즈는 줄지 않고 증가만 한다.
불필요한 사이즈를 줄이기 위해 아래 명령을 실행한다.

```
diskpart
select vdisk file="C:\Users\haroo\AppData\Local\Packages\CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc\LocalState\ext4.vhdx"
compact vdisk
```

만약 파일이 사용중이라고 나오면 아래 명령으로 wsl을 종료후 진행

```
> wsl -l -v
  NAME                   STATE           VERSION
* Ubuntu                 Running         2

> wsl -t Ubuntu

> wsl -l -v
  NAME                   STATE           VERSION
* Ubuntu                 Running         2
```