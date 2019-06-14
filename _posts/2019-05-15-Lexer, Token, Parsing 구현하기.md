---
layout:     post
title:      Lexer, Token, Parsing 구현하기
author:     쭌프로
tags:       JAVA 자료구조
subtitle:   Lexer, Token, Parsing 연습코드
category:   JAVA
---

<!-- Start Writing Below in Markdown -->

![Description](https://alalstjr.github.io/jjunpro.github.io/img/java_bg.png)

공부하면서 작성한 <b>주관적인 개인 노트</b>입니다. <br/>
내용이 정확하지 않습니다.

# Lexer, Token, Parsing 란 무엇인가?

<a href="Lexer, Token, Parsing 개념정리">Lexer, Token, Parsing 개념노트 바로가기</a>

# Lexer (어휘 분석)

어떠한 기준으로 토큰을 생성하여 저장 할 것인지 <br/>
Class Enum TokenType 를 생성하여 기준을 만들어 줍니다.

<script src="https://gist.github.com/alalstjr/ac41ff8d8c03ccade36b7504ed86052b.js"></script>

TokenType 에는 두가지 형태로 토큰을 나누었습니다.
<b>형태가 없는 토큰</b> 과 <b>형태가 있는 토큰</b>

## 형태가 없는 토큰

공백 혹은 주석 등등 토큰에 저장될 필요가없는 목록입니다.

## 형태가 있는 토큰

문자열 혹은 숫자 등등 토큰에 저장되어야 하는 목록입니다.

isAuxiliary() 메서드로 토큰의 형태를 확인합니다. <br/>
lexer 검색도중 형태가 없는 토큰이 매칭되면 true 를 반환합니다.

# Token 객체생성

<script src="https://gist.github.com/alalstjr/8ad3cd9486fac6561274e8745bb9e596.js"></script>

Token의 객체 상태(State)와 필드(field)를 작성합니다.

Token의 객체와 타입을 정의하였으니 이제 Lexer를 작성해보겠습니다.

# Class AnalyzerException 

개발자가 원하지 않는 방향으로 진행되는경우 예외처리하는 Class를 생성합니다.

<script src="https://gist.github.com/alalstjr/a70408c2a236c12b6ccb29fb04468f52.js"></script>

# Class Lexer 생성

<script src="https://gist.github.com/alalstjr/fbaa620b2d87d8a141f05c830131930a.js"></script>

입력된 Code를 분석하는 정규식데이터를 저장할 공간과 결과를 저장하는 Token List를 만들어줍니다.
각각 TreeMap, ArrayList 인스턴스합니다.

그후 launchRegEx() 메서드를 실행 함으로서 regEx 정규식 조건을 추가합니다.

tokenize 입력된 소스를 토큰화하는 메서드입니다.

입력된 소스를 regEx 정규식 검사를 하며 하나씩 토큰을 찾아 저장하도록 진행합니다.
만약 regEx 리스트에 맞지않는 정보가 있을경우 예외처리를 하여 AnalyzerException 로 넘어갑니다.

정규식비교 처리는 separateToken() 메서드에서 처리합니다. <br/>
Pattern, Matcher 를 사용하여 Token에 결과값을 저장하여 반환합니다.

결과 값은 두가지 경로에 저장이 됩니다.

하나는 모든 결과값을 저장하는 getTokens() <br/>
형태가없는 토큰은 제외한 getFilteredTokens() 

# 실행 결과

<script src="https://gist.github.com/alalstjr/a897224d959f4e4d71c0a0bb7803de25.js"></script>

모든 Token을 저장한것과 <br/>

![Description](https://alalstjr.github.io/jjunpro.github.io/img/2019/05/2019-05-16-1.png)

형태가없는 것은 제외한 Token을 각각 출력해 보았습니다.<br/>

![Description](https://alalstjr.github.io/jjunpro.github.io/img/2019/05/2019-05-16-2.png)

정상 출력되는것을 확인하였습니다.

만약 등록되지않은 TokenType 입력된경우 

![Description](https://alalstjr.github.io/jjunpro.github.io/img/2019/05/2019-05-16-3.png)

String sourceCode = "void java"; 가 입력된경우 

제가 정의한 정규식 패턴규칙은 'String' 으로 둘러싸있는 경우에만 문자열로 인식한다고 등록해 놨기때문에
예외처리되어 오류를 출력합니다.

# 참고자료

## java enum 이란?

<a href="http://woowabros.github.io/tools/2017/07/10/java-enum-uses.html">우아한 형제들 - Java Enum 활용기</a>
<a href="https://mainpower4309.tistory.com/15">[자바/JAVA 개발] 자바 Enum 클래스란??</a>

## 정규식

<a href="https://hamait.tistory.com/342">정규표현식 (Regex) 정리</a>
<a href="https://hermeslog.tistory.com/310">[정규식] Java에서의 정규식 정리</a>

- 정규식 해석기
    https://regexper.com/

- 자바 정규식 기본정리 : Matcher, Pattern, find(), group()
    https://m.blog.naver.com/bb_/220863282423

- 특정문자 포함
    https://okky.kr/article/324090
