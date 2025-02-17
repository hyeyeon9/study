# 1. **Spring Framework**

: Road Johnson이 ‘Export One-on-One J2EE Development without EJB’ 책을 통해서 소개

- 2003년 2월부터 오픈 소스로 시작된 프로젝트

## 특징

- 경량의 컴포넌트
- **IoC ( Inversion of Control : 제어의 역행 ) 컨테이너** 기반에서 관리됨
    - Servlet/JSP가 tomcat 컨테이너에서 관리된 것과 유사
    - **클래스를 직접 생성하지 않고 의존성도 직접 설정하지 않는다. 모두 Spring에게 맡긴다.**
- JDBC 추상화 ( Mybatis 처럼 wrap한 클래스들 제공  ⇒ 예외처리 불필요 )
- **선언적 트랜잭션**  ( 어노테이션으로 트랜잭션 처리 가능 ⇒ **`@Transction`** 지정 )
    - 모두 성공하면 자동으로 commit, 하나라도 실패하면 모두 자동으로 rollback
- 다양한 뷰( html 화면 ) 기술 ( JSP, Thymeleaf, velocity 등 )
- 검증된 **Spring MVC 아키텍쳐 제공**
- REST API 지원 ( 클라이언트와 서버간에 JSON 데이터 포맷으로 통신하는 방법 )

## Spring Framework

https://spring.io/

- Spring Framework
- Spring Boot
- Spring AI
- Spring Security
- Spring Cloud
- …

## Spring Framework 버전

https://spring.io/projects/spring-framework#learn  

- 6.x 버전 ( 2022년 )
- JDK 17+

## 용어 정리

1. **POJO ( Plain Olld Java Object )**
    
    : **특정 프레임워크나 라이브러리에 종속되지 않는 순수한 Java 객체**를 의미
    
    - **어떠한 클래스 또는 인터페이스를 상속 및 구현하지 않아서 어떤 개발환경에서도 사용 가능한 특징**을 가진다.
    - Spring의 핵심 원칙
2. Java Beans
    - EJB 에서 사용했던 용어
    - 특정한 규칙을 가진다.
        - public 기본 생성자만 존재
        - getter / setter 메서드 존재
        - implements Serialzable
3. **Spring bean**
    
    **: POJO 기반의 Spring 어플리케이션에서 만든 모든 자바 클래스를 의미**
    
4. **Ioc ( Inversion of Control : 제어의 역행 )**
    
    : 필요한 빈(클래스)를 직접 생성하거나 bean 간의 **의존성을 직접 설정하지 않고 외부 컨테이너에서 설정하는 개념**
    
5. **IoC Container**
    
    : IoC 방법으로 빈(클래스)를 관리한다는 의미에서 IoC 컨테이너라고 부른다. 
    
    - 하드웨어 개념이 들어갔으나 일반 클래스이다. ( XXXApplicationContext : **클래스(빈)들을 관리하는 IoC 컨테이너 클래스** )
    - 계층 구조
        
        ```
        BeanFactory (인터페이스)  MessageSource(인터페이스)
        	         |		
        	 ApplicationContext (인터페이스, org.springframework.context) 
        			     |
           AnonotationConfigApplicationContext (클래스, Java SE 환경의 IoC Container)
           GenericXmlApplicationContext (클래스, 자바 SE 환경의 IoC Container)
           ...
          
           XXXWebApplicationContext (클래스, 자바 EE 환경의 IoC Container)
        ```
        
6. **의존성 주입 ( Dependency Injection : DI )**
    
    : 임의의 클래스에서 다른 클래스를 참조할 떄  **직접 생성하는 것이 아니라 외부에서 생성한 후 생성자 또는 setter 메서드를 이용해서 설정하는 방법**
    
    - **`생성자 주입`** ( **Constructor-based Dependency Injection** )
    - setter 메서드 주입 ( **Setter-based Dependency Injection** )

---

# 2. 환경 설정

1. **JDK 17 설치**
2. **SpringBoot 3.2.8** ( Spring Framework 6.X 내장됨 )
    - SpringBoot 3버전은 JDK 17+ 필요함
3. **개발툴 설치**
    
    https://spring.io/tools
    
    - STS ( Spring Tool Suite ) 를 지원
    - 현재 지원하는 종료 2가지
        - sts3 : Spring Framework와 Spring Boot 를 각각 개발할 수 있는 개발툴
        - sts4 : Spring Boot 만 지원되는 개발툴
    - **Spring Tool Suite 4**
        - 한글 인코딩 확인
            - window > preferences > General > workspace > 인코딩 UTF-8
        - JSP/CSS/js 사용을 위한 web 플러그인 추가
            - help > market place > Eclipse Enterprise Java and Web Developer 설치
4. **tomcat 설치 안 함**
    - **SpringBoot에서는 내장 tomcat 을 사용**한다.

---

# 3. SpringBoot 프로젝트 작성

- **로컬로 프로젝트 작성**
    
    STS  ⇒ File ⇒ New ⇒ Spring Starter Project
    
- **웹사이트 이용**
    - https://start.spring.io/
    - project : **maven 이용**

---

# 4. 빌드툴

: **개발할 때 도움받을 수 있는 도구**

- 전통적인 프로그램 개발 프로세스는 아래와 같다.
    - 소스 —> 필요한 jar 다운로드 및 컴파일 —> 단위테스트 —> 패키징 —> 배포
- 자동화 종류 2가지
    - **Maven**
        
        : **설정정보를 `pom.xml` 파일에 설정**
        
        - 빌드 과정 단계
            1. validate
            2. compile
            3. test
            4. package
            5. install ( 패키징 ) , clean ( 패키징 삭제 )
            6. deploy
    - Gradle
        
        : 설정정보를 build.gradle 파일에 설정
        
- **필요한 의존성을 설정하는 방법**
    
    https://mvnrepository.com/ 에서 필요한 키워드를 입력하고 maven ( pom.xml )또는 gradle 항목에서 복사해서 사용
    

---

# 5. maven 빌드툴의 기본 디렉터리 구조

- **`src/main/java`**
    
    : *.java 저장, 패키지 지정
    
- **`src/main/resources`**
    
    : *.java 제외한 나머지 파일 저장  ( jdbc.properties, Configuration.xml, Mapper.xml 등 )                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                
    
- **`src/test/java`**
    
    : 단위 테스트용 .*java 저장
    
- **`src/test/resources`**
    
    : 단위 테스트용 *.java 가 필요한 파일 저장
    
- **`JRE System Library`**
    
    **`Maven Dependency`**
    
    : **`pom.xml` 에 등록된 의존성 파일들(*.jar)이 저장**
    
    - 기본 저장 디렉터리는 **C:\사용자\.m2\repository** 이다.
        - 네트워크 이슈로 가끔 다운로드가 안 되는 경우가 발생할 수 있음 ( repository.zip )
- **`pom.xml`**
    
    : 전반적이 **설정정보 저장**
    
    ( 버전, 의존성파일, …)
    
    - 계층구조로 되어 있음 ( 부모에 해당되는 pom.xml이 있음 )

---

# 6. Application 파일

: `src/main/java`에 저장되어 있고 **반드시 필요한 코드**

- **프로그램 시작점 역할**

```java
@SpringBootApplication
public class DemoApplication {

	public static void **main**(String[] args) {
		SpringApplication.run(DemoApplication.class, args);
		System.out.println("DemoApplication");
	}

}
```

- SpringBoot  웹 어플리케이션 개발시 배포는 jar로도 가능하다. **main 메서드**를 가지고 있기 때문이다. ( 일반적으로 비웹은 jar로 배포, 웹은 war로 배포함 )

## **@SpringBootApplication 의 3가지 기능**

https://docs.spring.io/spring-boot/reference/using/using-the-springbootapplication-annotation.html

- [`@EnableAutoConfiguration`](https://docs.spring.io/spring-boot/3.4.1/api/java/org/springframework/boot/autoconfigure/EnableAutoConfiguration.html) : **`pom.xml` 에 `<dependency>`태그로 등록된 라이브러리**를 보고, 그에 알맞는 **최적의 설정정보를 `자동으로 설정`**한다.
    - 예 > spring-boot-starter-web 을 지정하면 자동으로 웹어플리케이션 개발을 위한 설정들이 자동으로 셋팅된다.
- [`@ComponentScan`](https://docs.spring.io/spring-framework/docs/6.2.x/javadoc-api/org/springframework/context/annotation/ComponentScan.html) : **자동으로 빈(클래스) 를 찾아서 `new` 를 한다. 또한 의존성 주입 (@Autowired)이 가능하도록 한다.**
- [`@SpringBootConfiguration`](https://docs.spring.io/spring-boot/3.4.1/api/java/org/springframework/boot/SpringBootConfiguration.html) : 자동으로 추가되는 설정 이외의 **개발자가 필요시 추가적인 Configuration 설정이 가능**

✅ **정리**

- **`@EnableAutoConfiguration` 덕분에 pom.xml 에 의존성 파일을 추가하면 스프링 부트가 자동으로 환경을 감지하고 필요한 설정을 진행한다.**
- **`@ComponentScan` 은 `@Component`, `@Service`, `@Controller`, `@Repository` 가 붙은 클래스를 자동으로 찾아서 빈으로 등록한다.**
- **`@SpringBootConfiguration` 은 개발자가 추가적인 설정을 정의할 수 있도록 한다. 주로 `@Bean` 을 사용해서 특정 객체를 수동으로 빈으로 등록할 때 사용한다.**

---

# 7. Spring boot의 추가적인 설정 정보 방법

: **`src/main/resource/application.properties`** 에 설정

예 > DB연동시 필요시 4가지 정보,

   tomcat의 port 번호, …

   jsp 경로를 위한 prefix, suffix, .. 등등

---

# 8. 로깅 (logging) 처리

## 1) 개념

: 어플리케이션을 개발할 떄 문제가 발생되면 대부분 콘솔 정보를 보고 문제를 해결한다. 이때 **콘솔에 출력되는 정보를 로그**라고 부른다.

- 필요시 로그 출력은 이전에는 `System.out.println` 으로 해결했으나 앞으로는 **전문적인 로그 관리 라이브러리를 사용**해야 한다.
- **대표적인 로그 관리 라이브러리**
    - log4j (구현체)
    - logback (구현체, 스프링부트 기본 로그)
- **`SLF4j`**
    
    : 인터페이스로서 `Log4j` 와 `Logback` 구현체들이 `SLF4j` 인터페이스를 상속해서 만들어진다. 따라서 실제로 `SLF4j` 사용하면 `Log4j` 에서 `logback` 으로 변경시 코드를 수정할 필요가 없다.
    
- **로그 레벨 5가지**
    - `trace`
    - `debug`
    - `info ( 기본 )`
    - `warn`
    - `error`
    
    동작방식은 지정된 레벨 및 하위까지 포함해서 로그가 출력된다.
    
- **구현 방법**
    1. **Logger 생성**
        
        **//  Logging의 인터페이스 기능인 slf4j 사용**
        
        **`import org.slf4j.Logger;`**
        
        **`import org.slf4j.LoggerFactory;`**
        
        **`Logger logger = LoggerFactory.getLoger( 클래스명.class );`**
        
    2. **로그레벨에 해당되는 메서드 호출**
        - **`logger.trace | debug | info | warn | error(값);`**
        
        ```java
        package com.exam;
        
        import org.slf4j.Logger;
        import org.slf4j.LoggerFactory;
        
        @SpringBootApplication
        public class Application implements CommandLineRunner{
        	
         	 // 1. Logger 얻기
        	 Logger logger = LoggerFactory.getLogger(getClass());                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             
        
        	public static void main(String[] args) {
        		SpringApplication.run(Application.class, args);
        	}
        
        	@Override
        	public void run(String... args) throws Exception {
        		System.out.println("Application");
        		// 2. log 레벨 메서드 호출
        		**logger.trace("trace 입니다.");
        		logger.trace("trace {} ","입니다."); // {}에 "입니다"갸 치환돼서 들어감
        		logger.debug("debug {} ","입니다.");
        		logger.info("info {} ","입니다."); // info가 기본이라 info부터 하위까지(warn, error) 실행됨
        		logger.warn("warn {} ","입니다.");
        		logger.error("error {} ","입니다.");**
        		}
        }
        ```
        
    3. **application.properties 에셔 로그레벨 변경**
        - **문법** : **`logging.level.클래스명 =`**
        - **`logging.level.root = warn`**  :  **`warn | error`**
            
            ![image (28)](https://github.com/user-attachments/assets/14a40e85-9689-4588-8fa8-e8a889c5b2ca)

            
        - **`logging.level.root = debug`**  : **`debug | info | warn | error`**
            
           ![image (29)](https://github.com/user-attachments/assets/6a4372db-3265-47d0-997f-46ddcbc0a1f0)

            
        - **특정 패키지에서의 로그레벨 지정 가능**
            - **`logging.level.com.exam = warn`**
                - `com.exam` 패키지는 `warn` 레벨부터 로그가 찍힌다.
        - **로그파일 저장 가능**
            - [**`logging.file.name](http://logging.file.name/) = C:\\Temp\\app.log`**
                - 지정한 위치에 로그 파일이 저장된다.
             
---
# 9. 빈 (Bean)

## 1) 개념

: **Spring IoC 컨테이너가 관리하는 객체**를 의미한다. **개발자가 직접 객체를 생성(new)하지 않고, 스프링이 객체를 생성하고 관리한다.**

- **직접 new 하지 않는다.**

## 2) 빈 생성 방법

https://docs.spring.io/spring-boot/reference/using/structuring-your-code.html

- **자동 빈 생성 방법**
    
    : 권장하는 방법은 권장패키지 구조를 이용하는 것이다.
    
    - step 1 : **권장패키지 구조**를 이용하기
        - **`@SpringBooApplication` 어노테이션이 있는 클래스의 패키지와 하위 패키지만 스프링이 스캔**하기 때문에, 빈으로 생성하고 싶은 클래스는 반드시 하위 패키지로 들어가야 한다.
    - step 2 : **클래스에 어노테이션을 붙이면 자동으로 빈이 생성된다.**
        - **@Component**  : 범용적으로 사용
        - **@Service**          : ServiceImpl 역할
        - **@Repository**    : DAO 역할
        - **@Controller**     : 서블릿 역할
        - **@Configuration** : 설정 정보를 추가할 때 ( application.properties 대신에 )
        - **어노테이션에 이름 설정이 가능**하다.
            - @Repository("dao")

## 3) 빈 접근하는 방법

: **`ApplicationContext` 를 사용해서 빈에 접근할 수 있다.**

- **DeptDAO**

```java
@Repository
public class DeptDAO {
	private Logger logger = LoggerFactory.getLogger(getClass());                                                                                     
	public DeptDAO() {
		logger.info("Logger:{}", "DeptDAO 생성자");
	}
	
	// 데이터 리턴하는 메서드
	public List<String> list(){
		return Arrays.asList("홍길동", "이순신");
	}
}
```

- **DeptServiceImpl.java**

```java
@Service("xxx")
public class DeptServiceImpl implements DeptService {
	 private Logger logger = LoggerFactory.getLogger(getClass());   
	
	 // Service에서 DAO 접근하고자 한다. 
	 DeptDAO dao;
	 
	// 생성자 주입
	 public DeptServiceImpl(DeptDAO dao) {
		logger.info("Logger:{}", "DeptServiceImpl 생성자" + dao);
		this.dao = dao;
	}
	 
     // 데이터 리턴하는 메서드
	public List<String> list(){
			return dao.list();
	}
}
```

- **Application.java**

```java
@SpringBootApplication
public class Application implements CommandLineRunner{
	
	// 서비스에 접근하기 위해서 일단 컨텍스트에 먼저 접근해야한다.
	@Autowired
	ApplicationContext ctx;
	// AnnotationConfigApplicationContext
	
	// 1. Logger 얻기
	private Logger logger = LoggerFactory.getLogger(getClass());                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                
	public static void main(String[] args) {
		SpringApplication.run(Application.class, args);
	}

	@Override
	public void run(String... args) throws Exception {
		logger.info("Logger : {}","Application " + ctx);
		
		// 빈 참조
		DeptServiceImpl service =  ctx.getBean("xxx", DeptServiceImpl.class);
		
		List<String> list = service.list();
		logger.info("List : {}", list); // List : [홍길동, 이순신]
	}
}
```

- **`@Autowired ApplicationContext ctx;`**
    - `ctx`는 **Spring IoC 컨테이너**를 나타내며, ***빈을 검색하거나 가져오는 작업을 처리***
    - **`@Autowired`** 를 사용하면 Spring이 `ApplicationContext` 을 자동으로 주입
- **`DeptServiceImpl service =  ctx.getBean("xxx", DeptServiceImpl.class);`**
    - Spring 컨테이너에서 이름이 `“xxx”`인 빈을 검색한다.
    - 검색된 빈의 타입은 `DeptServiceImpl` 이어야 한다.
    - 검색된 빈은 `service` 변수에 주입된다.
    - 이후 service를 통해 빈의 메서드를 호출하거나 참조할 수 있다.

 ---
 # 13. 빈 스코프 (Bean Scope)

https://docs.spring.io/spring-framework/reference/core/beans/factory-scopes.html#page-title

## 1) 개념

: Spring에서 빈은 기본적으로 **싱글톤**으로 관리된다. 

**싱글톤은 ApplicationContext(스프링 컨테이너)에서 단 한번만 생성되는 것으로,** 여러번 빈을 요청해도 항상 동일한 인스턴스(100번지)를 반환해준다.

- 필요에 따라서 다른 스코프로 빈을 설정할 수 있다.

<aside>
💡

Spring 컨테이너와 ApplicationContext의 관계

- **Spring 컨테이너**
    
    : 스프링 애플리케이션의 생명주기를 관리하는 중앙 역할을 수행
    
    - 빈(Bean)을 관리하며, 의존성 주입과 같은 기능을 제공
- **ApplicationContext**
    - Spring 컨테이너의 구현체 중 하나
    - 가장 많이 사용되는 컨테이너로, BeanFactory를 확장한 인터페이스
        - 빈의 생성 및 관리
        - 빈 검색 (getBean)
        - 빈 생명주기 관리
</aside>

## 2) Scope의 종류

### **1. Singleton Scope**

: 기본 스코프로, 빈이 **단 한번만 생성**되어 빈을 여러번 요청해도 **항상 동일한 인스턴스를 반환한다.**

- 여러 사용자가 공유 가능
- **`스레드-언세이프`** : 동시에 여러 사용자가 사용하는 문제 발생 가능

### **2. Prototype Scope**

: 빈 요청 시마다 **매번 새로운 인스턴스를 생성해서 반환한다.**

- 여러 사용자 공유 불가능 (
- **`스레드-세이프`**

### **3. Request scope (웹 환경)**

: HTTP 요청마다 새로운 빈이 생성되고, 요청이 끝나면 소멸된다.

- HttpServletRequest scope와 동일한 라이프사이클

### **4. Session Scope (웹 환경)**

: Http 세션동안 하나의 빈이 유지된다. ( 하나의 브라우저 )

- HttpSession  scope와 동일한 라이프사이클

### **5. Application Scope** (웹 환경)

: 애플리케이션 전체에서 동일한 빈이 유지된다. ( 서버 다운동안 )

- ServletContext scope와 동일한 라이프사이클

## 3) scope 값 변경

: **`@Scope` 어노테이션**을 ****이용해서 scope를 설정할 수 있다. 

- **문법**
    - `@Scope(ConfigurableBeanFactory.SCOPE_SINGLETON)` == `@Scope("singleton")`
    - `@Scope(ConfigurableBeanFactory.SCOPE_PROTOTYPE)` == `@Scope("prototype")`
- **예제**
    
    ```java
    @Service("xxx")
    @Scope(value =  ConfigurableBeanFactory.SCOPE_PROTOTYPE)
    // @Scope("prototype") 도 가능
    public class DeptServiceImpl implements DeptService {
    	 private Logger logger = LoggerFactory.getLogger(getClass());   
    	
    	 // Service에서 DAO 접근하고자 한다. 
    	 DeptDAO dao;
    	 
    	// 생성자 주입
    	 public DeptServiceImpl(DeptDAO dao) {
    		logger.info("Logger:{}", "DeptServiceImpl 생성자" + dao);
    		this.dao = dao;
    	}
    }
    ```
    

# 14. 빈의 초기화 작업 및 소멸 작업 (cleanup)

: 서블릿의 lifecycle과 비슷한 개념으로, 애플리케이션의 시작 및 종료 시에 특정 작업을 수행한다. 

- **구현방법**
    
    : **`@PostConstruct`**
    
    - public void start()
    - **초기화 작업 메서드**에 사용
    - Spring 컨테이너가 빈을 생성한 후에 호출
    
      **`@PreDestroy`**
    
    - public void shutdown()
    - **소멸 작업 메서드**( cleanup )에 사용
    - Spring 컨테이너가 빈을 소멸하기 직전에 호출
    
- **예제**
    
    ```java
    @Controller(value = "TodoController") // value로 이름 지정 가능
    public class TodoController {
    	private  Logger logger = LoggerFactory.getLogger(getClass());
    	
    	// 생성자
    	public TodoController() {
    		logger.info("logger : {}", "TodoController 생성자");
    	}
    	
    	// 초기화 작업
    	@PostConstruct
    	public void init() {
    		logger.info("logger : {}", "init 메서드");
    	}
    
    	// cleanup 작업
    	@PreDestroy
    	public void clenup() {
    		logger.info("logger : {}", "clenup 메서드");
    	}
    }
    ```
    
    - **실행순서**
        - **빈 생성자가 가장 먼저 호출**
        - **@PostConstruct 호출로** init() 메서드 실행
        - **@PreDestroy** **호출** clenup() 메서드 실행
     
---
# 10. 의존성 주입 ( Dependency Injection : DI )

## 1) 개념

: 특정 A클래스가 다른 B클래스를 참조할 때 A클래스에서는 B의 참조변수가 필요하다. 이때, **외부에서 생성된 객체(B)를 A에게 전달하는 설계 패턴**이다

- **외부에서 필요한 객체를 넣어주는 개념**으로 **의존성 주입**이라고 한다.
- **클래스 간의 결합도를 낮추고, 유연성과 재사용성을 높일 수 있다.**

## 2) 의존성 주입 방법

### 1. 생성자 이용 (권장)

: 필요한 객체를 생성자를 통해 전달받아 의존성을 주입하는 방식이다.

- **생성자의 매개변수로 필요한 객체를 전달해, 생성자가 실행되면서 의존성이 주입된다.**

- **예제**

```
                              DeptService 
  Application.java    ←—→   DeptServiceImpl  ←—→  DeptDAO/UserDAO
```

```java
@Service
public class DeptServiceImpl implements DeptService {
	 private Logger logger = LoggerFactory.getLogger(getClass());   
	
	 // Service에서 DAO 접근하고자 한다. 
	 **DeptDAO deptDAO;
	 UserDAO userDAO;**
	 
	// 생성자 주입  ( 생성자를 통해서 deptDAO와 userDAO 각각의 번지가 서비스가 생성될떄 주입돼서 인스턴스 변수에 할당된다. )
	 **public DeptServiceImpl(DeptDAO deptDAO, UserDAO userDAO)** {
		logger.info("Logger:{}", "DeptServiceImpl 생성자" + deptDAO +" " +userDAO);
		// com.exam.dao.DeptDAO@e044b4a   com.exam.dao.UserDAO@11a82d0f
		this.deptDAO = deptDAO;
		this.userDAO = userDAO;
	}

}
```

- **`DeptServiceImpl`** 생성자에서 **`DeptDAO`**와 **`UserDAO`** 객체를 전달받아 인스턴스 변수에 저장한다.
- **생성자에 주입받고 싶은 객체를 매개변수로** 넣어주면 된다.
- **어떤 객체를 필요로 하는지 명시적으로 나타내기에 의존성을 분명**하게 확인 가능하다.

### 2. `@Autowired` 어노테이션 이용 ( 필드 주입 )

: `@Autowired` 을 사용해서 필드에 직접 의존성을 주입하는 방식

- 코드가 간결하지만 의존성이 숨겨져 있어 테스트나 유지보수가 어려울 수 있다.

- **예제**

```
                              DeptService 
  Application.java    ←—→   DeptServiceImpl  ←—→  DeptDAO/UserDAO
```

```java
@Service
public class DeptServiceImpl implements DeptService {	

	 **@Autowired
	 DeptDAO deptDAO;
	 @Autowired
	 UserDAO userDAO;**	
}
```

- Spring이 컨테이너에서 자동으로 두 객체를 주입한다.
- 권장되지 않는 방식으로, 생성자 주입을 사용하도록 하자.

# 12. @Qualifier

## 1) 개념

: 기본적으로 생성자 주입 또는 @Autowired는 **동일한 타입을 주입**시킨다. 따라서 동일한 타입이 하나인 경우에는 그것이 주입된다.

- **문제점** :
    
    **동일한 타입이 여러개인 경우에는 어떤 클래스를 주입할 지 모르기 때문에 명시적으로 주입할 클래스를 알려줘야 한다**. 
    
- **해결** :
    
    이때 **`@Qualifier(”빈이름”)`** 을 사용한다.
    

- **예제**
    
    ```
                                     DeptService           CommonDAO (인터페이스)
         Application.java    ←—→   DeptServiceImpl  ←—→  DeptDAO/UserDAO
    ```
    
    - **CommonDAO (인터페이스)**
        
        ```java
        public DeptServiceImpl(CommonDAO dao) {
        		this.dao = dao;
        	}
        ```
        
        - `CommonDAO` 인터페이스를 구현하는 `DeptDAO` 와 `UserDAO`가 존재
            
             ⇒ 동일한 타입의 2가지 빈이 존재
            
    - **ServiceImpl ( 생성자 주입 )**
        
        ```java
         public DeptServiceImpl(**@Qualifier("dept")** CommonDAO dao) {
        		logger.info("Logger:{}", "DeptServiceImpl 생성자" + " " + dao);
        		this.dao = dao;
        	}
        ```
        
        - **`@Qualifier(”dept”)`** 를 통해서 `CommonDAO` 의 여러 빈 중 **`dept`** 라는 이름의 빈이 주입된다.
            - 주입할 빈의 이름을 지정한 경우 이름을 사용하고, 이름이 없는 경우에는 클래스의 이름을 소문자로 시작하는 형태로 사용한다.
            
            ```java
            @Repository("**dept**")
            public class DeptDAO implements CommonDAO{
            ```
            
            - 여기서는 **`dept`** 사용
    - **ServiceImpl**  **( @AutoWired )**
        
        ```java
        	 // Service에서 DAO 접근하고자 한다. 
        	 **@Autowired
        	 @Qualifier("dept")**
        	 CommonDAO dao;
        ```
        
        - `@Autowired` 아래에  **`@Qualifier("dept")`**를 명시적으로 사용하면 된다.
