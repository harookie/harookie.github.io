windows에서 youtube_dl을 이용해 mp3 다운로드
------------------------------------------

1. ffmpeg 설치, 설치 방법은 [여기][ffmpeg_설치] 참조
1. 아나콘다 설치, 설치 방법은 [여기][아나콘다_설치] 참조
1. 아나콘다 pip로 youtube_dl 설치
    - `pip install youtube_dl`
1. 다운로드!! 예제
    ```
    youtube-dl.exe -x --audio-format mp3 -o "카더가든 - 우리의 밤을 외워요.%(ext)s" https://www.youtube.com/watch?v=iBx1mWMbgN8
    ```

[ffmpeg_설치]: ./2021-09-07-windows_ffmpeg_설치
[아나콘다_설치]: ./2021-03-09-anaconda_설치