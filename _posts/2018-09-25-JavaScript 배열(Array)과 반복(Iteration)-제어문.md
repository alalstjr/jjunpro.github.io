---
layout:     post
title:      Javascript의 배열(Array)과 반복(Iteration)-제어문
author:     쭌프로
tags: 		  JavaScript
subtitle:   JavaScript 공부 노트
category:   JavaScript
---
<!-- Start Writing Below in Markdown -->

<div class="box">
  <div class="pro-txt">
    <a href="https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Loops_and_iteration" target="_balnk">MDN - 루프와 반복</a>
  </div>
  <div class="small-title">JavaScript 배열(Array)과 반복(Iteration)</div>
  <p>무언가를 반복적으로 시행할때 빠르고 간편하게 방법을 제공합니다.</p>
  <p>반복문이 필요한 이유는</p>
  <p>반복 처리가 필요한 일을 사람 대신 프로그래밍으로 처리해 줌으로서</p>
  <p>불필요한 작업을 줄여줍니다.</p>
  <p>간단한 예제로 수많은 상품 리스트가 존재합니다.</p>
  <p>수많은 상품의 정보를 바꿔줘야 하는데 하나하나 바꾸기에는 많은 작업이 소요됩니다.</p>
  <p>하지만 반복문을 활용하여 한번만 수정하면 나머지가 수정되도록 합니다.</p>
</div>

<div class="box">
  <div class="small-title">반복 while문</div>
  <p>while문 을 확인하기 전에 배열 하나를 생성하여</p>
  <p>그 배열 내부의 갯수를 하나하나 삭제 하는 반복문을 들어 보겠습니다.</p>
  <p>배열 생성에는 New Array 를 활용하여 만들 수 있지만 권장하지는 않습니다.</p>
{% highlight javascript %}
  var array_list = ['사과','배','포도','딸기','바나나'];
{% endhighlight %}
  <p>배열 array_list 에서 while문을 활용하여 하나하나 지워보도록 하겠습니다.</p>
</div>

<div class="box">
  <p>while() {} 조건이 참이면 코드 블럭을 실행한다.</p>
  <p>조건이 맞으면 실행하라 이는 조건문 if 문과 비슷해 보입니다.</p>
  <p>하지만 차이점이 있습니다.</p>
  <p>if문은 단 한번 실행하지만</p>
  <p>while문은 조건이 참일경우 계속 실행합니다.</p>
  <p>while문은 조건을 거짓으로 변경하는 중단점이 필요합니다.</p>
  <p>만약 중단점이 존재하지 않는다면 무한 반복에 빠지게 됩니다.</p>
{% highlight javascript %}
while( array_list.length ) {
  array_list.pop();
  // 여기서 pop() 는 배열의 맨 끝부분을 제거하는 배열 메서드입니다.
  console.log(array_list);
}
{% endhighlight %}
<div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-25-6.png" alt="자바스크립트 출력확인" />
</div>
  <p>결과를 확인해 보면 첫번째 반복 조건문이 array_list.length 가 5 참 이므로</p>
  <p>array_list.pop() 메서드를 실행하여 맨뒤 배열을 삭제 합니다.</p>
  <p>다시 조건문을 확인하여 array_list.length 값이 4 참 이므로</p>
  <p>다시한번 pop 메서드를 실행합니다.</p>
  <p>이렇게 array_list.length 값이 0 거짓 이 될때까지 실행 반복한후</p>
  <p>반복문을 빠져 나가는것을 확인할 수 있습니다.</p>
</div>

<div class="box">
  <div class="small-title">제어문</div>
  <p>continue 문</p>
  <p>반복(순환) 중 조건이 충족할 경우, 조건 확인 영역(초기영역)으로 이동</p>
  <p>break 문</p>
  <p>반복(순환) 중 조건이 충족할 경우, 실행 종료 (반복문 종료)</p>
  <p>label 문</p>
  <p>참조 가능한 식별자로 continue, break에 의해 식별</p>
</div>

<div class="box">
  <div class="small-title">제어문 예제</div>
  <p>while 문 증가 식을 간단하게 만들어 보겠습니다.</p>
  <div class="small-title">continue문</div>
{% highlight javascript %}
var while_if = true;
var count = 0;
var limit_count = 8;
 
while(while_if) {
  // 선 증가 연산자로 1씩 증가
  ++count;
  // 조건이 count 가 3 or 7 일경우에는 반복문을 초기로 돌립니다.
  if( count === 3 || count === 7 ) {
    continue;
  }
  console.log(count);
  if( count >= limit_count ) {
    while_if = false;
  }
}
{% endhighlight %}
<div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-25-7.png" alt="자바스크립트 출력확인" />
</div>
<p>while 문 중간 조건문 count 가 3 과 7 이 해당되어 있는 부분은 continue 건너뛰어서</p>
<p>출력 되지 않는 것을 확인할 수 있습니다.</p>
</div>

<div class="box">
<div class="small-title">break문</div>  
{% highlight javascript %}
var while_if = true;
var count = 0;
var limit_count = 8;
 
while(while_if) {
  // 선 증가 연산자로 1씩 증가
  ++count;
  // 선 증가가 있다면 후 증가도 있습니다.
  // 후 증가는 count++ 로 표현합니다.
  
  // 조건이 count 가 3 or 7 일경우에는 반복문을 초기로 돌립니다.
  if( count === 3 || count === 7 ) {
    continue;
  }
  if( count === 5 ) {
   break;
  }
  console.log(count);
  if( count >= limit_count ) {
    while_if = false;
  }
}
{% endhighlight %}
<div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-25-8.png" alt="자바스크립트 출력확인" />
</div>
<p>count 값이 5 인 조건에 해당되어 제어문 break 으로 인해 반복문을 빠져 나오는것을</p>
<p>확인하실 수 있습니다.</p>
</div>

<div class="box">
  <div class="small-title">label 문</div>
  <p>2중 중첩 반복문일 경우에 사용합니다.</p>
{% highlight javascript %}
var while_if = true;
var count = 0;
var innerCount = 0;
var limit_count = 8;

loopCount:
while(while_if) {
  ++count;
  if( count === 3 || count === 7 ) {
    continue;
  }
  // 반복문 안에 반복문 하나 더 만듭니다.
  while(true) {
    // innerCount를 후 증가 시킵니다.
    innerCount++;
    if( innerCount === limit_count / 2 ) {
      break loopCount;
    }
    console.log('innerCount:',innerCount);
  }
  if( count === 5 ) {
   break;
  }
  console.log('count:',count);
  if( count >= limit_count ) {
    while_if = false;
  }
}
{% endhighlight %}
<div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-25-9.png" alt="자바스크립트 출력확인" />
</div>
<p>조건문 innerCount === limit_count / 2 으로 인해 innerCount값이 4일때 loopCount 해당되는 반복문을 중단시킵니다.</p>
<p>그래서 결과값이 innerCount 3 까지만 출력되고 반복문이 넘어가는 것입니다.</p>
</div>

<div class="box">
  <div class="small-title">while문 과 do ~ while 문 의 차이점</div>
{% highlight javascript %}
// while 반복문
while(false) {
  console.log('조건이 거짓이면 반복 실행되지 않습니다.')
}
  
// do ~ while 반복문
do {
  console.log('do ~ while 문의 경우 조건이 거짓이라도 1회는 실행됩니다.')
} while(false);
{% endhighlight %}
<p>while 반복문 은 조건이 거짓이면 실행되지않고 반복문을 빠져나오지만</p>
<p>do ~ while 반복문의 경우에는 조건이 거짓이라도 단 1회는 실행을 하고 반복문을 빠져나오는 차이점이 있습니다.</p>
</div>

<div class="box">
  <div class="small-title">for 문</div>
  <p>조건이 거짓으로 판별될 때까지 반복 C언어 반복문과 비슷합니다.</p>
  <p>for ([초기문]; [조건문]; [증감문]) {...}</p>
  <p>while문을 for 문으로 바꾸면서 연습해 보도록 하겠습니다.</p>
{% highlight javascript %}
var i = 0;
while (i < 10) {
  console.log(i);
  ++i;
}
{% endhighlight %}
<div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-25-10.png" alt="자바스크립트 출력확인" />
</div>
<p>위 while문을 for문으로 바꾸어 보겠습니다.</p>
{% highlight javascript %}
for (var i = 0; i < 10; ++i){
  console.log(i);
}
{% endhighlight %}
<div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-25-10.png" alt="자바스크립트 출력확인" />
</div>
<p>결과는 동일하게 출력 됩니다.</p>
<p>변수 선언구간이 구분되어있는 while문</p>
<p>for문 안에 변수 선언이 들어가있는 반복문 (for문도 변수 선언구간을 밖으로 뺄수 있지만 빼지않습니다. while 문과 차이가 없어지기 때문입니다.)</p>
</div>

<div class="box">
  <div class="small-title">중복된 반복문</div>
  <p>중복된 while 문</p>
{% highlight javascript %}
var i = 0; var j = 4;
while ( i < 10 ) {
  while ( j > 0 ) {
    console.log('j:',j);
    j = j - 2;
  }
  console.log('i:', i);
  ++i;
}
{% endhighlight %}
<div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-25-11.png" alt="자바스크립트 출력확인" />
</div>
  <p>중복된 for문</p>
{% highlight javascript %}
for ( var i = 0; i < 10; ++i ) {
 for ( var j = 4; j > 0; j = j -2 ){
  console.log('j:',j);
 }
 console.log('i:', i);
}
{% endhighlight %}
<div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-25-11.png" alt="자바스크립트 출력확인" />
</div>
  <p>둘의 결과는 동일합니다.</p>
<p>for문을 중첩되지 않고 사용할 수 있는 방법도 있습니다.</p>
{% highlight javascript %}
for ( var i = 0, j = 4; i < 10; ++i, j -= 2 ) {
 if ( j > 0 ){
  console.log('j:',j);
  continue;
 }
 console.log('i:', i);
}
{% endhighlight %}
  <p>결과는 위와 동일하게 출력됩니다.</p>
  <p>초기값과 증감값을 묶어 줄수 있다는 것을 확인하는 방법이였습니다.</p>
</div>
  
<div class="box">
  <div class="small-title">for문에 label 문 활용하기</div>
{% highlight javascript %}
outFor:for ( var i = 0; i < 10; ++i ) {
 inFor:for ( var j = 4; j > 0; j = j -2 ){
  console.log('j:',j);
  break outFor;
 }
 console.log('i:', i);
}
{% endhighlight %}
<div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-25-12.png" alt="자바스크립트 출력확인" />
</div>
  <p>label 제어문 으로 인해 j값 4 만 출력되는 것을 확인하실 수 있습니다.</p>
</div>
  
<div class="box">
  <div class="small-title">배열과 for문을 활용한 예제</div>
<iframe height='265' scrolling='no' title='배열과 for문을 활용한 색상변환 예제' src='//codepen.io/alalstjr/embed/NLZeaM/?height=265&theme-id=0&default-tab=js,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/alalstjr/pen/NLZeaM/'>배열과 for문을 활용한 색상변환 예제</a> by alalstjr (<a href='https://codepen.io/alalstjr'>@alalstjr</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
  간단히 코드펜에서 확인해 보세요~
</div>

<div class="box">
  <div class="small-title">for ~ in 문</div>
  <p>배열이 아닌, 객체를 순환할 때 사용</p>
  <p>for (variable in object) {</p>
  <p>  statements</p>
  <p>}</p>
  <p>배열을 순환 처리할 수 있지만 성능 문제로 배열은</p>
  <p>for 문을 사용하는 것이 좋다.</p>
{% highlight javascript %}
var object_box = {
  name:'쭌프로',
  type:'blog',
  localhost:'https://alalstjr.github.io/jjunpro.github.io/'
}
{% endhighlight %}
  <p>하나의 객체를 생성하고 객체 안에는 블로그의 정보를 담았습니다.</p>
  <p>객체를 순환 할때는 for문을 사용할 수 가없습니다.</p>
  <p>이유는 length 속성이 존재 하지 않기때문에 총 몇개의 속성이 있는지 알수가 없습니다.</p>
  <p>그렇기에 객체 반복문인 for ~ in 문을 사용해야합니다.</p>
{% highlight javascript %}
var object_box = {
  name:'쭌프로',
  type:'blog',
  localhost:'https://alalstjr.github.io/jjunpro.github.io/'
}

for (var property in object_box) {
	console.log(property); //key 값
}
{% endhighlight %}
<div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-25-13.png" alt="자바스크립트 출력확인" />
</div>
<p>property 값(key)을 출력하는것을 확인하실 수 있습니다.</p>
<p>value 값을 얻고 싶다면 object_box[property] 로 확인할 수 있습니다.</p>
<p>for ~ in 문의 활용 으로 in 을 활용하여 객체의 속성값의 존재 유무를 확인할 수도 있습니다.</p>
<div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-25-14.png" alt="자바스크립트 출력확인" />
</div>
</div>
