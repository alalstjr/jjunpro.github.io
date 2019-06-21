---
layout:     post
title:      Java Spring 어노테이션 정리
author:     쭌프로
tags:       JAVA
subtitle:   Java Spring 어노테이션 정리 노트
category:   JAVA
---

<!-- Start Writing Below in Markdown -->

![Description](https://alalstjr.github.io/jjunpro.github.io/img/java_bg.png)

# @Column 

칼럼의 이름을 이용하여 지정된 필드나 속성을 데이블의 칼럼에 매핑한다.
생략되면 속성과 같은 이름의 칼럼으로 매핑된다.

> @Column(name = "bo_num", length = 10)

private Long num; 

일경우 bo_num 컬럼으로 매핑

https://www.slideshare.net/zipkyh/ksug2015-jpa2-jpa

# @ConfigurationProperties

- yaml파일 읽는다. default로 classpath:application.properties 파일이 조회된다. <br/>
속성 클래스를 따로 만들어두고 그 위에 (prefix="mail")을 써서 프로퍼티의 접두사를 사용할 수 있음 <br/>
mail.host = mailserver@mail.com <br/>
mail.port = 9000 <br/>
mail.defaultRecipients[0] = admin@mail.com <br/>
mail.defaultRecipients[1] = customer@mail.com <br/>

출처: https://jeong-pro.tistory.com/151 [기본기를 쌓는 정아마추어 코딩블로그]
