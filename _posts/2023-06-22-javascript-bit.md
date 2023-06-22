---
layout: single
title: 자바스크립트 비트 연산자
subtitle: 무심코 썼던 것들을 다시 익혀보자!
tags: [자바스크립트]
toc : false
categories: Javascript
author_profile: false
sidebar:
    nav: "docs"
sitemap: true
toc: true
header:
  teaser: https://www.biteinteractive.com/wp-content/uploads/2021/05/git-vs-github.png

---

<br/>
<br/>


<p align="center"  style="color:#8E99AB; font-size :18px">안녕하세요! 도도히 입니다! <br/>회사에서 필터 기능을 만들때마다 아주 자주 다뤘던 연산자인데<br/>
제대로 익히지 않고 쓰다보니, 오랜만에 보니까 누가 물어봤을때 "어..? 뭐더라" 해버렸습니다.<br/>
찾아보니, 자바스크립트에서 꽤나 중요한 부분이라 이건 블로그감이다! 하고 블로그를 쓰러 찾아왔습니다.</p>


<br/>

***

<br/>


# Git 이란?

명령어를 살펴보기 전, 먼저 git 에 대해서 다시 숙지를 해보자!

> 형상 관리 도구 (Configuration Management Tool) 중 하나.<br/>쉬운 말로 버전 관리 시스템 중 하나이다.

Git은 소프트웨어를 개발하는 기업의 핵심 자산인 소스코드를 효과적으로 관리할 수 있게 해주는 무료, 공개 소프트웨어이다.


## 특징

### 1. Distributed development
* 전체 개발 이력을 각 개발자의 로컬환경에 복사본을 제공, 변경된 이력을 다시 하나의 저장소로 복사.
* 이러한 변경은 추가 개발지점을 가져와, 로컬 개발 지점과 동일하게 병합 가능.
* 저장소는 git protocol 및 http로 쉽고 효율적으로 접근 가능.

### 2. Strong support for non-linear development

* 신속하고 편리한 branch , merge 지원
* 비선형(여러갈래) 개발 이력을 시각화하고 탐색 할 수 있는 강력한 도구 제공.


### 3. Efficient handling of large projects

* 매우 빠르고, 대형 프로젝트나 이력이 많은 작업에 매우 합리적.
* 일부 작업에선 더 빠르며, 다른 버전 관리 시스템보다 빠르게 요청 가능.


### 4. Cryptographic authentication of history

* git의 이력은 성공한 개발이력의 commit에 의해 저장.
* 배포 후엔, 예전 버전으로 변경하는 것은 불가능.
* 예전 버전을 암호화 가능.

### 5. Toolkit design

* GIT은 C로 작성된 많은 소규모 도구 모음.
* 많은 스크립트들이 기능 보강을 제공. 
* Git은 새로운 기발한 작업을 위한 손쉬운 사용과 쉬운 스크립팅을 위한 도구를 제공.
  

## 장점

* 같은 파일을 여러 명이 동시에 작업하는 병렬 개발 가능.
* 브랜치를 통해 개발 후, 본 프로젝트에 합치는 방식(Merge)의 개발 가능.
* 분산 버전관리이기 때문에 인터넷이 연결되지 않은 곳에서도 개발 가능.
* 중앙 저장소가 날라가도 원상복구가 가능.
* 팀 프로젝트가 아닌, 개인 프로젝트여도 git을 통해 버전을 관리하면 체계적인 개발 가능.
* 프로그램 패치, 배포하는 과정도 간단하게 개발 가능.

<br/>

# 🤷🏻‍♀️ Git Github 차이

> - Git : 형상 관리 도구(버전 관리 시스템)<br/> 
- Github : 형상 관리 도구(버전 관리) 웹호스팅 서비스

Git은 프로젝트를 진행하면서, 소스코드들의 변경 정보를 관리할때 사용한다고 이해하면 쉽다.
Github은 그 소스코드의 변경 정보를 관리할 저장소(서버)를 제공해준다고 이해하면 쉽다.

Github은 버전 관리 시스템을 지원하는 웹 호스팅 서비스의 기능을 통해,<br/>
`push` , `pull request` 이벤트에 반응하여 자동으로 작업(배포 등)을 실행할 수 있다. 

ex) GitHub, GitLab, BitBucket

<br/>

## 💡 Git 사용시 필수 용어

### Repository
> 저장소를 의미. 저장소는 히스토리, 태그, 소스, branch에 따라 버전을 저장한다.

저장소를 통해 작업자가 변경한 모든 히스토리를 확인 할 수 있다.

### Working Tree
> 저장소를 어느 한 시점을 바라보는 작업자의 현재 시점.


### Staging Area
> 저장소에 커밋하기 전에 커밋을 준비하는 위치.

### Commit
> 현재 변경된 작업 상태를 점검. 저장소에 저장하는 작업

### Head
> 현재 작업중인 Branch를 가르킴.

### Branch
> 가지 또는 분기점을 의미.

작업 할때는 현재 상태를 복사하여, Branch애서 작업을 한 후 완전하다 싶을 때 Merge를 하여 작업을 한다.

### Merge
> 다른 Branch의 내용을 현재 Branch로 가져와 합치는 작업

### 😋 Real 간단 요약
A와 B가 같은 프로젝트를 작업할때<br/>
master / main 이 프로젝트의 기준점.<br/>
master 나 main 에서 각 A 와 B 의 분기점(branch) 를 생성해줌.<br/>
작업이 완료 된 브랜치는, master에 "내 코드 합쳐줘" 라는 merge 작업 진행.


<br/>

# 👀 Git 명령어 살펴보기

### git init

> git을 다루고 싶은 폴더에서 git을 셋팅을 하는 준비를 한다.

### git clone `복사한 레포 주소`

> 원격 레포지토리의 저장소를 로컬 컴퓨터로 복제한다.

### git add .

> 모든 파일이나, 변경 내용을 스테이징 영역(작업중인 영역)에 추가한다.

### git commit `저장 내용`

> 스테이징 영역(작업중인 영역)의 추가된 파일을 저장시킨다.

### git push origin `내 브랜치 명 or master`

> 로컬에 커밋된 내용들을 repository로 올린다.

### git pull origin `내 브랜치 명 or master`

> repository에 올라가져 있는 내용들을 로컬로 가져온다.

### git branch `내가 만들 브랜치명`

> head 기준으로 branch 를 생성한다.

* git branch -m `현재 브랜치명` `바꿀 브랜치명` : 브랜치 이름 바꾸기
* git branch -D `브랜치명` : 브랜치 삭제

### git checkout `이동할 브랜치명`

> 다른 브랜치로 이동한다.

* git checkout -b `브랜치명` : 브랜치 생성 후 생성한 브랜치로 이동

### git merge `합칠 브랜치 명 or master`

> HEAD 브랜치에 합칠 브랜치 or master 내용을 병합한다.

### git status

> 현재 Git 프로젝트의 명령어를 확인합니다.

현재 master 브랜치로 체크아웃 되어 있으며, 커밋 내역이 없다는 내용입니다.

### git log

> commit 히스토리를 표시한다.

### git remote add origin `복사한 레포 주소`

> 로컬로 작업한 프로젝트를 repository에 연결하여 관리합니다. 

repository를 먼저 만들어놓지 않고 로컬환경에서 프로젝트를 만들어 작업한 경우에 사용된다.
만들어놓은 프로젝트 있다면
깃헙에서 프로젝트를 저장할 repository 를 생성해준다.
로컬에 만들어놓은 프로젝트 폴더에서 터미널을 켜고
git init으로 깃 셋팅을 시작한다.
git remote add origin `레포 주소` 로 내 프로젝트와 레포지토리를 이어준다.

### git reset --hard `커밋 id` 

> 특정 commit 시점으로 되돌리기

이미 conflict 해결하고 Push 까지 한 상황인데 실행했더니
confilct 해결을 잘못해서, 화면이 켜지지 않는다 or 에러가 말도안되게 날 경우에
다시 conflict 해결하기 전 시점으로 돌아가서 다시 conflict을 해결하는 편이엇다.

### git merge --abort

> merge 취소하기

merge 후 conflict이 나버리면, 해결 전엔 이탈하지 못한다....😣
그래서 conflict이 난 후, 커밋을 하기 전 상태라면, 해당 명령어로 머지 시작 전으로 돌아가버린다.


<br/>
<br/>


*** 


> [참고자료](https://goddaehee.tistory.com/91)
<p align="center"  style="color:#8E99AB; font-size :18px">




블로그까지 찾아와주신 분들에게 도움이 되었음 좋겠습니다!🙇‍♀️ </p>



<br/><br/>
