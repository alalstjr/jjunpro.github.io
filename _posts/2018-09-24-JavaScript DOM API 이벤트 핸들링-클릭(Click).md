---
layout:     post
title:      Javascript의 DOM API 이벤트 핸들링-클릭
author:     쭌프로
tags: 		  JavaScript
subtitle:   JavaScript 공부 노트
category:   JavaScript
---
<!-- Start Writing Below in Markdown -->

<div class="box">
	<div class="small-title">DOM API 클릭(Click) 이벤트 핸드링</div>
	<p>가장 많이 사용하는 클릭(Click) 이벤트에 대해 정리하겠습니다.</p>
	<p>클릭(Click) 이벤트는 마우스로 작동하는 이벤트이지만 동시에 접근성도 준수 가능한 이벤트 입니다.</p>
	<p>이제부터는 선택자 함수는 생략하고 바로 $('selector') 로 바로 넘어가겠습니다.</p>
{% highlight javascript %}
  // HTML
  <a href="#" class="event">
	<img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-16-3.png" alt="자바스크립트 연습"/>
  </a>
	
  // CSS
  .event {
  	display: block;
  	width: 100%;
  	max-width: 300px;
  	position: absolute;
  	left: 50%;
  	top: 50%;
  	transform: translate(-50%,-50%);
  	text-decoration: none;
  	color: #333;
  }
  .event img {
  	width: 300px;
  }
  .event:active {
  	background-color: #fff;
  	color:aqua;
  	border: 1px solid aqua;
  }
{% endhighlight %}
<p>예제를 시작하기전에 사용할 이미지와 오디오 를 미리 불러와 셋팅하는 작업을 먼저해야합니다.</p>
<p>만약에 미리 셋팅하지 않고 Click 했을때 불러온다면 화면에 바로 이미지가 보이는게아니라 잠깐 깜빡버리게 보여집니다.</p>
<p>이를 느리게 불러온다 해서 lazyload 라 부릅니다.</p>
<p>미리 완성 된 예제를 통해 확인해 보도록 하겠습니다.</p>
<p>완성된 예제에서 관리자 창을 열어서 Network 클릭후 불러온 파일리스트 를 확인하시면 파란선을 넘은 파일 3개가 보입니다.</p>
<div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-24-1.png" alt="자바스크립트 출력확인" />
</div>
<p>파란선을 넘어서 불러온 파일이 웹이 로딩이 된후 불러온 파일이란것을 알려주는 것 입니다.</p>
<p>미리 파일을 로드 시킴으로서 깜빡임 오작동없이 바로 이미지 교체를 볼 수 있는것입니다.</p>
<p>lazyload 의 코드</p>
{% highlight javascript %}
var img ;
var sound ;
var lazyload_urls = [
  // 처음 클릭전의 이미지
  'https://alalstjr.github.io/jjunpro.github.io/static/img/post/2018-09-16-3.png',
  // 클릭 후의 변화 이미지
  'https://alalstjr.github.io/jjunpro.github.io/static/img/post/2018-09-16-2.png',
  // 클릭시 사운드
  'https://alalstjr.github.io/jjunpro.github.io/static/media/switch.mp3'
];
lazyload_urls.forEach(function(url, index){
  var max = lazyload_urls.length - 1;
  // 레이지 이미지 로드
  if(index < max) {
    img = new Image();
    img.src = url;
  }
  // 클릭 사운드
  else {
    sound = new Audio()
    sound.src = url;
    click();
  }
});
{% endhighlight %}

<p>lazyload 문제도 해결하였으니 Click 이벤트를 만들어 보겠습니다.</p>
<p>우선 Click 의 대상을 해당 클레스명이 event 를 찾아 변수에 할당합니다.</p>
{% highlight javascript %}
  // 우선 event 의 변수 초기값을 설정합니다.
  var event = null;

  function click() {
	// 클레스명이 event 인 엘리먼트를 이벤트 변수에 담아줍니다.
	event = $('.event');
	// 클릭 이벤트를 만들어 toggle_event 의 함수를 연결시켜 줍니다.
	event.addEventListener('click',toggle_event);
  }
  // 클릭 함수를 실행합니다.
  click();

  // toggle_event 전달 인자값 e 를 넣습니다. 여러가지 속성을 파악하기 필요한 값입니다.
  function toggle_event(e) {
	console.log('클릭')
  }
{% endhighlight %}
<div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-16-4.png" alt="자바스크립트 출력확인" />
</div>
<p>클레스 명이 event 인 click 을 클릭했을때 정상적으로 click() 함수가 실행되며 동시에 연결된</p>
<p>함수 toggle_event() 가 실행되어 console.log를 정상적으로 출력하는것을 확인할 수 있었습니다.</p>
</div>
<div class="box">
	<div class="small-title">클릭한 대상의 속성(img,url..) 값 가져오기</div>
	<p>클릭한 대상의 이미지 속성을 가져와야 합니다.</p>
	<p>속성을 가져오기 위해서는 target 이벤트를 활용합니다.</p>
{% highlight javascript %}
// 우선 event 의 변수 초기값을 설정합니다.
var event = null;

function click() {
  // 클레스명이 event 인 엘리먼트를 이벤트 변수에 담아줍니다.
  event = $('.event');
  // 클릭 이벤트를 만들어 toggle_event 의 함수를 연결시켜 줍니다.
  event.addEventListener('click',toggle_event);
}
// 클릭 함수를 실행합니다.
click();

function toggle_event(e) {
  e.preventDefault();
  // element의 속성은 e 의 target이벤트 안에 있습니다.
  var target = e.target;
  // element 속성의 src 를 target을 활용해 변경합니다.
  target.src = 'https://alalstjr.github.io/jjunpro.github.io/img/2018-09-16-2.png';
}
{% endhighlight %}
<p>이제 이미지가 변경 되는것 까지 확인하였습니다.</p>
<p>하지만 이미지는 단 한번 변경되면 이전 이미지로 돌아가지 않습니다.</p>
<p>Click 이벤트로 이미지가 전/후 로 변화되는 효과를 주는것을 toggle 이라 부릅니다.</p>
<p>toggle 효과를 주기위해서 조건문과 변수로 스위치를 만들어 줘야합니다.</p>
<p>변수 var click_state = false 를 추가한 후에 조건문을 주어서 이미지 변경 전/후 를 넣어줍니다.</p>

{% highlight javascript %}
function toggle_event(e) {
	e.preventDefault();
	// element의 속성은 e 의 target이벤트 안에 있습니다.
	var target = e.target;
	// element 속성의 src 를 target을 활용해 변경합니다.
  
  // 초글 (on/off) 코드분기
  if(click_state){
	  target.src = 'https://alalstjr.github.io/jjunpro.github.io/static/img/post/2018-09-16-2.png';
  } else {
	  target.src = 'https://alalstjr.github.io/jjunpro.github.io/static/img/post/2018-09-16-3.png';
  }
  // 클릭한 상태 변경 click_state 의 값을 반대로 스위치 변경
  // 참일경우 거짓으로 거짓일경우 참으로
  click_state = !click_state;
}
{% endhighlight %}
<p>toggle 효과가 잘들어간 것을 확인하실 수 있습니다.</p>
<p>마지막으로 효과음을 넣을차례입니다.</p>
{% highlight javascript %}
  // 연속으로 Click 했을 경우 소리의 오작동을 방지하기 위해
  // currentTime 을 이용하여 0 으로 초기화 해줍니다.
  sound.currentTime = 0;
  sound.play();
{% endhighlight %}
<p>효과음은 sound 변수에 담겨진 mp3 파일을 play 로 실행시키면서 동시에</p>
<p>currentTime 으로 클릭했을때 초기화하여 사운드 오작동이 없도록 하였습니다.</p>
<p>설명이 어렵다면 완성본을 보면서 천천히 파악해 보셔도 좋습니다.</p>
<iframe height='265' scrolling='no' title='API click 이벤트 ' src='//codepen.io/alalstjr/embed/QVREPx/?height=265&theme-id=0&default-tab=js,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/alalstjr/pen/QVREPx/'>API click 이벤트 </a> by alalstjr (<a href='https://codepen.io/alalstjr'>@alalstjr</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
</div>

