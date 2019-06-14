---
layout:     post
title:      JSP request method 모음
author:     쭌프로
tags:       JAVA JSP
subtitle:   JSP 내장 객체 모음
category:   JAVA
---

<!-- Start Writing Below in Markdown -->

![Description](https://alalstjr.github.io/jjunpro.github.io/img/java_bg.png)

# JSP 기본 내장객체 모음

void removeAttribute(key) 키값이 key인 객체를 삭제한다. <br/>
Enumeration getAttributeNames() 관련된 모든 속성의 이름을 읽어 들인다. <br/>
 
request 객체에서 제공하는 파라미터와 관련된 메소드 <br/>
getParameterNames() 모든 파라미터의 이름을 구한다. <br/>
getParameter(String name) 지정한 이름을 가진 파라미터 중 첫 번째 파라미터 값을 구한다. <br/>
getParameterValues(String name) 지정한 이름을 가진 파라미터의 모든 값을 String[]으로 구한다.

# 요청 해더 및 기타 요청 관련 메소드

getHeaderNames() 요청과 관련된 모든 해더의 이름을 구한다. <br/>
getHeader(name) 이름이 name인 해더의 값을 String으로 구한다. <br/>
getHeader(name) 이름이 name인 모든 헤더의 값을 String[]으로 구한다. <br/>
getIntHeader(name) 이름이 name인 헤더의 값을 int형으로 구한다. <br/>
getDateHeader(name) 이름이 name인 헤더의 값을 long형으로 구한다. <br/>
getCookies() 요청과 관련된 모든 쿠키를 구한다. <br/>
getMethod() 요청 방식이 GET인지 POST인지 구한다. <br/>
getRequestURI() HTTP 요청 URL에서 줄에 있는쿼리 문자를 제외한 부분을 구한다. <br/>
getQueryString() 요청한 URL다음에 오는 쿼리 문자열을 구한다. <br/>
getSession(flag) 요청과 관련된 세션 객체를 구한다. 만약 세션이 존재하지 않고 flag가 true이면 새로운 세션 객체를 생성한다. <br/>
getRequestDispatcher(path) 지정한 로컬 URL에 대한 요청 Dispatcher를 구한다. <br/>
getRemoteHost() 요청한 호스트의 완전한 이름을 구한다. <br/>
getRemoteAddr() 요청한 호스트의 네트워크 주소를 구한다. <br/>
getRemoteUser() 요청한 사용자의 이름이 존재할 경우 구한다. <br/>
getSession() 요청과 관련된 세션 객체를 구한다. 만약 존재하지 않으면 새로 생성한다. <br/>
getCharacterEncoding() 요청에서 사용된 인코딩을 구한다. <br/>
setCharacterEncoding(env) 요청에서 사용된 인코딩을 env로 지정한다.  
 
# 요청 관련 정보 

요청 방식: <%= request.getMethod() %> <br/>
요청 URI: <%= request.getRequestURI() %> <br/>
요청 프로토콜: <%= request.getProtocol() %> <br/>
서블릿 경로: <%= request.getServletPath() %> <br/>
요청 쿼리 스트링: <%= request.getQueryString() %> <br/>
서버 이름: <%= request.getServerName() %> <br/>
서버 포트: <%= request.getServerPort() %> <br/>
클라이언트 접속 주소: <%= request.getRemoteAddr() %> <br/> 
클라이언트 접속 호스트: <%= request.getRemoteHost() %> <br/>
인증 스키마: <%= request.getAuthType() %> <br/>
로케일: <%= request.getLocale() %> <br/>
사용하는 브라우저: <%= request.getHeader("User-Agent") %> 

response 기본 객체 헤더 및 응답의 컨텐트 타입 설정과 관련된 메소드 <br/>
addCookie(Cookie) 응답에 지정한 쿠키를 저장한다. <br/>
containsHeader(header) 이름이 header인 헤더를 포함하고 있는지 검사한다. <br/>
setHeader(name,value) 이름이 name인 헤더의 값을 value로 지정한다. <br/>
setIntHeader(name,value) 이름이 name인 헤더의 값을 int형 값인 value로 지정한다. <br/>
setDateHeader(name,date) 이름이 name인 헤더의 값을 long형 값이 date로 지정한다. <br/>
addHeader(name,value) 이름이 name이고 값이 String형 value인 헤더를 추가한다. <br/>
addIntHeader(name,value) 이름이 name이고 값이 Int형 value인 헤더를 추가한다. <br/>
addDateHeader(name,value) 이름이 name이고 값이 long형 date인 헤더를 추가한다.

<% <br/>
response.setHeader("Pragma","no-cache"); <br/>
if(request.getProtocol().equals("HTTP/1.1")) { <br/>
    response.setHeader("Cache-Control","no-cache"); <br/>
} <br/>
%>
 
 
response 기본 객체가 응답 내용 형식을 지정하는 메소드 <br/>
setContentType(String) MIME 타입을 지정하며, 추가적으로 글자의 인코딩 타입을 지정할수 있다. <br/>
getCharacterEncoding() 응답하는 내용의 캐릭터 인코딩 형태를 구한다.
 
URL 재작성과 관련된 response 객체의 메소드 <br/>
encodeRedirectURL(url) 세션 정보를 포함하기 위해 sendRedirect()메소드에서 사용할 URL을 인코딩한다. <br/>
encodeURL(name) 세션 정보를 포함하고 있는 링크에서 사용할 URL을 인코딩한다. <br/>
sendRedirect(url) 지정한 리다이렉트 URL을 사용하여 브라우저에 리다이렉트 응답을 보낸다.
 
<% <br/>
String val = request.getParameter("val"); <br/>
if (val == null || val.equals("")) { <br/>
   response.sendRedirect("http://localhost:8080/"); <br/>
} else if (val.equals("a")) { <br/>
   response.sendRedirect("http://localhost:8080/requestMethod.jsp"); <br/>
} else { <br/>
   %> <html> <head><title>오류</title></head> <body> 잘못된 파라미터를 입력하셨습니다. <p> 파라미터 "val"의 값은 없거나 "a"이어야 합니다. </body> </html> <% <br/>
} <br/>
%>

# 출처

<a href="http://bamtol.net/v5/bbs/board.php?bo_table=pp_server&wr_id=9">밤톨 넷 JSP 기본 내장객체 모음</a>
