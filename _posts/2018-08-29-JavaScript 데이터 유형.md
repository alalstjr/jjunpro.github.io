---
layout:     post
title:      Javascript의 데이터 유형
author:     쭌프로
tags: 		  JavaScript
subtitle:   JavaScript 공부 노트
category:   JavaScript
---
<!-- Start Writing Below in Markdown -->

<div class="box">
<div class="small-title">JavaScript 는 동적형 언어 입니다.</div>
<p>이것은 변수를 선언할 때 데이터 형을 지정할 필요가 없고</p>
<p>데이터 형이 스크립트 실행 도중 필요할때 <strong>자동으로 변환하는것</strong>을 의미합니다.</p>
</div>

<div class="box">
<p>예제를 들어보겠습니다.</p>
{% highlight javascript %}
  var str = 'String';
  var num = 12345;
  var bul = falsel;
{% endhighlight %}
<p>위의 변수를</p>
{% highlight javascript %}
  > str = true;
  > str
  > str = true
{% endhighlight %}
<p>str 변수에 논리형 데이터 true 를 넣은다음 다시 str 출력했을때 결과는</p>
<p>> ture 가 출력되는 것을 볼수 있습니다.</p>
<p>이처럼 처음에 문자값이였던 변수에 다른 데이터 형을 집어넣어도 <strong>오류가 발생하지않습니다.</strong></p>
<p>이것을 <strong>동적형 언어</strong>라고 부릅니다.</p>
</div>

<div class="box">
<div class="small-title">정적형 언어</div>
<p>동적형 언어를 알아보았으니 다음은 정적형 언어를 알아보겠습니다.</p>
{% highlight javascript %}
  var str:string = 'String';
  var num:number = 12345;
  var bul:boolean = falsel;
{% endhighlight %}
<p>동적형 언어와 다르게 변수 뒤에 <strong>해당 변수의 데이터 형을 지정</strong>해줍니다.</p>
<p>그러면 해당 변수에 다른 데이터 형이 들어갈 경우 <strong>오류를 발생 하게 됩니다.</strong></p>
<p>정적형 언어의 장점은 <strong>디버깅</strong> 하기가 좋습니다.</p>
<p>긴 문장의 코드에 str:string 이라는 문자형 데이터 변수에</p>
<p>숫자를 넣을경우 오류를 발생시켜서 코드가 망가지지않게 할수 있습니다.</p>
<p>(아무래도 처음부터 깨끗하게 정돈하고 관리하는 <strong>정리정돈 같은 개념</strong> 같습니다.)</p>
</div>

<div class="box">
<p>다시 자바스크립트의 동적형 언어로 돌아오겠습니다.</p>
<p>자바스크립트의 특징중 하나는 자동으로 데이터 형이 변환되는거 였습니다.</p>
<p>이것은 <strong>장점이 될수 있으며 혹은 단점이 될수있는 기능</strong>입니다. (양날의 도끼같은 느낌을 받았습니다.)</p>
<p>예제를 들어보겠습니다.</p>	
{% highlight javascript %}
  var str = 'String';
  var num = 12345;
{% endhighlight %}
</div>

<div class="box">
<p>이처럼 문자형 데이터 값과 숫자형 데이터 값이 있습니다.</p>
<p>이 둘을 더하면 어떤 결과가 나타날까요?</p>
</div>

<div class="box">
{% highlight javascript %}
  var str = 'String';
  var num = 12345;
  
  str + num
  // 숫자형인 num 이
  
  'String' + 12345
  // 문자형으로 변환되어 더해집니다.
  
  'String' + '12345'
  // 결과는 문자형 데이터 입니다.
  
  > String12345
{% endhighlight %}
</div>

<div class="box">
<p>결과는 문자와 숫자가 합쳐진 문자형 데이터값이 출력됩니다.</p>
<p>이것이 매우 혼란 스러울때를 경험담(실무에서)으로 얘기해보자면</p>
<p>어느 계산식에 있는 input 의 value값 을 가져와서 변수와 더해 값을 출력하는 것이였습니다. </p>
<p>하지만 왜인지 계속 NaN(숫자가 아니다) 를 출력해서 왜그런가해서 천천히 찾아보아습니다.</p>
{% highlight javascript %}
 // HTML
 <input value="100" class="num">

 // JavaScript
 var firstNum = 100;
 var num = $('.num').val();

 var result = firstNum + num ;
 console.log(result);

 > 100100
{% endhighlight %}
<p>value 값에는 숫자형이 아닌 문자형으로 저장되는것을 모른체 결과값을 저장했습니다.</p>
<p>둘의 데이터 형이 다르기때문에 숫자형인 firstNum 값은 문자형으로 변환되어서 계산식에 들어갔습니다.</p>
<p>결과 값은 200 이 아닌 100100을 출력했습니다. </p>
<p>숫자로 더해지는 방법은 없을까요?</p>
</div>

<div class="box">
<p>해결할 방법으로 데이터 형을 변경해주는 여러가지 방법을 알아봅시다.</p>
<p>var num 에는 100 이라는 문자형 데이터가 들어가 있습니다.</p>
{% highlight javascript %}
  var num = "100";
  > num
  > "100"
  var num = Number(num);
  > num
  > 100
{% endhighlight %}
<div class="small-title">이렇게 Number() 의 함수를 사용하여 데이터형을 숫자로 바꿔주는 방법도 있으며</div>
{% highlight javascript %}
  var num = "100";
  > +num;
  > 100
  > num  - 0;
  > 100
  ..* / ..곱하기 나누기 등등
{% endhighlight %}
<p>등등 문자형에 연산식을 넣으면 숫자형으로 자동 변환 됩니다.</p>
<p>실무에서 다른 사람이 만든 코드를 보았을때</p>
<p>>num - 0; 이라는 코드를 처음보았다면 "왜 이런코드가 여기 들어가있지? 어차피 결과는 num인 100 이잔아?"</p>
<p>문자형인 num 을 <strong>숫자형으로 바꿔주는 코드라는것을 모른체</strong> 필요없다는 생각에 지운다면 코드는 망가질것입니다.</p>
</div>

<div class="box">
<p>만약에 문자형이 들어간 데이터형을 Number() 로 변환할경우 무슨일이 일어날까요?</p>
{% highlight javascript %}
  var num = "num100";
  > Number(num);
  > NaN
{% endhighlight %}
<p>변수의 값에 문자가 포함되어있어 NaN(숫자가 아니다) 라는 구문이 출력됩니다.</p>
<p>문자 값을 숫자로 변경할 경우</p>

<div class="small-title">parseInt(string,radix), parseFloat(string,radix) 활용하기</div>

<div class="pro-txt">
	<a href="https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/parseInt" target="_blank">parseInt(string,radix), parseFloat(string,radix) 함수 를 이용하여 데이터 형을 변경할 수 있습니다. - MDN</a>
</div>
</div>
<div class="box">
{% highlight javascript %}
  var num = "100num";
  > parseInt(num,10);
  > 100

  var num_s = "100.21num";
  > parseFloat(num_s,10);
  > 100.21
{% endhighlight %}

<p>parse 는 '해석한다' 라는 의미를 가지고 있으며</p> 
<p>Int 는 'Integer = 정수', Float 는 'Float = 실수' 를 의미합니다.</p>
<p>뒤에있는 10 은 10진수를 의미하며 일반적으로 많이 사용합니다.</p>

<div class="small-title">논리형 데이터로 변경하는 경우</div>
{% highlight javascript %}
  var str = 'String';
  var num = 12345;
  var bul = falsel;
  var fun = function(){};
  var list = [1,2,3];
  var obj = {};
{% endhighlight %}

<p>논리형으로 변경하는 경우는 Boolean(str)</p>
{% highlight javascript %}
  Boolean(str)
  > true

  Boolean(num)
  > true

  Boolean(bul)
  > true

  Boolean(fun)
  > true // 함수도 논리형으로 인식합니다.

  Boolean(list)
  > true // 배열도 논리형으로 인식합니다.

  Boolean(obj)
  > true // 오브젝트도 논리형으로 인식합니다.

  !!bul
  > true

  !str
  > false // ! 하나는 부정을 의미합니다. (반대)

  Boolean(' ')
  > true // 공백은 참을 의미합니다.
{% endhighlight %}

<p>논리형으로 변경하는 경우 고질적인 문제에 주의해야 합니다.</p>
<p>Boolean() 에 1 을 넣어도 -1 을 넣어도 글자는 넣어도 전부 true 값을 출력했습니다.</p>

{% highlight javascript %}
Boolean(0)
> false

0 == false
> true
{% endhighlight %}
<p>하지만 0 을 넣을 경우에는 false 를 출력하는 것을 볼 수 있으며</p>
<p>0 하고 false 는 같을 수가 없는데 자바스크립트 언어에서는 둘이 같다고 출력합니다.</p>
<p>또 다른 경우에는 </p>
{% highlight javascript %}
Boolean(null)
> false

Boolean(undefined)
> false

Boolean('')
> false
{% endhighlight %}

<p>한꺼번에 모아서 정리하자면</p>
<p>!!0 , !!'', !!null, !!undefined</p>
<p>는 전부 false 를 출력합니다.</p>
</div>
