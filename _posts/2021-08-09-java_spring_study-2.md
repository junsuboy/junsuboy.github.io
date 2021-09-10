---
title: "[JAVA_Spring] @Autowired, @Resource @Inject"
excerpt: "의존성 주입 Annotation에 대해 알아보자"

categories:
  - JAVA_Spring
tags:
  - [JAVA_Spring]

comments: true
toc: true
toc_sticky: true

date: 2021-08-09
last_modified_at: 2021-08-09
---

# 1. @Autowired

`@Autowired` 는 주입하려고 하는 객체의 타입이 일치하는 객체를 자동으로 주입한다.
`@Autowired` 는 필드, 생성자, Setter에 붙일 수 있다.

단, `@Autowired` 를 필드, Setter에 붙여서 사용할 경우 반드시 기본 생성자가 정의되어 있어야 한다.

<br><br>

## 1) @Autowired - 필드 주입

```java
public class WordRegisterServiceUseAutowired {

	@Autowired
	private WordDao wordDao;

	public WordRegisterServiceUseAutowired() { }
}
```

<br><br>

## 2) @Autowired - 생성자 주입

```java
public class WordRegisterServiceUseAutowired {

	private WordDao wordDao;

	@Autowired
	public WordRegisterServiceUseAutowired(WordDao wordDao) {
		this.wordDao = wordDao;
	}
}
```

<br><br>

## 3) @Autowired - Setter 주입

public class WordRegisterServiceUseAutowired {

    private WordDao wordDao;

    public WordRegisterServiceUseAutowired() { }

    @Autowired
    public void setWordDao(WordDao wordDao) {
    	this.wordDao = wordDao;
    }

}

<br><br>

## 4) @Qualifier 애노테이션

<br>

XML 설정 파일

```xml
<bean id="wordDao1" class="com.word.dao.WordDao" >
	 <qualifier value="usedDao"/>
</bean>
<bean id="wordDao2" class="com.word.dao.WordDao" />
<bean id="wordDao3" class="com.word.dao.WordDao" />
```

위와 같이 동일한 타입의 빈 객체가 여러개 정의되어 있을 경우 우선적으로 사용할 빈 객체의 `<bean>` 태그 하위에 `<qualifier>` 태그를 설정한다.

<br><br>

자바 코드

```java
public class WordRegisterServiceUseAutowired {

	@Autowired
	@Qualifier("usedDao")
	private WordDao wordDao;

	public WordRegisterServiceUseAutowired() { }
}
```

그리고 자바 코드에서는 `@Autowired` 와 함께 `@Qualifier` 를 사용해서 `@Qualifier` 에 XML 설정 파일에서 설정한 `<qualifier>` 태그의 `value` 값을 지정해준다.

이렇게 하면 동일한 타입의 빈이 여러 개일 경우 우선적으로 특정 빈이 주입된다.

<br><br><br>

# 2. @Resource

`@Resource`는 주입하려고 하는 객체의 이름(id)이 일치하는 객체를 자동으로 주입한다.
`@Resource` 는 Java 제공 애노테이션이며 필드, Setter에 붙일 수 있다. 생성자에는 붙일 수 없다.

`@Autowired` 와 마찬가지로 반드시 기본 생성자가 정의되어 있어야 한다.

<br><br>

## 1) 의존성 설정

```xml
<dependency>
    <groupId>javax.annotation</groupId>
    <artifactId>javax.annotation-api</artifactId>
    <version>1.3.2</version>
</dependency>
```

프로젝트에서 사용하기 위해 `javax.annotation-api` 의존성을 추가한다.

<br><br>

## 2) @Resource - 필드 주입

import javax.annotation.Resource;

public class WordRegisterServiceUseResource {

    @Resource
    private WordDao wordDao;

    public WordRegisterServiceUseResource() { }

}

<br><br>

## 3) @Resource - Setter 주입

import javax.annotation.Resource;

public class WordRegisterServiceUseResource {

    private WordDao wordDao;

    public WordRegisterServiceUseResource() { }

    @Resource
    public WordRegisterServiceUseResource(WordDao wordDao) {
    	this.wordDao = wordDao;
    }

}

<br><br><br>

# 3. @Inject

`@Inject` 는 `@Autowired` 와 유사하게 주입하려고 하는 객체의 타입이 일치하는 객체를 자동으로 주입한다.
`@Resource` 는 Java 제공 애노테이션이며 필드, 생성자, Setter에 붙일 수 있다.

` @Autowired` 와 마찬가지로 필드, Setter에 사용할 경우 반드시 기본 생성자가 정의되어 있어야 한다.

<br><br>

## 1) 의존성 설정

```xml
<dependency>
    <groupId>javax.inject</groupId>
    <artifactId>javax.inject</artifactId>
    <version>1</version>
</dependency>
```

프로젝트에서 사용하기 위해 `javax.inject` 의존성을 추가한다.

<br><br>

## 2) @Inject - 필드 주입

```java
import javax.inject.Inject;

public class WordRegisterServiceUseAutowired {

	@Inject
	private WordDao wordDao;

	public WordRegisterServiceUseAutowired() { }
}
```

<br><br>

## 3) @Inject - 생성자 주입

```java
import javax.inject.Inject;

public class WordRegisterServiceUseAutowired {

	private WordDao wordDao;

	@Inject
	public WordRegisterServiceUseAutowired(WordDao wordDao) {
		this.wordDao = wordDao;
	}
}
```

<br><br>

## 4) @Inject - Setter 주입

```java
import javax.inject.Inject;

public class WordRegisterServiceUseAutowired {

	private WordDao wordDao;

	public WordRegisterServiceUseAutowired() { }

	@Inject
	public void setWordDao(WordDao wordDao) {
		this.wordDao = wordDao;
	}
}
```

<br><br>

## 5) @Named 애노테이션

`@Autowired` 의 `@Qualifier` 와 같이 사용할 수 있는 것이 `@Inject` 에서는 `@Named` 이다.

`@Qualifier` 와 달리 `@Named` 에는 빈 이름(id)를 지정하므로 `@Autowired` , `@Qualifier` 를 사용할때에 비해 XML 설정 파일이 다소 짧아진다는 특징이 있다.

<br><br>

XML 설정 파일

```xml
<bean id="wordDao1" class="com.word.dao.WordDao"/>
<bean id="wordDao2" class="com.word.dao.WordDao"/>
<bean id="wordDao3" class="com.word.dao.WordDao"/>
```

`<Qualifier>` 태그가 필요한 `@Qualifier`와 달리 `@Named`는 XML 설정 파일에 추가적으로 설정할 것이 없다.

<br><br>

자바 코드

```java
import javax.inject.Inject;
import javax.inject.Named;

public class WordRegisterServiceUseInject {

	@Inject
	@Named("wordDao1")
	private WordDao wordDao;

	public WordRegisterServiceUseInject() {

	}
}
```

`@Named` 에 빈 이름(id)를 지정한다.
