---
layout:     post
title:      JPA Repository 쿼리 limit 설정
author:     쭌프로
tags:       JAVA
subtitle:   포트폴리오 개발일지
category:   JAVA
---

<!-- Start Writing Below in Markdown -->

![Description](https://alalstjr.github.io/jjunpro.github.io/img/java_bg.png)
 
게시판의 이미지 업로드시 가장 먼저 올린 이미지를 게시판 썸네일로 등록하는 작업을 하는 도중 오류가 발생하여 해결하는 과정을 담은 글입니다.
 
fileBoNum {1} 이고 <br/>
fileType 이 {image} 이고 <br/>
FileNo 차순중 {첫번째} 칼럼만 불러온다.

아래 코드는 Spring JPA의 JpaRepository를 구현한 인터페이스에 쿼리 메소드 

{% highlight matlab %}
  @Repository
  public interface DBFileRepository extends JpaRepository<DBFile, String>{
    DBFile findByFileBoNumAndFileDivisionOrderByFileNoAsc(long num, int division);
  }
{% endhighlight %}

를 Spring JPA의 JpaRepository를 구현한 인터페이스에 쿼리 메소드를 작성하여 실행하였습니다.

DB에 File자료가 하나만 있을때는 쿼리를 한번 실행할때 정상적으로 값을 불러왔습니다.

> DBFile(id=d12d97b4-8187-4a15-bd6e-dea00e6f8515, fileNo=0, fileBoNum=1, fileName=2019-05-28-1.png, fileSize=48975, fileType=image/png, fileDivision=1, fileDownload=0, dateTime=2019-06-27T20:27:46.999113400)

문제는 File자료가 2개 이상 들어간 다음 쿼리를 실행하면 문제가 생겼습니다.

> query did not return a unique result: 2

첫번째 무슨 오류인지 구글링 검색을 해보았습니다.

출처 : http://javastoreroom.blogspot.com/2013/07/orghibernatenonuniqueresultexception.html

이 Exception에 대한 이유는 데이터베이스에서 하나 이상의 값에 액세스하고 있기 때문입니다. 이 문제를 해결할 수있는 해결책이 있습니다. 

1. 데이터베이스 값 (ID, 이름 등)이 고유 한 복제 수정인지 확인하십시오. 
2. 데이터베이스를 변경하지 않으려면 get (0)을 0 인덱스 값만 반환하십시오. 
3. 그렇지 않으면 uniqueResult ()를 List ()로 대체합니다. 

여러 오류 해결법이 있었지만 이해는 가지않아 참고만하였습니다.

두번째 logger 기록을 확인하였습니다.

{% highlight matlab %}
   쿼리실행 - 1
  Hibernate: select dbfile0_.id as id1_1_, dbfile0_.bf_datetime as bf_datet2_1_, dbfile0_.bf_bo_num as bf_bo_nu3_1_, dbfile0_.bf_file_division as bf_file_4_1_, dbfile0_.bf_file_download as bf_file_5_1_, dbfile0_.bf_file_name as bf_file_6_1_, dbfile0_.bf_no as bf_no7_1_, dbfile0_.bf_file_size as bf_file_8_1_, dbfile0_.bf_file_type as bf_file_9_1_ from upload_file dbfile0_ where dbfile0_.bf_bo_num=? and dbfile0_.bf_file_division=? order by dbfile0_.bf_no desc
  결과값 { DBFile(id=35a5dc62-9646-4851-9c90-218498ff3dfd, fileNo=0, fileBoNum=3, fileName=2019-05-28-1.png, fileSize=48975, fileType=image/png, fileDivision=1, fileDownload=0, dateTime=2019-06-27T20:30:42.411586500) }

  쿼리실행 - 2
  Hibernate: select dbfile0_.id as id1_1_, dbfile0_.bf_datetime as bf_datet2_1_, dbfile0_.bf_bo_num as bf_bo_nu3_1_, dbfile0_.bf_file_division as bf_file_4_1_, dbfile0_.bf_file_download as bf_file_5_1_, dbfile0_.bf_file_name as bf_file_6_1_, dbfile0_.bf_no as bf_no7_1_, dbfile0_.bf_file_size as bf_file_8_1_, dbfile0_.bf_file_type as bf_file_9_1_ from upload_file dbfile0_ where dbfile0_.bf_bo_num=? and dbfile0_.bf_file_division=? order by dbfile0_.bf_no desc
  결과값 { error }

  2019-06-27 20:30:42.532 ERROR 20296 --- [nio-8080-exec-1] o.a.c.c.C.[.[.[/].[dispatcherServlet]    : Servlet.service() for servlet [dispatcherServlet] in context with path [] threw exception [Request processing failed; nested exception is org.springframework.dao.IncorrectResultSizeDataAccessException: query did not return a unique result: 2; nested exception is javax.persistence.NonUniqueResultException: query did not return a unique result: 2] with root cause
  javax.persistence.NonUniqueResultException: query did not return a unique result: 2
{% endhighlight %}

첫번째 결과값 데이터가 '하나' 일때는 정상 적으로 값을 가져오고 두번째 데이터가 2개로 쌓여있을때 오류가 발생하였습니다.
'뭘까 왜 두개일때는 오류가 나지..' 라는 생각으로 코드를 다시한번 읽어보았습니다.
읽어보니 조건으로 다 맞춰서 값은 가져오는데 모든 값을 가져오는 것이였습니다.

'FileNo 내림차순중 {첫번째} 칼럼만 불러온다.' 라고 주석걸어두고 쿼리를 작성했는데 빠트린것이였습니다..
그러다보니 값은 여러개 가져오는데 자료형은 배열도 리스트형도 아니라서 컴파일러가 혼돈이와서 망가진것이였습니다.

> DBFile[] findByFileBoNumAndFileDivisionOrderByFileNoAsc(long num, int division);

이런식으로 배열로 바꿔주면 정상적으로 값이 담기는 것을 확인할 수 있었습니다.

이제 코드를 수정해야할 단계입니다.

> DBFile findTop1ByFileBoNumAndFileDivisionOrderByFileNoAsc(long num, int division);

limit를 주는 메서드 네임은 findTop{num}By 입니다.

위 쿼리를 풀어서 다시 읽어보면

findTop1By 단 1개만 찾습니다,
FileBoNum 값이 num 인것 그리고
FileDivision 값이 division 인것 을 
FileNo 값을 오름차순으로 정렬해서 값을 가져옵니다.

# 결과

![Description](https://alalstjr.github.io/jjunpro.github.io/img/2019/06/2019-06-27-1.png)

이미지 파일 첨부를 3개 넣었습니다 그중에서도 2019-05-28-1.png 파일이 가장 위에 위치하고있습니다.
그렇다면 제가 원하는 쿼리 출력 모습은 세번 모두 2019-05-28-1.png 을 출력해야합니다.

{% highlight matlab %}
  Hibernate: select dbfile0_.id as id1_1_, dbfile0_.bf_datetime as bf_datet2_1_, dbfile0_.bf_bo_num as bf_bo_nu3_1_, dbfile0_.bf_file_division as bf_file_4_1_, dbfile0_.bf_file_download as bf_file_5_1_, dbfile0_.bf_file_name as bf_file_6_1_, dbfile0_.bf_no as bf_no7_1_, dbfile0_.bf_file_size as bf_file_8_1_, dbfile0_.bf_file_type as bf_file_9_1_ from upload_file dbfile0_ where dbfile0_.bf_bo_num=? and dbfile0_.bf_file_division=? order by dbfile0_.bf_no asc limit ?
  결과값 {DBFile(id=be5e6f85-da6e-4c1a-8953-14b4fe984606, fileNo=0, fileBoNum=2, fileName=2019-05-28-1.png, fileSize=48975, fileType=image/png, fileDivision=1, fileDownload=0, dateTime=2019-06-27T20:58:23.606149900)}

  Hibernate: select dbfile0_.id as id1_1_, dbfile0_.bf_datetime as bf_datet2_1_, dbfile0_.bf_bo_num as bf_bo_nu3_1_, dbfile0_.bf_file_division as bf_file_4_1_, dbfile0_.bf_file_download as bf_file_5_1_, dbfile0_.bf_file_name as bf_file_6_1_, dbfile0_.bf_no as bf_no7_1_, dbfile0_.bf_file_size as bf_file_8_1_, dbfile0_.bf_file_type as bf_file_9_1_ from upload_file dbfile0_ where dbfile0_.bf_bo_num=? and dbfile0_.bf_file_division=? order by dbfile0_.bf_no asc limit ?
  결과값 {DBFile(id=be5e6f85-da6e-4c1a-8953-14b4fe984606, fileNo=0, fileBoNum=2, fileName=2019-05-28-1.png, fileSize=48975, fileType=image/png, fileDivision=1, fileDownload=0, dateTime=2019-06-27T20:58:23.606149900)}

  Hibernate: select dbfile0_.id as id1_1_, dbfile0_.bf_datetime as bf_datet2_1_, dbfile0_.bf_bo_num as bf_bo_nu3_1_, dbfile0_.bf_file_division as bf_file_4_1_, dbfile0_.bf_file_download as bf_file_5_1_, dbfile0_.bf_file_name as bf_file_6_1_, dbfile0_.bf_no as bf_no7_1_, dbfile0_.bf_file_size as bf_file_8_1_, dbfile0_.bf_file_type as bf_file_9_1_ from upload_file dbfile0_ where dbfile0_.bf_bo_num=? and dbfile0_.bf_file_division=? order by dbfile0_.bf_no asc limit ?
  결과값 {DBFile(id=be5e6f85-da6e-4c1a-8953-14b4fe984606, fileNo=0, fileBoNum=2, fileName=2019-05-28-1.png, fileSize=48975, fileType=image/png, fileDivision=1, fileDownload=0, dateTime=2019-06-27T20:58:23.606149900)}
{% endhighlight %}

쿼리문도 제가 원하는 값으로 나왔으며 결과값 또한 정상적으로 원하는 값이 세번 똑같이 나왔습니다.


