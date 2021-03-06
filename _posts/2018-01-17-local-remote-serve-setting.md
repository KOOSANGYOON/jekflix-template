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

# (2018.01.17 ~ 2018.01.18)

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

---
#### 1-3-3) 서버에 자바 소스코드 배포

먼저, 서버에 접속한다. (1-3-2 참고)

우리는 command 상에서 자바를 다운로드 받아야 한다. 하지만 command 에서는 브라우져를
이용할 수 없다. 따라서 command 로만 다운로드를 받아야 한다. 이를 위해서 `wget` 이라는
명령어를 활용해서 특정 주소에 있는 프로그램을 다운로드 받을 수 있다.
사용 방법은, 브라우져에서 JDK 다운로드 주소를 확인하고, 복사해서 wget 명령어 뒤에 덧붙인다.

> ex) wget http://download.oracle.com/jdk-9.0.4_linux-x64_bin.tar.gz

하지만 제대로 다운로드가 되지 않고 일부만 다운로드 되어있다. 문제가 무엇일까?
브라우져 상에서는 '라이센스에 동의함' 에 체크를 하고 다운로드를 받지만, 터미널에서는 그것을
하지 않았기 때문이다. 이를 위한 옵션을 적어주어야 한다.
따라서 ` --header "Cookie: oraclelicense=accept-securebackup-cookie"` 옵션이 필요하다.

> ex) wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/jdk-9.0.4_linux-x64_bin.tar.gz

설치 이후, 압축을 풀기 위해서는 `tar` 명령어를 이용한다.
> ex) tar -xvf jdk-9.0.4_linux-x64_bin.tar.gz

이로써 설치는 끝이났다. 하지만 현재의 상태는 java 명령어를 사용할 수 있는 공간이 제한적이다. (다운로드 받은 jdk 디렉토리의 bin 에서 사용 가능)
따라서 jdk를 사용하고 싶을때, 사용할 때마다 jdk 디렉토리로 들어가서 작업을 해야한다.
ubuntu의 전역에서 사용하기 위해서는 어디서나 사용할 수 있도록 path 설정을 해줘야 한다.

먼저 jdk-9.0.4 와 같은 이름은 사용하기에 불편하기 때문에 별칭을 부여한다. 이는 `ln` 명령어로 부여가 가능하다.

> ex) ln -s jdk-9.0.4/ java

이렇게 해주면, 앞으로 jdk-9.0.4 디렉토리를 가고 싶을 때, cd java 로 이동할 수 있다.
이후에 홈 디렉토리로 이동하여 .bash_profile 파일을 만들어서 path 설정을 해보자.
`vi` 명령어를 이용하여 스크립트를 만들도록 한다.

> ex) vi .bash_profile

.bash_profile 의 내용으로 `PATH=$PATH:~/java/bin` 을 적고 저장/종료한다.
이후에 ubuntu 를 재시작하여야 적용이 되지만, 재시작 없이 적용시키는 `source` 명령어를
이용하여 바로 적용시킨다.

> ex) source .bash_profile

여기까지 완료되면 홈 디렉토리에서 자바 명령어를 실행해보자. (ex) java -version
> 잘 실행됨을 확인할 수 있다.

JAVA 세팅이 끝났다면, 우리가 프로젝트에서 설정한 Jar 파일들을 다운받아야 한다. 터미널에서
git repository 와 연결된 디렉토리로 가서(우리가 작업중인 프로젝트 디렉토리),
`mvnw` 파일을 실행한다.

> ./mvnw clean package 이 명령어를 사용하면 프로젝트가 빌드된다.

빌드 후에 target 디렉토리로 가보면, jar 파일이 생성되어 있다. 이 파일을 이용하여
서버를 시작할 수 있다.

> java -jar "jar파일이름"

서버가 시작됨을 확인할 수 있다. 서버를 시작한 후에는, 우리가 만들고 배포한 파일을 웹 상에서 켤 수 있도록 해주어야 한다. 우선 `curl` 명령어로 포트를 확인한다. curl = "see (발음이 C) URL"

> ex) curl http://localhost:8080

이렇게 해주면, 8080포트를 열어서 내가 만든 파일을 켜줄 수 있다. chrome 주소창 상에서 내 서버의 퍼블릭 IP 주소를 적고, 뒤에 :8080 을 붙여보자. 사이트가 켜 짐을 확인할 수 있다.

사이트를 종료하는 방법은, 다음과 같은 방식으로 가능하다. (8080말고 다른 포트를 열었다면, 그 포트 번호를 적어준다.)
> lsof -i :8080

이 명령어를 이용해서 현재 8080포트의 상태를 확인할 수 있다. 서버가 켜져 있음을 알 수 있다.
이를 종료해주려면, kill -9 "PID번호" 명령으로 종료할 수 있다.
-9 는 모든 프로세스를 종료하겠다는 옵션이다.

> ex) kill -9 1824

이렇게 프로세스를 종료한다. 이후에 서버를 종료해주는 것은 AWS의 EC2에서 인스턴스를
종료해줌으로써 가능하다.

---
