---
layout:     post
title:      Lexer, Token, Parsing 개념정리
author:     쭌프로
tags:       JAVA
subtitle:   Lexer, Token, Parsing 노트
category:   JAVA
---

<!-- Start Writing Below in Markdown -->

![Description](https://alalstjr.github.io/jjunpro.github.io/img/java_bg.png)

# Lexer란 무엇인가?

Lexer는 <b>lexical analysis(어휘 분석)</b> 를 합니다.<br/>
텍스트를 받아서 한 글자 한 글자 읽어나가다가 <b>의미를 가진 단어</b>를 만나면 
Lexer에서는 그 단어를 전체 텍스트로부터 <b>잘라서 Token이란 것</b>으로 만듭니다.

## Lexer 간단 예제

<script src="https://gist.github.com/alalstjr/6171f24c1cfe8cd54b364369b40dbdd4.js"></script>

이런식으로 단어를 token으로 만듦과 동시에 자신이 읽었던 문자를 잊어버리고 다시 텍스트를 읽어나갑니다.

# Token은 무엇인가?

lexer는 글자들을 모아서 단어를 만들어 Token에 담는 일을 합니다. <br/>
하지만 단순한 단어 데이터는 가공하지 않거나 그것을 구조적으로 표현하지 않으면 
다른 곳에서 쉽게 사용할 수가 없습니다. <br/>
Token은 단어를 구조적으로 표현할 수 있게 도와주는 구조체입니다.

# 참고자료

<a href="https://medium.com/teamnexters/koa%ED%8C%80-%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%A3%BC%EA%B0%84-%EB%AF%B8%EC%85%98-2-938634d86921">
  새로운 Smart Contract 프로그래밍 언어 만들기 — Lexer
</a>
<a href="https://medium.com/teamnexters/%EC%83%88%EB%A1%9C%EC%9A%B4-smart-contract-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%EC%96%B8%EC%96%B4-%EB%A7%8C%EB%93%A4%EA%B8%B0-parser-579b319926d6">
  새로운 Smart Contract 프로그래밍 언어 만들기 — Parser
</a>
