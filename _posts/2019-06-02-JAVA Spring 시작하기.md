---
layout:     post
title:      JAVA Spring 시작하기
author:     쭌프로
tags:       JAVA
subtitle:   JAVA Spring 시작하기 공부 노트
category:   JAVA
---

<!-- Start Writing Below in Markdown -->

![Description](https://alalstjr.github.io/jjunpro.github.io/img/java_bg.png)

<a href="https://github.com/alalstjr/C-Language/tree/master/1906">Git 코드 저장소</a>

# Home.jsp의 실행 과정

서버 구동시 가장 먼저 참조하는 파일은 web.xml <br/>
웹프로젝트의 배치 기술서(deploy descriptor) 웹 프로젝트의 환경 설정 파일

## 스프링의 주요 특징

- POJO(Plain Old Java Object) 기반의 구성 : 별도의 API가 필요하지 않은 일반적인 자바 코드를 이용하여 개발 가능
- 의존성 주입(DI)을 통한 객체 간의 관계 구성
- AOP(Aspect Oriented Programming) 지원 : 반복적인 코드를 줄이고 개발자가 비즈니스 로닉에만 집중할 수 있도록 지원
- 편리한 MVC 구조
- WAS에 종속적이지 않은 개발 환경

## Ioc(Inversion of Control, 제어의 역전) - 객체에 대한 제어권

- 기존에는 개발자에게 제어권이 있었음(new 연산자)
- 객체의 제어권을 스프링에게 넘김
- 인스턴스의 라이프 사이클(생성부터 소멸까지)을 개발자가 아닌 스프링 프레임웍이 담당

## DI(Dependency Injection, 의존관계 주입)

- 객체 간의 의존성을 개발자가 설정하는 것이 아닌 스프링 컨테이너가 주입시켜 주는 기능
- 객체를 쉽게 확장하고 재사용할 수 있음

# Spring Mybatis의 연동

## 로킹툴

- 로깅툴을 사용하는 이유
  - System.out.println() 명령어는 IO 리소스를 많이 사용하여 시스템이 느려질 수 있음
  - 로그를 파일로 저장하여 분석할 필요가 있음
  
- 로깅툴의 종류
  - commons-logging : 스프링 3에서 사용하던 로깅툴
  - log4j : 효율적인 메모리 관리로 많이 사용됨
  - logback : log4j 보다 성능이 더 우수하여 최근에 많이 사용됨
  - SLF4J : logback을 사용하기 위한 인터페이스
  
