---
layout:     post
title:      Spring Security Filter Bean 주입받기
author:     쭌프로
tags:       JAVA Spring-Boot Spring-Security
subtitle:   Spring Security Filter Bean 주입받기
category:   JAVA
---

<!-- Start Writing Below in Markdown -->

![Description](https://alalstjr.github.io/jjunpro.github.io/img/java_bg.png

이번 Spring Security JWT 발급 Form Login 기능 만드는 공부를 하던중 
ObjectMapper 클래스를 주입받아 사용하려고 @Autowired 어노테이션으로 불러와 사용하였습니다.

> FormLoginFilter.java

~~~
public class FormLoginFilter extends AbstractAuthenticationProcessingFilter {

    @Autowired
    private ObjectMapper objectMapper;
    
    ...
~~~

> WebJsonConfig.java

~~~
@Configuration
public class WebJsonConfig {

    @Bean
    public ObjectMapper objectMapper() {
        ObjectMapper objectMapper = new ObjectMapper();
        return objectMapper;
    }
}
~~~

이상태로 objectMapper 확인해 보면 Null 값으로 Bean 값을 가져오지 못하는 상황이 발생하였습니다.

아무래도 IOC 컨테이너가 FormLoginFilter 상태를 알지 못해서 못불러오는거 같아서 
FormLoginFilter 클래스에 @Component 를 주어 IOC 컨테이너가 해당 클래스의 존재를 알 수 있도록 하였습니다.
하지만 에러가 발생하였습니다.

~~~
Description:
Parameter 0 of constructor in com.backend.koreanair.filter.FormLoginFilter required a bean of type 'java.lang.String' that could not be found.

Action:
Consider defining a bean of type 'java.lang.String' in your configuration.
~~~

개인적으로 검색 결과 이미 AbstractAuthenticationProcessingFilter 클래스에 Bean 으로 주입되어 있는 상태인데
커스텀 Filter 에 또 Bean 주입을 시도하려 해서 발생하는 오류인거 같았습니다. (쭌피셜)

이번엔 AbstractAuthenticationProcessingFilter Bean 주입 방법 으로 다시한번 더 검색하였습니다. 

https://stackoverflow.com/questions/48107157/autowired-is-null-in-usernamepasswordauthenticationfilter-spring-boot

저와 똑같은 상황의 개발자의 문의 그리고 답변이 있어서 참고하게 되었습니다.

IOC 컨테이너 ApplicationContext 를 WebSecurityConfig.java 에서 filter로 보내서 
직접적으로 Bean을 사용할 수 있도록 하는 방법이였습니다.

> WebSecurityConfig.java

~~~
@Configuration
@EnableWebSecurity
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {

    private FormLoginFilter formLoginFilter() throws Exception {
        FormLoginFilter filter = new FormLoginFilter("/api/account/login", getApplicationContext());
        filter.setAuthenticationManager(super.authenticationManagerBean());

        return filter;
    }
}
~~~

FormLoginFilter 클래스에 IOC 컨테이너 getApplicationContext를 보내줍니다.

> FormLoginFilter.java

~~~
public class FormLoginFilter extends AbstractAuthenticationProcessingFilter {
    ...
    
    @Autowired
    private ObjectMapper objectMapper;

    public FormLoginFilter(String defaultFilterProcessesUrl, ApplicationContext ctx) {
        super(defaultFilterProcessesUrl);
        this.objectMapper = ctx.getBean(ObjectMapper.class);
    }
    
    ...
}
~~~

이렇게 전달받은 ApplicationContext 에서 Bean 을 직접적으로 꺼내서 사용할 수 있습니다.

# AbstractAuthenticationProcessingFilter 상속받은 클래스에서 @Autowired 작동하지 않은 이유

https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/web/filter/GenericFilterBean.html?is-external=true

~~~
이 설계 방식의 이유-Spring 보안에서 지원하는 인증 처리 메커니즘은 확장되는 필터를 기반으로합니다 GenericFilterBean.
이 일반 필터 기본 클래스는 Spring ApplicationContext 개념에 종속 되지 않습니다 . 필터는 일반적으로 자체 컨텍스트를로드하지 않고 필터의 ServletContext를 통해 액세스 할 수 있는 Spring 루트 애플리케이션 컨텍스트에서 서비스 Bean에 액세스합니다 (WebApplicationContextUtils 참조).

따라서 ApplicationContext서비스 빈에 액세스하려면 필터에 를 제공해야합니다 .
~~~
