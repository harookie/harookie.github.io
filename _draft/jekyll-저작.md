---
layout: post
title: Jekyll Linux 세팅
---

### 

### 1. 필수 패키지 설치

```bash
sudo apt install build-essential dh-autoreconf -y
sudo apt install gcc libffi6 libffi-dev -y
```

#### 2. jekyll 설치  
ruby등을 설치전 필요한 기본 패키지들을 설치 해준다.  
workspace는 git 프로젝트들을 모아놓을 디렉토리다.  
이름을 변경해도 무관하고, 생성하지 않아도 상관없다.
```bash
sudo apt install ruby-full -y
sudo gem update --system
sudo gem install jekyll bundler
cd ~ ; mkdir workspace ; cd ~/workspace
```

#### 3-1. 신규 프로젝트로 생성
```bash
$ jekyll new harookie.github.io
$ cd harookie.github.io
$ git init
$ git remote add origin https://github.com/harookie/harookie.github.io.git
$ git add .
$ git commit -m "first commit"
```

#### 3-2. github 프로젝트 clone
```bash
$ git clone https://github.com/harookie/harookie.github.io
$ cd harookie.github.io
$ jekyll new harookie.github.io
```

#### 4. jekyll 서버 시작
```bash
$ bundle exec jekyll server --host 192.168.0.2 --port 80 --watch
$ bundle exec jekyll serve --host harookie.iptime.org --watch
$ jekyll serve --host 192.168.0.2 --watch
```

#### 기타
[설치참조 페이지](https://github.com/jekyll/jekyll/blob/master/docs/_docs/installation.md)
