# 1. 자바 개발 플랫폼 3가지

1. **Java SE ( Java Standard Edition )**
    - 자바 spec
    - 환경구축빙법 : **JDK 17 설치**
    - 개발프로그램 형태 : 비웹 환경의 로컬로 실행되는 프로그램 개발이 가능
2. **Java EE ( Java Enterprise Edition )**
    - **servlet/JSP spec** ( spec은 인터페이스 라고 생각 )
        
        실제로 ***Servlet/JSP spec을 구현한 구현체***는 ***Tomcat 서버***가 제공하는 구현체를 사용할 것이다.
        
        - *jar 형태로 제공된다.
        - jsp-api.jar 와 servlet-api.jar 이 제공됨
    - 개발프로그램 형태 : 웹 어플리케이션 개발 가능
    - SE가 구축된 상태에서 EE(Tomcat)를 구축해야 EE 사용이 가능하다.
3.  **Java ME (Java  Micro Edition )**
    - 개발프로그램 형태 : 휴대용 장치에서 실행되는 개발 가능

---

# 2. 환경 설정

1. **Java SE 환경 구축 : JDK 17 설치**
    - JDK 설치후 2개의 환경변수 설정
        
        **JAVA_HOME=C:\Program Files\Java\jdk-17 <=== JDK의 홈디렉터리 경로 설정
        PATH=%JAVA_HOME%\bin;기본PATH <=== 윈도우의 프로그램에 명령어 경로 설정
        C:\Program Files\Java\jdk-17\bin;기본PATH**
        

1. **Eclipse 설치**
    - https://www.eclipse.org/
    - JDK 17 지원여부 확인 필수
    - eclipse-jee-2024-06-R-win32-x86_64.zip
    - 설치는 zip 파일 다운 후 압축 풀기

1. **Tomcat 서버 ( Tomcat 컨테이너 )**
    - https://jakarta.apache.org/
    - **JDK 17 버전을 지원하는 Tomcat 10 다운로드**
    - jsp-api.jar 와 servlet-api.jar 을 제공함
        
        (  Servlet 6.0 and Pages 3.1  ) : Pages는 JSP
        
        - Oracle에서 제공하는 spec이 Servlet 6.0 and Pages 3.1 이고, 이를 구현한 구현체가 Tomcat 10 이다.
    - apache-tomcat-10.1.28.zip
        - 설치는 zip 파일 다운 후 압축 풀기
    - **기본 port 번호 : 8080**
        - 만약 Oracle DB를 설피하면 내부적으로 tomcat을 설치함 (8080)
    
    <aside>
    💡
    
    tomcat 9  vs  tomcat 10
    
    - tomcat 9 : JDK11까지만 지원됨
        
                     패키지명은 **javax**.servletm
        
               패키지 관리는 Oracle로 했음
        
    - tomcat 10 : JDK17부터 지원됨
    
                       패키지명은 **jakarta**.servlet
    
                 패키지 관리를 Apache에서 관리함
    
    - 서블릿관련 API 문서
    
    https://tomcat.apache.org/tomcat-10.1-doc/servletapi/index.html
    
    </aside>
    
    - 필요시 환경변수 설정 가능
        
        CATALINA_HOME=C:\servlet_study\apache-tomcat-10.1.28
        

---

# 3. eclipse 와 Tomcat 연동

1. eclipse 실행 
    - C:\servlet_study\eclipse 에 workspace 파일 생성
    - 작업 디렉토리를 C:\servlet_study\eclipse\workspace 로 설정
    - Java EE Persperctive ( 디폴트 설정 )
    - 한글인코딩 설정 ( 디폴트지만 아닌 경우 설정해주기 )
        - window > preference > General > workspace > ㅆext file encoding > UTF-8 선택
        - window > preference > Web > html,css,jsp > encoding > UTF-8 선택
    - JDK 17로 변경
        - window > preference > Java > Compiler > JDK 버전을 17로 변경

1. eclipse 와 Tomcat 연동
    
    ![image (16)](https://github.com/user-attachments/assets/5e71603f-4acf-4933-8c41-d7e86eca7c38)

    ![image (15)](https://github.com/user-attachments/assets/70ba3a29-4d42-4d2f-add5-570b47202950)

- 서버생성 확인

![image (14)](https://github.com/user-attachments/assets/7088f4ea-a414-4624-8ce8-76f4f2da042f)


- 이후 서버 설정하기

---

# 4. 프로젝트 생성

- file > New > Dynamic Web Project 선택  ( 프로젝트 명 : HelloTest )
- Web Module 에서 출력된 내용은 아래와 같다.
    1. Context Root 
        - 기본값은 프로젝트명이다. ( 변경가능 )
        - 웹브라우저에서 요청시 사용된다.
            
            http://localhost:8090/ 까지 요청하면 Tomcat의 webapp 까지 도착
            
            이후 넘어갈 도착지를 Context Root로 알려주는 개념
            
            ( 예 > http://localhost:8090/HelloTest , [http://localhost:8090/](http://localhost:8090/docs/index.html)컨텍스트명)
            
        
        - 컨텍스트명(논리적인 경로 )
            - docs
            - examples
            - /
            - a
        
        - webapps안의 실제폴더(물리적인 경로)
            - docs
            - examples
            - ROOT
            - HelloTEST
        
        - 용도
            
            : 실제 tomcat의 배포경로인 webapps에 만들어지는 물리적인 폴더인 웹어플리케이션을 찾을때 사용하는 논리적인 이름을 context라고 한다.
            
        - 변경방법
            
            : 이클립스 servers 탭 > tomcat 서버 클릭 > module > edit > Path 에  context명 수정( 반드시  / 로 시작)
            
    2. Content Directory
        - 개발자가 만든 소스가 저장되는 eclipse 디렉터리
    3. web.xml
        - 배치 지시자 ( deployment descriptor )라 부르고 생성된 웹 어플리케이션(HelloTest)의 전반적인 설정정보를 담당하는 역할
        
          *  웹 어플리케이션 설정 정보를 등록하는 방법 2가지
        
        - web.xml
        - 어노테이션 ( @로 시작 )

---

# 5. 생성된 웹어플리케이션 디렉터리 구조

HelloTest

Java Resource

src/main/java    <== 소스파일 저장

Libraries

JRE System Library [ Java SE 17 ]           <==    JDK 라이브러리 

Servlet Runtime [apach-Tomcat v10.1]  <==    jsp-api.jar, servlet-api.jar

src

main

java          <==   소스파일 (java) 저장

webapp    <==   웹 관련 파일 ( jsp, css, js, img등 )이 이클립스에 저장되는 디렉터리

WEB-INF   <==    대문자로 지정, 웹 어플리케이션에서는 필수임. 이 안의 파일들은 웹 브라우저에서 접근이 불가(보안상)

lib        <==    외부에서 가져와서 사용하는 라이브러리 ( .jar ) 등록 폴더

           나중에 mybatis.jar 와 mysql-connector.jar 2개의 파일을 저장할 예정

web.xml  <==  웹 어플리케이션의 전반적인 설정정보를 담당

*.jsp    <==   jsp, css, js, img등은 WEB-INF와 같은 레벨에 만들어야 햔다.

*.css

*js

images

---

# 6. tomcat 의 배포된 디렉터리 구조

tomcat/webapps  <==   배포 경로 ( deploy path )

HelloTest  <==  웹 어플리케이션 ( 물리적인 디렉터리 )

META-INF

WEB-INF

classes

lib

web.xml

main.jsp

css

js

images

![image (13)](https://github.com/user-attachments/assets/2035056e-5e96-47c0-b308-71c2f62d6ef1)


http://localhost:8090/HelloTest/main.jsp

http://localhost:8090/a/main.jsp

위 두 경로 요청시 둘 다 정상적으로 결과가 반환된다. 

---

# 7. 서버에 작성 가능한 3가지 컴포넌트

 클라이언트                                                            서버 ( tomcat : 8090 )

(웹 브라우저)   —————- 요청 ——————> 1) html ( 정적 컴포넌트 )

                                                                             - src/main/webapp 에 저장

                                                                          2) jsp   ( 동적 컴포넌트 )

                                                                        - src/main/webapp 에 저장

                <—————- 응답 ———-———   3) 응답 ( 동적 컴포넌트 )

                                                                             - src/main/webapp 에 저장

                  

---

# 8. 3가지 컴포넌트 웹 브라우저에서 요청하는 URL

- 문법 :  http://서버IP:port번호/컨텍스트명/자원 (html, jsp, servlet)
1. 정적 컴포넌트 ( html )  -   디렉터리가 없는 경우
    
    요청 URL  :  http://서버IP:port번호/컨텍스트명/html자원
    
     클라이언트                                                            서버 ( tomcat : 8090 )
    
              a. http://localhost:8090:컨텍스트명/main.html
    
                   —————————요청————————> b. main.html 검색
    
                                                                                          없으면 404 에러
    
                                                                                          있으면 다운로드
    
             <———— c. main.html 다운로드  —————
    

    d. main.html렌더링

1. 정적 컴포넌트 ( html )  -   디렉터리가 있는 경우
    
    요청 URL  :  http://서버IP:port번호/컨텍스트명/디렉터리명/html자원
    
    예 >  a. http://localhost:8090:컨텍스트명/html/test.html
    

1. 동적 컴포넌트 ( jsp )  -  디렉터리 없는 경우
    
    요청 URL  :  http://서버IP:port번호/컨텍스트명/jsp자원
    
     클라이언트                                                            서버 ( tomcat : 8090 )
    
              a. http://localhost:8090:컨텍스트명/main.html
    

               —————————요청————————> b. main.jsp 검색

                                                                                      없으면 404 에러

                                                                                      있으면  3단계 실행됨

                          ( C:\servlet_study\apache-tomcat-10.1.28\work\컨텍스트명 폴더에서 확인 가능 )

                                                                                  가. 변환단계

                                                                                  main.jsp  —> main_jsp.java

                                                                                  나. 컴파일 단계

                                                                                  main_jsp.java  —> main_jsp.class

                                                                                  다. 실행 단계

                                                                                  main_jsp.class  —> html로 결과가 나옴

         <———— c.  html 다운로드  —————

    d.  html렌더링

---
# 9. 서블릿 ( servlet )

: 서블릿은 ***자바 기반의 동적 웹 어플리케이션 개발을 위한 서버 측 기술***로, **클라이언트의 요청을 처리하고 응답을 생성하는 역할**을 한다. 

- Java EE 스펙의 일부로, **Tomcat 서버에서 주로 실행된다.**

## 1) 서블릿 특징

- ***.java** 로 작성됨
- 저장위치는 이클립스의 **src/main/java 에 저장되고 반드시 패키지를 사용**해야 한다.
- **main 메서드가 없다**. 즉, 시작점이 없다.
    
    이유는 사용자가 요청하는 컴포넌트가 시작점 역할을 한다. 
    
- 사용자가 직접 new 하지 않아도 **tomcat 컨테이너가 필요한 시점에 new 하고 소멸까지 담당**한다.
- 실행결과는 html로 나온다.
- Servlet 6.0 버전은 Tomcat 10 이상 필요로 하고 패키지명은 javax가 아닌 jakarta 패키지로 시작된다.
- Tomcat 10의 servlet-api.jar에 포함된 패키지를 사용해서 서블릿을 구현할 수 있다.
    - 참조할 API 문서는 https://tomcat.apache.org/tomcat-10.1-doc/servletapi/index.html 이다.

## 2) 구현방법

1. **패키지로 작성**
2. extends HttpServlet   (  jakarta.servlet.http 패키지, 추상클래스 )
    
    ```
    * 계층구조 ( 중요 *** )
    
     Servlet (인터페이스)  , ServletConfig (인터페이스)
            |
            |
       GenericServlet (추상) 
            |
        HttpServlet (추상) 
            |
      사용자 정의 서블릿
    ```
    
    - **Servlet** (인터페이스)   ⇒   jakarta.servlet 패키지
        
        https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/Servlet.html
        
        - [**init**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/Servlet.html#init(jakarta.servlet.ServletConfig))([**ServletConfig**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletConfig.html) config)  :  서블릿 생성시 자동으로 호출 콜백
        - [**destroy**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/Servlet.html#destroy())()  :   서블릿이 삭제시 자동으로 호출 콜백
        - [**service**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/Servlet.html#service(jakarta.servlet.ServletRequest,jakarta.servlet.ServletResponse))([**ServletRequest**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletRequest.html) req, [**ServletResponse**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletResponse.html) res)  :  서블릿이 해야하는 실제 작업을 정의하는 메서드
        - [**getServletConfig**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/Servlet.html#getServletConfig())()  :  ServletConfig 를 리턴해주는 메서드
    
    - **ServletConfig** (인터페이스)    ⇒   jakarta.servlet 패키지
        
        https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletConfig.html
        
        - [**getInitParameter**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletConfig.html#getInitParameter(java.lang.String))([**String**](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html) key)  :  문자열로 값을 반환
        - [**getInitParameterNames**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletConfig.html#getInitParameterNames())()  :  key 값만 반환 , [**Enumeration](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Enumeration.html)** 타입으로 반환 ( Iterator 비슷한 기능 )
        - [**getServletContext**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletConfig.html#getServletContext())()  :  [**ServletContext**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletContext.html) 타입을 반환
            - 최종적으로 사용자가 만든 서블릿에서 [**ServletContext**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletContext.html)을 얻는 방법은  **`ServletContext sc = getServletContext**();` 이다.
    
    - **ServletContext** (인터페이스)   ⇒   jakarta.servlet 패키지
        
        https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletContext.html
        
        - [**addFilter**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletContext.html#addFilter(java.lang.String,jakarta.servlet.Filter))([**String**](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html) filterName, [**Filter**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/Filter.html) filter)
        - [**createFilter**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletContext.html#createFilter(java.lang.Class))([**Class**](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Class.html)<T> c)
        - [**addServlet**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletContext.html#addServlet(java.lang.String,jakarta.servlet.Servlet))([**String**](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html) servletName, [**Servlet**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/Servlet.html) servlet)
        - [**createServlet**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletContext.html#createServlet(java.lang.Class))([**Class**](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Class.html)<T> c)
        - [**setAttribute**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletContext.html#setAttribute(java.lang.String,java.lang.Object))([**String**](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html) name, [**Object**](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Object.html) object) , [**getAttribute**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletContext.html#getAttribute(java.lang.String))([**String**](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html) name). [**removeAttribute**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletContext.html#removeAttribute(java.lang.String))([**String**](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html) name)
        - [**getContextPath**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletContext.html#getContextPath())()
        - [**getInitParameter**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletContext.html#getInitParameter(java.lang.String))([**String**](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html) name)
        - [**getInitParameterNames**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletContext.html#getInitParameterNames())()
    
    - **GenericServlet** (추상)    ⇒   jakarta.servlet 패키지
        
        https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/GenericServlet.html
        
        - [**init**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/GenericServlet.html#init())()
        - [**log**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/GenericServlet.html#log(java.lang.String))([**String**](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html) message)
        - 나머지는 위 인터페이스 메서드 재정의

- **HttpServlet** (추상)   ⇒   jakarta.servlet.http 패키지
    
    https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/http/HttpServlet.html
    
    - [**doGet**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/http/HttpServlet.html#doGet(jakarta.servlet.http.HttpServletRequest,jakarta.servlet.http.HttpServletResponse))([HttpServletRequest](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/http/HttpServletRequest.html) req, [HttpServletResponse](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/http/HttpServletResponse.html) resp)
        
        **: 클라이언트에서 get 방식으로 요청시 처리하는 메서드**
        
    - [**doPost**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/http/HttpServlet.html#doPost(jakarta.servlet.http.HttpServletRequest,jakarta.servlet.http.HttpServletResponse))([HttpServletRequest](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/http/HttpServletRequest.html) req, [HttpServletResponse](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/http/HttpServletResponse.html) resp)
        
        **: 클라이언트에서 post 방식으로 요청시 처리하는 메서드**
        
    - [**doDelete**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/http/HttpServlet.html#doDelete(jakarta.servlet.http.HttpServletRequest,jakarta.servlet.http.HttpServletResponse))( … )
    - [**doPut**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/http/HttpServlet.html#doPut(jakarta.servlet.http.HttpServletRequest,jakarta.servlet.http.HttpServletResponse)) ( … )
    
    ⇒ method 불일치 : get 요청  —> doPost 처리하고자 하면 405 에러 발생함
    

- 사용자 정의 서블릿
    
    : 위에서 살펴본 메서드를 바로 사용하거나 재정의 할 수 있다.
    
1. **doGet(기본)** 또는 **doPost** 를 반드시 재정의해야 한다.
    
    ```
    package com.servlet;
            public void MyServlet ectends HttpServlet{
    public void doDet(**HttpServletRequest req, HttpServletResponse resp**) {
    			// 실제 코드 작업
    		}
    	}
    ```
    

- **HttpServletRequest**   ⇒  요청관련 작업 담당
    
    https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/http/HttpServletRequest.html
    
    - [**String](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html) [getParameter](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletRequest.html#getParameter(java.lang.String))([String](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html) name)**
        
        :  키값(name)을 넣어서 value를 얻어올 수 있다.
        
    - [**String**](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html)[] [getParameterValues](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletRequest.html#getParameterValues(java.lang.String))([String](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html) name)
    : name은 하나인데 value가 여러개일떼, 배열로 반환
    - [**Enumeration**](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Enumeration.html)<[String](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html)> [getParameterNames](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletRequest.html#getParameterNames())()
    : name을 알아와야 할 때
    - **void [setAttribute](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletRequest.html#setAttribute(java.lang.String,java.lang.Object)) ([String](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html) name, [Object](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Object.html) o)**
        
        : 키-벨류를 쌍으로 저장할 수 있는 메서드
        
    - [**RequestDispatcher**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/RequestDispatcher.html) [getRequestDispatcher](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletRequest.html#getRequestDispatcher(java.lang.String))([String](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html) path)
        
        : **지정된 path로 요청**이 들어감. JS의 location.href와 비슷한 기능
        
    - [**Cookie**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/http/Cookie.html)[] [**getCookies**](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/http/HttpServletRequest.html#getCookies())()
        
        : **쿠키 정보**를 얻어오는 매서드
        
        - **쿠키과 세션**
            
            <aside>
            💡
            
            세션 
            
            - 로그인 시 유지, 웹사이트 이용시간
            
            쿠키
            
            - 광고용 상품정보, 로그인 정보 저장
            </aside>
            
    - [**HttpSession](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/http/HttpSession.html) [getSession](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/http/HttpServletRequest.html#getSession())**()
        
        : **세션 정보**를 얻어오는 메서드
        
    - [**String](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html) [getHeader](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/http/HttpServletRequest.html#getHeader(java.lang.String))**([**String**](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html) name)
        
        : header 값 조회
        
- **HttpServletResponse**   ⇒   응답관련 작업 담당
    
    https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/http/HttpServletResponse.html
    
    - **void [addCookie](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/http/HttpServletResponse.html#addCookie(jakarta.servlet.http.Cookie))([Cookie](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/http/Cookie.html) cookie)**
        
        : **쿠키정보를 웹브라우저에 추가**하는 메서드
        
    - **void [sendRedirect](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/http/HttpServletResponse.html#sendRedirect(java.lang.String))([String](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html) location)**
    : **지정된 location 경로로 요청**을 보내는 메서드, redirect 방법으로 부른다.
    - **void [setContentType](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletResponse.html#setContentType(java.lang.String))([String](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html) type)**
        
        : **서버가 클라이언트에게 전달한 데이터의 터입(MIME 타입)을 설정하는** 메서드 
        
    - [**PrintWriter**](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/io/PrintWriter.html) [getWriter()](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletResponse.html#getWriter())
        
        : [PrintWriter](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/io/PrintWriter.html) 타입 반환, **PrintWriter의 print(값)을 이용해서 클라이언트에게 응답을 전달**하는 메서드
        
1. **서블릿 맵핑 ( servlet mapping )**
    
    : **서블릿 요청시 *별칭을 사용해서* 요청하는 방법**
    
    1. 별칭 사용하지 않는 경우 ( OLD  버전, 현재 사용불가 )
        
        문법 : **`http://서버ip:port번호/컨텍스트명/servlet/패키지명을 포함한 서블릿명`**
        
        - http://localhost:8090/app01/servlet/com.servlet.MyServlet
    2. 별칭 사용하는 경우 ( 현재는 반드시 별칭을 사용해야 함 )   ⇒  **매핑**
        
        문법 : **`http://서버ip:port번호/컨텍스트명/별칭`**  
        
        - http://localhost:8090/app01/test
    
    - **서블릿 메핑 정보를 저장하는 방법** 2가지
        1. **web.xml**  ( 기본 )
            - Spring framework 에서도 xml을 사용
            - TestServlet.java
                
                ```java
                package com.servlet;
                
                public class TestServlet extends HttpServlet {
                	
                	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
                	    //  console에 출력됨
                		System.out.println("TestServlet"); 
                	}
                }
                
                ```
                
            - web.xml
                
                ```xml
                <?xml version="1.0" encoding="UTF-8"?>
                <web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="https://jakarta.ee/xml/ns/jakartaee" xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee https://jakarta.ee/xml/ns/jakartaee/web-app_6_0.xsd" id="WebApp_ID" version="6.0">
                  **<servlet>**
                    <servlet-name>TestServlet</servlet-name>
                    <servlet-class>com.servlet.TestServlet</servlet-class>
                  </servlet>
                  **<servlet-mapping>**
                    <servlet-name>TestServlet</servlet-name>
                    <url-pattern>**/test**</url-pattern>
                  </servlet-mapping>
                </web-app>
                ```
                
        2. **어노테이션 (@)**
            - @WebServlet(”/test3”)
                
                ```java
                package com.servlet
                
                **@WebServlet("/test3")**
                public class TestServlet3 extends HttpServlet {
                
                	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
                	    //  console에 출력됨
                		System.out.println("TestServlet3"); 
                	}
                }
                ```
---
# 서블릿의 LifeCycle

# 10. 서블릿의 LifeCycle

: **Tomcat 컨테이너가 서블릿(JSP)을 생성부터 삭제까지 관리**한다. 이때 생성 또는 삭제할 때 콜백되는 메서드가 제공된다.

1. **init() 메서드**
    
    : 서블릿이 생성될 떄 호출
    
    - **서블릿이 생성될 때 단 한번만 실행된다.**

1. **서비스 메서드**
    
    : 서블릿에 요청할 때 호출
    
    - **doGet() 또는 doPost()**
    - **클라이언트가 요청할 때마다 매번 실행된다.**
    
2. **destroy() 메서드**
    
    : **서블릿이 삭제될 때 호출**
    
    - 서블릿을 수정한 후 기다리면 tomcat 컨테이너가 재실행되면서 destroy를 확인할 수 있다.

---

# 11. thread-safe 와 thread-unsafe

1. **인스턴스 변수**
    
    : 서블릿은 단 한번만 생성되기 때문에 인스턴스 변수는 **여러 사용자들간에 공유가 가능**하다.
    
    - **thread-unsafe**

1. **doGet 메서드의 로컬변수**
    
    : 로컬변수이기 때문에 사용자들간에 **공유 불가능**
    
    - **thread-safe**
    

⇒ 따라서 ***여러 사용자가 공유할 목적이 아니라면 로컬 변수로 사용해야 한다.*** 만약 인스턴스 변수 및 static 변수로 만들면 여러 사용자가 공유할 수 있게 된다.

```java
package com.servlet;

@WebServlet("/test")
public class TestServlet extends HttpServlet {
	// 인스턴스 변수
	// 여러 사용자들간에 공유가 됨 => thread-unsafe
	int num = 10;
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		num++;
		System.out.println("TestServlet 인스턴스변수 : "+ num);
		
		// 로컬변수는 thread-safe 
		int size = 10;
		size++;
		System.out.println("TestServlet 로컬 변수 : "+size);
	
	
// 인스턴스 변수는 공유가 되기에 계속 ++ 되고, 로컬변수는 한번만 ++ 된다.
//		TestServlet 인스턴스변수 : 11
//		TestServlet 로컬 변수 : 11
//		TestServlet 인스턴스변수 : 12
//		TestServlet 로컬 변수 : 11
//		TestServlet 인스턴스변수 : 13
//		TestServlet 로컬 변수 : 11

	}
}
```

---
# 12. 서블릿의 응답처리

## 1) 개념

: **서블릿에서 html을 작성해서 웹 브라우저에게 html 응답하는 작업**을 의미

- httpServletResponse API 이용

## 2) 순서

1. **MIME 타입 지정**
    
    : ***웹브라우저에게 전달하는 데이터 타입***을 알려주는 작업 
    
    **`response.setContentType(”text/html”);`**
    
    - Tomcat 10은 한글 응답이 자동으로 처리되지만 Tomcat 9는 한글 응답이 처리되어 있지 않는다.
    - 이런 경우 **`response.setContentType(”text/html;charset=utf-8”);`**  사용
2. **I/O 객체 얻기**
    
    **`PrintWriter out = response.getWriter();`**
    
3. **print(값) 이용해서 값 출**력 ( 웹 브라우저에서 렌더링 됨 )
    
    **`out.print(”<html>”);`**
    
    `…`
    
    **`out.print(”</html>”);`**
    

```java
package com.servlet;

@WebServlet("/test")
public class TestServlet extends HttpServlet {

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		
		// 콘솔에 출력
		System.out.println("TestServlet");
		
		// 웹 브라우저에 출력 (응답처리) 
		response.setContentType("text/html");
		
		PrintWriter out = response.getWriter();
		
		out.print("<html>");
		out.print("<body>");
		out.print("hello, 안녕하세요");
		out.print("</body>");
		out.print("</html>");
	}
}
```

---

# 13. 서블릿 요청처리

## 1) 개념

: **웹 브라우저에서 사용자 입력폼에 값을 입력하고 서블릿으로 전달하는 방법**처리

- HttpServletRequest API 이용

## 2) 메서드

- **request.getParameter(String name)**
- **request.getParameterValues(String name)**
- **request.getParameterNames()**

## 3) 아키텍처

### 실습 (GET)

1. **request.getParameter(String name)**
    
    : name(key)에 해당하는 value를 출력
    
    - memberFrom.html
        
        ```html
        <!DOCTYPE html>
        <html>
        <head>
        <meta charset="UTF-8">
        <title>Insert title here</title>
        </head>
        <body>
        http://localhost:8090/app05/memberForm.html 
        http://localhost:8090/app05/mem?userid=aaa&passwd=1234
        
        <h1>1. request.getParameter(name) 실습 - GET방식</h1>
        	**<form action="mem" method="get">**
        		아이디: <input type="text" name="**userid**"> <br>
        		비번: <input type="text" name="**passwd**"> <br>
        		<input type="submit" value="로그인">
        	</form>
        
        </body>
        </html>
        ```
        
    - MemberServlet.java
        
        ```java
        package com.servlet;
        
        import jakarta.servlet.ServletException;
        import jakarta.servlet.annotation.WebServlet;
        import jakarta.servlet.http.HttpServlet;
        import jakarta.servlet.http.HttpServletRequest;
        import jakarta.servlet.http.HttpServletResponse;
        import java.io.IOException;
        
        **@WebServlet("/mem")**
        public class MemberServlet extends HttpServlet {
        
        	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        	
        		**String userid = request.getParameter("userid");
        		String passwd = request.getParameter("passwd");**
        		
        		System.out.println(userid + " " +passwd);
        	}
        
        }
        
        ```
        

1. **request.getParameterValues(String name)**
    
    : name(key)로 접근하고, key의 value가 여러개일때 사용해 배열로 값을 출력
    
    - memberFrom.html
        
        ```html
        	<h1>3. request.getParameterValues(name) 실습 - GET방식</h1>
        	<form action="mem3" method="get">
        		아이디: <input type="text" name="userid"> <br>
        		비번: <input type="text" name="passwd"> <br>
        		취미:
        		야구 <input type="checkbox" name="hobby" value="야구"> <br>
        		농구 <input type="checkbox" name="hobby" value="농구"> <br>
        		축구 <input type="checkbox" name="hobby" value="축구"> <br>
        		
        		<input type="submit" value="로그인">
        	</form>
        ```
        
    - MemberServlet3.java
        
        ```java
        @WebServlet("/mem3")
        public class MemberServlet3 extends HttpServlet {
        
        	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        		String userid = request.getParameter("userid");
        		String passwd = request.getParameter("passwd");
        		
        		// 체크박스에서 체크된 값만 넘어간다. 
        		String [] hobbies = request.getParameterValues("hobby");
        		
        		System.out.println(userid + " "+passwd);
        		
        		System.out.println(Arrays.toString(hobbies));
        	}
        }
        ```
        

1. **request.getParameterNames()**
    
    : 파라미터의 name(key)를 얻어와서, 키를 통해 value를 출력
    
    - memberFrom.html
        
        ```html
        	<h1>4. request.getParameterNames() 실습 - GET방식</h1>
        	<form action="mem4" method="get">
        		아이디: <input type="text" name="userid"> <br>
        		비번: <input type="text" name="passwd"> <br>
        		이메일: <input type="text" name="email"> <br>
        		주소: <input type="text" name="address"> <br>
        		<input type="submit" value="로그인">
        	</form>
        ```
        
    - MemberServlet4.java
        
        ```java
        @WebServlet("/mem4")
        public class MemberServlet4 extends HttpServlet {
        
        	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        		**Enumeration<String> enu = request.getParameterNames();**
        		while(enu.hasMoreElements()) {
        			String key = enu.nextElement();
        			String value = request.getParameter(key);
        			System.out.println(key + "  " +value);
        		}
        	}
        }
        ```
        

⇒ GET 방식으로 요청했을 경우

- 한글처리가 자동으로 설정됨 (tomcat10)
- 일치하지 않는 name을 지정하면 null 값이 반환됨
- post(get) 요청햇는데 doGet(doPost)로 받으면 **405 에러**가 발생됨
- 상대경로 / 절대경로
    - <form action =”상대경로/절대경로”>
        
        : 절대경로는 action = ”/컨텍스트명/서블릿맵핑” 형식이고,
        
          상대결로는 action=”/서블릿맵핑” 이다.
        

### 실습 (POST)

: post 방식이기에 url에 전달되는 데이터 정보가 보이지 않는다. 나머지 데이터를 받아오고 출력하는 방법은 get방식과 동일하다.

1. **request.getParameter(String name)**
    - memberFrom.html
        
        ```html
        	<h1>2. request.getParameter(name) 실습 - POST방식</h1>
        	<form action="**mem2**" method="**post**">
        		아이디: <input type="text" name="**userid**"> <br>
        		비번: <input type="text" name="**passwd**"> <br>
        		<input type="submit" value="로그인">
        	</form>
        ```
        
    - MemberServlet2.java
        
        ```java
        @WebServlet("/**mem2**")
        public class MemberServlet2 extends HttpServlet {
        
        	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        	
        		**String userid = request.getParameter("userid");
        		String passwd = request.getParameter("passwd");**
        		
        		System.out.println(userid + " " +passwd);
        	}
        }
        ```
        

⇒ POST 방식으로 요청했을 경우

- 한글처리가 자동으로 설정됨
- tomcat 9 한글이 깨지는경우, 한글처리를 명시적으로 해야한다.
    
    `request.setCharacterEncoding(”utf-8”);`
    

### doGet과 doPost

: HttpServlet 클래스에서 제공하는 메서드로, HTTP 요청을 처리하는 서블릿의 핵심 메서드이다.

- doGet 메서드
    - 클라이언트가 서버에 데이터를 요청할 때 사용
    - URL의 쿼리 파라미터를 통해 데이터를 전달
        - URL에 데이터를 포함해 데이터 크기가 제한됨
        - 또한 전달되는 데이터가 URL상으로 노출됨
    - 브라우저나 프록시 서버에서 요청이 캐싱될 수 있다.
        - 동일한 요청은 서버가 아닌 캐시에서 응답받을 수 있음
    - 검색 요청 및 데이터 조회의 용도

- doPost 메서드
    - 클라이언트가 서버에 데이터를 제출하거나 업데이트를 요청할 때 사용
    - 요청 데이터는 HTTP 요청 본문(body)에 포함되어 전달
        - 데이터가 본문에 포함되기에 대용량 데이터 전송에 적합
        - 데이터 노출이 없기에 보안성이 높음
    - 기본적으로 캐싱되지 않는다.
    - 사용자 로그인/회원가입, 파일 업로드, 데이터 생성 및 수정의 용도

---
# 14. scope

## 1) 개념

: 자바의 변수(로컬변수, 인스턴스변수, static변수)처럼 **tomcat 컨테이너가 자동으로 생성해주는 3가지 객체의 scope**를 의미한다.

## 2) 3가지 scope

: **변수처럼 데이터를 저장할 수 있는 능력**을 가진다는 공통점이 있다.

1. **request scope**
    - **`*httpServletRequest API*`**
        
        https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/http/HttpServletRequest.html
        
    - 데이터 처리
        - **저장방법 : request.[setAttribute](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletContext.html#setAttribute(java.lang.String,java.lang.Object))([String](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html) name, [Object](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Object.html) object)**
        - **조회방법 : request.[getAttribute](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletContext.html#getAttribute(java.lang.String))([String](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html) name)**
        - **삭제방법 : request.[removeAttribute](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletContext.html#removeAttribute(java.lang.String))([String](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html) name)**
    - 저장된 데이터의 범위 ( lifecycle )
        - **doGet 메서드안에서만** 유지되어 사용가능하다. 즉, 사용자가 요청을 해서 응답을 받을때 까지 살아있다.
2. **session scope**
    - **`*httpSession API*`**
        
        https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/http/HttpSession.html
        
        - **session 받아오는 방법**
            
            **`HttpSession session = request.[getSession](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/http/HttpServletRequest.html#getSession())**()**;**`
            
    - 데이터 처리
        - **저장방법 : session.[setAttribute](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/http/HttpSession.html#setAttribute(java.lang.String,java.lang.Object))([String](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html) name, [Object](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Object.html) value)**
        - **조회방법 : session.[getAttribute](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/http/HttpSession.html#getAttribute(java.lang.String))([String](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html) name)**
        - **삭제방법 : session.[removeAttribute](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/http/HttpSession.html#removeAttribute(java.lang.String))([String](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html) name)**
    - 저장된 데이터의 범위
        - 요청한 **웹브라우저와 scope가 동일**하다.
        - 사용자가 요청시 사용한 웹브라우저를 **계속 open하고 있으면 사용 가능**하고, close하면 데이터가 제거된다. ( 크롬으로 열면 크롬에서만, ***브라우저가 동일해야 적용된다**.* )
        - 보안이슈로 일정시간 이상 브라우저를 open해두면 세션이 끊기도록 ***타임아웃 기능***을 주로 사용한다.
            - tomcat의 타임 아웃은 30분이다. (수정가능)
    - 용도 : **로그인**
    
3. **application scope**
    - **`*ServletContext API*`**
        
        https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletContext.html
        
        - **context 받아오는 방법**
            
            **`ServletContext application = [getServletContext()](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletConfig.html#getServletContext())**;`
            
    - 데이터처리
        - **저장방법 : application.[setAttribute](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletContext.html#setAttribute(java.lang.String,java.lang.Object))([String](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html) name, [Object](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Object.html) object)**
        - **조회방법 : application.[getAttribute](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletContext.html#getAttribute(java.lang.String))([String](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html) name)**
        - **삭제방법 : application.[removeAttribute](https://tomcat.apache.org/tomcat-10.1-doc/servletapi/jakarta/servlet/ServletContext.html#removeAttribute(java.lang.String))([String](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html) name)**
    - 저장된 데이터의 범위
        - **tomcat 컨테이너와 scope가 동일**하다. ( scope가 제일 길다. )
        - tomcat 컨테이너를 종료하지 않으면 계속 사용 가능하다. 종료하면 데이터가 제거된다.
    - 용도 : 블로그 접속자수

### 실습(set)

```java
@WebServlet("/set")
public class SetServlet extends HttpServlet {
	
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		
		// scope 저장
		// 1. request scope에 저장 (요청 ~응답)
		**request.setAttribute("request", "request scope");**
		
		// 2. session scope (요청한 웹브라우저와 스코프 동일)
		**HttpSession session = request.getSession();**
		**session.setAttribute("session", "session scope");**
		
		// 3. application scope (tomcat 컨테이너)
		**ServletContext application = getServletContext();
		application.setAttribute("application", "application scope");**
		
		// 응답처리
		**response.setContentType("text/html");**
		
		**PrintWriter out = response.getWriter();**
		
		**out.print("<html>");**
		out.print("<body>");
		out.print("request scope 값 : "+ request.getAttribute("request") +"<br>"); 
		out.print("session scope 값 : "+ session.getAttribute("session") +"<br>");
		out.print("application scope 값 : "+ application.getAttribute("application") );
		out.print("</body>");
		out.print("</html>");
	}
}
```

### 실습(get)

```java
@WebServlet("/get")
public class GetServlet extends HttpServlet {

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
	
		// scope 조회
		// 1. request scope
		**String s =  (String)request.getAttribute("request");**
		
		// 2. session scope
		**HttpSession session = request.getSession();
		String s2 =  (String)session.getAttribute("session");**
		
		// 3. application scope (tomcat 컨테이너)
		**ServletContext application = getServletContext();
		String s3 =  (String)application.getAttribute("application");**
		
		// 응답처리
		**response.setContentType("text/html");**
		
		**PrintWriter out = response.getWriter();**
		
		**out.print("<html>");**
		out.print("<body>");
		out.print("request scope 값 : "+ s +"<br>"); 
		out.print("session scope 값 : "+ s2 +"<br>");
		out.print("application scope 값 : "+ s3 );
		out.print("</body>");
		out.print("</html>");
		
	}
}
```

1. **request scope**
    
    request scope의 생존 범위는 사용자의 요청 ~ 응답까지
    
    응답이 나온 직후(set 실행후) 사라진다. 따라서 request scope는 null 로 출력된다.
    
    - [localhost:8090/app06/set](http://localhost:8090/app06/set)
      	![image (17)](https://github.com/user-attachments/assets/ca705ac8-761f-4162-9311-2a0cd41d5362)

        
    - [localhost:8090/app06/get](http://localhost:8090/app06/get)

       ![image (18)](https://github.com/user-attachments/assets/91d248d0-a2b7-4699-8965-fa469d83bfd8)

        
2. **session scope**
    - session scope는 **같은 브라우저에 한해서 웹브라우저가 open되어 있으면 계속 생존**한다.
        - [localhost:8090/app06/get](http://localhost:8090/app06/get)  : Edge에서 열었을 때
          	![image (19)](https://github.com/user-attachments/assets/6229fb5b-a3f0-486f-a52b-1ced76d7261e)
		set과 같은 브라우저를 사용하고, 브라우저가 open된 상태이기에 값이 출력된다. 
        
        - http://localhost:8090/app06/get : Chrome에서 열었을 때
            ![image (20)](https://github.com/user-attachments/assets/9c273903-d039-4449-bd5b-5ff8c424420b)

            
        
              브라우저는 open된 상태이지만, set과 다른 브라우저이기에 null로 출력된다.
        
    - **브라우저가 닫힌 경우**
        
        위에서 확인한 브라우저 창을 닫은 후, 다시 Edge에서 [localhost:8090/app06/get](http://localhost:8090/app06/get) 로 접속하면 null로 출력된 것을 확인할 수 있다.
		![image (21)](https://github.com/user-attachments/assets/31d4ed45-22ff-475c-9442-8b3bde7c42ef)

        

3.  **application scope**
    
    tomcat 컨테이너가 종료되기전까지 계속 생존한다. 위 실습에서 항상 값이 출력되는 것을 확인할 수 있었다.

---
# filter

# 15. 필터 (filter)

## 1) 용도

: 서블릿에 요청하기 전이나 응답한 후에 특별한 작업을 수행

- HTTP 요청 및 응답에 전처리와 후처리를 수행할 수 있는 컴포넌트

## 2) 구현

: 서블릿과 마찬가지로 필터 클래스를 작성하고 등록해야 한다. 

1. 패키지
2. implements filter
3. 메서드 재정의
    
    `doFilter( request, response, FilterChain chaih ) {`
    
     `// 요청을 다음 필터 또는 서블릿으로 전달`        
    
    `chain.doFilter( request, response );`          
    
    `}`
    
4. web.xml 등록 ( 필터 맵핑 )
    
    ```html
      <filter>
        <filter-name>MyFilter</filter-name>
        <filter-class>com.filter.MyFilter</filter-class>
      </filter>
      <filter-mapping>
        <filter-name>MyFilter</filter-name>
        <url-pattern>/*</url-pattern>
      </filter-mapping>
    ```
    

### 특징

- 요청 및 응답 처리
- 체인 형태의 동작
    - 여러 필터를 설정해 순차적으로 진행 가능
- 공통 작업 처리
    - 보안 체크(인증), 로깅, ..
- 동작 흐름 :
    1. 클라이언트 요청
    2. 필터에서 전쳐리 작업
    3. 요청이 다음 필터로 전달 또는 최종 리소스(서블릿/JSP)로 전달 
    4. 응답 생성 
    5. 필터에서 후처리 작업 
    6. 응답이 클라이언트에 전달

---
# 16. DB 연동 ( MyBatis 이용 )

## 1) 2개의 jar

- mybatis-3.5.14.jar
- mysql-connector-j-8.0.33.jar

: JavaSE 환경에서는 프로젝트 > Build Path > Configure Build Path > libraries > class path 선택 후 add external에서 2개의 jar 파일을 선택

- JavaEE 환경에서는 EB-INF/lib 안에 2개의 jar 파일을 복사
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/686c9583-1330-4ae4-99da-86732a9a0b13/67ccaa5f-4ca2-41c8-af1d-be188cba6659/208c57b7-0ff0-46df-8a97-a5cb9f93c4cf.png)
    

## 2) DB 연동을 위한 4가지 정보 설정

- jdbc.properties
- com.confing 패키지 이용

## 3) DTO 작성

- com.dto.EmpDTO.java 작성

## 4) 2개의 xml

- Configuration.xml
- DeptMapper.xml
- com.confiig 패키지 이용

## 5) MySqlSessionFactory.java

- com.confiig 패키지 이용

## 6) DAO, Service 작성

- com.dao.EmpDAO.java
- com.service.EmpService.java, com.service.EmpServiceImpl.java

## 7) 서블릿 작성

- com.servlet.EmpListServlet

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/686c9583-1330-4ae4-99da-86732a9a0b13/78768f52-c82d-45d0-a497-0d0df94f8370/6644aec5-2180-4355-a970-69884620ce53.png)

![구조](https://prod-files-secure.s3.us-west-2.amazonaws.com/686c9583-1330-4ae4-99da-86732a9a0b13/b3fc82e4-4c8a-47f1-a7f4-792e037655c2/bb5e615b-386b-45df-b61a-4a5f7d85dde9.png)

구조

---

# 17. 요청 위임

## 1) 개념

1. 일반적인 경우
    
    웹브라우저 <====== 요청/응답 ======⇒ 서블릿
    

b. 요청 위임한 경우

웹 브라우저 ======= 요쳥 =========⇒ 서블릿

              <==================== ( 서블릿, JSP, html )

## 2) 요청위임 방법 2가지

### 1. forward 방식

- **HttpServletRequest API** 이용
- 문법 :
    
    `request.getRequestDispatcher(”타겟.jsp”).forward(request, response);`
    
- 특징 :
    - **URL 변경이 되지 않는다**. 서블릿으로 그대로 남는다.
    - 하나의 request로 서블릿 및 JSP까지 사용한다.
    - 서블릿에서 3가지 스코프(request, session, application)에 데이터를 저장하고 JSP에서 가져올 때 **모든 스코프의 데이터를 참조할 수 있다.**

### 2. redirect 방식

- **HttpServletResponse API** 이용
- 문법 :
    
    `response.sendRedirect(”타겟.jsp”);`
    
- 특징
    - **URL이 변경된다**. ***서블릿에서 타겟 URL(jsp)로 변경된다.***
    - 두개의 request로 서블릿하고 JSP 각각을 사용한다.
    - 서블릿에서 3개의 스코프(request, session, application) 중 **request 스코프에 저장된 데이터는 참조할 수 없다.**

### 실습

- ForwardServlet.java
    
    ```java
    public class ForwardServlet extends HttpServlet {
    	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    		System.out.println("MyServlet");
    		// **forward**를 사용하면 **같은 번지에서 작업 가능**하다.
    		// redirect를 하면 요청 위임시 다른 번지에서 작업이 이루어진
    		
    		// 같은 번지에서 set, get이 이루어지기에 **request 스코프 값을 가지고 올 수 있다.**
    		request.setAttribute("request", "request");
    		
    		HttpSession session = request.getSession();
    		session.setAttribute("session", "session");
    		
    		ServletContext application = getServletContext();
    		application.setAttribute("application", "application");
    	
    		request.getRequestDispatcher("target.jsp").forward(request, response);
    	}
    }
    ```
    
- RedirectServlet.java
    
    ```java
    public class RedirectServlet extends HttpServlet {
    	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    		System.out.println("RedirectServlet");
    
    		// redirect를 하면 request는 찾을 수 없다. set을 한 번지와
    		// get을 허는 번지가 달라지기 때문이다.
    		request.setAttribute("request", "request"); // null
    		
    		HttpSession session = request.getSession();
    		session.setAttribute("session", "session");
    		
    		ServletContext application = getServletContext();
    		application.setAttribute("application", "application");
    		
    		response.sendRedirect("target.jsp");
    	}
    }
    ```
    
- target.jsp
```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>

</head>
<%
String req = (String)request.getAttribute("request");
String sess = (String)session.getAttribute("session");
String app = (String)application.getAttribute("application");
%>
<body>
	<h1>target.jsp</h1>
	request : <%= req %> <br>
	session : <%= sess %> <br>
	application : <%= app %> <br>
</body>
</html>
```

---
# 18. 세션관리

## 1) 개요

: HTTP 프로토콜이 connectionLESS, stateLESS 인 특징으로 인해서 **이전 페이지에서 작업했던 상태 및 데이터**를 현재 페이지에서 사용할 수 없게 된다. 

따라서 이전 상태를 알 수 있도록 하기 위해서 **세션관리 기능을 사용**한다.

## 2) 구현방법

### 1. 세션이용

: **tomcat 서버에** 여러 서블릿(jsp)이 사용할 수 있는 **공유데이터를 저장하는 방법**

- **HttpSession API** 이용
    
    https://jakarta.ee/specifications/platform/9/apidocs/jakarta/servlet/http/httpsession
    
- 작업순서
    1. **공유데이터 저장하는 서블릿**
        - **저장소(세션) 얻기**  ⇒  HttpSession을 얻기
            
            // 저장소(세션)이 있으면 반환하고 없으면 생성해서 반환
            
            **`HttpSession session = request.getSession();`**
            
            `HttpSession session = request.getSession(true);`
            
            // 저장소(세션)이 있으면 반환하고 없으면 null 반환
            
            `HttpSession session = request.getSession(false);`
            
        - 공유데이터 저장 : key - value 형식
            
            **`session.setAttribute( “key”, “value” );`**
            
        
    2. **저장된 공유데이터를 사용하는 JSP(서블릿)**
        - 저장소(세션)을 얻기
            
            **`HttpSession session = request.getSession();`**
            
        - 공유데이터 참조
            
            **`String str = (String)session.getAttribute(”key”);`**
            
        - str 값 체크하기
            
            **`if(str != null)** {` 
            
            `// a작업(예> 로그인) 거친 후`
            
            `// 필요한 작업 수행` 
            
            `}else{` 
            
            `// a작업 거치지 않음`
            
            `// **a작업을 수행하도록 redirectforward 해줌 => response.sendRedirect(”a작업”)** }` 
            
    3. 삭제
        - 전체 세션 삭제
            
            **`session.[invalidate](https://jakarta.ee/specifications/platform/9/apidocs/jakarta/servlet/http/httpsession#invalidate--)();`**
            
            예 > 로그아웃
            
        - 엔트리 삭제
            
            **`session.[removeAttribute](https://jakarta.ee/specifications/platform/9/apidocs/jakarta/servlet/http/httpsession#removeAttribute-java.lang.String-)**([**String**](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html?is-external=true) key);`
            
        - time-out 이용한 삭제
            
            **`session.[setMaxInactiveInterval](https://jakarta.ee/specifications/platform/9/apidocs/jakarta/servlet/http/httpsession#setMaxInactiveInterval-int-)(초단위); //지정한 초가 지난 후 삭제`**
            
- 특징 :
    - **요청한 브라우저와 같은 스코프**를 가진다.
    - **요청한 웹브라우저의 id 값이 자동으로 서버에 전달**된다.
        
        크롬웹브라우저(AAA)    ⇒    jsessionid=AAA    ⇒   세션(AAA)
        
    - 세션에 저장하는 데이터는 Object 이기에 **모든 데이터를 저장**할 수 있다.
- **세션관련 메서드**
    - **HttpSession session = request.getSession();**
        
        : 세션 생성
        
    - session.[**setAttribute](https://jakarta.ee/specifications/platform/9/apidocs/jakarta/servlet/http/httpsession#setAttribute-java.lang.String-java.lang.Object-)(key, value);**
        
        : 세션에 값을 저장, value는 Object 타입
        
    - session.[**getAttribute](https://jakarta.ee/specifications/platform/9/apidocs/jakarta/servlet/http/httpsession#getAttribute-java.lang.String-)(key);**
        
        : 세션에 저장된 값을 조회, 형변환 필요
        
    - session.[**removeAttribute**](https://jakarta.ee/specifications/platform/9/apidocs/jakarta/servlet/http/httpsession#removeAttribute-java.lang.String-)([**String**](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html?is-external=true) name);
        
        : 세션에 저장된 엔트리 삭제
        
    - session.[**invalidate**](https://jakarta.ee/specifications/platform/9/apidocs/jakarta/servlet/http/httpsession#invalidate--)()
        
        : 세션 즉시 삭제 ( 저장소 삭제 )
        
    - session.[**setMaxInactiveInterval**](https://jakarta.ee/specifications/platform/9/apidocs/jakarta/servlet/http/httpsession#setMaxInactiveInterval-int-)(int interval)
        
        : 지정된 초 이후에 세션 삭제
        
    - session.[**getId**](https://jakarta.ee/specifications/platform/9/apidocs/jakarta/servlet/http/httpsession#getId--)()
        
        : jseesionid 얻기
        
    - session.[**isNew**](https://jakarta.ee/specifications/platform/9/apidocs/jakarta/servlet/http/httpsession#isNew--)()
        
        : 조회된 session이 처음 만든 세션인지?
        
    - session.[**getCreationTime**](https://jakarta.ee/specifications/platform/9/apidocs/jakarta/servlet/http/httpsession#getCreationTime--)()
        
        : 세션이 생성된 시간을 long 타입으로 리턴
        

### 2. 쿠키이용

: **웹브라우저(클라이언트)에** 여러 서블릿(jsp)이 사용할 수 있는 **공유데이터를 저장하는 방법**

- **Cookie API** 이용
    
    https://jakarta.ee/specifications/platform/9/apidocs/jakarta/servlet/http/cookie
    
- 특징
    - **클라이언트에 저장된다.**
    - **String 값만 저장** 가능
    - 도메인당 50개 저장 가능, 각 4kb로 제한
    - 세션보다 보안에 취약하고 가장 큰 단점은 사용자가 쿠키를 사용하지 않도록 설정이 가능하다.
- **쿠키 아키텍처**
    
    브라우저 ————  **a. 요청** ———————>  서블릿 (A)
    
                                                                                **b. 쿠키생성** 
    
                                                                                  Cookie c = new Cookie(key, value)
    
                                                                                  // 웹브라우저 메모리 / PC 파일
    
                                                                                **c. [setMaxAge](https://jakarta.ee/specifications/platform/9/apidocs/jakarta/servlet/http/cookie#setMaxAge-int-)(int expiry)**
    
                                                                                 값 : 양수, 지정된 값만큼 pc파일에 저장
    
                                                                                 값 : 음수, 웹브라우저 메모리에저 저장(기본)
    
                                                                                 값 : 0, 쿠키 즉시 삭제 ( 세션의 invaildate() )
    
                                                                                **d. 쿠키를 클라이언트에 전송**
    
                                                                                 response.[**addCookie**](https://jakarta.ee/specifications/platform/9/apidocs/jakarta/servlet/http/httpservletresponse#addCookie-jakarta.servlet.http.Cookie-)([**Cookie**](https://jakarta.ee/specifications/platform/9/apidocs/jakarta/servlet/http/cookie) cookie);
    

                 <——————  **e. 응답(쿠키**) ——————

**f. 클라이언트에 쿠키 저장**

- 웹브라우저 메모리
- PC 파일

                  ——————  **g. 요청(쿠키)** —————>   서블릿(B), 서블릿(C), JSP

                                                                                          **h. 쿠키 얻기**

                                                                                           Cookie [] cookies = **request.getCookie();**

                                                                                           for(Cookie c : cookies){

                                                                                           String key = c.getName();

                                                                                           String vlaue = d.getValue();

                                                                                           }

                 ————  **i. 쿠키 삭제 요청(쿠키)** —————>  서블릿(D)

                                                                                           Cookie [] cookies = request.getCookie();

                                                                                           for(Cookie c : cookies){

                                                                                           String key = c.getName();

                                                                                           if(”aaa”.equals(key){

                                                                                           **c.setMaxAge(0);**

                                                                                           response.addCookie(c);

                                                                                           }

                                                                                           }
