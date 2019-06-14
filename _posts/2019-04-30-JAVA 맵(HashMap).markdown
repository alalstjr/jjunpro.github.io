---
layout:     post
title:      JAVA 맵(HashMap)
author:     쭌프로
tags:       JAVA
subtitle:   JAVA 맵(HashMap) 정리노트
category:   JAVA
---

<!-- Start Writing Below in Markdown -->

![Description](https://alalstjr.github.io/jjunpro.github.io/img/java_bg.png)

# 맵(HashMap)의 사용 방법

1. 해싱(hashing)기법을 사용해서 데이터를 저장하기 때문에 <b>많은 양의 데이터</b>를 검색할 때 성능이 뛰어납니다.

2. 데이터를 <b>Key와 Value</b> 구조로 저장
  - Key 컬렉션 내의 키(Key) 중에서 유일해야 한다.
  - Value 키(Key)와 달리 데이터의 중복을 허용한다.
  
3. 자료 추가
  - 맵.put(key, value)

4. 자료 조회
  - 맵.get(key)
  
5. 코드
  - HashMap<String, Object> map = new HashMap<String, Object>();
  
## 맵(HashMap) 사용 예제

<script src="https://gist.github.com/alalstjr/2eb79baaf9d9f811dcc1813a189da76e.js"></script>

<p>
  System.out.println(map); <br/>
  결과값 {미국=워싱턴, 일본=동경, 영국=런던, 중국=북경, 한국=서울} 결과가 순서대로가 아닙니다. <br/>
  HashMap은 빠르게 찾는것이 목적만을 가지고 있기때문에 순서대로 출력하지 않습니다. <br/>
  순서대로 출력을 원한다면 ArrayList 를 사용해야 합니다.
</p>

