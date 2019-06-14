---
layout:     post
title:      JAVA Linked List 와 ArrayList
author:     쭌프로
tags:       JAVA
subtitle:   JAVA 자료구조 정리노트
category:   JAVA
---

<!-- Start Writing Below in Markdown -->

![Description](https://alalstjr.github.io/jjunpro.github.io/img/java_bg.png)

# Linked List 와 ArrayList

![Description](https://alalstjr.github.io/jjunpro.github.io/img/2019-05-01-1.png)

ArrayList - 순차저인 메모리 구조를 가지고 있으며 추가, 삭제 작업이 빈번할 경우 성능이 떨어집니다. <br/>
LinkedList - 비순차적인 메모리 구조를 가지고 있으며 추가, 삭제 작업이 빈번할 경우 성능이 우수합니다.

## LinkedList의 특징 및 장점

LinkedList는 몇 개의 참조자만 바꿈으로써 새로운 자료의 삽입이나 기존 자료의 삭제를 위치에 관계없이 빠른 시간안에 수행 할 수 있습니다. <br/>
LinkedList는 무한 개수의 자료를 삽입할 수 있는 반면 (메모리의 용량이 무한정하다고 가정할 때), <br/>
ArrayList는 크기가 한정되어 있기 때문에 결국 포화 상태에 이르게 됩니다. 

![Description](https://alalstjr.github.io/jjunpro.github.io/img/2019-05-01-2.png)
![Description](https://alalstjr.github.io/jjunpro.github.io/img/2019-05-01-3.png)

## LinedList의 단점

ArrayList에서는 무작위 접근(random access)이 가능하지만,  <br/>
LinkedList에서는 순차접근(sequential access) 만이 가능합니다. <br/>
LinkedList는 단방향성을 갖고 있기 때문에 <b>인덱스를 이용하여 자료를 검색</b>하는 애플리케이션에는 적합하지 않습니다.  <br/>
때문에 LinkedList 보다는 ArrayList가 훨씬 빠릅니다.

ArrayList는 자료들을 하나의 연속적인 묶음으로 묶어 자료를 저장하는 반면,  <br/>
LinkedList는 자료들을 저장 공간에 불연속적인 단위로 저장하게 됩니다.  <br/>
그렇기 때문에 LinkedList는 메모리 이곳저곳에 산재해 저장되어 있는  <br/>
노드들을 접근하는데 ArrayList보다는 긴 지연 시간이 소모됩니다

## LinedList 예제

<script src="https://gist.github.com/alalstjr/fcddbd0208a10dccd12d3331693884bf.js"></script>

## 더 자세하게 알고싶다면?

<a href="http://www.nextree.co.kr/p6506/">자료구조: Linked List 대 ArrayList</a>
