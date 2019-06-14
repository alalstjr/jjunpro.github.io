---
layout:     post
title:      JSP MyBatis 설문조사 만들기
author:     쭌프로
tags:       JAVA
subtitle:   MyBatis를 활용하여 설문조사 만들기
category:   JAVA
---

<!-- Start Writing Below in Markdown -->

![Description](https://alalstjr.github.io/jjunpro.github.io/img/java_bg.png)

# 설문조사 TABLE 만들기

CREATE TABLE survey ( <br/>
&nbsp;&nbsp;&nbsp; survey_num INT NOT NULL PRIMARY KEY AUTO_INCREMENT, <br/>
&nbsp;&nbsp;&nbsp; question VARCHAR(4000) NOT NULL, <br/>
&nbsp;&nbsp;&nbsp; ans1 VARCHAR(500) NOT NULL, <br/>
&nbsp;&nbsp;&nbsp; ans2 VARCHAR(500) NOT NULL, <br/>
&nbsp;&nbsp;&nbsp; ans3 VARCHAR(500) NOT NULL, <br/>
&nbsp;&nbsp;&nbsp; ans4 VARCHAR(500) NOT NULL, <br/>
&nbsp;&nbsp;&nbsp; status CHAR(1) DEFAULT '1' <br/>
);

INSERT INTO survey VALUES(1, "좋아하는 과일은 무엇입니까?", "사과", "배", "포도", "딸기", "1")

CREATE TABLE survey_result (
&nbsp;&nbsp;&nbsp; answer_num INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
&nbsp;&nbsp;&nbsp; survey_num INT NOT NULL REFERENCES survey(survey_num),
&nbsp;&nbsp;&nbsp; num INT NOT NULL
);

## 응답 결과 백분율 SQL View 테이블 만들어 활용하기

create view survey_v as
select survey_num, num, count(*) sum_num,
	round((select count(*) from survey_result
		where survey_num = s.survey_num and num = s.num) * 100.0 /
		(select count(*) from survey_result
		where survey_num = s.survey_num), 1) rate
from survey_result s
where survey_num = 2
group by survey_num, num
order by num;


# 실습코드예제

<a href="https://github.com/alalstjr/Java-study/tree/master/190520-MyBatis%ED%99%9C%EC%9A%A9%20%EB%A9%94%EB%AA%A8%EC%9E%91%EC%84%B1%20%EC%98%88%EC%A0%9C%20%EC%BD%94%EB%93%9C">Java 코드 저장소</a>

# 참고자료

## MySQL
<a href="https://m.blog.naver.com/PostView.nhn?blogId=seilius&logNo=130165456506&proxyReferer=https%3A%2F%2Fwww.google.com%2F">[MySQL] View 테이블 만들기 </a>
