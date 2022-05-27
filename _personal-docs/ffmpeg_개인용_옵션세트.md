### 추가할 내용
- 사운드파일에 앨범이미지 삽입하기
  - 참고 링크 : `https://www.wrapuppro.com/programing/view/9dHUHYC3FXbQp1b`
  - 예제 : `​ffmpeg -i input.mp3 -i album.jpg -map 0:0 -map 1:0 -c copy -id3v2_version 3 -metadata:s:v title="Album cover" -metadata:s:v comment="Cover (Front)" output.mp3`



### 주요 옵션 리스트
- `-i` : 입력 파일명
- `-c` : 코덱
  - copy : 스트림 단순 합치기
  - libx265, libx264 : x265이 용량이 절반임.
- `-s` : 사이즈 변환(W x H)
- `movflags +faststart` : 메타 정보가 든 moov atom을 파일 첫부분으로 옮겨서 빠르게 재생할 수 있도록 만들어 주는 옵션


### 영상 합치기
```shell
$ # 영상 합치기 1, 사이즈/코덱등이 모두 동일할때 가능
$ ffmpeg -hide_banner -i "concat:in1.mp4|in2.mp4" -c copy "out.mp4"
$ # 영상 합치기 2, 1방법이 안될때 사용
$ # fl.txt내에 아래 내용이 들어가야함.
$ # file 'in1.mp4'
$ # file 'in2.mp4'
$ ffmpeg -hide_banner -f concat -safe 0 -i fl.txt "out.mp4"
```



```shell
$ # 코덱 변경 예제 1
$ FILE_NAME="in.avi"
$ time ffmpeg -i $FILE_NAME -vcodec libx265 output/${FILE_NAME:0:(-4)}.mp4
$ # 코덱 변경 예제 1
$ ffmpeg -i "in.mp4" -vcodec libx265 "out.mp4"
```
> 참조 : https://www.nuridol.net/command/ffmpeg


---

### 참고 명령

```shell
$ # 사용 가능한 코덱 목록 확인
$ ffmpeg -encoders
```

```bash
$ # 영상 정보 조회 => 코덱, 사이즈, 길이등
$ ffprobe in.mp4 2>&1 | grep Video
```

---

### 이미지 합치기
```shell
$ # 가로로 붙이기
$ montage -mode concatenate cover-*.jpg out.jpg
$ # 세로 컬럼수 지정 (예제의 "1x" => 1라인)
$ montage -mode concatenate -tile 1x cover-*.jpg out.jpg
```

---

## ffmpeg 설치
### Mac
```zsh
% brew install ffmpeg, vcs, imagemagick, youtube_dl
```
### Windows

https://ffmpeg.org 에서 컴파일된 버전을 다운로드 받은뒤 PATH를 설정하고 사용한다.


$ ffmpeg -i "concat:in1.mp4|in2.mp4" -codec libx264 "out.mp4"


time ffmpeg -i "output.mp4" -codec libx264 "libx264.mp4"
time ffmpeg -i "output.mp4" -codec libx265 "libx265.mp4"
ffmpeg -i "output.mp4" -codec libx265 "libx265.mp4"
libx264
libx265


김경호
다신
k2





time ffmpeg -i in.mp4 -vcodec libx265 out.mp4 > stdout.txt 2> stderr.txt
time ffmpeg -i in.mp4 -vcodec mpeg4 out.mp4 > stdout.txt 2> stderr.txt


ffmpeg -i Anal\ Intensive\ 08.ISO -t 5 -vcodec libx265 "in.mp4"





Video Contact Sheet
http://outlyer.net/etiq/projects/vcs/



```shell
# save and change IFS
OLDIFS=$IFS
IFS=$'\n'
FFMPEG_OPTS="-vcodec libx265 -movflags +faststart -preset:v veryfast -crf 22 -hide_banner -loglevel info"

mkdir -p output
mkdir -p screenshots
 
# read all file name into an array
fileArray=($(ls -1 *.mp4))
 
# restore it
IFS=$OLDIFS
 
# get length of an array
tLen=${#fileArray[@]}
 
# use for loop read all filenames
for (( i=0; i<${tLen}; i++ ));
do
  FULL_FILE_NAME="${fileArray[$i+1]}"
  FILE_NAME=${FULL_FILE_NAME:0:(-4)}
  # change codec
  time ffmpeg -i $FULL_FILE_NAME $FFMPEG_OPTS output/$FILE_NAME.mp4
  # make screenshots
  vcs -c 7 -n 35 --height=50% --anonymous output/$FILE_NAME.mp4 -o screenshots/$FILE_NAME
done
```


2
7
8
12


evili angel
joey silvera

Jasmine Rouge

Patricia Diamond
Vanda Vitus
Karli Sweet
Rita Cardinale
Carol Sampaio

Arschgefickt und Abgerotzt 16

Euro girls love big black cocks #23

The Beat Down 6121:06
The Beat Down


Claudia Atkins
Karlie Sweet
Illana Moore

Arschgefickt und Abgerotzt




FILE_NAME="Anal Intensive 01.mp4"
ffprobe -i $FILE_NAME -hide_banner -loglevel info 




$ zsh ./test.sh 2> time.txt

mkdir -p output
mkdir -p 

FILE_NAME="Please 05.avi"
time ffmpeg -i $FILE_NAME -vcodec libx265 -movflags +faststart -preset:v veryfast -crf 22 -hide_banner -loglevel info output/${FILE_NAME:0:(-4)}.mp4


FFMPEG_OPTS="-hide_banner -loglevel info"

ffmpeg -hide_banner -i "2.mp4" -s 624x480 "2_conv.mp4"
ffmpeg -hide_banner -f concat -i fl.txt "Please 01_copy.mp4"
ffmpeg -hide_banner -i "concat:4.mp4|5.mp4" -c copy "Please 01_copy.mp4"
ffmpeg -hide_banner -i "Please 01_copy.mp4" -vcodec libx265 -movflags +faststart -preset:v veryfast -crf 22  "Please 01.mp4"


ffmpeg -hide_banner -f concat -i fl.txt "Please 01_copy.mp4"
ffmpeg -hide_banner -f concat -vcodec libx265 -movflags +faststart -preset:v veryfast -crf 22 -i fl.txt "Please 01_copy.mp4"

ffprobe -hide_banner -loglevel info "Please 01_copy.mp4" 2>&1 | grep "Video"
ffprobe -hide_banner -loglevel info 2.mp4 2>&1 | grep "Video"
ffprobe -hide_banner -loglevel info 3.mp4 2>&1 | grep "Video"
ffprobe -hide_banner -loglevel info 4.mp4 2>&1 | grep "Video"
ffprobe -hide_banner -loglevel info 5.mp4 2>&1 | grep "Video"


file '1.mp4'
file '2.mp4'
file '3.mp4'
file '4.mp4'
file '5.mp4'






FILE_NAME="Please 04.wmv"
time ffmpeg -i $FILE_NAME -vcodec libx265 -movflags +faststart -preset:v veryfast -crf 22 -hide_banner -loglevel info output/${FILE_NAME:0:(-4)}.mp4
FILE_NAME="Please 09.wmv"
time ffmpeg -i $FILE_NAME -vcodec libx265 -movflags +faststart -preset:v veryfast -crf 22 -hide_banner -loglevel info output/${FILE_NAME:0:(-4)}.mp4
FILE_NAME="Please 10.wmv"
time ffmpeg -i $FILE_NAME -vcodec libx265 -movflags +faststart -preset:v veryfast -crf 22 -hide_banner -loglevel info output/${FILE_NAME:0:(-4)}.mp4