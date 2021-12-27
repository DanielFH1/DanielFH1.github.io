---
title: "GitHub 페이지 작성에 대해"
excerpt: "방법론적인 얘기와 자잘한 팁들"

categories:
  - Blog
tags:
  - [Blog, jekyll, Github]

toc: true # Table of contents. 포스트의 헤더들만 보여주는 목차.
toc_sticky: true # 스크롤을 따라 목차 움직임

date: 2021-12-28
last_modified_at: 2021-12-28
---

# 1. 블로그 작성 방법
## 1-1. 실시간으로 코드의 변화를 보면서 작성하기
깃허브 페이지를 작성하며 불편했던 것은 내가 **Markdown**으로 작성하는 글들이 실제 블로그 페이지에서 어떻게 보일지를
실시간으로 확인하기가 어렵다는 것이다.  
**Markdown**프로그램을 이용한다 해도, 내 블로그에 직접 보이는 모습이 아닐 뿐더러,
일일이 **commit**해서 변화를 확인하는 것도 굉장히 번거로운 일이다.  

1. 이 문제는, **command**창에(Dir 위치를 깃허브 폴더 안으로 지정해준 뒤)
```
bundle exec jekyll serve
```
를 입력하면 웹사이트를 서버에 올리고 <http://127.0.0.1:4000> 이런 주소를 받게 된다.  

2. 여기서 각자 보유하고 있는 **Atom** 이나 **VS Code**같은 코드 에디터를 사용해서  
Local 컴퓨터 내의 **GitHub Page**폴더에서 작업을 하고 저장을 해준다.  
3. 그 후 <http://127.0.0.1:4000> 주소로 들어가 새로고침을 눌러주면 적용이 되어있는 모습을 볼 수 있다.  

그리고 모든 작성이 끝났다면, **command**창에
```
git add .
git commit -m "commit comment"
git push
```
를 입력해줘서 원격 저장소에 Push를 해준 뒤 마무리하면 된다.
