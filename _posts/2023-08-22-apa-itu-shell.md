---
title: 블로그 시작
date: 2023-08-22 11:58:47 
tags: 
description:
image: 
published: true
---


github blog 를 드디어 개설했다<br>
만드는게 이렇게 어려울줄은 몰랐다<br>
구글링하면서 따라했는데 몇시간동안 헤매다 이틀차에 겨우 성공..<br>
ruby git jekyll 모시깽이니 이해할 수 없지만 일단 따라했다<br>
아무튼 작성법도 배우면서 천천히 따라가봐야겠다<br>
개설방법은 다음과 같다<br>
<hr/>


## 1. New Repository
Github 에서 새로운 Repository 를 생성하고
name을 username.github.io 형식으로 생성한다
<br><br>


## 2. Clone
터미널 창을 열어 github에서 복사한 주소를 입력한다
 ```
 git clone 주소
 ```
 <br><br>


## 3. Jekyll install

Jekyll 이용하여 테마를 꾸밀 수 있다<br>
원하는 테마를 여러 사이트를 통해 다운받을 수 있다<br>
```
gem install jekyll bundler
```
터미널창에 입력 시 아마 안될거다<br>
루비라는 것을 또 깔아 줘야한다<br>
여기서 어찌저찌 구글링하다 성공

지정경로에다가 다음 명령어 입력
```
jekyll new ./
```

테마를 다운받은 zip파일을 압축을 풀어서 지정경로에 폴더에 복사한다

```
bundle install
```
<br><br>

## 4. Local server open
터미널 창에 다음 명령어를 입력
```
bundle exec jekyll serve
```
127.0.0.1:4000 을 브라우저에 입력
<br><br>

## 5. Git push
원격에 push
```
git add .
git commit -m "커밋 메세지"
git push
```
<br><br>

마크다운문법도 알아보면서 작성하려니 마냥 쉽지만은 않다<br>
그래도 나름 재미를 붙이는 중이다<br>
이제 페이지 수정도 해봐야하는데 천천히 들여다 봐야겠다<br>

