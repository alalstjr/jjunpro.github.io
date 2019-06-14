---
layout:     post
title:      Javascript의 DOM API 이벤트 핸들링-키보드
author:     쭌프로
tags: 		  JavaScript
subtitle:   JavaScript 공부 노트
category:   JavaScript
---
<!-- Start Writing Below in Markdown -->

 <div class="box">
  <div class="small-title">JavaScript DOM API 이벤트 핸들링-키보드(KeyBoard)</div>
  <p>우리 프로그래밍 개발자들은 모든이들의 편의성과 접근성을 고려 해야하기 때문에</p>
  <p>마우스로 작동하는 Click 이벤트뿐만 아니라 KeyBoard 도 생각해서 프로그래밍 을 해야합니다.</p>
 </div>
 
 <div class="box">
  <p>KeyBoardEvent 에는 keydown, keypress, keyup 세가지가 존재합니다.</p>
  <p>이벤트 발생 순서는 keydown → keypress → keyup 순으로 나열 됩니다.</p>
  <br/>
  <p>키가 처음 눌러지면 keydown 이벤트가 발생합니다.</p>
  <p>keydown이 발생하는 조건 버튼은</p>
  <p>keydown - 영문, 숫자, space, enter, 한글, tab, caps, lock, shift, ctrl, alt(option), command, arrow, F1 ~ F12</p>
  <br/>
  <p>keydown 이벤트 이후 keypress 이벤트가 발생합니다.</p>
  <p>keypress - 영문, 숫자, space, enter</p>
  <br/>
  <p>키를 놓으면 keyup 이벤트가 발생합니다.</p>
  <p>keyup - tab, caps lock발생 X</p>
 </div>
 
 <div class="box">
  <p>KeyBoardEvent 실행 방법에는 구형 과 신형 방법이 있습니다.</p>
  <p>IE 8-)예전 방식인 구형은 window.onkeydown = function(){}; 으로 이벤트를 조작하지만</p>
  <p>IE 9+)신형 방식은 window.addEventListener('keydown', function(){}); 으로 이벤트를 실행 조작합니다.</p>
 </div>

<div class="box">
 <p>window.addEventListener('keydown', function(){}); 의 함수 전달받는 인자값에는 event, evt, e 세개를 받을 수 있습니다.</p>
 <p>ex) function(event), function(evt), function(e) 이런식으로 인자값을 받을 수 있습니다.</p>
 <p>간단한 KeyBoardEvent 를 구현해 보고 확인해 보도록 하겠습니다.</p>
{% highlight javascript %}
 window.addEventListener('keydown',function(e){
  console.log('이벤트 작동'+e.type);
 });
{% endhighlight %}
<div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-25-1.png" alt="자바스크립트 출력확인" />
</div>
 <p>정상적으로 KeyBoardEvent 가 작동되는 것을 확인하실 수 있습니다.</p>
 <p>좀더 KeyBoardEvent 에 대해 알아보기 위해서 keyCode, code, key 도 추가해보도록 하겠습니다.</p>
</div>

<div class="box">
 {% highlight javascript %}
 window.addEventListener('keydown',function(e){
  console.log('이벤트 작동'+e.type, '=', e.keyCode, '|', e.code, '|', e.key);
 });
{% endhighlight %}
 <p>이제 화면에서 키보드의 자판을 클릭해보고 결과를 확인해 봅니다.</p>
<div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-25-2.png" alt="자바스크립트 출력확인" />
</div>
 <p>결과는 사용자가 무엇을 클릭했는지 해당의 keyCode 값 code 값 key 값을 전부 출력하는것을 확인할 수 있었습니다.</p>
</div>

<div class="box">
 <p>하지만 모든 브라우저가 같은 결과를 보여주는 것은 아닙니다.</p>
 <p>호환성 문제로 브라우저 마다 지원하는 것이 다르기 때문입니다.</p>
<div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-25-3.png" alt="자바스크립트 출력확인" />
</div>
 <p>익스플로러 에서는 code 값을 지원하지 않아 찾을 수 없다는 표시가 나옵니다.</p>
 <p>익스플로러 뿐만 아니라 파이어 폭스나 크롬의 code 값이 다르게 표시됩니다.</p>
 <p>code 경우는 아직 테스트 중인 상태라고 보시면 될꺼같습니다.</p>
 <p>그렇다면 저희가 사용해야할 값은 사람이 읽기 어려운 숫자로 된 keyCode 이지만</p>
 <p>모든 브라우저에서 호환되는 keyCode 를 활용하시면 됩니다.</p>
 <p>keyCode 를 활용하여 간단한 KeyBoard 표시 박스를 만들어 보겠습니다.</p>
</div>

<div class="box">
{% highlight javascript %}
// HTML
<div id="box">
  <div class="body">
    키보드를 클릭해보세요.
  </div>
  <div>키보드 화살표 Left, Right, Up 버튼을 클릭하세요.</div>
</div>
 
// CSS
#box {
  width:100%;
  max-width:600px;
  margin:0 auto;
  padding:5% 0;
  text-align:center;
}
#box .pink {
  width:200px;
  height:200px;
  margin:0 auto;
  background-color:pink;
  display:flex;
  align-items: center;
  justify-content: center;
  margin-bottom:10px;
}
{% endhighlight %}
<p>간단하게 눈으로 결과를 확인할 수 있게 만들어주고 자바스크립트 기능을 넣어 확인해 보도록 하겠습니다.</p>
</div>

<div class="box">
{% highlight javascript %}
window.addEventListener('keydown',function(e){
  switch(e.keyCode){
    case 32:
      console.log('스페이스바');
      break;
    case 37:
      console.log('왼쪽');
      break;
    case 39:
      console.log('오른쪽');
  }
});
{% endhighlight %}
 <p>간단하게 만든후에 방향키 오른쪽 왼쪽 스페이스바 를 클릭해 보고 결과를 확인해 봅니다.</p>
 <div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-25-4.png" alt="자바스크립트 출력확인" />
</div>
 <p>결과는 조건문에 맞춰서 해당키를 눌렀을경우에만 결과값이 출력되는것을 확인하실 수 있습니다.</p>
 <p>이를 활용하여 pink 를 움직여 보도록 하겠습니다.</p>
</div>

<div class="box">
{% highlight javascript %}
// CSS
.jump {
  animation: jump 0.4s steps(2);
}
@keyframes flow {
  to {
    transform: translateX(-110vw);
  }
}
@keyframes jump {
  to {
    transform: translateY(-10vw);
  }
} 
{% endhighlight %}
 <p>CSS 부분에 에니메이션을 추가해 줍니다. pink 박스가 뛰어 오르는듯한 모션을 css 로 추가한것입니다.</p>
{% highlight javascript %}
var pink = document.querySelector('.pink');

window.addEventListener('keydown',function(e){
  switch(e.keyCode){
    case 32:
      jump();
      break;
    case 37:
      moveLeft();
      break;
    case 39:
      moveRight();
  }
});

pink.addEventListener('animationend', jump_remove);

function jump_remove() {
  pink.classList.remove('jump');
}

function jump() {
  pink.classList.add('jump')
}

function moveLeft() {

}

function moveRight() {

}
{% endhighlight %}
<p>자바스크립트로 해당 클레스를 추가하고 제거하는방식으로 움직임을 컨트롤 하면</p>
<p>간단한 움직임 점프 모션을 구현하실 수 있습니다.</p>
<p>위 아래로만 될까요?? 오른쪽 왼쪽도 한번 모션을 추가해 보도록 하겠습니다.</p>
</div>

<div class="box">
 <p>moveLeft 함수에 기능을 추가합니다.</p>
{% highlight javascript %}
function moveLeft() {
  pink.style.transform = 'translateX(-30px) rotateY(180deg)';
}
{% endhighlight %}
 <p>왼쪽 방향키를 클릭했을경우 pink 박스가 왼쪽으로 30px 이동하는것을 확인합니다.</p>
 <p>하지만 단 한번만 이동하고 그 이상 움직이지 않습니다.</p>
 <p>그 이유는 원위치에서 30px 만큼 고정되어 움직였기때문에 그 이상 px을 추가할 수 없기 때문입니다.</p>
 <p>고정된 30px이 아닌 추가하여 이동시키려면 현제 위치값을 가져와 더해주어서 이동시켜야 합니다.</p>
 <p>우선 console.log() 로 pink 박스의 초기 위치값을 확인합니다.</p>
{% highlight javascript %}
 console.log(pink.style.transform);
 // 결과는 "" 빈문자열 false 을 출력합니다.
 // 이를 숫자 0 초기값으로 변환해 주어야하므로
 console.log(pink.style.transform || 0);
 // 으로 하여 값이 false 일경우 0이 출력 되라 라는 구문을 만듭니다.
 // 이렇게 초기값 0 이 완성 되었습니다.
{% endhighlight %}
 <p>초기값을 변수에 담아 활용하도록 하겠습니다.</p>
</div>

<div class="box">
{% highlight javascript %}
function moveLeft() {
  var disX = pink.style.transform || 0;
  console.log(disX);
  pink.style.transform = 'translateX(-30px) rotateY(180deg)';
}
{% endhighlight %}
 <div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-25-5.png" alt="자바스크립트 출력확인" />
</div>
 <p>초기값 0 과 움직였을때 위치값이 출력되는것을 확인하실 수 있습니다.</p>
 <p>이제 움직였을때 위치값의 숫자만 가져와 더해주면 되는 부분만 남았습니다.</p>
 <p>translateX(-30px) rotateY(180deg) 값에서 숫자 -30 만 가져와 문자열을 숫자로 바꿔줘야합니다.</p>
 <p>이때 사용하는 것이 replace() 함수 입니다.</p>
{% highlight javascript %}
"translateX(-30px) rotateY(180deg)".replace('translateX(','')
 // 'translateX(' 로 시작하는 부분을 공백으로 대체한다.
 
 // 결과는 -30px) rotateY(180deg)".replace('translateX(','') 의 형태가 됩니다.
 // 이상태에서 parsInt 를 추가하여 원하는 값만 빼옵니다.
 
 parseInt(-30px) rotateY(180deg)".replace('translateX(',''),10);
 // 결과는 -30 을 정상적으로 숫자값으로 빼오는것을 확인하실 수 있습니다.
{% endhighlight %}
</div>

<div class="box">
{% highlight javascript %}
function moveLeft() {
  var disX = window.parseInt(pink.style.transform.replace('translateX(',''), 10) || 0;
  disX -= 30;
  // 해당 값을 계속 30씩 빼줍니다. 
  console.log(disX);
  pink.style.transform = 'translateX(' + disX + 'px) rotateY(180deg)';
}
{% endhighlight %}
 <p>결과를 확인해보면 pink 박스는 왼쪽으로 움직이며 console.log 에는 이동한 위치값이 출력되는것을 확인하실 수 있습니다.</p>
 <p>오른쪽 또한 똑같이 값을 주고 반대 + 를 주면 됩니다.</p>
 </div>
 
 <iframe height='265' scrolling='no' title='Keyboard  이벤트' src='//codepen.io/alalstjr/embed/PdroyW/?height=265&theme-id=0&default-tab=js,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/alalstjr/pen/PdroyW/'>Keyboard  이벤트</a> by alalstjr (<a href='https://codepen.io/alalstjr'>@alalstjr</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
