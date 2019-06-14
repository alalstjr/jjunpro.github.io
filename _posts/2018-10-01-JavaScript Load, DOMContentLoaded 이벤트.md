---
layout:     post
title:      Javascript의 Load, DOMContentLoaded
author:     쭌프로
tags: 		  JavaScript
subtitle:   JavaScript 공부 노트
category:   JavaScript
---
<!-- Start Writing Below in Markdown -->

<div class="box">
  <div class="small-title">JavaScript Load 이벤트</div>
  <p>HTML, CSS , JS 해석에 관련하여 정리하겠습니다.</p>
  <p>HTML의 해석 순서는 위에서 부터 아래로 해석하며 내려갑니다.</p>
  <div class="pro-txt">
    <a href="https://www.growingwiththeweb.com/2014/02/async-vs-defer-attributes.html" target="_balnk">HTML의 해석 참고 사이트</a>
  </div>
  <p>아래 html 코드가 있습니다.</p>
{% highlight javascript %}
<!DOCTYPE html>
<html lang="ko-KR">
  <head>
  <meta charset="UTF-8">
  <title>Javascript Slide Example</title>
  <link rel="stylesheet" href="link">
  <script src="link_1"></script>
  <script src="link_2"></script>
  </head>
    <body>
      <header>
        <div class="JJun">쭌프로</div>
          <div>블로그</div>
        </header>
    </body>
</html>
{% endhighlight %}
  <p>코드를 위에서 부터 해석하며 웹상으로 불러옵니다.</p>
  <p>html 에서 시작하여 내려오다가 CSS 파일을 불러오는 link 코드를 만납니다.</p>
  <p>다행이 CSS link 는 HTML 파싱(해석)을 방해하지 않아 멈추지않고 내려갑니다.</p>
  <p>하지만 js 파일을 불러오는 script 코드를 마주치는 순간 HTML 파싱(해석)은 잠시 멈추게 됩니다.</p>
  <p>script 파일을 서버에 요청하고 다운로드 한후에 실행 시켜야 하기 때문입니다.</p>
  <p>이렇게 중간에 script 파일이 HTML 파싱(해석)을 중단시키는 상황이 발생되면</p>
  <p>사용자가 봐야하는 웹상의 모습이 순간 멈칫한다던가 느리게 불러오는 현상(최악의 UX)이 일어납니다.</p>
  <p><strong>주의사항!</strong> script는 항상 link 아래 위치에 존재해야 합니다.</p>
  <p>만약 script가 link 보다 위에 존재한다면</p>
  <p>script가 불러오는 시간동안 CSS 파일을 못불러오기 때문에 사용자는 HTML 구조만 보고 있어야 합니다.</p>
</div>

<div class="box">
  <div class="small-title">HTML 파싱(해석)</div>
  <div class="img-box">
     <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-10-01-1.png" alt="자바스크립트 출력확인" />
  </div>
  <p>HTML 파싱(해석)하는 과정에서 중간에 script 를 해석하며 불러오는 시간으로</p>
  <p>HTML 파싱(해석)이 늦어지는 현상을 해결하려면 우선</p>
  <p>모든 HTML 이 불러와진 다음에 script 를 적용시키는 것입니다.</p>
  <p>이를 적용시키기 위해서 사용하는 것이 load 이벤트 입니다.</p>
{% highlight javascript %}
window.addEventListener('load',function(){
	console.log('Load');
});
{% endhighlight %}
  <p>결과를 확인하기 전에 크롬 개발자 환경 창에서 Network클릭후 Disable cachi 체크후 새로 고침을 합니다.</p>
  <div class="img-box">
     <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-10-01-1.png" alt="자바스크립트 출력확인" />
  </div>
  <p>결과는 모든 HTML의 파싱으로 이미지와 CSS, script 를 불러오는데 총 69밀리초가 소비되었습니다.</p>
  <p>(이미지가 더많거나 script 사이즈가 크면 클수록 load 시간은 길어집니다.)</p>
  <p>결론은 load 란 69밀리초가 지난 이후에 console.log 를 출력해 주세요. 라고 해석하면 될거 같습니다. </p>
</div>

<div class="box">
	<div class="small-title">JavaScript DOMContentLoaded 이벤트</div>
	<p>Load 이벤트는 모든 DOMContent(이미지,기타파일)가 불러왔을경우에 실행합니다.</p>
	<p>서버에 요청지연되거나 혹은 이미지의 크기가 크다면 자바스크립트 실행이 늦어질 수 있습니다.</p>
	<p>사용자가 홈페이지를 이용하려고 하는시점에 웹페이지 로딩이 늦어질경우 메뉴가 안나온다던가</p>
	<p>웹페이지에 존재하는 여러가지 액션을 잠시동안 중단된 상탱로 있어야 합니다.</p>
</div>

<div class="box">
	<p>DOMContentLoaded 란?</p>
	<div class="img-box">
	   <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-10-01-2.png" alt="자바스크립트 출력확인" />
	</div>
	<p>저의 블로그의 콘솔 Network 를 통해서 DOMContentLoaded 를 확인해보겠습니다.</p>
	<p>첫번째 WaterFall 부분을 확인하시면 파란색 줄로 그어진곳을 경계로 왼쪽이 DOMContentLoaded 부분입니다.</p>
	<p>HTML, CSS, JS 가 불러와지는 구역입니다.</p>
	<p>오른쪽은 DOMContentLoaded 가 전부 불러와진 후 이미지파일 같은 기타 파일이 불러와집니다.</p>
	<p>두번째 아래 보시면 DOMContentLoaded가 불러와진 시간은 3초이며</p>
	<p>나머지 Load 되는 시간이 41.53초 입니다.</p>
	<p>만약에 제 블로그에서 41초나 걸리는시간동안 자바스크립트가 실행이 안된다면</p>
	<p>메뉴이동도 안되고 효과는 없고 사용자가 당황해할 수 있습니다.</p>
	<p>이를 방지하기 위해 사용하는 것이 DOMContentLoaded 이벤트 입니다.</p>
</div>

<div class="box">
	<p>DOMContentLoaded 이벤트를 사용하여 스크립트를 불러오는 시간을 DOMContent 앞까지 당겨와도</p>
	<p>DOMContent를 다운받는 시간이 길면 길어질 수록 실행은 늦어집니다.</p>
	<p>이를 해결하기 위해서는 DOMContentLoaded 를 사용하지않고 스크립트 배치 위치만 바꿔주면 됩니다.</p>
	{% highlight javascript %}
	<!DOCTYPE html>
	<html lang="ko-KR">
	  <head>
	  <meta charset="UTF-8">
	  <title>Javascript Slide Example</title>
	  <link rel="stylesheet" href="link">
	  </head>
	    <body>
	      <header>
		<div class="JJun">쭌프로</div>
		  <div>블로그</div>
		</header>
		<script src="link_1"></script>
		<script src="link_2"></script>
	    </body>
	</html>
	{% endhighlight %}
	<p>script 불러오는 위치를 body 끝부분 바로 위에서 불러오는것입니다.</p>
	<p>이렇게 되면 웹에 다운받고 실행시킬 준비가 되어 있는 상태가 되어 lose time 없이 바로 실행시킬 수 있습니다.</p>
</div>

<div class="box">
	<div class="small-title">Lose Time 잃어버린 시간 을 줄이는 방법</div>
	<p>DOMContentLoaded 이벤트 없이도 Lose Time을 줄이는 방법으로 script 위치를 body 끝부분에 배치하는 방법도 있으며</p>
	<p>head 에 위치해도 Lose Time를 줄이는 방법이 있습니다.</p>
	<div class="small-title">script defer 속성 - 연기시키다.</div>
	<div class="img-box">
	   <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-10-01-4.png" alt="자바스크립트 출력확인" />
	</div>
	<p>웹 로드 시간에 스크립트 다운로드 요청을 합니다.</p>
	<p>defer 속성으로 인해 parsing(해석)을 멈추지않고 계속 진행하며 내려갑니다.</p>
	<p>그리고 모든 parsing(해석)이 끝나면 실행합니다.</p>
	<p>defer 속성을 사용함으로서 parsing(해석) 지연현상을 방지할 수 있습니다.</p>
</div>

<div class="box">
	<div class="small-title">script async 속성 - 비동기 속성</div>
	<div class="pro-txt">
	  <a href="http://private.tistory.com/24" target="_balnk">출처 : 공부해서 남 주자 sync(동기) , Async(비동기)</a>
	  <p>동기적 일처리 방식 : 순차적으로 일을 스스로 끝내 나가는 방식</p>
	  <p>동기방식은 설계가 매우 간단하고 직관적이지만 결과가 주어질 때까지 아무것도 못하고 대기해야 하는 단점</p>
	  <p>비동기적 일처리 방식 : 해야 할 일을 위임하고 기다리는 방식</p>
	  <p>동기보다 복잡하지만 결과가 주어지는데 시간이 걸리더라도 그 시간 동안 다른 작업을 할 수 있으므로 자원을 효율적으로 사용</p>
	</div>
	  <div class="img-box">
	     <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-10-01-5.png" alt="자바스크립트 출력확인" />
	  </div>
	  <p>비동기 속성으로 인해 웹페이지가 불러와 지는 동안에 script 도 같이 불러옵니다.</p>
</div>

<div class="box">
	<p>JavaScript Load 이벤트는 이미지와 기타 파일들을 모두 로드한 이후에 실행합니다.</p>
	<p>JavaScript DOMContentLoaded 이벤트는 문서객체구조가 완성되면 실행합니다.</p>
</div>
