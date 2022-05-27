WSL2 디스크 사이즈 줄이기
===

WSL2가 사용하는 가상 디스크의 사이즈는 줄지 않고 증가만 한다.
불필요한 사이즈를 줄이기 위해 아래 명령을 실행한다.

```
diskpart
select vdisk
select vdisk file="C:\Users\haroo\AppData\Local\Packages\CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc\LocalState\ext4.vhdx"
compact vdisk
```