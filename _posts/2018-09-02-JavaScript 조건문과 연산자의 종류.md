---
layout:     post
title:      Javascript의 조건문과 연산자의 종류
author:     쭌프로
tags: 		  JavaScript
subtitle:   JavaScript 공부 노트
category:   JavaScript
---
<!-- Start Writing Below in Markdown -->

JavaScript의 조건문

<div class="pro-txt">
조건문의 참고 자료는 <a href="https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Control_flow_and_error_handling#%EC%A1%B0%EA%B1%B4%EB%AC%B8" target="_blank">MDN 의 조건문</a> 입니다.
조건문은 특정 조건이 참인 경우에 실행하는 명령의 집합입니다. JavaScript는 두 가지 조건문을 지원합니다: if...else and switch.
조건문에서의 '~문' 은 statement 라 부르는데 간단하게 Code Block{} 을 가지고있는 명령문장 이라 생각하시면 됩니다.
</div>

글로 감을 잡고 바로 예제를보며 확인해보는게 빠를꺼 같습니다.

{% highlight javascript %}
  var state = true;
  
  if( state == true ){
    console.log("state는 참 입니다.");
  } else if ( state == "다른 조건" ) {
    console.log("state는 다른 조건입니다.");
  } else {
    console.log("state는 거짓 입니다.");
  }
  
  // 결과는 state가 true 라는 논리형 데이터를 가지고있기 때문에 "state는 참 입니다." 를 출력합니다.
  > state는 참 입니다.
  
  // 만약 state 가 "다른 조건" 이면 "state는 다른 조건입니다." 출력하고
  var state = "다른 조건";
  > state는 다른 조건입니다.
  
  // 만약 state 가 false 이면 true 도 아니고 "다른 조건" 도 아니기 때문에 else 로 이동하여 "state는 거짓 입니다." 를 출력합니다.
  var state = false;
  > state는 거짓 입니다.
  
{% endhighlight %}

참 or 거짓 이라는 조건을 활용하면 여러가지 갈림길이 생기고 선택지도 많이 생깁니다. 
이를 활용해서 웹페이지에서 많은 기능을 구현할 수 있죠.

전에 만들었던 함수를 조건문을 추가하여 직접만든 함수의 기능을 더욱 향상 시켜 보겠습니다.
{% highlight javascript %}
 function $(selector) {
   return document.querySelectorAll(selector);
 }
 
 console.log($('#box'));
{% endhighlight %}

위에있는 코드에 조건문을 추가해 보도록 하겠습니다.

{% highlight javascript %}
 function $(selector, context) {
   if( !context ){  // 앞에 ! 가 붙을 경우 context가 존재하지않을경우 (undefined) 부정을 나타냅니다.
   // (context == undefined) 이런형태의 부정형태도 됩니다. 다만 최대한 짧게 줄이는 것이 프로그래머의 역할이니 짧게 쓰도록 하겠습니다.
     context = document;   
   }
   
   return context.querySelectorAll(selector);
 }
 
 console.log($('.title',$('#box_two')));
{% endhighlight %}

기존 코드와 변화된 점과 추가된 기능을 설명드리자면

function $(selector) 처음엔 인자값을 하나 selector 만 가져왔습니다. 
그러다 보니 사용자가 원하는 값이 아닌 맨위에 존재하는 selector 만 가져옵니다.
그래서 함수에 사용자가 원하는 값 내부에 있는 selector 을 가져왔으면 좋겠으니
조건문을 추가하여 
if( !context ){ context 가 존재하지 않을경우 document 를 추가하고 document 내부(전체)에서 selector를 찾고
context 가 존재할경우 인자값을 넣어 context내부에서 사용자가 원하는 값을 찾게 도와줍니다.

제가 쓴글로는 이해가 어려울 수 있으니 바로 예제를 보여드리겠습니다.

{% highlight javascript %}
  //HTML
  <div id="box">
    <div class="title">안녕하세요. MIN SEOK 블로그입니다.</div>
    <span>댓글로 응원의 한마디 작성해주세요!</span>
  </div>
  <div id="box_two">
    <div class="title">이쪽 타이틀을 불러오고 싶어요.</div>
  </div>
{% endhighlight %} 

사용자는 id가 box_two 인 div 안에있는 class명이 title 인 div 를 가져오고 싶어합니다.

사용자는 기존에 만든 사용자 함수 를 이용해 불러왔습니다.
{% highlight javascript %}
 function $(selector) {
   return document.querySelectorAll(selector);
 }
 console.log($('.title'));
 > <div class="title">안녕하세요. MIN SEOK 블로그입니다.</div>
{% endhighlight %}

하지만 값은 첫번째 title 을 불러옵니다. 
그 이유는 매개변수 return값이 document 로 되어있어서 전체를 찾아 불러왔기 때문입니다.
document 맨위부터 차례로 내려가다보니 box_two 보다 위에있는 box 내부의 title을 불러왔기 때문입니다.
이 문제를 해결하기 위해 조건문을 추가하여 사용자가 직접 지정해주도록 해주었습니다.

{% highlight javascript %}
 function $(selector, context) {
   if( !context ){
     context = document;   
   }
   
   return context.querySelectorAll(selector);
 }
 
 console.log($('.title',$('#box_two')));
 
 > <div class="title">이쪽 타이틀을 불러오고 싶어요.</div> 
{% endhighlight %}

$('.title',$('#box_two')) #box_two 내부에있는 .title 값을 가져와라 
만약에 $('.title') 전달 인자 값에 context가 없다면 document를 추가하여 문서 전체에서 찾아와라
라는 조건문을 추가하였습니다.

<div class="box">
  <div class="small-title">비교연산자 와 논리연산자의 조건문</div>
  <br/>
  <div class="small-title">비교연산자</div>
  <div class="pro-txt">
    <p>비교 연산자는 피연산자들을 비교하고 비교에 따라 논리 값을 반환합니다. 피연산자들은 숫자, 문자열, 논리형, 객체 를 사용할 수 있습니다. 문자열은 유니코드 값을 사용하여 표준 사전순서를 기반으로 비교합니다. 만약 두 피연산자가 다른 형태일 경우,자바스크립트는 대부분 비교를 위해 피연산자를 적절한 타입으로 변환합니다. 이런 행동은 보통 숫자로 피연산자를 숫자로 비교하는 형태로 나타납니다. 형태를 바꾸기의 유일한 예외는 엄격한 비교를 수행하는 === 과 !== 연산이 관련되는 경우입니다.</p>
    <a href="https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Expressions_and_Operators" target="_balnk"> - MDN 연산자</a>
</div>
  <div class="small-title">비교연산자의 종류</div>
    
  <p>글로 보는것보다 바로 예제를 통해 확인해보고 빠르게 이해해 보도록 하겠습니다.</p>
  
  <div class="small-title">같은 (==) : 피연산자들이 같으면 참을 반환</div>
  {% highlight javascript %}
    if( 10 == 10 ){
      console.log(true);
      // 숫자형 데이터인 10 와 10 이 '같으면' true를 출력해라!
    }
    > true
    // 숫자형인 10이 둘다 '같기때문에' true를 출력합니다.
   {% endhighlight %} 
   
   <div class="small-title">다른 (!=) : 피연산자들이 다르면 참을 반환</div>
   {% highlight javascript %}
    if( 10 != 10 ){
      console.log(true);
      // 문자형 데이터인 10 와 10 이 '같지않으면' true를 출력해라!
    }
    > 
    // 숫자형인 데이터인 10 와 10이 '같기때문에' 아무것도 출력하지 않습니다.
  {% endhighlight %}
  </div>
  <div class="box">
  <p>하지만 저희는 == 와 != 는 되도록이면 쓰지않는것을 습관화 해야합니다.</p>
  <p>왜 쓰면 안되는지 예제를 통해 같이 확인해 보겠습니다.</p>
  {% highlight javascript %}
    if( 10 == '10' ){
      console.log(true);
      // 숫자형 데이터인 10 와 문자형인 데이터인 10 이 '같으면' true를 출력해라!
    }
    > true
  {% endhighlight %}
  
  <p>자바스크립트의 동적형 언어이기 때문에 조건문에서 자동으로 형을 바꾸어 주기 때문입니다.</p>
  <p>섬세한 코딩작업에 상황에 따라 자유자제로 바뀐다면 어느순간 코드는 망가지고 디버깅 하기가 힘들어 질것입니다.</p>
  <p>코딩작업은 정리정돈처럼 잘 정리하고 규칙있게 작성하는것이 중요하다고 생각합니다.(Min 의 개인적인 생각..)</p>
  <p>그래서 우리는 그냥 '같다' 가 아닌 '절대로 같다' 를 사용해서 코드를 처음부터 탄탄하게 만들어</p>
  <p>나가야 한다고 생각합니다. 저만이 아닌 팀원들과 다른이를 위해서 입니다.</p>
  
  <p>바로 예제를 통해 확인해 보도록 하겠습니다.</p>
  
  <p>하지만 저희는 == 와 != 는 되도록이면 쓰지않는것을 습관화 해야합니다.</p>
  <p>왜 쓰면 안되는지 예제를 통해 같이 확인해 보겠습니다.</p>
  
  <div class="small-title">엄격하게 같음 (===) : 피연산자들이 피연산자들하고 같은 형태이면 참을 반환</div>
  {% highlight javascript %}
    if( 10 === '10' ){
      console.log(true);
      // 숫자형 데이터인 10 와 문자형인 데이터인 10 이 '절대 같으면' true를 출력해라!
    }
    > 
    // 숫자형인 데이터인 10 와 10이 '데이터 형이 다르기 때문에' 아무것도 출력하지 않습니다.
  {% endhighlight %}
  
  <div class="small-title">엄격하게 다름 (!==) : 피연산자들이 다르거나 형태가 다름</div>
  {% highlight javascript %}  
    if( 10 !== '10' ){
      console.log(true);
      // 숫자형 데이터인 10 와 문자형인 데이터인 10 이 '절대 같으면' true를 출력해라!
    }
    > true
    // 숫자형인 데이터인 10 와 10이 '데이터 형이 같기 때문에' true를 출력합니다.
  {% endhighlight %}
  
  <div class="small-title">~ 보다 큰 (>) : 왼쪽의 피연산자 보다 오른쪽의 피연산자가 크면 참을 반환</div>
  {% highlight javascript %}  
  if(10 > 100){
    console.log(true);
  }
  >
  // 오른쪽이 더 크기때문에 조건이 틀려 아무것도 출력하지 않습니다.
  {% endhighlight %}
  
  <div class="small-title">~ 보다 크거나 같음 (>=) : 왼쪽의 피연산자 보다 오른쪽의 피연산자가 크거나 같으면 참을 반환</div>
  {% highlight javascript %}  
  if(10 >= 100){
    console.log(true);
  }
  >
  // 오른쪽이 더 크고 같지않기 때문에 조건이 틀려 아무것도 출력하지 않습니다.
  {% endhighlight %}
  
  <div class="small-title">~ 보다 작은 (<) : 왼쪽의 피연산자 보다 오른쪽의 피연산자가 작으면 참을 반환</div>
  {% highlight javascript %}  
  if(10 < 100){
    console.log(true);
  }
  > true
  // 오른쪽이 더 크기때문에 조건이 맞아 true를 출력합니다.
  {% endhighlight %}
  
  <div class="small-title">~ 보다 작거나 같음 (<=) : 왼쪽의 피연산자 보다 오른쪽의 피연산자가 작거나 같으면 참을 반환</div>
  {% highlight javascript %}  
  if(10 <= 10){
    console.log(true);
  }
  > ture
  // 왼쪽보다 오른쪽이 더 크거나 작지않지만 값이 같기때문에 true를 출력합니다.
  {% endhighlight %}
</div>
 
<div class="box">
  <div class="small-title">논리 연산자</div>
  
  <div class="small-title">AND -> &&</div>
  <p>A 그리고 B => A && B 라고 작성해야합니다.</p>
  <p>좀더 보기 쉽게 표현한다면 => true && true</p>
  <p>A 도 참 이고 B도 참 이여야 한다.</p>
  
  <div class="small-title">OR -> ||</div>
  <p>A 또는 B => A || B 하고 작성해야합니다. (Backspace 아래 하이픈기호입니다.)</p>
  <p>이것 또한 => true || False</p>
  <p>A 와 B 중에 하나라도 해당된다면 참이다.</p>
  
  <div class="small-title">NOT -> !</div>
  <p>이전 시간에 많이 봐왔기에 따로 예제는 적지 않겠습니다.</p>
  <p>부정 연산자입니다.</p>
  
   <div class="small-title">typeof 데이터형을 알려주는 연산자</div>
   {% highlight javascript %}
   typeof 5
   > number
   
   typeof '글자'
   > string
   
   typeof false
   > boolean
   
   typeof function(){}
   > function
   
   typeof object
   > undefined
   
   typeof {}
   > object
   
   typeof []
   > object
   // typeof 에 [] 는 배열이지만 출력은 object를 출력하는 오류가 발생합니다.
   // 이를 해결하기 위해서 배열만큼은 Array.isArray([]) 를 활용합니다.
   
   typeof null
   > object
   // null 또한 object 를 출력하는 오류가 발생합니다.
   
   typeof 에는 이렇게 array 와 null 값을 올바르게 반환하지 못하는 특징이 있습니다.
   {% endhighlight %}
</div>
