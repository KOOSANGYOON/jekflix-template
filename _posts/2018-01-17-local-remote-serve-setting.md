---
layout: post
title: 반복주기 학습
date: 2018-01-17T17:32:40.000Z
image: 'https://github.com/KOOSANGYOON/TIL/blob/master/TIL201801/web.png?raw=true'
description: TIL (local & remote 환경 세팅 / AWS 서버 학습)
category: TIL
tags:
  - TIL
  - CODING
  - AWS
  - JAVA
twitter_text: 반복주기 학습 (local & remote 환경 세팅 / AWS 서버 학습)
introduction: 반복주기 학습 (local & remote 환경 세팅 / AWS 서버 학습)
---

# (2018.01.17)

## TIL

## 1. 반복주기 학습 (local & remote 개발)
### 1-1) 학습 방향과 학습 방법
### 1-2) 로컬 개발 환경 세팅
  - 1-2-1) 설치 및 설정
  - 1-2-2) server 실행 방법
  - 1-2-3) html 파일 추가

### 1-3) 원격 서버에 적용하기 (AWS)
  - 1-3-1) AWS 서버 생성하기
  - 1-3-2) 서버 접속하기

---
## 1. 반복주기 학습 (local & remote 개발)

### 1-1) 학습 방향과 학습 방법

로컬 개발 환경을 세팅하고, 간단한 HTML을 개발한 후, GitHub을 통해 원격 서버에
소스 코드를 배포하는 전체 과정에 대해 학습했다. POBI(박재성 님) 의 youtube 동영상을
시청하면서 그대로 따라해보는 식의 방법으로 학습했다.

---
### 1-2) 로컬 개발 환경 세팅

#### 1-2-1) 설치 및 설정

- 설치 과정
1) `STS` 를 설치한다.

2) `JDK` 를 설치한다.

3) STS 실행 후, `Spring Starter Project` 생성
> (command + n) -> `Spring Starter Project` 생성

- 설정 과정

1) setting 값 설정
 - Name : "원하는 project 이름"
 - Type : Maven
 - Packaging : Jar
 - Group : "원하는 domain"

2) Dependencies 설정
 - `web`, `mustache`, `devtools` 추가

---
#### 1-2-2) server 실행 방법

좌측 하단의 `boot Dashboard` 에서 원하는 project 의 서버를 실행시킨다.

-> (Start or restart the process associated with the select element) 버튼 클릭

-> http://localhost:8080 을 확인해보면 서버가 시작되어있다.

---
#### 1-2-3) html 파일 추가

Spring boot 프로젝트는 default 로 `src/main/resources` 디렉토리 아래에 `static` 에 html 파일을 생성해 놓으면 브라우저를 통해 접근할 수 있다.

- `static` 아래에 새로운 html 파일 생성
 > index.html 로 생성한다.

- \<body> ... \</body> 사이에 내용을 적고, (예를들어 Hello, World!) http:localhost:8080/index.html 에서 확인 가능.
#### -> 하지만, 매번 수정시마다 refresh 해줘야 하는 불편함이 있다.
> 이를 해결하는 방안으로는 chrome extension을 설치하는 방법이 있다.

- "live reload" 를 검색하여 chrome 웹스토어에서 `chrome 에 추가` 를 선택한다.
> 정상적으로 추가가 되었다면, 주소창 옆에 `Enable LiveReload 버튼` 이 생성된다.

- 설치 후에는, 본인이 refresh 하길 원하는 주소로 이동후에 `Enable ~` 버튼을 클릭한다.
> 클릭 후에 버튼 위에 마우스를 대면, "LiveReload connected" 라고 뜬다.

- 활성화 되어있는 상태에서, STS 내의 코드를 수정하고, 저장을 하는 순간 chrome창에 변경된 내용이 게시된다.

> LiveReload 기능은 처음에 Dependencies에 추가했던 devtools 와 연동되는 기능이다.

---
### 1-3) 원격 서버에 적용하기 (AWS)

#### 1-3-1) AWS 서버 생성하기

- aws 홈페이지 접속한다.

- EC2 서비스를 선택하고, 자신의 계정으로 login 한다.

- instances 를 선택하고, start instances 를 선택한다.

- 서버를 선택한다. (주로 Ubuntu 사용)

- `instances 세부정보 구성` 에서, instances 를 세팅한다. (주로 default)

- `스토리지 추가` 와 `태그 추가` 를 지나 `보안 그룹 구성` 으로 이동
 - Type 에서 `HTML` 추가.
 > default 로 80포트가 열리게 되어있다. 특정 다른 포트를 사용하고 싶다면, Type에서 Custom TCP Rule 추가 후, 원하는 포트를 연다.

- `검토 및 시작` 클릭 -> 지금까지 작성한 세팅을 확인할 수 있다. -> `시작` 클릭

---
#### 1-3-2) 서버 접속하기

서버 시작 후에 인스턴스를 확인해보면, 내가 만든 서버가 실행중임을 알 수 있다.
내 서버의 우측을 살펴보면, `퍼블릭 DNS` 와 `IPv4 퍼블릭 IP` 를 확인할 수 있다.
두가지를 통해 모두 서버에 접속이 가능하지만, IP를 이용한 접속 방법만 적어보자면,

터미널에서 나의 접속 key가 위치한 디렉토리로 이동 후, 명령어를 입력한다. 명령어는 아래와 같다.
> ssh -i "내 키파일 이름" ubuntu@"내 퍼블릭 IP 주소 (copy/paste 이용)"

> ex) ssh -i developerkey.pem ubuntu@112.223.111.001

 (추가 정보) 한글 버젼으로 세팅하는 명령어
 > sudo locale-gen ko_KR.UTF-8