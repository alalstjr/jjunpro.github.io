---
layout:     post
title:      JSP MyBatis 란
author:     쭌프로
tags:       JAVA
subtitle:   JSP MyBatis를 활용한 메모장 구현하기
category:   JAVA
---

<!-- Start Writing Below in Markdown -->

![Description](https://alalstjr.github.io/jjunpro.github.io/img/2019/05/2019-05-22-3.jpg)

# MyBatis

1. 개발자가 지정한 SQL, 저장프로시저를 지원하는 프레임워크

2. 프로그램 소스 안에 SQL문을 작성하던 기존 JDBC 방식과 달리 SQL문을 프로그램에서 분리하여 XML 파일에 별도로 작성

3. MyBatis의 장점
  - 코딩량 절감
  - 간편한 유지보수 (SQL을 변경하고자 할 경우 기존처럼 프로그램을 수정하는 것이 아니라 
  XML 파일의 SQL문만을 변경하면 되기 때문에 SQL변환이 자유로움)
  
4. ibatis 라는 이름으로 2.5까지 개발

5. 3.0 버전부터 MyBatis로 이름이 바뀜

6. https://blog.mybatis.org/p/products.html 설치 주소

7. MyBatis 설정 방법
  - MyBatis-x.x.x.jar lib 폴더에 복사
  - MyBatisManager.java - MyBatis framework을 실행할 수 있는 세션
  - sqlMapConfig.xml - MyBatis 기본설정 파일
  - mapper 파일 - 실제 sql query문장
  
# MyBatis를 활용한 한줄 메모장

web.xml (배치기술서)

Controller
  - MemoController.java
  
Model
  - MemoDTO.java
  - MemoDAO.java

View
  - memo.jsp : ajax 요청 페이지, 메모입력
  - memo_list.jsp : 메모목록
  - memo_view.jsp : 메모 보기, 수정, 삭제 기능
  
## CRUD

- Create : insert
- Read : select
- Update : update
- Delete : delete

## 메모장 목록

list.do (web.xml에 맵핑)

Controller
  - MemoController.java

Model
  - MemberDAO.java
  - MemberDTO.java
  
View
  - memo_list.jsp
  
list.do => MemoController.java => MemoDAO.java = > 메모리스트 리턴 =>
request객체에 저장 => memo_list.jsp로 포워딩

# 실습코드예제

<a href="https://github.com/alalstjr/Java-study/tree/master/190520-MyBatis%ED%99%9C%EC%9A%A9%20%EB%A9%94%EB%AA%A8%EC%9E%91%EC%84%B1%20%EC%98%88%EC%A0%9C%20%EC%BD%94%EB%93%9C">Java 코드 저장소</a>

# mySql memo table 생성

CREATE TABLE memo ( <br/> 
&nbsp;&nbsp;num int NOT NULL PRIMARY KEY AUTO_INCREMENT, <br/>
&nbsp;&nbsp;writer VARCHAR(50) NOT NULL, <br/>
&nbsp;&nbsp;memo VARCHAR(4000) NOT NULL, <br/>
&nbsp;&nbsp;post_date DATETIME DEFAULT CURRENT_TIMESTAMP <br/>
);

![Description](https://alalstjr.github.io/jjunpro.github.io/img/2019/05/2019-05-22-1.png)

메모 테이블의 num 값은 고유 값으로 지정하면서 게시글 작성시 자동으로 숫자가 카운트업 하도록 설정하였습니다. <br/>
메모작성시 자동으로 시간이 저장되도록 초기값을 CURRENT_TIMESTAMP 설정하였습니다.

# MyBatis 초기 설정

src/sqlmap/sqlMapConfig.xml 생성

<script src="https://gist.github.com/alalstjr/ad60332846afe2c8524a0cebf3238732.js"></script>

src/sqlmap/MyBatisManager.xml 생성

<script src="https://gist.github.com/alalstjr/1077d815d296bddab3a91279c4820c1e.js"></script>

## 싱글톤 패턴 사용

애플리케이션이 시작될 때 어떤 클래스가 최초 한번만 메모리를 할당하고(Static) 그 메모리에 인스턴스를 만들어 사용하는 디자인패턴.
고정된 메모리 영역을 얻으면서 한번의 new로 인스턴스를 사용하기 때문에 메모리 낭비를 방지할 수 있음

String resource = "sqlmap/sqlMapConfig.xml"; <br/>
Resources.getResourceAsReader(resource); 코드를 해석하면 <br/>
Java Resources의 src디렉토리에서 sqlmap/sqlMapConfig.xml 파일을 <br/>
Reader클래스를 이용해서읽어 들이겠다는 코드입니다.

# View Page memo.jsp 생성

WebContent/include/header.jsp

<script src="https://gist.github.com/alalstjr/51761a719a12fc7dedf6067290c561ea.js"></script>

WebContent/page/memo.jsp

<script src="https://gist.github.com/alalstjr/bd7802efaa6981088c7a6b5908754c78.js"></script>

WebContent/page/memo_list.jsp

<script src="https://gist.github.com/alalstjr/63bb4bd25f6ec407b799840792908155.js"></script>

WebContent/page/memo_view.jsp

<script src="https://gist.github.com/alalstjr/debbb10898eb859af0a8518448e6dd99.js"></script>

부트스트랩 공부할겸 활용하여 조금 보기 좋게 꾸며 보았습니다.

![Description](https://alalstjr.github.io/jjunpro.github.io/img/2019/05/2019-05-22-2.png)

# Memo DTO, DAO 생성

src/memo/dao/MemoDTO.java 생성

<script src="https://gist.github.com/alalstjr/44da010c2620e71a7618c1cda7deafcf.js"></script>

src/memo/dao/MemoDAO.java 생성

<script src="https://gist.github.com/alalstjr/9684521799d9db727f45b682a6752799.js"></script>

# 특정 상황

input에 태그를 입력하면 해당 태그의 효과가 적용됩니다.

## 문제

&lt;font color="red"&gt;Hello&lt;/font&gt; <br/>
&lt;xmp&gt; : 태그 입력시 html소스를 해석하지 않고 그대로 출력 
  
## 해결책

DAO에서 문자 변환 처리를 해서 값을 넘깁니다.

태그 문자를 변환해야 함 <br/>
&lt; = ＆lt; <br/>
&gt; = ＆gt; <br/>
공백문자 처리 
스페이스 = ＆nbsp;

replace메서드를 활용하여 문자를 치환함

# 쿼리 실행소 memo.xml 생성

src/memo/mapper/memo.xml 생성

<script src="https://gist.github.com/alalstjr/0c41cdcc2da06d942da99dfd92381ce9.js"></script>

memo.xml 의 namespace 와 select id 값은 MemoDAO의 설정한 값과 동일해야 합니다.

# MemoController 생성

<script src="https://gist.github.com/alalstjr/c3e45a38f03a1aac4d92c7953f3d44b9.js"></script>

# 참고자료

<a href="https://hyeonstorage.tistory.com/278">sqlMapConfig 코드</a>
<a href="https://hunit.tistory.com/200">sqlMapConfig-mysql 코드</a>
<a href="https://0taeng.tistory.com/26">[Oracle] CHAR, VARCHAR, VARCHAR2 [개발자 령탱]</a>
<a href="https://jsonobject.tistory.com/122">mysql date 기본값 설정</a>

## 실글톤 패턴
<a href="https://jeong-pro.tistory.com/86">싱글톤 패턴을 사용하는 이유</a>

## 부트스트랩
<a href="https://tworab.tistory.com/79">부트스트랩 테이블 꾸미기</a>
<a href="https://www.codingfactory.net/10731">부트스트랩 버튼색성</a>

## MySQL
<a href="https://all-record.tistory.com/104">JSP에서 DB연동 하기 - JNDI, DBCP(커넥션풀) 이용</a>
<a href="http://faq.hostway.co.kr/Linux_DB/7421">데이터 타입/MYSQL DATE</a>
<a href="https://wansdream.net/entry/MySQL-CONCAT-%ED%95%A8%EC%88%98%EB%A1%9C-2%EA%B0%9C-%EC%9D%B4%EC%83%81%EC%9D%98-%ED%95%84%EB%93%9C%EC%BB%AC%EB%9F%BC-%EA%B2%B0%ED%95%A9%ED%95%98%EA%B8%B0">MySQL CONCAT 함수로 2개 이상의 필드(컬럼) 결합하기</a>
<a href="https://webisfree.com/2014-01-28/[mysql]-%ED%95%84%EB%93%9C%EC%97%90%EC%84%9C-%ED%8A%B9%EC%A0%95%EB%AC%B8%EC%9E%90-%ED%8F%AC%ED%95%A8-%EB%98%90%EB%8A%94-%EC%A0%9C%EC%99%B8%ED%95%9C-db-%EA%B2%80%EC%83%89-like-not">필드에서 특정문자 포함 또는 제외한 DB 검색, LIKE ,NOT</a>

<a href="https://zetawiki.com/wiki/MySQL_%EC%BB%AC%EB%9F%BC%EB%AA%85_%EB%B3%80%EA%B2%BD,_%EC%BB%AC%EB%9F%BC_%EC%9E%90%EB%A3%8C%ED%98%95_%EB%B3%80%EA%B2%BD">mysql 데이블 속성 변경</a>
<a href="http://blog.naver.com/PostView.nhn?blogId=imf4&logNo=220762181574">mysql 1씩 증가</a>
<a href="https://recoveryman.tistory.com/126">데이터 칼럼 구조</a>
