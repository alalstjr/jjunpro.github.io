---
layout:     post
title:      Javascript의 개인필기
author:     쭌프로
tags: 		  JavaScript
subtitle:   JavaScript 공부 노트
category:   JavaScript
---
<!-- Start Writing Below in Markdown -->

인강을 듣다가 document.ELEMENT_NODE 에 대한 활용과 설명을 해주는데..
역시 그냥 듣고는 이해가 잘 안갑니다.
이해가 알될때는 백지노트 공부법을 많이하는 저로서 바로 내용을 정리하고 파악해보도록 하겠습니다.

{% highlight javascript %}
  document.ELEMENT_NODE
  > 1
{% endhighlight %} 
JavaScript 에서 document.ELEMENT_NODE 는 1 을 출력합니다. 
document.ELEMENT_NODE 는 상수입니다.
상수란 그 값이 변하지 않는 불변량으로, 변수의 반대말 이라는 뜻을 가지고 있습니다.
<div class="img-box">
  <img src="https://alalstjr.github.io/jjunpro.github.io/img/2018-09-04-1.png" alt="자바스크립트 출력확인" />
 </div>
이는 document.ELEMENT_NODE 값에 어떠한 값을 넣어도 변경되지않고 1 을 나타낸다는 것입니다. (상수는 관례적으로 대문자를 쓴다고 한다..)

JavaScript 선언에도 상수 선언이 존재합니다.
바로 const 입니다.
{% highlight javascript %}
  const box = "빈박스";
  
  box = "가득찬 박스";
  > 이미 빈박스라는 값이 고정되어있어서 에러가 발생합니다.
{% endhighlight %} 

DOM 에는 Node 라는것이 존재합니다.

Node 에는 여러가지 Type 이 존재하는데
ELEMETN , ATTRIBUTE , TEXT , COMMENT , DOCUMENT 의 타이틀이 존재하며
타이틀을 구분할수 있습니다.

document.body.nodeType 
> 1

document.body.nodeType === document.ELEMENT_NODE
> true

document.nodeType === document.ELEMENT_NODE
> false

document.nodeType === document.DOCUMENT_NODE
> true

document.DOCUMENT_NODE
> 9

document.ELEMENT_NODE
> 1

이를 통해서 비교를 합니다.

더 자세한 사항은 
<div class="pro-text">
  <a href="https://developer.mozilla.org/ko/docs/Web/API/Node/nodeType" target="_blank">MDN ELEMENT_NODE</a>
</div>
