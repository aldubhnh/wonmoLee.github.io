---
layout: post
title: "AOP에 대하여"
date: 2020-07-10 12:00:00 +0700
categories: [Spring]
tags: [Spring, 스프링, AOP, 관점 지향 프로그래밍]
toc: true
toc_sticky: true
---



---

# AOP

> -Abstract-
>
> AOP는 애플리케이션 전체에 걸쳐 사용되는 기능을 재사용하도록 지원하는 것이다.



## AOP 개념

객체지향의 기본원칙을 적용하여도 핵심기능에서 부가기능을 분리하여 모듈화하는 것은 어려운일이다. 이러한 고충을 덜고자 탄생한 개념이 AOP이며 이러한 AOP는 애플리케이션에서의 기능분리와 핵심기능에서 부가기능을 분리하여 모듈화를 돕는다. 이렇게 분리한 부가기능을 Aspect라는 독특한 모듈형태로 만들어 설계하고 개발하는 방법을 AOP라고 하는 것이다.

AOP는 OOP가 가지는 문제점을 보완하기위해 나온 개념이라고 보면된다. AOP는 부가기능을 Aspect로 정의하며, 핵심기능에서 부가기능을 분리함으로써 핵심기능을 설계하고 구현할 때 객체지향적인 가치를 지킬 수 있도록 도와준다.



`AOP 예시`

![](https://t1.daumcdn.net/cfile/tistory/99F4E5475C722F6C09)

업무로직을 포함하는 기능을 `핵심기능`, 핵심기능을 도와주는 로깅, 보안, 트랜잭션을 `부가기능`이라고 부른다.



&nbsp;

## AOP 용어

- target

  - 핵심 기능을 담고 있는 모듈로 타겟은 부가기능을 부여할 대상이 된다.




- Advice

  - 타겟에 제공할 부가기능을 담고 있는 모듈이다.




- Join Point

  - Advice가 적용될 수 있는 위치를 의미한다.

  - 타겟 객체가 구현한 인터페이스의 모든 메서드를 의미한다.




- Pointcut

  - Advice를 적용할 타겟의 메서드를 선별하는 정규표현식이다.
  - Pointcut 표현식은 excution으로 시작하고 메서드의 Signature를 비교하는 방법을 주로 이용한다.




- Aspect

  - AOP의 기본 모듈이다.
  - Advice + Pointcut을 의미한다.
  - AOP개념을 적용하면 핵심기능 코드 사이에 침투된 부가기능을 독립적인 Aspect로 구분해 낼 수 있으며, 구분된 부가기능 Aspect를 런타임 시에 필요한 위치에 동적으로 참여하게 할 수 있다.
  - 싱글톤 형태의 객체로 존재한다.




- Advisor

  - Advice + Pointcut을 의미한다.

  - Spring AOP에서만 사용되는 용어이다.




- Weaving

  - Weaving은 Pointcut에 의해서 결정된 타겟의 Join Point에 부가기능을 삽입하는 과정을 말한다.
  - Weaving은 AOP가 핵심기능의 코드에 영향을 주지 않으면서 필요한 부가기능을 추가할 수 있도록 해주는 핵심적인 처리과정이다. 



&nbsp;

## Spring AOP 특징

- Spring은 proxy 기반 AOP를 지원한다.

  - Spring은 target객체에 대한 proxy를 만들어 제공한다.

  - target을 감싸는 proxy는 런타임에 생성된다.

  - proxy는 advice를 target객체에 적용하면서 생성되는 객체이다.




- proxy가 호출을 가로챈다.

  - proxy는 target객체에 대한 호출을 가로챈 다음 advice의 부가기능 로직을 수행하고 난 후에 target의 핵심기능 로직을 호출한다.(전처리 Advice)

  - target의 핵심기능 로직 메서드를 호출한 후에 부가기능을 수행하는 경우도 있다.



- Spring AOP는 메서드 조인 포인트만 지원한다.

  - Spring은 동적 proxy를 기반으로 AOP를 구현하므로 메서드 Join Point만 지원한다.

  - target의 메서드가 호출되는 런타임 시점에만 advice를 적용할 수 있다.

