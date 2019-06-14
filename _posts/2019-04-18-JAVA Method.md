---
layout:     post
title:      JAVA Method
author:     쭌프로
tags: 		  JAVA
subtitle:   JAVA Method 정리
category:   JAVA
---
<!-- Start Writing Below in Markdown -->

![Description](https://alalstjr.github.io/jjunpro.github.io/img/java_bg.png)

# JAVA Method 정리

클래스(Class)의 구성 요소는 variable(속성) + method(동작) 으로 이루어져 있으며
variable(속성)은 객체, 요소, 또는 파일의 성질을 정의하는 명세
method(동작)은 어떠한 특정 작업을 수행하기 위한 명령문의 집합 입니다.

## method 의 사용 목적

모듈화로 인해 코드의 가독성을 높여주고 
기능의 변경이 필요할 때도 손쉽게 유지보수가 가능하며
중복되는 코드의 반복적인 프로그래밍을 피할 수 있습니다.

## method 호출(Call)의 종류

### Java 인자 전달 방식: Call-by-{Value | Reference}?

메서드나 함수의 인자 전달을 설명 할 때 항상 등장하는 단어 parameter와 argument
두 단어 모두 인자를 표현하는 단어지만 구분해서 쓰자면 formal-parameter(형식인자)와 actual-parameter(실인자)
<script src="https://gist.github.com/alalstjr/47636e903c4d69c925f236fcd2d3b9a9.js"></script>

1. 값에 의한 호출(Call By Value) - 데이터 복사(깊은 복사)
<script src="https://gist.github.com/alalstjr/a0d05b0d778d8632ab0cde49f137681c.js"></script>

2. 주소값에 의한 호출(Call By Reference) - 데이터 참조
<script src="https://gist.github.com/alalstjr/9f5bd9e56b7dcd5d02a95784adc2bc0b.js"></script>

## 가변형 매개변수

형식 매개변수와 실매개변수의 형과 개수는 항상 일치해야하지만
<script src="https://gist.github.com/alalstjr/71201d0869ca5c048b9819c8fb18cbfe.js"></script>

실 매개변수의 개수가 상황에 따라 가변적인 경우가 발생할 수 있다.

자 바 5.0에서 소개되는 기법 중에서 가변인수(Varargs)라는 것이 있다. 
가변인수라는 것은 필요에 따라 매개변수(인수)를 가변적으로 조정할 수 있는 기술이다. 
가변인수가 없던 시절에는 가변인수 대신 컬렉션이나 배열을 이용해서 가변인수를 대체하고 있었다.
<script src="https://gist.github.com/alalstjr/6589fc7f8dacb80a3f0021942d6feb50.js"></script>

## 메서드 오버로딩(method overloading)

하나의 클래스에 같은 이름의 메서드를 여러 개 정의하는 것
오버로딩의 조건
- 메서드의 이름이 같아햐 한다.
- 매개변수의 개수 또는 타입이 달라야 한다.
- 매개변수는 같고 리턴타입이 다른 경우는 오버로딩이 성립되지 않는다.
(리턴타입은 오버로딩을 구현하는데 아무런 영향을 주지 못한다.)

ex) 
public void print();
public void print(int n);
public void print(String str);
-public String print(); 에러 발생 

## 참고자료

속성의 개념 https://ko.wikipedia.org/wiki/%EC%86%8D%EC%84%B1_(%EC%BB%B4%ED%93%A8%ED%84%B0_%EA%B3%BC%ED%95%99)
메소드의 개념 http://tcpschool.com/java/java_methodConstructor_method
Java 인자 전달 방식 http://mussebio.blogspot.com/2012/05/java-call-by-valuereference.html
가변형 매개변수 https://gyrfalcon.tistory.com/entry/Java-Varargs [Minsub's Blog]
