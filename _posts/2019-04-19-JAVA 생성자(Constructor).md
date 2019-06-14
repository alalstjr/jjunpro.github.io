---
layout:     post
title:      JAVA 생성자(Constructor)
author:     쭌프로
tags: 		  JAVA
subtitle:   생성자(Constructor) 정리
category:   JAVA
---
<!-- Start Writing Below in Markdown -->

![Description](https://alalstjr.github.io/jjunpro.github.io/img/java_bg.png)

# 생성자(Constructor)의 특징

클래스 이름과 같은 method 이며 리턴타입이 없습니다.
인스턴스(new)가 생성되는 시점에 단 한번 자동호출 되며 
개발자가 직접 호출할 수 없습니다.
생성자를 선언해 주지않으면 캄퍼일러에서 자동으로
기본생성자를 선언해 줍니다.
(컴퓨터한테 시키지말고 직접 쓰도록 하자..)

객체의 초기화 작업을 처리하는 역활을 합니다.

# this 와 this() 

1. this
- this 객체 자신을 가리키는 참조변수(객체의 시작 주소를 가리킴)
- 멤버변수와 지역변수의 이름이 같은 경우 구별하기 위해 사용

2. this()
- 생성자가 여러개일때 다른 생성자를 호출할때 사용
- this() 코드는 생성자에서 철번째 라인에 작성해야 한다.

<script src="https://gist.github.com/alalstjr/729bedddc63941344a31fbb0d8fbe34b.js"></script>

# 싱글톤 패턴 (Singleton Pattern)

애플리케이션이 시작될 때 어떤 클래스가 최초 한번만 메모리를 할당하고(Static) 그 메모리에 인스턴스를 만들어 사용하는 디자인패턴.

출처: https://jeong-pro.tistory.com/86 [기본기를 쌓는 정아마추어 코딩블로그]
