---
title: "[JAVA_Spring] JAVA Spring"
excerpt: "JAVA Spring 개요"

categories:
  - JAVA_Spring
tags:
  - [JAVA_Spring]

comments: true
toc: true
toc_sticky: true

date: 2021-08-05
last_modified_at: 2021-08-05
---


![image](https://user-images.githubusercontent.com/86935775/132630105-e375b3fa-a30e-45ed-b298-851bf80320cd.png)


# 제공 기능

스프링 프레임워크는 주요기능으로 **DI, AOP, MVC, JDBC** 등을 제공

- DI : Dependency Injection, 의존 주입
- AOP : Aspect Oriented Programming, 관점 지향 프로그래밍
- MVC : Model-View-Controller, 사용자 인터페이스, 데이터 및 논리 제어를 구현하는데 널리 사용되는 소프트웨어 디자인 패턴. 소프트웨어의 비즈니스 로직과 화면을 구분하며 더 나은 업무의 분리와 향상된 관리를 제공.
- JDBC : Java Database Connectivity, 자바에서 데이터베이스에 접속할 수 있도록 하는 자바 API. JDBC는 데이터베이스에서 자료를 쿼리하거나 업데이트하는 방법을 제공.

<br><br><br>

# 제공 모듈

- `spring-core` : 스프링의 핵심인 DI(Dependency Injection)와 IoC(Inversion of Control)를 제공

- `spring-aop` : AOP구현 기능 제공 spring-jdbc 데이터베이스를 쉽게(적은 양의 코드) 다룰 수 있는 기능 제공

- `spring-tx` : 스프링에서 제공하는 트랜잭션 관련 기능 제공

- `spring-webmvc` : 스프링에서 제공하는 컨트롤러(Controller)와 뷰(View)를 이용한 스프링MVC 구현 기능 제공

스프링 프레임워크에서 제공하고 있는 모듈을 사용하려면, 모듈에 대한 의존설정을 개발 프로젝트에 XML 파일등을 이용해서 개발자가 직접 하면 됨

<br>
<br>
<br>

# 스프링 컨테이너(IoC)

스프링에서 객체를 생성하고 조립하는 **컨테이너(container)** 로, 컨테이너를 통해 생성된 객체를 **빈(Bean)** 이라고 부른다.

<br><br>

## 기본 구조

`> src > main > java`

: java를 이용해 실제 기능 구현

<br>

`> src > main >resources`

: 보조적인 역할들의 파일 (스프링 설정 파일- XML, 프로퍼티 파일 등이 관리됨)

<br>
 

`applicationContext.xml`

스프링 컨테이너의 객체를 만들어주는 파일.

메모리의 스프링컨테이너에 로딩이 됨

<br>


`>`

`pom.xml` : 필요한 모듈을 가져오는 기능

요즘은 xml 대신 annotation 기능을 사용하기도 함

<br><br>

## 주요 개념

`Maven` : 라이브러리를 연결해주고 빌드를 위한 플랫폼

 
`Module` : 라이브러리

`pom.xml`에 필요한 모듈(라이브러리)을 명시해놓으면 내 컴퓨터에 모듈을 import하여 사용할 수 있게 됨

라이브러리 한개를 추가해도 의존관계에 있는 다른 라이브러리를 함께 import함


## 일반 Java와 Spring의 차이

**Common Java Project** : Java 순수 언어로 프로젝트를 만들어 나감

**Spring Project** : `Spring Framework`는 Main Repository 수많은 Spring Module이 존재하고 있고 그것을 `pom.xml` 등을 이용해 쉽게 Module을 가져와 개발을 진행하게 됨