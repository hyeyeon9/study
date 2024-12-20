# 1. web 아키텍처

클라이언트(웹 브라우저)    ——>     url로 요청    ——>     서버에서 요청처리 후 결과 전달(웹 서버)

### 웹 컴포넌트

- html : *html, 정적 컴포넌트(항상 결과가 동일)
- jsp : *.jsp, 동적 컴포넌트(결과가 달라짐), 자바기술
- servlet: *.java, 동적 컴포넌트(결과가 달라짐), 자바기술

## 1) html인 경우

             **웹 브라우저**     

**`라. test.html 렌더링`** 

=⇒  html은 서버에서 저장되고 클라이언트(프론트엔드)에서 실행된다. 정적인 특징을 가지기에 항상 동일한 화면을 보여준다.

                **`가. 요청(test.html)`**  

  ======================= >

 < =======================

           **`다. 응답 (test.html 다운)`**

**웹서버 ( Apache, IIS,ngnix, …)**

test.html

**`나. 요청한 html 검색`**

- 없는 경우 : **404 (File Not Found) 에러코드 발생**, 에러페이지를 사용자에게 보내줌
- 있는 경우 : 찾은 test.html 보내줌

---

## 2) jsp 인 경우

             **웹 브라우저**     

**`라. html 렌더링`** 

=⇒ jsp는 서버에 저장되고 서버에서 실행되기 때문에 동적인 특징을 가진다. 즉, 항상 동일한 화면이 아니라 동적인 화면을 보여진다.

                **`가. 요청( test.jsp )`**  

  ======================= >

 < =======================

             **`다. 응답 ( html 다운)`**

**웹 컨테이너 ( Tomcat )**

test.jsp 

**`나. 요청한 jsp 검색`**

- 없는 경우 : 404 (File Not Found) 에러코드 발생, 에러페이지를 사용자에게 보내줌
- 있는 경우 : **3가지 단계**를 가진다.
    1. 변환단계           
        - test.jsp  —> test_jsp.java
    2. 컴파일 단계                        
        - test_jsp.java  —> test_jsp.class
    3. 실행 단계                      
        - test_jsp.class  —> 결과는 html로 만들어짐

---

## 3) servlet 인 경우

             **웹 브라우저**     

**`라. html 렌더링`** 

=⇒ j서블릿은 서버에 저장되고 서버에서 실행되기 때문에 동적인 특징을 가진다. 즉, 항상 동일한 화면이 아니라 동적인 화면을 보여진다.

                **`가. 요청( test.jsp )`**  

  ======================= >

 < =======================

             **`다. 응답 ( html 다운)`**

 **웹 컨테이너 ( Tomcat, 웹 서버 기능 포함 )**

 test.java(서블릿)

**`나. 요청한 jsp 검색`**

- 없는 경우 : 404 (File Not Found) 에러코드 발생, 에러페이지를 사용자에게 보내줌
- 있는 경우 :
    - 실행 —> 결과를  html로

---

# 2. 요청 URL

- **서버의 주소**

: IP번호 또는 도메인 

- **port 번호**

클라이언트 

서버 ( IP : 210.103.221.3 )

Apache 웹서버 ( port : 80 ) // 80인 경우 생략 가능

Tomcat 컨테이너 ( port : 8080)

MySQL DB서버( port : 3306 )

Oracle DB서버( port : 1521 )

- **타겟** ( test.html, test.jsp, [Test.java](http://Test.java) )

: 폴더를 이용해서 저장도 가능하다.

- **최종젹인 요청 URL**
    - **http://서버IP:port번호/타겟**
    - http://서버IP:port번호/폴더/타겟
    - https://서버IP:port번호/타겟
    - https://서버IP:port번호/폴더/타겟
    - 예 > **http://210.103.221.3:80/test.html**

---

# 3. 환경설정

1. node 설치
    
    https://nodejs.org/ko
    
    - cmd창에서 **`node -v`** 으로 설치확인

1. VSCode  설치
    
    https://code.visualstudio.com/
    

---

# 4. 웹 개요

- 1991년에0 World Wide Web (WWW) 용어가 처음 나옴
- 1993년에 웹 표준 단체 창설( W3C )
    
    https://www.w3.org/
    
    html / css / javascript 표준안 작성 ⇒ 웹 브라우저에서 실행된다. ( 크롬, 엣지, 파이어폭스, … )
    
    - html / css / javascript 은 W3C에서 만들고 이것을 실행하는 웹 브라우저는 다른 회사에서 만들기 때문에 항상 자신의 웹 브라우저가 W3C에서 만든 문법을 지원하는지 확인해야 한다.
    

### 모질라( Mozilla ) 사이트

https://developer.mozilla.org/ko/

: W3C에서 제안한 표준안의 가이드를 제공한다.

https://developer.mozilla.org/ko/docs/Web/HTML

https://developer.mozilla.org/ko/docs/Web/CSS

https://developer.mozilla.org/ko/docs/Web/JavaScript

- 모질라 사이트에서 웹 브라우저 지원 여부를 확인할 수 있다.

---

# 5. 웹 표준

## 1) 기본 개념

: 특정 기기(pc,모바일)와 사용자의 상태와 무관하게 누구든지 정보 접근이 가능한 웹을 만들어야 한다.

## 2) 준수확인

https://developer.mozilla.org/ko/

## 3) 구현 방법

- 역할 분담
    1. **데이터 구조** 담당
        - **html**
    2. **디자인** 담당
        - **css**
    3. **동적처리** 담당
        - **javascript**
    
     ⇒ 모두 서버쪽에 저장되지만 서버에서 응답될 떄 다운로드되어 클라이언트에서 실행된다.
    

---

# 6. html (hyper text markup language)

: 웹 페이지를 작성하기 위한 언어

- hyeper text : 링크(link) 의미
- markup language :  정보 표시용 방법, **태그**로 구성된다.

### XML ( eXtensible Markup Language )

: **확장가능한 마크업 언어**로서 태그명을 임의로 재정 가능하다. ( 예 >     <홍길동>, <lotte>    )

- 추가로 특정태그의 사용 규칙을 정할 수도 있다. 규칙을 정하는 2가지 방법은 dtd(**.dtd)와 xsd(**.xsd) 이다.
- 용도는 데이터 저장
- 플랫폼(OS, 프로그램언어, .)에 **독립적**
- 단점으로는, 데이터를 표현하기 위한 추가적인 데이터(메타 데이터)가 필요하다.
    - 해결책으로 JSON (JavaScript Object otation) 포맷 사용
    - {name : “홍길동”}

## html 특징

- **태그로 구성**된다.
    - 태그는 시작태그와 종료태그로 구성
    - 태그는 중첩형태
    - 종료태그가 없는 태그도 존재
        - <img>, <input>, <br>, <hr>, <link>
    - 몸체(body)가 없는 태그 ( 빈 태그 ) 존재
        - <태그></태그>  ⇒  </태그>
- 태그명은 소문자 권장
- **시작태그는 속성을 포함할 수 있고** 속성명은 정해져 있다.
    - 속성명은 모든 태그에서 사용할 수 있는 전역속성 ( id, class ) / 특정 태그에서만 사용가능한 속성 ( href, vlaue, .. )
- 속성명을 임의로 지정할 수 있다. ( 커스텀 속성 )
    
    문법 : **`data-속성명 = “속성값”`** 
    
         `예 > <p id=”xxx” data-ssg=”yyy”>hello</p>`
    

# 7. html 버전

: html 작성시에는 항상 사용할  html 버전을 명시해야 된다. 이유는 웹 브라우저가 버전을 확인하고 렌더링하기 때문이다. 

- 우리는 html5 버전을 사용할 예정이다.
- <! DOCTYPE html >: html 5 버전 설정 방법

# 8. html 기본 구조

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link>
    <script></script>
</head>
<body>
    <h1 id="hello_h1">Hello!!</h1>
</body>
</html>
```

- DOM 트리
    
    ⇒ 웹 브라우저는 위의 코드를 트리구조로 정리한다. 
    
    - html이 root 노드의 자식으로 head 노드와 body 노드가 형제관계를 맺는다. 각 노드안의 태그와 태그안의 속성들이 부모-자식 관계를 이루면서 트리구조를 완성한다.
    
    ```
                        html
                         |
               head                body
                 |                  |
        meta title link script      h1 
                                     |
                                 id   "Helo!!"
    ```
    
- CSS 또는 JS를 이용해서 DOM 트리를 접근할 수 있고 스타일 및 DOM 처리(수정, 삭제, 추가)를 할 수 있다.
