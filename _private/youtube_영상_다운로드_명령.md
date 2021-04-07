[string]$singer= "영탁"
[string]$song= "부산에 가면"
[string]$url= "https://www.youtube.com/watch?v=JPDetAiAFZ8"
[string]$dest= "C:\Users\haroo\Desktop\mp3"
[string]$filepath= "$dest\$singer - $song.%(ext)s"
youtube-dl.exe -x --audio-format mp3 -o $filepath $url
