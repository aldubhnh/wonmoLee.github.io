---
layout: post
title: "Filter, Interceptor"
date: 2020-07-09 21:00:00 +0700
categories: [Spring]
tags: [Spring, 스프링, Filter, Interceptor, AOP]
toc: true
toc_sticky: true
---



![](https://t1.daumcdn.net/cfile/tistory/997BAE4D5C8B3F7D10)



---

# Filter

>-Abstract-
>
>Filter : 요청과 응답을 걸러 정제하는 역할을 한다.



## Filter 개념

Filter는 J2EE의 표준이며 Servlet2.3부터 지원되는 기능이다.

Filter는 Servlet Container에 의해 동작이 제어되는 Java Class로 HTTP Request가 Service에 도착하기전, HTTP Response가 Client에 도착하기 전에 제어하는 역할을 한다.

Request를 처리할 때에 Dispatcher Servlet이 작업을 처리하기 전에 동작하고 Response를 처리할 때엔 Dispatcher Servlet에 의해 작업이 끝난 이후 동작한다. 또한 자원의 처리가 끝난 후 응답내용에 대해서도 변경하는 처리를 할 수 있다. 보통 web.xml에 등록하고, 일반적으로 인코딩 변환 처리, XSS방어 등의 요청에 대한 처리로 사용된다.



## Filter의  실행메서드

- init() - 필터 인스턴스 초기화
- doFilter()  - 전/후 처리
- destroy() - 필터 인스턴스 종료

```java
public interface Filter {

public void init(FilterConfig filterConfig) throws ServletException;

public void doFilter(ServletRequest request, ServletResponse response,
FilterChain chain)
throws IOException, ServletException;

public void destroy();
}
```



&nbsp;

# Interceptor

>-Abstract-
>
>Interceptor : 요청과 응답을 가로채는 역할을 한다.



## Interceptor 개념

Filter는 스프링 컨텍스트 외부에 존재하면서 스프링과 무관한 자원에 대해 동작하는 반면, Interceptor는 스프링의 DispatcherServlet이 컨트롤러를 호출하기 전, 후로 끼어들기 때문에 스프링 컨텍스트(Context, 영역) 내부에서 컨트롤러(Handler)에 관한 요청과 응답에 대해 처리한다.

Interceptor는 스프링의 모든 빈 객체에 접근할 수 있으며, Interceptor는 여러개를 사용할 수 있고 로그인 체크, 권한 체크, 프로그램 실행시간 계산작업, 로그확인 등의 업무처리에 활용된다.



## Interceptor의 실행메서드

- preHandler() - 컨트롤러 메서드가 실행되기 전
- postHandler() - 컨트롤러 메서드 실행 직 후 view페이지 렌더링 되기 전
- afterCompletion() - view페이지가 렌더링 되고 난 후

```java
public interface HandlerInterceptor {

    boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler)
            throws Exception;

    void postHandle(
            HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView)
            throws Exception;

    void afterCompletion(
            HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex)
            throws Exception;

}

```