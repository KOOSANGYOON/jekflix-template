---
layout: post
title: 첫 웹 프로젝트 구현 (사용자 등록, 목록 확인)
date: 2018-01-22T18:24:20.000Z
image: 'https://github.com/KOOSANGYOON/TIL/blob/master/TIL201801/login.jpg?raw=true'
description: TIL
category: TIL
tags:
  - TIL
  - CODING
  - WEB
  - MUSTACHE
  - JAVA
twitter_text: 첫 웹 프로젝트 구현 (사용자 등록, 목록 확인)
introduction: 첫 웹 프로젝트 구현 (사용자 등록, 목록 확인)
---

# (2018.01.22 ~ 2018.01.23)

## TIL

## 1. DB 없이 회원가입, 사용자 목록조회 기능 구현해보기
### 1-1) 학습 방향과 학습 방법
### 1-2) MVC 간단 설명 및 mustache 초간단 학습
### 1-3) 회원가입 기능 구현

## 2. DB를 사용해 데이터 저장하기 (반복주기 3-1)
### 2-1) 데이터베이스 설정
### 2-2) User 클래스 DB 테이블에 mapping
### 2-3) Controller 에서 repository 사용
### 2-4) 실습
---
### 1-1) 학습 방향과 학습 방법

ㄱ) POBI(박재성 님)의 YOUTUBE 동영상을 보며 직접 따라해보기.

ㄴ) 리눅스 명령어 반복숙달

ㄷ) 서버 시작 및 종료 반복숙달

---
### 1-2) MVC 간단 설명 및 mustache 초간단 학습

1) 새로운 package 생성 및 내부에 class 생성. -> controller로 만들 예정.
- 컴파일러는 이 클래스가 컨트롤러인지 알 수 없다. 따라서 어노테이션을 달아주어야 한다.
> @Controller

- 이후에 command + shift + m 단축키로 import 한다. 이로써 컨트롤러 클래스로써의
역할 부여가 끝난다.

2) 이제 컨트롤러 클래스 안에 메서드를 만들어보자.

```java
package net.slipp.web;

import org.springframework.stereotype.Controller;

@Controller
public class WelcomeController {
	public String welcome() {
		return "welcome";
	}
}
```

이후에 static -> templates 안에 html 파일을 만들어준다. 이름은 welcome.html로 한다.

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Welcome</title>
</head>
<body>
Hello, World!
</body>
</html>
```

이렇게 만들어 준 뒤, 컨트롤러에 어떤 방식으로 저 html 파일을 띄워줄지에 대한 어노테이션을
달아준다.

```java
package net.slipp.web;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class WelcomeController {
	@GetMapping("/helloworld")
	public String welcome() {
		return "welcome";
	}
}
```
> @GetMapping 어노테이션을 달면 자동으로 GetMapping 이 import 된다.

컨트롤러에서 "welcome" 는 단순히 그 단어(String)가 아닌, welcome.html 을
리턴해준다는 의미로 변경된다. (뒤의 파일 형식까지 적어줄 필요 없다.)

이후 html 문서를 수정하여 출력되는 화면을 변경해주면 된다.
이 때, Model에 정보들을 담아서 출력해주는 방식은,

```java
package net.slipp.web;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class WelcomeController {
	@GetMapping("/helloworld")
	public String welcome(String name, int age, Model model) {
		System.out.println("name : " + name + ", age : " + age);
		model.addAttribute("name", name);
		model.addAttribute("age", age);
		return "welcome";
	}
}
```

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Welcome</title>
</head>
<body>
{{name}}, Hello, World!</br>
you are {{age}} years old.
</body>
</html>
```

와 같은식으로 구현하면 된다.

---
### 1-3) 회원가입 기능 구현

server로 data를 전달할 때에 html 문서 내에서 <\form> 태그를 사용한다.
<\form> 태그 안에는 action 속성을 부여할 수 있다. action 속성은 server에 요청을
보낼 때, 어떤 url 주소로 보낼건지에 대한 속성이다. 이는 아래와 같이 사용 가능하다.
> <\form action="/testpage">

---
### 2-1) 데이터베이스 설정

---
### 2-2) User 클래스 DB 테이블에 mapping

---
### 2-3) Controller 에서 repository 사용

---
### 2-4) 실습