---
layout:     post
title:      JAVA static, final 다형성
author:     쭌프로
tags: 		  JAVA
subtitle:   JAVA static, final 정리노트
category:   JAVA
---
<!-- Start Writing Below in Markdown -->

![Description](https://alalstjr.github.io/jjunpro.github.io/img/java_bg.png)

# static 

정지의 상태, 고정적인, 변화가 없는

## static member

<p>
  static variable(정적 변수) <br/>
  static method(정적 메소드) <br/>
  어디서든 공유해서 사용할 수 있는 변수, 메소드
</p>

## static member의 특징

<p>
  프로그램이 실행되면 메모리(클래스 영역)에 자동으로 로딩됨 <br/>
  프로그램이 끝날 때까지 메모리에 상주함 <br/>
  <b>static method 에서는 static member 만 사용 가능함</b>
</p>
<script src="https://gist.github.com/alalstjr/847f5a20446721d391503e6c5b1049ee.js"></script>

<p>
  단하나의 static 변수만 존재가능합니다. <br/>
  그러므로 new 를 통해서 객체를 아무라 생산해도  <br/>
  static 변수는 단 하나만 변경없이 고정으로 존재합니다.
</p>

## dynamic member의 특성

<p>
  프로그램 실행 중에 필요할 때 만들어지고 필요 없으면 삭제됨 <br/>
  stack, heap 영역에 저장됨 <br/>
  메모리 측면으로는 dynamic member 변수가 활용이 더 높다.
</p>

# final 

<p>
  final이 붙은 요소는 변경할 수 없습니다. <br/>
 <br/>
  final variable 변수 값을 변경할 수 없습니다. <br/>
  final method  오버라이딩이 금지됩니다. <br/>
  final class 상속이 금지됩니다. <br/>

  final 은 최종의 단계이기 때문에 무엇하나 변경하며 상속해줄 수 없습니다.
</p>

# 다형성(polymorphism)

<p>
  여러 가지 형태를 가질 수 있는 능력 <br/>
  하나의 참조변수로 여러 자료형의 객체를 참조할 수 있는 것 <br/>
  Object a = 10; <br/>
  Object a = 10.5; <br/>
  Object a = "문자열"; <br/>

  간단하게 예제를 확인하겠습니다.
</p>

<script src="https://gist.github.com/alalstjr/f050cbff7925d8e39933009fae19297e.js"></script>

<p>
  결과 b 객체와 a 의 객체는 각각 어떤 int a 변수의 값을 출력할까요? <br/>
<br/>
  첫번째 <br/>
  BB b = new BB(); <br/>
  b.print(); <br/>
  BB객체의 변수 내부의 a 의 값 20 을 의미합니다. <br/>
  결과는 20 입니다.  <br/>
  (super.print 를 할경우 부모 값의 print를 하는것이므로 10을 출력하게 할 수 있습니다.) <br/>
<br/>
  두번째 <br/>
  AA a = new BB(); <br/>
  a.print(); <br/>
  여기서도 그러면 AA 객체의 변수 내부의 a의 값 10 을 가져와야하지만 <br/>
  실질적으로 메모리에는 BB객체가 올라가 있기때문에  <br/>
  결과는 20을 출력합니다. 
</p>
