---
layout:     post
title:      Javascript의 기초문법
author:     쭌프로
tags: 		  JavaScript
subtitle:   JavaScript 공부 노트
category:   JavaScript
---
<!-- Start Writing Below in Markdown -->

<div class="box">
  <p>안녕하세요.</p>
  <p>개발자의 개인 필기 노트 블로그의 SEOK 입니다.</p>
  <p>오늘 작성하는 개인 필기는 JavaScript 언어를 직접 작성하고 실제로 출력되는 모습을 같이 봐야</p>
  <p>이해하기 쉽고 머리 더 오래 남을 거라 생각합니다. </p>
  <p>(개인적으로 실무에서 눈으로 공부만 하고 프로젝트를 작업하면 여러 응용문제를 해결하기 어려웠습니다.</p>
  <p>하지만 직접 내 손으로 작성하고 결과물을 보니 머리에 남는 게 많았습니다)</p>
</div>
<div class="box">
  <div class="small-title">개발에 필요한 개발자도구</div>
  <p>여러 가지 언어를 작성하고 저장하며 코드를 작성하게 도와주는 무료 프로그램은 많이 있습니다.</p>
    <p>(대표적인 코드 에디터는 : <a href="https://code.visualstudio.com/" target="_blank">Visual Studio Code - Code Editing</a>, 저는 웹 개발을 할 때에는 <a href="http://brackets.io/" target="_blank">Brackets</a>을 사용 중입니다)</p>
  <p>이 두 개 말고도 수도 없이 많은 코드 에디터 프로그램이 존재합니다.</p>
  <p>자신에게 맞는 코드에디터를 고르시고 설치하시면 충분할 것 같습니다.</p>
    
  <p>바로 지금 이 블로그를 보게 해 주는 웹 브라우저 프로그램에는 개발자 도구가 존재합니다.</p>
  <p>대표적으로 (Chrome 크롬, Firefox 파이어폭스, Internet Explorer 익스플로러) 가 있습니다.</p>
  <p>저는 Chrome 크롬을 사용 중이기에 크롬 기준으로 설명하겠습니다. 다른 개발자 도구도 전부 비슷할 거라 생각합니다. </p>
  <p>Chrome 크롬 에서의 개발자도구 창 여는 방법은 F12 버튼 or ctrl+shift+c 를 눌러주시면 바로 개발자창을 확인하실 수 있습니다.</p>
</div>
<div class="box">
  <p>오늘 참고하면서 공부할 <a href="https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Values,_variables,_and_literals" target="_blank">MDN-문법과 타입</a> 페이지 입니다.</p>
  <div class="pro-txt">
    <p>JavaScript는 Java로부터 구문 대부분을 빌려온 것 뿐만 아니라 Awk, Perl 및 Python의 영향도 받았습니다.</p>
    <p>JavaScript는 <strong>대소문자를 구별</strong>합니다.</p>
  </div>
  <p>JavaScript는 HTML과 CSS와는 다르게 대소문자를 엄격하게 구별합니다.</p>
  <p>직접 작성해 보고 결과의 차이를 확인해 보면서 머릿속에 확실하게 넣어줍니다.</p>

  {% highlight javascript %}
  var code = true;

  console.log(code);
  {% endhighlight %}
  <p>이렇게 작성할 경우</p>

  <div class="img-box">
    <img src="{{ site.baseurl }}/static/img/post/2018-08-26-1.png" alt="자바스크립트 출력확인" />
  </div>
  <p>ture 가 출력되는 것을 확인하실 수 있습니다. (ture는 값이 존재한다는 것을 의미합니다)</p>

  {% highlight javascript %}
  var code = true;

  console.log(COde);
  {% endhighlight %}
  <p>하지만 이렇게 작성할 경우</p>

  <div class="img-box">
    <img src="{{ site.baseurl }}/static/img/post/2018-08-26-2.png" alt="자바스크립트 출력확인" />
  </div>
  <p>빨간색으로 경고표시를 해주는듯한 텍스트가 나옵니다.</p>
  <p>출력문을 해석하면</p>
  <div class="pro-txt">
    <p>COde is not defined - COde가 정의되지 않았습니다.</p>
  </div>
  <p>저장되어있는 코드는 소문자로만 이루어져 있는데</p>
  <p>출력하려는 코드의 네임에는 대문자가 섞여 있어서 JavaScript가 code 라는 값을 찾을 수가 없어 출력할 수 없었습니다.</p>

  <p>이처럼 JavaScript에서는 <strong>대소문자 구분이 매우 중요</strong>합니다. 초보자가 많이 실수하는 것 중 하나이기에 길게 설명했습니다.</p>
  <p>꼭 머릿속에 넣어주세요.</p>
</div>
<div class="box">  
  <div class="small-title">JavaScript 의 주석</div>
  {% highlight javascript %}
  // 한 줄 주석

  /* 이건 더 긴,
   * 여러 줄 주석입니다.
   */

  /* 그러나, /* 중첩된 주석은 쓸 수 없습니다 */ SyntaxError */
  {% endhighlight %}
  <p>중첩된 형태로는 주석을 사용할수는 없습니다.</p>
  {% highlight javascript %}
  /*
    /*주석을 중첩하여 사용할수 없습니다.*/
  */
  {% endhighlight %}
  <div class="img-box">
    <img src="{{ site.baseurl }}/static/img/post/2018-08-26-3.png" alt="자바스크립트 출력확인" />
  </div>
  <p>보시다시피 문법 오류가 나옵니다.</p>

  <p>주석은 자주 사용됩니다.</p>
  <p>개인적으로 실무에서 사용할 때는 해당 코드의 변수(저장된)값의 설명을 적는다던가</p>
  <p>코드와 코드 사이의 구분 선을 만든다던가</p>
  <p>제가 만든 코드를 보기 쉽고 찾기 쉽게 하기 위해서 자주 쓰는 거 같습니다.</p>
  <p>제가 만든 코드를 저만 보는 게 아닌 다른 팀원도 많이 보기 때문입니다.</p>
  <p>그렇기에 주석으로는 꼭 자신이 만든 코드에 설명을 작성해서 표시해줍시다.</p>
</div>
<div class="box">
  <div class="small-title">JavaScript 의 선언</div>
  <p>JavaScript에서 선언은 3가지 방법이 있습니다.</p>
  <div class="pro-txt">
    <p>var</p>
    <p>변수를 선언. 추가로 동시에 값을 초기화.</p>
    <p>let</p>
    <p>블록 범위(scope) 지역 변수를 선언. 추가로 동시에 값을 초기화.</p>
    <p>const</p>
    <p>읽기 전용 상수를 선언.</p>
  </div>
  <p>메모리를 저장(참조:reference,할당:assignment)해주는 그릇입니다.</p>

  <p>메모리를 할당하는 모습을 코드로 바로 확인해보고 이해해보도록 하겠습니다.</p>
  {% highlight javascript %}
  console.log('값을 출력합니다.');
  {% endhighlight %}
  <p>이렇게 작성할경우 console.log 안에있는 텍스트는 한번 출력되고 메모리는 저장되지 않아 재사용할수 없습니다.</p>
  <p>다시 텍스트를 출력해야할 상황이 생긴다면</p>
  {% highlight javascript %}
  console.log('값을 출력합니다.');
  console.log('값을 출력합니다.');
  console.log('값을 출력합니다.');
  {% endhighlight %}
  <p>이런식으로 길게 비효율적으로 값을 새로 만들어 써야합니다.</p>

  {% highlight javascript %}
  var date = '값을 출력합니다.';
  console.log(date);
  {% endhighlight %}
  <p>변수(var) 메모리를 할당하는 방법은 = 을 작성하여 넣어줍니다.</p>
  <p> = 이라는 뜻은 '같다' 가 아니라 <strong>'할당해준다.'</strong> 라는 뜻으로 '넣는다, 대입한다' 라고 생각하면 될 거 같습니다.</p>
  <p>이렇게 변수(var) 에 할당하여 사용할 경우 date 라는 그릇에 메모리를 담아 사용 할 수 있습니다.</p>
  <p>이럴 경우 date 라는 변수 하나만 적는 것으로도 저장된 메모리는 <strong>재사용</strong>하기 쉽습니다.</p>
</div>
<div class="box">
  <div class="small-title">JavaScript 변수 선언 할 때의 주의할 점</div>
  <p>변수를 선언할 때에는 첫 글자에 ($ , _ , 영문자) 만 올 수 있습니다.</p>
  <p>변수에는 JavaScript의 예약어를 사용할 수 없습니다. (예약어란 JavaScript에서 사용하고 있는 단어입니다. ex: this,window ..등등)</p>
  <p>변수에는 띄어쓰기가 사이에 들어갈 수 없습니다.</p>

  <p>변수명 작성에는 보기 좋게 하기 위해서 카멜케이스,스네이크케이스 를 사용합니다.</p>
  <p>카멜케이스(camelCase) : 낙타의 등처럼 생겼다 해서 카멜케이스라 부릅니다.</p>
  <p>스네이크케이스(snake_case) : 뱀처럼 납작하다 해서 스네이크케이스라 부릅니다.</p>
  <p>두 가지 방법이 있으며 사용자마다의 취향이 있기 때문에 편한 걸로 선택하여 변수명을 작성해주면 됩니다.</p>

  <p>선언한 변수에는 <strong>단 하나의 값만 저장</strong>됩니다.</p>

  {% highlight javascript %}
  var date = '값을 출력합니다.';

  var date = '값을 바꿔줍니다.';
  console.log(date);
  {% endhighlight %}
  <p>이렇게 작성할 경우 변수에는 단 하나만의 값만 할당할수 있기때문에</p>  
  <div class="pro-txt">
    값을 바꿔줍니다.
  </div>
  <p>맨 <strong>마지막에 작성한 변수값만 저장</strong>하여 출력합니다.</p>
</div>
<div class="box">
  <div class="small-title">변수에 저장할 수 있는 데이터 유형</div>
  <p>6가지의 원시 데이터(Primitive Data) 유형이 있습니다.</p>
  <p>문자형(String) 과 숫자형(Number) 과 논리형(Boolean) 과 Null & Undefined 와 symbol(ES6+) 들이 존재합니다.</p>
  <p>문자형(String) : 문자형은 값을 " 나 ' 로 감싸고 있습니다. '100' 일경우 숫자가아닌 문자형으로 저장됩니다.</p>
  <p>숫자형(Number) : 변수에는 오로지 숫자만 할당되어야 합니다. 100 일경우 숫자형으로 저장됩니다.</p>
  <p>논리형(Boolean) : true참 , false거짓 주로 두개의 값을 비교할때 나오는 결과값입니다.</p>
  <p>null & undefined : 그자체의 데이터 값입니다.</p>
  
  <p>숫자나 문자 논리형은 객체가 맞습니다. 다만 객체로 사용하지 않습니다.</p>
  <p>90 이라는 숫자만 쓸경우 이것을 - 원시 데이터 값 이라고 부릅니다.</p>
    {% highlight javascript %}
      123;
    {% endhighlight %}
  <p>위 원시 데이터 값인 숫자를 객체로 생성할경우 아래처럼 작성해야 합니다.</p>
  <div class="img-box">
    <img src="{{ site.baseurl }}/static/img/post/2018-08-26-5.png" alt="자바스크립트 출력확인" />
  </div>
  <p>결과를 보게 되면 num 값에 Number{123} 이라는 객체를 생성한 것을 볼 수 있습니다.</p>
  <p>또 그 내부에는 원시값인 PrimitiveValue 값인 123 이 존재합니다.</p>
  <p>원시값을 구하기 위해서 매번 이렇게 길게 작성하여 구해야 할까요?</p>
  <p>아닙니다. 매우 비효율적이기 때문에 JavaScript의 엔진은 그냥 숫자만 나올 수 있게 허용해줍니다.</p>
  <p>이것을 (숫자 리터럴,부동 소수점 리터럴) 해준다고 말합니다.</p>
  <p>여기서 리터럴이란 무엇인가 개인적으로 생소한 단어라서 여러 곳에서 찾아보았습니다.</p>
  <div class="pro-txt">
    컴퓨터 과학 분야에서 리터럴(literal)이란 소스 코드의 고정된 값을 대표하는 용어다. 거의 모든 프로그래밍 언어는 정수, 부동 소수점 숫자, 문자열, 불린 자료형과 같은 용어를 가지고 있다. - <a href="https://ko.wikipedia.org/wiki/리터럴" target="_blank">위키백과</a>
  </div>
  <p>사전적인 의미로는 '있는 그대로의 의미' 라는 뜻을 가지고 있습니다.</p>
  <p>변수가 메모리가 할당되는 그릇이라 한다면</p>
  <p>리터럴은 그릇에 저장되는 값(그 시점의 값) 인 것이다.</p>
  <p>솔직히 아무리 찾아봐도 잘 모르겠다. 리터럴은 좀 더 찾아보고 크게 정리할 필요가 있을 거 같습니다.</p>
  <p>지금까지 찾아보고 느낀 걸로는 new 를 붙여서 함수를 만드는 것보다는</p>
  <p>함수 자체를 작성하여 만드는 것이 더 많이 사용한다는 것입니다.</p>
  {% highlight javascript %}
    var num = new Array(); // --- new 를 작성하여 배열생성
    var num = []; // ---이런식의 배열 생성 하는것을 권장한다.
  {% endhighlight %}
</div> 
<div class="box">
  <div class="small-title">객체(Object) 데이터 유형</div>
  <p>객체에는 일반, 배열, 함수 객체가 존재합니다.</p>
  <p>이러한 객체들 을 생성하려면 만들려고 하는 함수 앞에 new 를 작성하여 객체를 생성합니다.</p>
  {% highlight javascript %}
  new Function()
  > f anonymous() {
  
  }     // 이름이 없는 함수가 출력
  new Array()
  > []  // 배열의 함수가 출력
  new Object()
  > {}  // 일반적인 객체 출력
  {% endhighlight %}
  앞에서 중요하다 언급하던것이 JavaScript 는 대소문자를 확실하게 구분한다는 것 이였습니다.
  객체를 생성하는데 있어서도 대소문자는 매우 중요합니다.
  {% highlight javascript %}
  new array() // 대문자 Array() 가 아닌 소문자로 작성할경우
  {% endhighlight %}
  <div class="img-box">
    <img src="{{ site.baseurl }}/static/img/post/2018-08-26-4.png" alt="자바스크립트 출력확인" />
  </div>
  <p>역시 오류가 출력됩니다.</p>
  <div class="pro-txt">
    <div>JavaScript에서 값을 나타내기 위해 리터럴을 사용한다.</div>
    <div>스크립트에 부여한 고정값으로, 변수가 아니다.</div>
  </div>
</div>   
