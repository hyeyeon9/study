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
     
---
# 15. Profile

## 1) 개념

: 개발할 때 다양한 **환경**을 구축해서 개발한다. 

- dev 환경 (개발환경), Q/A 환경, prod 환경 (배포환경)

```
**//개발환경
Application <---------> DeptServiceImpl <---------> H2DAO <----> H2, Redis (경량 DB)

//배포환경
Application <---------> DeptServiceImpl <---------> MySQLDAO <----> MySQL, Oracle( enterprise DB)**
```

## 2) 구현방법

### 1. 프로파일에 따른 properties 선택

1. 각 환경에 맞는 application.properties 작성하기
    - application.properties ( 기본 )
        - **`spring.profiles.active=dev`** 로 설정하면  **application-dev.properties 와 연동**
    - application-profile명.properties
        
        예 > application-dev.properties (개발환경)   : H2 연동설정 정보
        
          application-prod.properties (배포환경)  : MySQL 연동설정 정보
        
    
- application.properties
    
    ```
    # application.properties (기본)
    spring.profiles.active=prod 
    ```
    
- application-prod.properties
    
    ```
    # application-prod.properties
    logging.level.com.exam=warn
    ```
    

위 프로파일에 따라서 `com.exam` 패키지 내의 로그 메세지는 `warn` 수준 이상 (warn, error)만  출력되는 것을 확인할 수 있다. 

## 2. 프로파일에 따른 빈 선택하는 방법

```java
@Repository
**@Profile("prod")**
public class MySQLDAO {
	private Logger logger = LoggerFactory.getLogger(getClass());                                
	
	public MySQLDAO() {
		logger.info("Logger:{}", "MySQLDAO 생성자");
	}
	
}
```

- `@Profile("**prod**")`를 지정해 `application-**prod**.properties` 와 연동하게 되고, 실행하면 `MySQLDAO` 의 생성자가 호출되어 로그가 찍히는 것을 확인할 수 있다.

---
# 16. AOP ( Aspect Oriented Programming : 관점 지향 프로그래밍 )

## 1) 개념

: 핵심코드 ( 로그인, 회원가입, 장바구니, .. ), 부수코드 ( 예외처리, 로깅, 보안, 트랜잭션처리 , ..) 등의 코드들이 각 레이어마다 혼합(핵심 + 부수) 되어 사용되는 문제가 있다. 

- **부수코드를 따로 분리해서 부수코드가 필요한 각 레이어에 주입해서 사용하자는 개념이 AOP (관점 지향 프로그래밍)이다.**
- **핵심 코드를 수정하지 않고도 공통 기능을 추가할 수 있다.**
- **공통적인 부가기능을 별도로 관리해서 코드 중복을 줄이고 유지보수성을 높인다.**

---

## 2) **Spring AOP** 기술

### **1) AspectJ**

: AOP **원천기술** ( 1995년 )

- **다양한 주입시점을 가진다**. ( 특정 메서드를 호출할 때, 변수값이 변경될 때, .. )

### **2) Spring AOP**

: 원천기술인 `AspectJ`에서 **일부분만 빌려서 사용하는 기술**

- pom.xml에 <dependency> 가 필요하다.
- **단 하나의 주입시점**을 가진다.
    - **핵심코드를 가진 Servlet의 특정 메서드를 호출할 때**

---

## 3) **AOP 핵심** 용어

- **target object**  :  **핵심 클래스**
- **aspect**      :  **부가기능 구현 클래스**
- **joinpoint  :  핵심 코드(`target object`)와 부가기능(`aspect`)가 만나는 시점**  ⇒  메서드 호출시
- **pointcut**   :  target object의 **어떤 메서드를 호출했을 떄 AOP를 적용할지** 지정하는 표현식
- **advice**      : **부가기능이 실행되는 시점과 방식**
    - `@Before` : 메서드 호출전
    - `@After` : 메서드 호출후
    - `@AfterReturning` : 메서드 호출해서 리턴값 성공시
    - `@AfterThrowing` : 메서드 호출해서 에러발생시
    - `@Around` : 메서드 호출전, 호출후, 성공시, 에러발생시 모두 포함하는 경우
- **weaving**  :  **AOP를 핵심코드에 조인(주입**)하는 과정

---

## 4) AOP 실습

### **1) AOP 의존성 주입**

- **`pom.xml`**
    
    ```xml
    <!-- AOP 설정-->
    <dependency>
    			<groupId>org.springframework.boot</groupId>
    			<artifactId>spring-boot-starter-aop</artifactId>
    </dependency>
    ```
    

### **2) target object ( 핵심 클래스 )**

- 로그인, 회원가입 등 **핵심 기능을 담당하는 클래스**를 의미한다.

```java
@Service("deptService")
public class DeptServiceImpl implements DeptService {
	@Override
	public String sayEcho() {
		logger.info("sayecho() : {}","안녕하세요!!");
		return "안녕하세요.";
	}

	@Override
	public List<String> list() {
		return Arrays.asList("홍길동","이순신");
	}
}
```

### **3) aspect  ( 부가기능 클래스 )**

- **로그처리와 같은 부가기능 구현 클래스**를 의미한다.

```java
@Component
**@Aspect**
public class LoggingAspect {
	public void loggingPrint1() {
		// 로그처리 담당
	}	
}
```

### **4) pointcut 지정**

: **target object 의 어떤 메서드를 호출할 때 join할지 나타내는 표현식**

- **포인트컷**은 **어떤 지점에서 AOP를 적용할지 지정하는 표현식**이다.

```java
**@Pointcut("execution(public String sayEcho())")**
	public void businessService() {}
```

- **`sayEcho()` 메서드가 호출되는 시점에 `businessService()` 포인트컷이 트리거된다. 이 포인트컷을 참조하는 `advice` 에서 부가기능 로직이 실행되는 것이다.**

**Pointcut 표현식**

1. **`execution()`**
    
    : 특정 메서드를 지정할 때 사용
    
2. **`bean()`**
    
    : 특정 컴포넌트(빈)의 이름 지정  ⇒  메서드를 포함하는 빈
    
    예 > bean(”service”)
    
    @Service(”service”)
    
    public class BoardServiceImpl(){ … }
    
3. **`witihin()`**
    
    : 특정 패키지 내 클래스 지정 
    
    예 > witihin(”com.exam.*”)
    
4. **`combine (   &&  ,  ||   ,   !   )`**
    
    : 표현식을 결합해서 대상 지정 가능
    
    예 > Pointcut(”execution(publiv String sayEcho()  ||   bean(service) )”
    

### **5) advice 지정**

- **@Before (메서드 실행 전)**
    
    : 메서드 실행 전에 로깅을 수행한다. 
    
    ```java
    @Before("execution(public String sayEcho())")
    public void beforeAdvice() {
        logger.info("LOGGER: {}", "@Before advice 실행 - 메서드 호출 전");
    }
    ```
    
- **@After (메서드 실행 후)**
    
    : 메서드 실행 후에 로깅을 수행
    
    ```java
    	// adive와 pointcut을 같이 표현
    	@After("execution(public String sayEcho())")
    	public void loggingPrint1() {
    		// 로그처리 담당
    		logger.info("Logger : {}", "@After advice1");
    	}
    	
    		// adive와 pointcut을 분리
    	@Pointcut("execution(public String sayEcho())")
    	public void businessService() {}
    	
    	@After("businessService()")
    	public void loggingPrint2() {
    		// 로그처리 담당
    		logger.info("Logger : {}", "@After advice2");
    	}
    ```
    
    - **`advice`** 와 **`pointcut`** 을 **같이 표현하거나 분리해서 표현 가능**하다. 위 코드에서는 **`@After`** 를 지정했기에  **`sayEcho()` 메서드를 호출한 후**에 **`포인트컷(businessService())`을 참조하는 어드바이스에서 로그 메서지가 출력**되는 것을 확인할 수 있다.

- **@AfterReturning (정상 실행 후, 반환값을 사용)**
    - 메서드가 정상적으로 실행되고 리턴값이 있는 경우 받아서 사용 가능
        
        ```java
        	@AfterReturning(pointcut = "bean(deptService)", returning = "xxx")
        	public void loggingPrint2(Object xxx) {
        		//로그처리 담당
        		logger.info("Logger : {}, {}", "@After 어드바이스2", xxx);
        	}
        ```
        
    - 분리해서 사용
        
        ```java
        // 분리해서
        	@Pointcut("been(*Service)")
        	public void businessService() {}
        	
        	@AfterReturning(pointcut = "businessService()", returning = "xxx")
        	public void loggingPrint4(Object xxx) {
        		//로그처리 담당
        		logger.info("Logger : {}, {}",  "@AfterReturning 어드바이스3", xxx);
        	}
        ```
        
    - JoinPoint 사용 가능
        
        ```java
        	@AfterReturning(pointcut = "bean(deptService)", returning = "xxx")
        	public void loggingPrint3(JoinPoint point,Object xxx) {
        		//로그처리 담당
        		logger.info("Logger : {}, {}, {}", 
        				"@AfterReturning 어드바이스3", xxx, point.getSignature().getName());
        		// Logger : @After 어드바이스3, 안녕하세요., sayEcho
        	}
        ```
        

- **@AfterThrowing (예외 발생 시)**
    
    : 에러가 발생할 때 
    
    - Service에서 에러를 발생하는 코드 작성
        
        ```java
        package com.exam.service;
        @Service("deptService")
        public class DeptServiceImpl implements DeptService {
        	Logger logger = LoggerFactory.getLogger(getClass());                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                
        
        	@Override
        	public String sayEcho() {
        		logger.info("sayecho() : {}","안녕하세요!!");
        		int num =10;
        		**int result = num/0;**
        		return "안녕하세요.";
        	}
        }
        ```
        
        - 기본 구조
            
            ```java
            	@AfterThrowing("within(com.exam.service.*)")
            	public void loggingPrint1() {
            		//로그처리 담당
            		logger.info("Logger : {}", "@AfterThrowing 어드바이스1");
            	}
            ```
            
        - 에러값 반환받기 가능
            
            ```java
            	@AfterThrowing(pointcut = "within(com.exam.service.*)",
            				   **throwing = "ex"**)
            	public void loggingPrint2(Exception ex) {
            		//로그처리 담당
            		logger.info("Logger : {} , {}", 
            					"@AfterThrowing 어드바이스2", ex.getMessage());
            		// [0;39m Logger : @AfterThrowing 어드바이스2 , / by zero
            	}
            ```
            
        - 분리해서 작성 가능
            
            ```java
            	// 분리해서
            	@Pointcut("within(com.exam.service.*)")
            	public void businessService() {}
            	
            	@AfterThrowing(pointcut = "businessService()", throwing = "xxx")
            	public void loggingPrint4(Exception xxx) {
            		//로그처리 담당
            		logger.info("Logger : {}, {}",  "@AfterThrowing 어드바이스3", xxx.getMessage());
            	}
            ```
            

- **@Around (메서드 실행 전/후 모두 적용)**
    - 기본구조
        
        ```java
        	@Around("within(com.exam.service.*)")
        	public Object loggingPrint1(ProceedingJoinPoint point) {
        		Object retval = null;
        		try {
        		logger.info("LOGGER : {}", "@Before 처리");
        		 **retval = point.proceed();**
        		 logger.info("LOGGER : {}, {}", "@After 처리", retval);
        		 // LOGGER : @After 처리, 안녕하세요.
        		}
        			catch (Throwable e) {
        					logger.info("LOGGER : {}", "@AfterThrowing 처리");
        		}
        		return retval;
        	}
        ```
        
        - `point.proceed()`가 **실제 메서드를 실행하는 부분**
        - 반환값을 조작하거나 실행 시간 측정 가능
    - 분리해서
        
        ```java
        // 분리해서
        	@Pointcut("execution(public String say2()) || bean(*Service)")
        	public void businessService() {}
        	
        	@Around("businessService()")
        	public Object loggingPrint2(ProceedingJoinPoint point) {
        		Object retval = null;
        		try {
        		logger.info("LOGGER : {}", "@Before 처리2");
        		 **retval = point.proceed();**
        		 logger.info("LOGGER : {}, {}", "@After 처리2", retval);
        		 // LOGGER : @After 처리, 안녕하세요.
        		}
        			catch (Throwable e) {
        					logger.info("LOGGER : {}", "@AfterThrowing 처리2");
        		}
        		return retval;
        	}
        ```
        
    - pointcut을 담아두는 클래스를 따로 생성해서 호출하기
 

  ---
  # Spring Boot + MyBatis + MySQL(데이터베이스) 연동

# 1. MyBatis + MySQL 연동 ( 기본방식 )

https://mybatis.org/spring-boot-starter/mybatis-spring-boot-autoconfigure/

## 1) 의존성 추가 : 2개의 jar 필요

- `mybatis.jar`
- `mysql-connector.jar`

⇒  **스프링부트에서는 pom.xml 에 <dependecy> 태그에 설정**

- https://mvnrepository.com/artifact/org.mybatis.spring.boot/mybatis-spring-boot-starter/3.0.3

```xml
<!-- https://mvnrepository.com/artifact/org.mybatis.spring.boot/mybatis-spring-boot-starter -->
<dependency>
		<groupId>org.mybatis.spring.boot</groupId>
		<artifactId>**mybatis-spring-boot-starter**</artifactId>
		<version>3.0.3</version>
</dependency>
```

- https://mvnrepository.com/artifact/mysql/mysql-connector-java/8.0.33

```xml
<!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>**mysql-connector-java**</artifactId>
    <version>8.0.33</version>
</dependency>

```

## 2) DB 연동을 위한 4가지 정보

: 이전에는 `jdbc.properties` 파일에 설정했었다. 스프링부트에서는 **`application.properties`** 파일에 설정한다. 

- 기존에 사용하던 4가지 정보
    
    ```java
    **jdbc.driver = com.mysql.cj.jdbc.Driver
    jdbc.url = jdbc:mysql://localhost:3306/testdb
    jdbc.userid = root
    jdbc.passwd = 1234**
    ```
    
- 스프링 부트
    
    ```java
    **# application.properties
    # DB 연동
    spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
    spring.datasource.url=jdbc:mysql://localhost:3306/testdb
    spring.datasource.username=root
    spring.datasource.password=1234**
    ```
    

## 3) DTO 작성 및 별칭

- **`com.exam.dto.DeptDTO` 작성**
- **`@Alias` 로 별칭등록**

```java
**@Alias("DeptDTO")**
public class DeptDTO {
	int deptno;
	String dname;
	String loc;
	...
	}
```

- DTO 클래스가 MyBatis에서 자동으로 매핑될 수 있도록 **`@Alias("DeptDTO")` 로 별칭을 등록해야 한다.**

## 4) Configuration.xml 필요없음

: 위 4가지 정보 등록, DTO 별칭, mapper 등록을 **Configuration.xml이 아니라 application.properties 가 담당**한다.

## 5) Mapper XML 작성

- com.exam.config.DeptMapper.xml 작성

## 6) DTO 별칭 등록 및 Mapper 등록

- DTO 별칭 등록
    - **`mybatis.type-aliases-package`**
- Mapper 등록
    - **`mybatis.mapper-locations`**

```java
# MyBatis 설정
mybatis.type-aliases-package=com.exam.dto
mybatis.mapper-locations=classpath:mapper/*.xml
```

## 7) java 파일 작성

```java
                         DeptService
Application.java <----> DeptServiceImpl <---->  DeptDAO <---> MySQL
```

## 8) MySqlSessionFactory.java 필요 X

: 기존에 MySqlSessionFactory.java 를 통해서  Service 클래스에서 session을 얻고, DAO 클래스에 전달해서 사용되었다.

- 스프링부트에서는 **`SqlSessionTemplate`** 를 사용한다.
    - Service클래스가 아니라 **DAO에서 직접 얻어서 사용한다. 이유는 commit()/rollback()처럼 직접 호출하는 방법의 트랜잭션 처리가 아니기 때문이다.**
    - **선언적 트랜잭션 방식**을 사용한다.
        - **`@Transactional`** 이용
        - **Service 클래스**에서 트랜잭션 처리를 담당한다.
        - **auto commit**
            - 성공하면 모두 자동으로 commit이 되고, 작업 중 하나라도 실패하면 모두 rollback이 된다.
            
            ```java
            @Transactional 
            public void tx(){
            	int n = dao.insert();
            	int n2 = dao.delete();
            }
            ```
            

## 9) DAO 구현

- **DAO에서 직접 Sqlsession을 얻어와서 사용**한다.

```java
@Repository
public class DeptDAO {
	**SqlSessionTemplate session;**
	// session 주입
	public DeptDAO(SqlSessionTemplate session) {
		this.session = session;
	}
	}
```

- mapper의 함수와 연결
    
    ```java
    	// mapper로 연동할 함수
    	public List<DeptDTO> findAll(){
    		List<DeptDTO> list = session.selectList("com.exam.config.DeptMapper.findAll");
    		return list;
    	}
    ```
    

## 10) Service 와 ServiceImpl

- Service 인터페이스
    
    ```java
    public interface DeptService {
    	public List<DeptDTO> findAll();
    }
    ```
    
- ServiceImpl 클래스
    
    ```java
    @Service("deptService")
    public class DeptServiceImpl implements DeptService {
    	DeptDAO dao;
    
    	// 생성자로 주입시키기
    	public DeptServiceImpl(DeptDAO dao) {
    		this.dao = dao;
    	}
    
    	@Override
    	public List<DeptDTO> findAll() {
    		return dao.findAll();
    	}
    	...
    }
    ```
    

## 11) Application.java 실행

```java
@SpringBootApplication
public class Application implements CommandLineRunner{
	
	// 1. Logger 얻기
	Logger logger = LoggerFactory.getLogger(getClass());                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                
	
	@Autowired
	DeptService service;
	
	public static void main(String[] args) {
		SpringApplication.run(Application.class, args);
	}

	@Override
	public void run(String... args) throws Exception {
		List<DeptDTO> list = service.findAll();
		logger.info("Logger list : {}", list);
		}
}
```

---

# 2. MyBatis + MySQL 연동 2 ( 권장방식 )

https://mybatis.org/spring-boot-starter/mybatis-spring-boot-autoconfigure/#quick-setup

- **`DAO`** 대신에 **`@Mapper` 인터페이스를 사용하는 방법**

## 1) DAO 삭제

: **DAO 대신 `@Mapper` 어노테이션이 붙은 인터페이스를 사용할 것**이다. 

## 2) **`DeptMapper.java` 작성**

: **`DeptMapper.xml`** 과 자동으로 연동하는 **인터페이스 `DeptMapper.java` 를 사용한다.** 

- **DeptMapper.xml의 namespace와 DeptMapper.java 의 패키지가 동일**해야 한다. ( 동일한 패키지 안 )
- **`DeptMapper.java`**
    - 구현 방법 :
        1. **`DeptMapper.xml`**의 id값과 일치하는 메서드를 지정
        2. **`parameterType`**과 일치하는 파라미터타입 지정 
        3. **`returnType`**과 일치하는 리턴타입 지정
        4. **`@Mapper` 어노테이션 지정해 매퍼로 등록**
    
- **DeptMapper.xml**
    
    ```java
    <?xml version="1.0" encoding="UTF-8" ?>
    <!DOCTYPE mapper
    PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
    "https://mybatis.org/dtd/mybatis-3-mapper.dtd">
    **<mapper namespace="com.exam.config.DeptMapper">**
    
    	<select id="findAll" resultType="DeptDTO">
    		<![CDATA[
    				select deptno, dname, loc
    				from dept
    				order by deptno desc
    		]]>
    	</select>
    
    </mapper>
    ```
    
- **DeptMapper.java**
    
    ```java
    **package com.exam.config;**
    
    import org.apache.ibatis.annotations.Mapper;
    
    **@Mapper
    public interface DeptMapper {
    	public List<DeptDTO> findAll(**)**;
    }**
    
    ```
    
    - 주요 확인 사항 :
        - DeptMapper.xml의 namespace와 DeptMapper.java의 **패키지가 동일해야 한다.**
        - **메서드 이름, 파라미터타입, 리턴타입이 일치**해야 한다.

## 3) Service 작업

: **`DeptDAO`**가 아니라 **`DeptMapper`**을 주입받기

- **DeptServiceImpl.java**

```java
package com.exam.service;

import com.exam.config.DeptMapper;
import com.exam.dto.DeptDTO;

@Service("deptService")
public class DeptServiceImpl implements DeptService {
	**DeptMapper mapper;**

	**// 생성자로 Mapper 주입시키기
	public DeptServiceImpl(DeptMapper mapper) {
		this.mapper = mapper;
	}**

	**@Override
	public List<DeptDTO> findAll() {
		return mapper.findAll();
	}**
}

```

- DeptDAO 대신 **DeptMapper를 생성자 주입으로 받아 사용**한다.
- **Mapper를 통해 데이터베이스와 직접 연동**한다.

## 4) Application.java

: 기존과 그대로 **`service`** 객체를 주입받아서 **`Service`**클래스 안의 메서드를 호출한다.

- **Application.java**

```java
package com.exam;

**@SpringBootApplication**
public class Application implements CommandLineRunner{
	
	// 1. Logger 얻기
	Logger logger = LoggerFactory.getLogger(getClass());                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                
	
	**@Autowired
	DeptService service;**
	
	public static void main(String[] args) {
		SpringApplication.run(Application.class, args);
	}

	@Override
	public void run(String... args) throws Exception {
		**List<DeptDTO> list = service.findAll();**
		logger.info("Logger list : {}", list);
		}
}
```

---

# ✅정리

- **스프링부트에서 데이터베이스 ( MyBatis + MySQL ) 연동하는 방법**
- 기존 방식 (DAO 사용) 보다 **@Mapper 사용 방식을 권장**
- **`@Mapper`** 릍 통해 더 간결하게 DB와 매핑 가능

---
# 19. Spring MVC

## 1) 서블릿/JSP의 MVC 아키텍처

- 요청URL : http://localhost:8090/컨텍스트명/서블릿맵핑
- JSP 기본적으로 지원됨
- 서블릿에서 데이터 얻은 후 JSP로 요청 위임( forward, redirect)

```java
웹 브라우저 <----> **서블릿** <----> 서비스 <----> DAO <---> MYSQL
	              - 개발자가 생성
	              - 서블릿 맵핑 (예> /test)
	              - 중요작업 2가지
		              a. 로직처리후 서비스 연동
			              : 사용자입력데이터 얻기 (request.getParameter)
				              세션처리 (HttpSession session = request.getSession())
				          b. jsp 선택
					          : forward / redirect
```

## 2) Spring MVC 아키텍처

- 요청URL : **`http://localhost:8090/컨텍스트명/서블릿맵핑/요청맵핑값`**
    - 예 >  http://localhost:8090/app/list
- 서블릿을 개발자가 만들지 않고 제공된다. ⇒ **`DispatcherServlet`**
- **`Controller`** 에서 중요작업이 진행된다.
- JSP가 기본적으로 지원되지 않음.
    - 따라서 **JSP를 사용하기 위해서는 의존성 추가 및 웹 디렉터리도 명시적으로 생성해야 한다.**

```java
                                                 **@Controller**      @Service    @Repository                                     
웹 브라우저 <----> DispatcherServlet서블릿 <----> **Controller** <----> 서비스 <---> DAO <---> MYSQL
	              - 제공됨                        - 중요작업 2가지
	              - 서블릿 맵핑(/)                  a. 로직처리후 서비스 연동 
		                                              b. jsp 선택
	                                              
	                                                @RequestMapping("/list")
	                                                public String aaa(){
		                                                // 게시판 목록보기
		                                               }
		                                              @RequestMapping("/write")
		                                              public String bbb(){
		                                                // 게시판 글쓰기
		                                               }
		             
```

- 기존에는 각 기능을 위한 서블릿을 매번 생성했지만, **`Controller 패턴`을 통해서 하나의 Controller 클래스에서 여러 기능을 처리하도록 구성할 수 있다.**
    - **각 기능은 컨트롤러 클래스 안의 개별 메서드로 구현**된다.

### **`@RequestMapping("값")`**

: 요청 URL과 컨트롤러 클래스 안의 특정 메서드를 매핑하기 위해 사용된다. 

- **특정 메서드의** `@**RequestMapping` 값을 요청 URL에 포함하면, 매핑된 메서드를 호출할 수 있다.**
    
    ```java
    @RestController
    public class UserController {
    
        @RequestMapping("/hello")  
        public String sayHello() {
            return "Hello, World!";
        }
    }
    ```
    
    - `/hello` 요청   ⇒   `sayHello()` 실행

## 3) Spring MVC 구현 순서

### **1. 웹 어플리케이션 개발을 위한 의존성 추가**

- **`spring-boot-starter-web`**

```java
**<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
</dependency>**
```

- Tomcat initialized with port 8080 (http)
    - 웹 개발을 위한 JAR 및 Tomcat 설치된다.
    - **tomcat의 기본 port 번호는 8080이며, 변경 가능하다.**
        - **`application.properties`**에서 변경 설정 가능
            - **`server.port=8090`**
    - 만약 404라면 **Whitelabel Error Page** 가 보여진다. 이것은 내부적으로 스프링부트가 404페이지를 만들어서 제공하는 것

### **2. Controller 작성**

- POJO 기반이고, **`@Controller`** 어노테이션 지정
- **각 기능에 해당되는 메서드를 작성**하고, **`@RequestMapping("/요청매핑값")`**을 설정한다.

```java
package com.exam.controller;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class TestController {
	
	Logger logger = LoggerFactory.getLogger(getClass());   
	
	// 요청 URL : http://localhost:8090/컨텍스트명/서블릿맵핑명/요청맵핑명
	
	**// 요청 URL : http://localhost:8090/list
	@RequestMapping("/list")
	public String aaa() {
		logger.info("LOGGER : {}", "aaa 호출" );
		
		return "";
	}
	
	// 요청 URL : http://localhost:8090/write
	@RequestMapping("/write")
	public String bbb() {
		logger.info("LOGGER : {}", "bbb 호출" );
		
		return "";
	}**
}
```

- **`http://localhost:8090/list` 요청 시 `aaa()` 메서드가 호출되어 아래와 같은 로그를 확인할 수 있다.**
    - `LOGGER : aaa 호출`

### 3. 컨텍스트명 변경 가능

- **`application.properties`**에서 설정
    
    ```xml
    # 컨텍스트명 변경 가능
    **server.servlet.context-path=/app**
    ```
    
- 위 코드의 경우, **`http://localhost:8090/app/list`** 로 호출해야 한다.

### 4. JSP 설정

1. JSP/CSS/HTML을 위한 **web 플러그인 추가**
2. **JSP 의존성 추가**
    
    : 스프링부트는 JSP를 기본적으로 지원 안 됨.
    
    - **tomcat-embed-jasper**
    - **jakarta.servlet.jsp.jstl-api**
    - **jakarta.servlet.jsp.jstl**
    
    ```java
    <dependency>
    	  <groupId>org.apache.tomcat.embed</groupId>
    	  <artifactId>**tomcat-embed-jasper**</artifactId>
    	  <scope>provided</scope>
    	</dependency>
    	
    <dependency>
    	  <groupId>jakarta.servlet.jsp.jstl</groupId>
    	  <artifactId>**jakarta.servlet.jsp.jstl-api**</artifactId>
    	</dependency>
    	
    <dependency>
    	  <groupId>org.glassfish.web</groupId>
    	  <artifactId>**jakarta.servlet.jsp.jstl**</artifactId>
    	</dependency>
    ```
    
3. **웹 디렉터리 명시적으로 생성**
    - **`src/main/resources/META-INF/resources/WEB-INF/views`  :***해당 폴더 안에 jsp를 만들어서 사용*
    
    ⇒  **jsp가 WEB-INF에 저장된다**. 따라서 웹 브라우저에서 직접 jsp를 접근할 수 없다. 
    
    - **jsp 접근은 `Controller`를 통해서 forward 또는 redirect로 접근이 가능하다.**
    - TestController.java
        
        ```java
        package com.exam.controller;
        
        @Controller
        public class TestController {
        	Logger logger = LoggerFactory.getLogger(getClass());   
        
        	**// 요청 URL : http://localhost:8090/app/list
        	@RequestMapping("/list")
        	public String aaa() {
        		logger.info("LOGGER : {}", "aaa 호출" );
        		return "/WEB-INF/views/sayHello.jsp";
        	}**	
        }
        ```
        
    - sayHello.jsp
        
        ```java
        <%@ page language="java" contentType="text/html; charset=UTF-8"
            pageEncoding="UTF-8"%>
        <!DOCTYPE html>
        <html>
        <head>
        <meta charset="UTF-8">
        <title>Insert title here</title>
        </head>
        <body>
        	**<h1>sayHello.jsp</h1>**
        </body>
        </html>
        ```
        
    - 서버 실행 후, 요청 URL : http://localhost:8090/app/list 로 접근
        
        ![jsp 접근한 것을 확인할 수 있다. ](https://prod-files-secure.s3.us-west-2.amazonaws.com/686c9583-1330-4ae4-99da-86732a9a0b13/08c6df15-ed6c-4781-80e9-a1628911a2f5/db36a9ee-0cb1-42f7-8818-ed4940ccdafc.png)
        
        jsp 접근한 것을 확인할 수 있다. 
        
    
    - `src/main/webapps/WEB-INF/views` 파일에 만드는 방법도 가능하지만 위의 방법을 권장한다.
4. **JSP 알려주기**
    
    : Controller 에서 구현된 메서드의 리턴값으로 알려준다. 
    
    ```java
    	**@RequestMapping("/list")
    	public String aaa() {
    		return "/WEB-INF/views/sayHello.jsp";
    	}**	
    ```
    
    - 컨트롤러의 메서드에서 String 타입을 리턴하면 리턴값에는 JSP 정보를 담긴다.
    - **문제점**
        - **JSP의 경로가 길다.**
    - **해결방법**
        - **application.prperties에 prefix와 suffix를 설정한다.**
            
            ```xml
            # JSP 용 prefix와 suffix
            **spring.mvc.view.prefix=/WEB-INF/views/
            spring.mvc.view.suffix=.jsp**
            ```
            
        - **prefix : `spring.mvc.view.prefix=/WEB-INF/views/`  (경로)**
        - **suffix : `spring.mvc.view.suffix=.jsp`  (확장자)**
            
            ```java
            	**@RequestMapping("/list")
            	public String aaa() {
            	  return "sayHello";
            	}**
            ```
            
            - **JSP 경로를 간단하게 작성 가능**하다.
5. **정적파일 (CSS, JS, Image)**
    
    `: src/main/resources`에 **`static`** 폴더를 생성하고, **그 안에 css, js, image 폴더를 각각 만들어 저장한다.**
    
    ![image.png](attachment:5c5ace0a-61ce-456f-a55f-7410e7eeb111:0b122db5-50fc-44b8-b3c7-d5a07a396b2b.png)
    

- **Controller에서의 JSP 요청은 `forward`로 처리**된다. 따라서 JSP로 이동하더라도 **URL 변경이 되지 않는다.**
    - **request scope에 데이터를 저장하면 JSP에서 사용할 수 있다.**

---

✅ **VSC의 Live Server처럼 소스코드 변경시 바로 서버에 반영하는 방법**

- **`devtools`** 의존성 추가

```xml
 <dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>**spring-boot-devtools**</artifactId>
		<scope>runtime</scope>
		<optional>true</optional>
</dependency>	
```

---
# 20. @RequestMapping

## 1) 용도

: 요청 URL에서 사용하는 요청맵핑명을 **`@RequestMapping(”/요청맵핑명”)`** 에 설정해서 요청에 대한 실제 처리를 위한 메서드를 선택할 수 있다.

## 2) 패턴

### 1. 메서드 레벨

- `@RequestMapping(”/list”)`
- `@RequestMapping(value=”/list”)`
- `@RequestMapping(value={”/list”, “/select”})`
- `@RequestMapping(value=”/board/list”)`
- `@RequestMapping(value=”/list*”)`
- `@RequestMapping(value=”/list/*”)`    :  *은 하나의 디렉터리
- `@RequestMapping(value=”/list/**”)`  :  **는 여러개의 디렉터리
- `@RequestMapping(value=”/list/*/some”)`
    - @`RequestMapping(value=”/list/******/some”)` : **에러발생**
        - 해결방법 :
            - `application.properties`에
                
                **`spring.mvc.pathmatch.matching-strategy=ant-path-matcher`** 추가하기
                

### 2. 클래스 레벨

: **클래스 레벨의 요청값과 메서드 레벨의 요청값이 결합**되어 **최종적으로 결합된 요청값으로 매핑**된다.

- 같은 클래스의 각 메서드들의 요청매핑값에 반복되는 값을 클래스 레벨 요청값으로 둬서 코드를 간단히 할 수 있다.

```java
@Controller
**@RequestMapping("/member")**
public class MemberController {
	
	Logger logger = LoggerFactory.getLogger(getClass());   
	**@RequestMapping("/list")**
	public String list() {
		logger.info("LOGGER : {}", "member/list 호출" );
	
		return "sayHello";
	}
}
```

- 최종 요청매핑값 : `/**member/list**`

1. **GET 및 POST 요청1**
    - **매핑값과 method가 다른 경우**
    
    ```java
    	@RequestMapping(value = "/req/get", method = RequestMethod.GET)
    	public String req_get() {
    		logger.info("LOGGER : {}", "GET");
    		return "main";
    	}
    	
    	@RequestMapping(value = "/req/post", method = RequestMethod.POST)
    	public String req_post() {
    		logger.info("LOGGER : {}", "POST");
    		return "main";
    	}
    ```
    
    - `Get` 요청은 `/req/get` 으로 들어오고, `Post` 요청은 `/req/post` 으로 들어온다.
    - 서로 다른 URL을 사용하기에 두 요청을 완전히 분리할 수 있다.
    
2. **GET 및 POST 요청2** 
    
    **: 매핑값은 같고 method만 다른 경우**
    
    ```java
    	// 요청매핑값은 같고 메서드가 모두 다른 경우
    	@RequestMapping(value = "/write", method = RequestMethod.GET)
    	public String writeForm() {
    		logger.info("LOGGER : {}", "GET-writeFrom");
    		return "main";
    	}
    	
    	@RequestMapping(value = "/write", method = RequestMethod.POST)
    	public String write() {
    		logger.info("LOGGER : {}", "POST-write");
    		return "main";
    	}
    ```
    
    - 같은 URL이지만, 요청 방식에 따라서 다른 메서드가 실행된다.
    - `GET` 요청 시 `writeForm()` 실행, `POST` 요청시 `write()` 실행
    - **보통 GET 요청은 폼을 제공하고, POST 요청은 데이터를 처리하는 방식으로 많이 사용된다.**
  
---
# 1. Controller의 요청 처리 작업

## 1) 사용자 입력 데이터 얻기

1. 이전 서블릿에서의 처리
    - **`HttpServletRequest`** **`HttpServletResponse`**  사용
    
    ```java
    public void doGet(HttpServletRequest request, HttpServletResponse response){
    
    String userid = request.getParameter("userid");
    String [] hobbies = request.getParameterValues("hobby");
    ```
    

1. Spring에서의 처리
    - **`HttpServletRequest`** 사용 가능
    
    ```java
    	@PostMapping("/write")
    	public String write(HttpServletRequest request) {
    		String userid = request.getParameter("userid");
    		String passwd = request.getParameter("passwd");
    		logger.info("LOGGER : {}, {}", userid, passwd);
    		return "main";
    	}
    ```
    
    - **`@RequestParam(” ”)`**
        
        ```java
        	@PostMapping("/write")
        	public String write(@RequestParam("userid") String id,@RequestParam("passwd") String pw) {
        		logger.info("LOGGER : {}, {}", id, pw);
        		return "main";
        	}
        ```
        
        - **`@RequestParam("userid") String id`**
            
            : URL의 **`userid`** 파라미터의 값을 받아와서 id 변수에 저장
            
        - **`@RequestParam("passwd") String pw`**
            
            : URL의 **`passwd`**파라미터의 값을 받아와서 pw 변수에 저장
            
        - **변수명이 같은 경우, 생략 가능**
            
            ```java
            	// @RequestParam("userid") String userid 처럼 두 변수명이 같은 경우 생략 가능
            	@PostMapping("/write")
            	public String write(@RequestParam String userid,
            						@RequestParam("passwd") String pw) {
            		
            		logger.info("LOGGER 2: {}, {}", userid, pw);
            		return "main";
            	}
            ```
            
        - **`@RequestParam(”/태그이름”)`**
            
            : **태그이름에 해당하는 파라미터가 URL로 무조건 넘어와야 한다. 그렇지 않은 경우 에러가 발생된다.** 
            
            - **해결방법 1**
                
                : **`required = false`** **라는 속성을 추가하여 값이 없는 경우 `null`로 출력되도록 한다.**
                
                - **`required = false`**
                
                ```java
                	@PostMapping("/write")
                	public String write(@RequestParam(**name = "userid2", required = false**) String id,
                						          @RequestParam("passwd") String pw) {
                		logger.info("LOGGER : {}, {}", id, pw);
                		return "main";
                	}
                ```
                
            - **해결방법 2**
                
                : null이 아니라 **default값이 출력**되도록 한다.
                
                - **`defaultValue = "xxx"`**
                
                ```java
                	@PostMapping("/write")
                	public String write(**@RequestParam( name = "userid2",
                	 								   required = false,
                	 								   defaultValue = "xxx") String id**,
                						@RequestParam("passwd") String pw) {
                		
                		logger.info("LOGGER : {}, {}", id, pw);
                		return "main";
                	}
                ```
                
    - **DTO에 담아서 사용 가능**
        - URL로 넘어가는 값의 name과 DTO로 받을 변수의 이름이 동일하면 아래와 같이 사용 가능하다.
        - LoginDTO
            
            ```java
            
            public class LoginDTO {
            	String userid;
            	String passwd;
            	...
            }
            ```
            
        - main.jsp
            
            ```java
            <form action="write" method="post">
            	아이디: <input type="text" name="userid"> <br>
            	비번: <input type="text" name="passwd"> <br>
            	<button>요청</button>
            </form>
            ```
            
        - Controller.java
            
            ```java
            	@PostMapping("/write")
            	public String write4(LoginDTO dto) {
            		
            		logger.info("LOGGER dto: {}, {}", dto.getUserid(), dto.getPasswd());
            		return "main";
            	}
            ```
            
            : **`form`에서 전송하는 `input`의 `name` 속성이 DTO의 필드명과 동일하면 자동으로 매핑**된다.
            
            - 내부적으로 `@ModelAttribute` 를 사용하여 **DTO 객체에 값을 자동으로 바인딩**하여 저장한다.
        
    - **Map 사용 가능**
        
        ```java
        	@PostMapping("/write")
        	public String write(@RequestParam Map<String, String> map) {
        		
        		logger.info("LOGGER map: {}", map); 
        		return "main";
        	}
        ```
        
    
    - URL로 전달되는 값이 **정수**이면 컨트롤러에서 직접 **Long 타입의 정수로 저장 가능**하다.
        
        ```java
        	@PostMapping("/write")
        	public String write(@RequestParam("userid") String id,
        						@RequestParam("passwd") String pw,
        						@RequestParam("age") Long age) {
        		
        		logger.info("LOGGER : {}, {}, {}", id, pw, age); //  hyeyeon, 1234, 20
        		return "main";
        	}
        ```
        
    
    - **체크박스와 같이 여러개의 값이 URL로 넘어오는 경우**
        - **main.jsp**
            
            ```html
            <h1>2. POST </h1>
            <form action="write" method="post">
            	아이디: <input type="text" name="userid"> <br>
            	비번: <input type="text" name="passwd"> <br>
            	<hr>
            	취미:<br>
            	야구: <input type="checkbox" name="**hobby**" value="야구"><br>
            	농구: <input type="checkbox" name="**hobby**" value="농구"><br>
            	축구: <input type="checkbox" name="**hobby**" value="축구"><br>
            	<button>요청</button>
            </form>
            
            ```
            
        - **List 사용 가능 ( 권장 )**
            
            ```java
            	// 리스트로 받을 수 있음
            	@PostMapping("/write1")
            	public String write1(@RequestParam("userid") String id,
            						@RequestParam("passwd") String pw,
            						**@RequestParam("hobby") List<String> list**) {
            		
            		logger.info("LOGGER : {}, {}, {}", id, pw, list);
            		// LOGGER : name1, 11, [야구, 농구]
            		return "main";
            	}
            ```
            
        - **배열 사용 가능**
            
            ```java
            	@PostMapping("/write2")
            	public String write2(@RequestParam("userid") String id,
            						@RequestParam("passwd") String pw,
            						**@RequestParam("hobby") String [] hobby**) {
            		
            		logger.info("LOGGER : {}, {}, {}", id, pw, hobby);
            		// LOGGER : guhaa03@nate.com, 123, [야구, 농구, 축구]
            		return "main";
            	}
            ```
            
        - **DTO 사용 가능**
            - **DTO로 사용시 URL로 넘어오는 파라미터의 이름과 DTO로 받을 변수명이 동일**해야 한다.
            - **Login.dto**
                
                ```java
                public class LoginDTO {
                	String userid;
                	String passwd;
                	List<String> hobby;
                	...
                }
                ```
                
            - java
                
                ```java
                	@PostMapping("/write")
                	public String write(LoginDTO dto) {
                		
                		logger.info("LOGGER : {}, {}, {}", dto.getUserid(), dto.getPasswd(), dto.getHobby());
                		// LOGGER : name, 5555, [야구, 축구]
                		return "main";
                	}
                ```
                

## 2) **요청 헤더값 보기**

1. 서블릿에서 헤더값 처리
    
    ```java
    **public void doGet(HttpServletRequest request, HttpServletResponse response){
    	Enumeration<String> enu = request.getHeaderNames();
    }**
    ```
    

1. **Spring Controller 처리**
    - **`@RequestHeader()` 이용**
        
        ```java
        @GetMapping("/main")
        		public String list(@RequestHeader("user-agent") String s,
        					   @RequestHeader("accept-language") String s2) {
        		
        			 logger.info("LOGGER:user-agent={}", s);
        			 logger.info("LOGGER:accept-language={}", s2);  // ko-KR,ko
        			return "main";
        		}
        
        ```
        
        - 나중에 **다국어처리(I18N)** 처리할 때 **`accept-language`** 헤더값을 사용하게 된다.

## 3) 요청 쿠키값 보기

1. 서블릿에서 쿠키 정보 
    
    ```java
    	// 서블릿 쿠키
    	@GetMapping("/set")
    	public String set(HttpServletRequest request, HttpServletResponse response) {
    		**Cookie c = new Cookie("userid", "홍길동");**
    		c.setMaxAge(3600); // 1시간
    		response.addCookie(c);
    		return "main";
    	}
    	
    	
    	// 서블릿 쿠키
    	@GetMapping("/get")
    	public String get(HttpServletRequest request, HttpServletResponse response) {
    		Cookie [] cookies = request.getCookies();
    		for (Cookie cookie : cookies) {
    			String name = cookie.getName();
    			String value = cookie.getValue();
    			logger.info("LOGGER : {}, {}", name, value);
    		}
    		return "main";
    	}
    ```
    

1. **Spring에서 Cookie 값 얻어오기**
    - **`@CookieValue`**
    ```java
      	// Spring 쿠키
	@GetMapping("/get2")
	public String get2(@CookieValue("userid") String s,
			               @CookieValue("JSESSIONID") String s2) {
		logger.info("LOGGER : userid = {}, JSESSIONID= {}", s, s2);
		return "main";

	}
```
---
