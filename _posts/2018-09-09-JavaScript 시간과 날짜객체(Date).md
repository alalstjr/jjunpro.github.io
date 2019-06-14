---
layout:     post
title:      Javascript의 시간과 날짜객체(Date)
author:     쭌프로
tags: 		  JavaScript
subtitle:   JavaScript 공부 노트
category:   JavaScript
---
<!-- Start Writing Below in Markdown -->

<div class="box">
  <div class="small-title">Date 날짜 객체</div>
  <div class="pro-txt">
    <a href="https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Date" target="_balnk">MDN- 날짜객체</a>
  </div>
  <p>날짜를 메서드 함수로 가져오는 방법</p>
{% highlight javascript %}
	var date_object = new Date();
	// Date 객체를 생성한후 변수에 참조
	
	console.log(
		"현재 년도 : ",date_object.getFullYear()
	);
	// 현재 년도를 구합니다.
	// 로컬 시간에 따라 명시된 날짜의 년도를 반환
	
	console.log(
		"현재 월 : ",date_object.getMonth() + 1
	);
	// 현재 월을 구합니다.
	// 로컬 시간에 명시된 월(0 ~ 11)을 반환합니다.
	// 0 = 1월 , 11 = 12월 
	// + 1 을 해주어서 사람이 보기 더 쉽게 해줍니다.
	
	console.log(
		"현재 일 : ",date_object.getDate()
	);
	// 현재 일을 구합니다.
	
	console.log(
		"현재 요일 : ",date_object.getDay()
	);
	// 주중의 몇번째 요일인지 반환 (0 - 6)
	// 0 = 일요일 , 6 = 토요일
	
	console.log(
		"현재 시간 : ",date_object.getHours(),
		"현재 시간 : ",date_object.getHours() - 12
	);
	// 시간(0 ~ 23)을 반환합니다.
	// 12 = 오후 12시

	console.log(
		"현재 분 : ",date_object.getMinutes()
	);
	// 분( 0 ~ 59 )을 반환
	
	console.log(
		"현재 초 : ",date_object.getSeconds()
	);
	// 초를 반환합니다.
	
	console.log(
		"현재 분 : ",date_object.getMilliseconds()
	);
	// 밀리초( 0 ~ 999 )를 반환합니다.
	// 1000밀리초 = 1초
	
	console.log(
		"현재 분 : ",date_object.getTime()
	);
	// 현재 시간을 밀리초 값으로 구하는 방법
	// 1970년 1월 1일 00:00:00 UTC 이후의 밀리 초 수로 변환
	// 지금까지 지나온 시간
{% endhighlight %}
<div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-09-1.png" alt="자바스크립트 출력확인" />
</div>
</div>
<div class="box">
	<div class="small-title">객체 메서드를 활용하여 잘짜 정보 가져오기</div>
{% highlight javascript %}
	var date_object = new Date();
	// Date 객체를 생성한후 변수에 참조
	
	console.log(
		"현재 년 월 일 : ",date_object.toLocaleDateString()
	);

	console.log(
		"현재 년 월 일 : ",date_object.toDateString()
		// 날짜를 영어로 가져옵니다.
	);
	
	console.log(
		"국제표준시간 : ",date_object.toISOString()
		// 국제 표준형태 시간
	);
	
	console.log(
		"지역시간 : ",date_object.toLocaleTimeString()
		// 지역 시간
	);
	
	console.log(
		"날짜 : ",date_object.toString()
		// 날짜를 문자로 가져옵니다.
	);
	
	console.log(
		"날짜 : ",date_object.toTimeString()
		// 날짜 문자를 함축하여 가져옵니다.
	);
	
	console.log(
		"날짜 : ",date_object.toUTCString()
		// 날짜를 문자로 가져옵니다.
	);
{% endhighlight %}  
	<div class="img-box">
	  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-09-2.png" alt="자바스크립트 출력확인" />
	</div>
</div>

<div class="box">
{% highlight javascript %}
	console.log(new Date(2018,1,20))
{% endhighlight %}
	<div class="img-box">
	  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-09-3.png" alt="자바스크립트 출력확인" />
	</div>
	<p>직접 날짜 객체를 활용하여 날짜를 만들 수 있습니다.</p>
</div>	

<div class="box">
	<div class="small-title">위에 메서드 함수를 참고하여 우리나라 날짜로 변화하기</div>
{% highlight javascript %}
	// 년도를 가져옵니다.
	function getYear(format) {
		var date = new Date();
		if(!format) {
			format = '';
		}
		// format 전달인자 값이 있으면 전달인자 값을 사용
		// 전달인자 값이 없다면 빈문자 사용
		// format 있을경우 "2018년"
		// format 없을경우 "2018"
		return date.getFullYear() + format;
	}
	
	// 월을 가져옵니다.
	function getMonth(format) {
		var date = new Date();
		if(!format) {
			format = '';
		}
		return (date.getMonth() + 1) + format;
	}
	
	// 일을 가져옵니다.
	function getDate(format) {
		var date = new Date();
		if(!format) {
			format = '';
		}
		return date.getDate() + format;
	}

	// 시간을 가져옵니다.
	function getHour(format) {
		var date = new Date();
		if(!format) {
			format = '';
		}
		return date.getHours() + format;
	}
	
	// 분을 가져옵니다.
	function getMinute(format) {
		var date = new Date();
		if(!format) {
			format = '';
		}
		return date.getMinutes() + format;
	}
	
	// 초를 가져옵니다.
	function getSecond(format) {
		var date = new Date();
		if(!format) {
			format = '';
		}
		return date.getSeconds() + format;
	}
	
	// 몇 밀리초를 가져옵니다.
	function getMillisecond(format) {
		var date = new Date();
		if(!format) {
			format = '';
		}
		return date.getMilliseconds() + format;
	}
	
	// 요일을 가져옵니다.
	function getDay(format) {
		var date = new Date();
		var day  = date.getDay();
		switch(day){
			case 0:
			day = '일';
			break;
			case 1:
			day = '월';
			break;
			case 2:
			day = '화';
			break;
			case 3:
			day = '수';
			break;
			case 4:
			day = '목';
			break;
			case 5:
			day = '금';
			break;
			case 6:
			day = '토';
			break;
		}
		if(!format){
			format = "";
		}
		return day + format;
	}
{% endhighlight %}
	
<div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-09-4.png" alt="자바스크립트 출력확인" />
</div>

<p>요일 같은 경우에는 swicth 문을 활용하여 숫자로 출력되는것을 </p>
<p>'월화수목금토일' 로 조건문을 찾아 변환하여 출력하게 하였습니다.</p>

<p>함수를 만들어 쉡게 Date 객체를 만들어 시간과 날짜를 불러올 수 있었습니다.</p>
<p>이를 활용해 실시간으로 시간이 바뀌는 디지털 시간을 시계를 만들어 보겠습니다.</p>
</div>

{% highlight javascript %}
	// CSS
	.watch {
		background-color: #faffe7;
		padding: 25px;
		border-radius: 25px;
		width: 100%;
		max-width: 300px;
		position: absolute;
		transform: translate(-50%,-50%);
		left: 50%;
		top: 50%;
	}
	
	// HTML
	<div class="watch">
		<span class="year"></span>년
		<span class="month"></span>월
		<span class="date"></span>일
		<span class="day"></span>요일
		<span class="hours"></span>시
		<span class="minutes"></span>분
		<span class="seconds"></span>초
		<span class="milliseconds"></span>밀리초
	</div>
{% endhighlight %}
<p>우선 보여지는 모습을 간단하게 꾸며줍니다.</p>
<div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-09-6.png" alt="자바스크립트 출력확인" />
</div>
<p>지금은 아무것도 없는 모습입니다.</p>

<div class="box">
	<p>우선 문서 객체를 지정하여 시간을 출력할 수 있도록 해야하므로</p>
{% highlight javascript %}
	function $(selector, context) {
	  if (typeof selector !== 'string' || selector.trim().length === 0) { return null; }
	  if (context && context.nodeType !== document.ELEMENT_NODE) { context = el(String(context)); }
	  if (!context) { context = document; }
	  return context.querySelector(selector);
	}
{% endhighlight %}
<p>함수 $ 를 불러옵니다.</p>
<div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-09-4.png" alt="자바스크립트 출력확인" />
</div>
	
{% highlight javascript %}
	var watch		= $('.watch');
	var year		= $('.year', watch);
	var month		= $('.month', watch);
	var date		= $('.date', watch);
	var day			= $('.day', watch);
	var hours		= $('.hours', watch);
	var minutes		= $('.minutes', watch);
	var seconds		= $('.seconds', watch);
	var milliseconds	= $('.milliseconds', watch);
{% endhighlight %}
<p>$ 함수를 사용하여 원하는 문서객체를 불러옵니다.</p>
<p>다음 쉽게 원하는 객체를 불러오기위해 변수에 각각 담아 정리합니다.</p>

{% highlight javascript %}
function viewDate() {
	year.textContent		= getYear();
	month.textContent		= getMonth();
	date.textContent		= getDate();
	day.textContent			= getDay();
	hours.textContent		= getHour();
	minutes.textContent		= getMinute();
	seconds.textContent		= getSecond();
	milliseconds.textContent	= getMillisecond();
}
{% endhighlight %}
<p>다음에는 실시간으로 시간을 표시해 주어야 합니다.</p>
<p>이를 표시해주기 위해서 textContent 를 활용합니다.</p>
<div class="pro-txt">
	<a href="https://developer.mozilla.org/ko/docs/Web/API/Node/textContent" target="_balnk">MDN - textContent</a>
	<p>자세한 textContent 의 내용은 MDN 에서 확인해주세요.</p>
</div>

<div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-09-7.png" alt="자바스크립트 출력확인" />
</div>
<p>이렇게 아무것도 없던 watch 박스 안의 내용을 채워 넣었습니다.</p>
<p>이제 이것을 새로고침으로 가 아닌 실시간으로 바뀔수 있도록 하겠습니다.</p>
<p>이를 작동하게 하는방법으로 window.setInterval 을 활용합니다.</p>
<p> window.setInterval 란 지정해준 시간마다 해당 함수를 실행시킬수 있도록 도와주는 함수입니다.</p>

{% highlight javascript %}
	viewDate();
	window.setInterval(viewDate,1000);
{% endhighlight %}

<p>결과는 1 초마다 함수를 실행하여 시간이 바뀌는것을 확인하실 수 있습니다.</p>
</div>
