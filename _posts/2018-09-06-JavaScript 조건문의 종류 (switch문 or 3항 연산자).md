---
layout:     post
title:      Javascript의 조건문의 종류 (switch문 or 3항 연산자)
author:     쭌프로
tags: 		  JavaScript
subtitle:   JavaScript 공부 노트
category:   JavaScript
---
<!-- Start Writing Below in Markdown -->

<div class="box">
  <p>JavaScript 공부 못한지 3일.. 요즘 회사에 일이 너무 많아 공부할 시간이 너무 부족하다.</p>
  <p>어서 JavaScript 를 더 공부해서 막히지 않고 작업하면 공부시간이 더 늘어날탠데..</p>
  <p>이번엔 외부 작업 스크립트 & 프론트 작업 수정이라 더욱 힘든 작업중이다..</p>
  <p>반조애 - http://www.vanzoe.co.kr/ 5년전 작업물이라 그런지 코드도 예전 코드이며 html은 표준이 되어 있지않는다.</p>
  <p>다행이 일부분 수정이라 그리 어려운 부분은 없지만 코드 분석에 어려움을 많이 느낀다..</p>
</div>

<div class="box">
  <div class="small-title">
    다른 조건문의 switch 문
  </div>

  <div class="pro-txt">
    <a href="https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/switch" target="_balnk"> - MDN switch문</a>
    <p>Swicth문은 프로그램이 표현식을 평가하고 값을 조건과 비교합니다. 만약 값이 일치한다면, 프로그램은 각 조건의 하위 문장을 실행합니다.</p>
  </div>
  <p>바로 예제를 통해 알아보도록 하겠습니다.</p>
</div>

<div class="box">
{% highlight javascript %}
  var buy = '아이스크림';
  
  if( buy === '과자' ) {
    console.log('과자를 구매합니다.');
  } else if ( buy === '음료수' ) {
    console.log('음료수를 구매합니다.');
  } else if ( buy === '아이스크림' ) {
    console.log('아이스크림를 구매합니다.');
  } else if (
    buy === '치약' ||
    buy === '칫솔'
  ) {
    console.log('치약 이나 칫솔 구매시 1+1행사도 둘다 드립니다.');
  } else {
     console.log('고객님이 찾으시는 물건이 없습니다.');
  }
{% endhighlight %}

<p>아이스 크림을 사려고 편의점에 들어갑니다.<p/>
<p>아이스 크림을 변수 buy 라고 생각하고 if문 조건문으로 물건을 찾아보겠습니다.</p>
<div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-06-1.png" alt="자바스크립트 출력확인" />
</div>
<p>이렇게 결과가 '아이스크림' 이라는 값을 출력하는 과정에</p>
<p>2번의 if문을 걸쳐서 찾습니다.</p>
<p>첫번째로 과자를 찾고 값이 다르기때문에 다음으로 넘어가</p>
<p>두번째로 음료수를 찾고 값이 다르기때문에 다름으로 넘어가</p>
<p>세번째 아이스크립을 찾고 값이 동일 하기 때문에 값을 출력합니다.</p>
<br/>
<p>만약에 buy 값이 젤리 라면 조건문에는 존재하지 않기때문에</p>
<p>처음부터 마지막(else)까지 조건문을 찾으며 내려가야 합니다.</p>
<br/>
<p>이럴경우 필요없는 행동이 많이 들어가게 됩니다.</p>
<p>찾는 값은 하나인데 전부 하나하나 비교를 해야 하기때문입니다.</p>
<br/>
<p>조건이 많을 경우 많은 행동을 할 필요없이 원하는 값을 찾는것이 switch 문입니다.</p>
</div>

<div class="box">
  <div class="small-title">switch 문</div>
{% highlight javascript %}
  buy = '치약';
	
  switch ( buy ) {
	  case '과자':
		  console.log('과자를 구매합니다.');
		  break;
	  case '음료수':
		  console.log('음료수를 구매합니다.');
		  break;
	  case '아이스크림':
		  console.log('아이스크림를 구매합니다.');
		  break;
	  case '칫솔':
	  case '치약':
		  console.log('치약 이나 칫솔 구매시 1+1행사도 둘다 드립니다.');
		  break;
	  default:
		  console.log('고객님이 찾으시는 물건이 없습니다.');
		  break;
  }
{% endhighlight %}
<p>구매할 물품인 치약을 switch 문에 변수로 넣습니다.</p>
<p>그럼 if문 처럼 위부터 마지막까지 하나하나 비교하지않고 이미 지정되어있는 case를 보고 바로 값을 출력합니다.</p>
<p>case 가 치약인 조건을 찾고 해당 조건에 출력문을 출력합니다.</p>
<div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-06-1.png" alt="자바스크립트 출력확인" />
</div>

<p>그리고 제어문(break) 를 통해 다음 출력을 막아줍니다.</p>
<p>만약 제어문(break) 를 사용하지 않을경우</p>
<div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-06-1.png" alt="자바스크립트 출력확인" />
</div>
<p>만약에 제어문(break) 이 없다면 해당 출력문부터 아래 출력문까지 전부 출력되기에 꼭 막아주어야 합니다.</p>

<p>많이 사용하는 건 if문이지만 조건이 많아지면 switch문을 사용하여 최적화 해주는게 좋다고 생각합니다.</p>
</div>

<div class="box">
	<div class="small-title">조건(3항) 연산자</div>
	<div class="pro-txt">
		<a href="https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Conditional_Operator" target="_balnk">
			condition ternary expresstion - MDN
		</a>
	</div>
	<p>3항 연산자에서 '3항' 이 가리키는 것은</p>
	<p><strong>조건 ? 값1 : 값2</strong> 라는 피연산자 3개가 ? 와 : 연산자 사이에 존재하는것을 의미합니다. </p>
	<p>3항 연산자는 변수에 할당할 수 있습니다.</p>
	<p>예외 ) Block 문은 변수에 할당할 수 없습니다.</p>
	<p>예제를 통해서 확인해 보도록 하겠습니다.</p>
</div>
<div class="box">
{% highlight javascript %}
var val = if(ture) = {'출력해라'};
{% endhighlight %}
	<p>var val 이라는 변수안에 if Block 문을 할당 하였습니다.</p>
	<p>하지만</p>
	<div class="img-box">
	  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-06-2.png" alt="자바스크립트 출력확인" />
	</div>
	<p>결과는 오류가 나옵니다. 변수에는 if Block 문을 할당할 수 없기 때문입니다.</p>
	
{% highlight javascript %}
var val = true ? '참입니다.' : '거짓입니다.';
{% endhighlight %}
	<p>3항 연산자는 정상적으로 변수에 할당할 수 있기때문에</p>
	<div class="img-box">
	  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-06-3.png" alt="자바스크립트 출력확인" />
	</div>
	<p>조건값이 true 인 '참입니다.' 가 정상적으로 출력하는것을 볼 수 있었습니다.</p>
	<p>3항 연산자를 사용하는 이유는 무엇일까요? </p>
{% highlight javascript %}
var val = true ? '참입니다.' : '거짓입니다.';
{% endhighlight %}
3항 연산자의 코드를 if Block 문으로 변환해보겠습니다.
{% highlight javascript %}
var val = true;
if( val ) {
	result = '참입니다';
} else {
	result = '거짓입니다.'
}
{% endhighlight %}
<p>한줄로 표시되는 3항 연산자에 비에서 if Block 문은 코드를 개행해야하며 줄도 길어집니다.</p>
<p>3항 연산자는 바로 변수에 조건문을 할당하여 사용할 수 있끼때문에 편리해서 많이 사용합니다.</p>
<p>많이 사용한다해서 if Block 문을 안쓰는것은 아닙니다.</p>
<p>처음 코드를 접하거나 보기 어려워하시는 분들은 if Block 문 으로 작업하시는게 가독성으로 보기 편하기때문에</p>
<p>if Block 문으로 작업하시는 분들도 많이 있습니다.</p>
</div>
<div class="box">
	<div class="small-title">3항 연산자도 연속하여 조건을 추가할 수 있다.</div>
	<p><strong>var val = val ? '' : 조건1 ? 참 : 조건2 ? 참 : 거짓;</strong></p>
	<p>3항 연산자 참 다음 거짓 결과가 아닌 조건문을 추가하면 else 처럼 계속하여 조건을 추가할 수 있습니다.</p>
{% highlight javascript %}
var val_2 = false;
var val_3 = false;

var val_1 = false ? '참입니다.' : val_2 ? '두번째 조건' : val_3 ? '세번째 조건' : '거짓입니다.';
{% endhighlight %}
	<div class="img-box">
	  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-06-4.png" alt="자바스크립트 출력확인" />
	</div>
	<p>위 결과는 세번째 조건이 false 이기때문에 거짓으로 '거짓입니다.' 를 출력 하였습니다.</p>
	<p>이렇게 3항 연산자 안에 조건문을 계속하여 추가할 수 있습니다.</p>
</div>
<div class="box">
	<p>3항 연산자는 if Block 문 보다 코드량이 대폭 줄어들어 최적화 하기에 좋습니다.</p>
	<p>단점으로는 가독성이 매우 떨어지므로 초보자가 보기 힘들며 숙련된 개발자라도</p>
	<p>오랜시간 해석해야하는 부분이 있는 장단점이 큰 3항 연산자 였습니다.</p>
	<p>부분마다 알맞게 사용해 주시면 좋을꺼같습니다.</p>
</div>

<div class="box">
	<div class="small-title">논리곱(&&) 과 논리합(||) 연산자의 활용</div>
	<p>논리곱(&&)은 그리고 를 의미하며 논리합(||)은 또는을 의미하는 연산자입니다.</p>
	<p>이를 코드로 표현한다면</p>
{% highlight javascript %}
var val_1 = true;
var val_2 = true;

if( val_1 && val_2 ) { 
	// true , false 값을 반환
	console.log('둘다 참 입니다.');
}
{% endhighlight %}
	<p>val_1 과 val_2는 둘다 true 이니 조건문 && 논리곱 으로인해 console.log를 출력합니다.</p>
	<p>만약 val_1변수가 false 가 할당되어있다면 아무것도 출력되지 않습니다.</p>
	<p>이것을 if문 밖으로 빼서 사용할 수 있습니다.</p>
{% highlight javascript %}
var val_1 = true;
var val_2 = true;

var data_1 = val_1 && console.log('참 입니다.'); // val_1 값이 참일때 실행
var data_2 = val_2 || console.log('참 입니다.'); // val_1 값이 거짓일때 실행
{% endhighlight %}
<div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-06-5.png" alt="자바스크립트 출력확인" />
</div>
<p>첫번째 val_1 값이 'true' 이므로 && 조건식에 맞음으로서 console.log('참 입니다.') 를 출력합니다.</p>
<p>&& 일때는 값이 참일 경우에만 값을 출력합니다.</p>
<p>두번째 val_2 값도 'true' 이므로 || 조건식에 맞지 않음으로 아무것도 출력하지 않습니다.</p>
<p>|| 일때는 값이 거짓일 경우에만 값을 출력합니다.</p>
{% highlight javascript %}
var val = true;
if( val ) { date = '값입니다.'; }
console.log(date);

var date = val && '값입니다.';
console.log(date);
// val 값이 true 참임으로 '값입니다.' 를 출력합니다.
// && 논리곱 연산자는 true 인것만 조건식에 맞습니다.

var date = val || '값입니다.';
console.log(date);
// val 값이 true 참임으로 '값입니다.' 를 출력하지 않습니다.
// || 논리합 연산자는 false 인것만 조건식에 맞습니다.
{% endhighlight %}
<div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-06-6.png" alt="자바스크립트 출력확인" />
</div>
<p>if Block문을 date 변수에 논리곱(&&) 과 논리합(||) 연산자를 할당하는방법으로 변환해보았습니다.</p>
<p>위에 식에서 val && '값입니다.'; 를 변수 val 값에 할당하여 사용했는데</p>
{% highlight javascript %}
console.log( val && '값입니다.' );
// and
console.log( val || '값입니다.' );
{% endhighlight %}
<p>이런식으로 변수값에 할당하지 않아도 값은 조건문에 따라 동일하게 출력됩니다.</p>
</div>
