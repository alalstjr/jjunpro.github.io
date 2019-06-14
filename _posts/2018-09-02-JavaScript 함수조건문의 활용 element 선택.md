---
layout:     post
title:      Javascript의 함수조건문의 활용 element 선택
author:     쭌프로
tags: 		  JavaScript
subtitle:   JavaScript 공부 노트
category:   JavaScript
---
<!-- Start Writing Below in Markdown -->

<div class="box">
  <p>조건문과 연산자를 정리하고 공부하였습니다.</p>
  <p>무엇인지만 개념만알고있다면 실제로 사용할 수 있는 가 에대한</p>
  <p>'감' 을 잡기가 사실 많이 힘듭니다.</p>
  <p>저도 처음 개념만 알고있는 상태로 실무에서 작업기에는 많은 시간이걸려</p>
  <p>JavaScript 적응하고 여러가지 기능을 활용하기 시작했습니다.</p>
  <p>이번에는 이전에 만든 함수를 조건문과 연산자를 더해 사용자가 더 쉽게 사용할수 있게 활용할 수 있도록</p>
  <p>수정 보안해보도록 하겠습니다.</p>
</div>

<div class="box">
{% highlight javascript %}
// HTML
<div class="box_1">
  <div class="select">no</div>
</div>
<div class="box_2">
  <div class="select">element</div>
</div>
{% endhighlight %}
</div>

<div class="box">
  <div class="small-title">HTML 에서 element CLASS명이 box_2 안에 있는 CLASS명이 select 인 div 를 찾아라</div>
  <p>조건문과 함수를 사용하지 않고 구하는방법은</p>
{% highlight javascript %}
// 변수 box 안에 CLASS 명이 box인 것을찾고 그안에서 item메서드를 활용하여 두번째인 div를 선택하여 값을 할당합니다.
var box = document.getElementsByClassName('box_2');
// 해당 box 안에서 CLASS 명이 select 인것을 찾아 값을 할당합니다. 
var select = box.querySelector('.select');
// 찾은 값을 콘솔창에 띄웁니다.
console.log(select);
{% endhighlight %}
<div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-02-1.png" alt="자바스크립트 출력확인" />
</div>
  <p>원하는 값을 불러오는것을 확인하실 수 있었습니다.</p>
  <p>다만 매번 원하는 값을 불러올때마다 코드를 길게 작성하여 똑같은것을 반복하여 작성할 필요가 있는지 의문이 듭니다.</p>
  <p>프로그래머는 코드량을 줄일 수 있다면 최대한 줄여주는것이 좋다고 생각합니다.</p>
  <p>위 코드를 한번 조건문과 함수를 이용하여 선택자함수를 만들어 보도록 하겠습니다.</p>
</div>

<div class="box">
{% highlight javascript %}
function $(selector, context) {
	if (typeof selector !== 'string' || selector.trim().length === 0) { return null; }
	if (context && context.nodeType !== document.ELEMENT_NODE) { context = $(String(context)); }
  if (!context) { context = document; }
	return context.querySelector(selector);
}
function $$(selector, context) {
	if (typeof selector !== 'string' || selector.trim().length === 0) { return null; }
	if (context && context.nodeType !== document.ELEMENT_NODE) { context = $(String(context)); }
	if (!context) { context = document; }
  return context.querySelectorAll(selector);
}
{% endhighlight %}
  
<p>차근차근 무엇이 들어가있는지 알아보도록 하겠습니다.</p>
<div class="small-title">첫번째 조건문</div>
<p>첫번째 조건문에서 typeof 란 해당 값의 데이터 형을 알려주는 기능을합니다.</p>
<p>typeof로 해당값이 문자인지 숫자인지 function 인지 등등 알려줍니다.</p>
<p>그러므로 사용자가 선택한 selector 값이 string 이 아니거나(or == ||)</p>
<p>trim 으로 양쪽 공백을 삭제한후에 글자의 길이가 0(글자값이 없다면) 이라면</p>
<p>null 값을 출력하여 아무것도 없음을 표시합니다.</p>
<div class="small-title">두번째 조건문</div>
<p>context 값 그리고(and == &&) context.nodeType 이 요소 노드들이 아니라면 $(selector, context) 에 값을 넣고 string 으로 변환하여 다시 $$(selector, context) context 값에 넣는다.</p>
<div class="small-title">세번째 조건문</div>
<p>context 에 값이 존재하지 않는다면 context 는 document로 대체한다.</p>
</div>
<div class="box">
<iframe height='265' scrolling='no' title='xaNGPj' src='//codepen.io/alalstjr/embed/xaNGPj/?height=265&theme-id=0&default-tab=js,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/alalstjr/pen/xaNGPj/'>xaNGPj</a> by alalstjr (<a href='https://codepen.io/alalstjr'>@alalstjr</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
</div>
<div class="box">
 <p>이렇게 조건문과 함수를 활용하여 간단하게 $ 와 $$ 를 이용하면 긴 문장을 다시 작성할 필요없이 element 를 선택할 수 있습니다.</p>
 <p>나중에는 $ 함수안에 같은 클레스 안에서 몇번째 클레스만 가져와라 라는 구문을 추가하도록 하겠습니다.</p>	
</div>
