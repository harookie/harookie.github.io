---
layout: post
title: ubuntu Desktop launcher(.desktop)
categories: ubuntu
---

Ubuntu에서 파일 

[Desktop 파일 메뉴 스펙]

[Desktop 파일 스펙]을 참조한다.

파일의 위치는 
`~/.local/share/applications`
`/usr/share/applications/`


```
[Desktop Entry]
Encoding=UTF-8
Version=1.0
Type=Application
Terminal=false
Exec=/home/harookie/local/idea-IU-191.7479.19/bin/idea.sh
Name=idea
Icon=/home/harookie/local/idea-IU-191.7479.19/bin/idea.png
Categories=Programming
```

[Desktop 파일 스펙]: https://developer.gnome.org/desktop-entry-spec/
[Desktop 파일 메뉴 스펙]: https://www.freedesktop.org/wiki/Specifications/menu-spec/
