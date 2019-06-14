---
layout:     post
title:      Javascript의 ReactJS-TimeAgo IE 개체인식 오류 해결
author:     쭌프로
tags: 		  JavaScript
subtitle:   JavaScript 공부 노트
category:   JavaScript ReactJS
---
<!-- Start Writing Below in Markdown -->

<div class="box">
  <div class="pro-txt">
    <a href="https://www.npmjs.com/package/react-timeago" target="_balnk">ReactJS-TimeAgo의 NPM</a>
  </div>
  <p>React 프로젝트 진행중에 날짜를 표기하는 모듈을 사용중에</p>
  <p>ReactJS-TimeAgo가 익스 플로러에서 <TimeAgo/> 를 사용시 개체 인식 오류가 발생하는 문제가 생겼습니다.</p>
  <div class="img-box">
    <img src="https://alalstjr.github.io/jjunpro.github.io/img/2019-1-26-1.png" alt="자바스크립트 출력확인" />
  </div>
  <p>처음에는 '익스 플로러에서는 다르게 적용하는 방법이 있나..?' 하는 생각에 </p>
  <p>TimeAgo의 사용방법을 많은 시간을 투자하여 검색해 보았습니다.</p>
  <p>하지만 원하는 검색 결과는 찾지 못하고 있었습니다.</p>
</div>

<div class="box">
  <p>혹시 진행중인 프로젝트의 코드 충돌로 인한 오류인가 해서 새로운 프로젝트를 만들어 실행시켜 보았습니다.</p>
  <p>create-react-app 으로 새롭게 프로젝트를 만든후에 똑같은 방법으로 TimeAgo를 설치하고 실행시켜 보았습니다.</p>
  <p>역시 익스 이외엔 전부 잘 작동하지만 익스플로러(IE)에서만 오류를 출력하고 있었습니다.</p>
  <p>하지만 이번에는 출력문이 다르게 나왔습니다.</p>
  <div class="img-box">
    <img src="https://alalstjr.github.io/jjunpro.github.io/img/2019-1-26-2.png" alt="자바스크립트 출력확인" />
  </div>
  <p>Promise가 정의되어 있지 않다는 문구가 있었습니다.</p>
  <p>바로 Promise 관련해서 검색을 해보았습니다.</p>
  <p>Promise란 javascript의 callback의 단점을 해결 하기 위해 만들어진것</p>
  그리고 최종적으로 찾은 검색 결과는 
  <div class="pro-txt">
    <a href="https://velopert.com/2597" target="_balnk">velopert 님의 비동기 처리 게시글에서 해결방법을 찾았습니다.</a>
  </div>
  <p>Promise는 신형 브라우저에만 내장되어있어서 구형인 익스플로러에서는 작동을 못한것이였습니다.</p>
  <p>Promise 기능을 갖고있지 않은 브라우저 자바스크립트 엔진들을 호환시켜주기 위해서는</p>
  <div class="pro-txt">
    <a href="https://babeljs.io/docs/en/babel-polyfill" target="_balnk">npm install --save @babel/polyfill</a>
  </div>
  <p>@babel/polyfill를 설치해 주시고 설정위치는</p>
  <p>2019년 1월 기준 create-react-app 기준 config/webpack.config.js 에서 entry 배열 내부에 "@babel/polyfill", "./app/js" 를 추가하시면 됩니다.</p>
  <p>./app/js 란 ReactDOM render하는 js 파일입니다.</p>
  <p>예를 들어 저같은 경우 App 을 렌더링 하는곳이 ./src/index.js 라서 이곳으로 설정하였습니다.</p>
  <div class="img-box">
    <img src="https://alalstjr.github.io/jjunpro.github.io/img/2019-1-26-3.png" alt="자바스크립트 출력확인" />
  </div>
  <p>다시 프로젝트를 실행시켜 보았더니 TimeAgo가 정상적으로 적용되었습니다.</p>
  <div class="img-box">
    <img src="https://alalstjr.github.io/jjunpro.github.io/img/2019-1-26-4.png" alt="자바스크립트 출력확인" />
  </div>
</div>

<div class="box">
  <p>이 오류 하나 찾는데 개인적으로.. 엄청 고생했습니다.. 처음엔 어디서 오류가 나는건지도 몰라서 하나하나 주석걸며 어디서 오류가 난건지</p>
  <p>찾는거 조차 고생했습니다.. 그래도 역시 한다면 한다! 오류해결해서 속 시원합니다.~</p>
  <p>혹시나 저랑 똑같은 오류가 있으신 분들 조그마한 참고가 됐면 좋겠습니다~</p>
</div>
