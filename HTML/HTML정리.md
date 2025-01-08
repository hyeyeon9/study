# 1. web 아키텍처

클라이언트(웹 브라우저)    ——>     url로 요청    ——>     서버에서 요청처리 후 결과 전달(웹 서버)

### 웹 컴포넌트

- html : *html, 정적 컴포넌트(항상 결과가 동일)
- jsp : *.jsp, 동적 컴포넌트(결과가 달라짐), 자바기술
- servlet: *.java, 동적 컴포넌트(결과가 달라짐), 자바기술

## 1) html인 경우

![image (3)](https://github.com/user-attachments/assets/751199ae-c38c-4cd6-8e60-d9e9a78db108)


---

## 2) jsp 인 경우

![image (4)](https://github.com/user-attachments/assets/7a14aca3-dec4-41b3-ac72-a72c2a5373ce)


---

## 3) servlet 인 경우

![image (5)](https://github.com/user-attachments/assets/c54e95ec-634d-465a-a6a6-17cc807ad279)


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

---
# 1. HTML 태그

## 1) html 요청 URL

http://127.0.0.1:5500/sample01_head_title.html

http : 프로토콜

127.0.0.1 : 서버 IP  ( [localhost](http://localhost) )

5500 : live server의 포트번호

sample01_head_title.html : 타겟

## 2) <title> 태그

![image (11)](https://github.com/user-attachments/assets/e4c3f962-0f9f-4496-9db0-31b1d7323923)


- html 문서의 타이틀 지정용도
- 웹 브라우저 탭에 보이며, 즐겨찾기 할 때 저장되는 값

## 3) <style> 태그

: css 설정방법 중 하나에서 사용된다.

- css 설정방법 3가지
    1. 인라인 스타일
        
        : html 태그에서 style 속성을 사용해서 css를 설정하는 방법
        
        ```html
          <h1 style="color: red">Hello!</h1>
        ```
        
    2. 내부 스타일
        
        : <style> 태그 내에서 css 문법을 이용해서 html 태그를 선택해 스타일을 적용하는 방법
        
        ```html
          <body>
            <h1>Hello!</h1>
            <h2 id="h2_id">Hello!!!!</h2>
            <h3 class="h3_class">Hello!!!????!</h3>
          </body>
          <style>
            h1 {
              color: blue;
            }
        
            #h2_id {
              color: red;
              background-color: pink;
            }
        
            .h3_class {
              color: brown;
            }
          </style>
        ```
        
    3. 외부 스타일
        
        : **.css* 외부파일을 생성해서 html에서 css 파일을 참조해서 적용하는 방법
        
        ```html
        <head>
        <link rel="stylesheet" href="external.css" >
        </head>
        ```
        

## 4) <link> 태그

: 주로 외부 스타일 지정시 사용한다.

- favicon 경로 지정시에도 사용

## 5) <script> 태그

: 자바스크립트 코드를 위한 태그

```html
  <head>
    <title>title 실습</title>
    <script>
      console.log("hello");
      console.log("hello");
    </script>
  </head>
   <body>
    <script>
      console.log("body에셔도 스크립트 태그 사용 가능");
    </script>
  </body>
```

![image (10)](https://github.com/user-attachments/assets/c4c73f7b-e3b2-400e-9763-80ef05196643)
console.log()의 결과는 콘솔창에서 확인가능

- JS 2가지 방법
    1. 내부
        
        : <script> 태그 안에 코드를 작성
        
         `<script> console.log("aa"); </script>`
        
    2. 외부
        
        : **.js*  외부파일을 생성하고, html에서 js 파일을 참조해서 사용
        
         `<script src="external.js"></script>`
        

## 6) body 태그의 자식태그

: html의 모든 태그는 box로 되어있다.

### 블록과 인라인

- **블록 레벨** ( 세로배치 )
    
    : 너비(width)가 웹 브라우저의 **전체 너비**를 차지하기에 태그마다 새로운 줄에 렌더링되어 보여진다.
    
    - **명시적으로 너비와 높이를 변경할 수 있다.**
    - div, p, table, h1~h6, ul, ol, li, tr, br, hr …
- **인라인 레벨** ( 가로배치 )
    
    : 너비(width)가 **자신이 가진 컨텐츠 크기만큼** 확보되어 렌더링된다. 
    
    - **명시적으로 너비와 높이를 지정할 수 없다.**
    - span, a, img, …
- CSS를 사용해서 서로간의 변경이 가능하다.

### 1. header 태그

: /<h1>  ~  /<h6> 

- 숫자가 작을수록 글자가 크다는 특징
- /<h1> : 32px , /<h4> : 16px
- 기본 폰트 : 16px ( 1rem과 동일 )

### 2. p 태그

: 문서의 문단(paragraph) 지정 목적

### 3. br 태그

: new line을 만들때 사용  ( \n 기능 )

- 종료태그가 따로 없다.

### 4. hr 태그

: 수평선 제공

- 종료태그 없다.

### 5. 텍스트 포맷 태그

- <b> hello </b>  : 굵은 글자
- <i> : 이태릭 글자
- <small> : 작은 글자
- <del> : 취소선 글자
- <ins> : 밑줄 글자
- <sub> : 아래 글자
- <sup> : 위 글자

### 6. 리스트

- ul : 순서 없는 리스트 (unordered list)
    
    ```html
    <ul type="circle">
          <li>A</li>
          <li>B</li>
          <li>C</li>
    </ul
    ```
    
- ol : 순서 있는 리스트 (ordered list)
    
    ```html
    <ol start="100">
          <li>A</li>
          <li>B</li>
          <li>C</li>
    </ol>
    ```
    

### 7. <a> 태그 ( anchor 태그 )

: 페이지간에 연결(링크)시 사용된다.

- `<a href = ”타겟” > 링크 </a>`
- 인라인 레벨
- 기본적으로 링크 색상이 다르다.
    - 방문전 : blue, 방문후 : purple, 활성화 : red
    - css로 색상 변경 가능
- target 속성
    - 링크된 문서를 어디에서 보여줄지를 설정가능
    - target = “_self” (기본값, 현재 창)
    - target = “_blank” (새로운 창)
    - `<a href="sample04_body5_list.html" target="_blank"> 다른파일 </a>`

1. 외부링크
    - `<a href="sample04_body5_list.html"> 다른파일 </a>`
    - `<a href="[http://google.com](http://google.com/)"> 구글 </a>`
2. 내부링크
    - 같은 파일 내부에서 특정 위치로 이동할 때 사용한다. href에 ‘#id’ 로 이동할 태그의 id를 지정해서 알려준다.
    
    ```html
        <a href="#title">제목</a>
        <a href="#2">특징</a>
        <a href="#body">역사</a>
    
        <h1 id="title">책</h1>
    
        <p id="2">
          <h1>특징</h1>
    		     ....
        </p>
    
        <p id="body">
          <h1>역사</h1>
    			   ,..
        </p>
    ```
    

1. 외부링크 && 내부링크
    
    ```html
    <a href="sample04_body6_anchor2.html#title" target="_blank">
       제목으로 바로가기
       </a>
    <a href="sample04_body6_anchor2.html#2" target="_blank"
          >특징으로 바로가기</a>
    ```
    

### 8. table 태그

![image (9)](https://github.com/user-attachments/assets/31186e42-fef0-42be-8912-b4aee6830125)



```html
    <table border="1">
      <tr>
        <th>이름</th>
  
        <th>나이</th>
        <th>지역</th>
      </tr>
      <tr>
        <td>길동</td>
        <td>20</td>
        <td>부산</td>
      </tr>
      <tr>
        <td>동길</td>
        <td>25</td>
        <td>서울</td>
      </tr>
    </table>
```

- 그룹핑 가능 ( 권장 )
    - <thead>  : 헤더
    - <tbody>  : 몸체
    - <tfoot>   : 총합
    
    ```html
    <table border="1">
          <thead>
            <tr>
              <th>제품명</th>
              <th>가격</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>TV</td>
              <td>100</td>
            </tr>
            <tr>
              <td>PC</td>
              <td>200</td>
            </tr>
          </tbody>
          <tfoot>
            <tr>
              <td>총합</td>
              <td>300</td>
            </tr>
          </tfoot>
        </table>
    ```
    

- **병합**

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/686c9583-1330-4ae4-99da-86732a9a0b13/4395b27f-e310-4a02-a4e1-d4506a040e8f/1ac9bb30-6326-4055-b7de-d161a10c1c5c.png)

- 열병합 :  colspan="갯수"
    
    ```html
     <table border="1">
            <thead>
              <tr>
                <th>이름</th>
                <th colspan="2">전화번호</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>홍길동</td>
                <td>010</td>
                <td>020</td>
              </tr>
            </tbody>
          </table>
    ```
    
- 행병합 :  rowspan="갯수"
    
    ```html
     <table border="1">
            <tr>
              <th>이름</th>
              <td>홍길동</td>
            </tr>
            <tr>
              <th rowspan="2">전화1</th>
              <td>010</td>
            </tr>
            <tr>
              <td>020</td>
            </tr>
          </table>
    ```
    

### 9. 태그 및 특정값 그룹핑

1. 태그 그룹핑
    - 전통적으로 **<div>** 사용
    - 현재는 시멘틱 태그 ( <nav>, <header>, <main>, <aside>, <section> )등과 같이 병행해서 사용한다.
    - 위 태그들은 **블럭 레벨**
        - 웹 브라우저의 전체 너비를 차지
        - width와 height 지정 가능
2. 특정값(문자열) 그룹핑
    - **<span>** 사용
    - **인라인 레벨**
        - 컨텐츠 너비만큼 차지
        - width와 height 지정 불가

### 10. 시멘틱 태그 ( sementic tag )

: ‘의미를 갖는다’ 뜻으로 각 태그가 자신만의 특정 의미가 있음을 알려줄 수 있다.

- <header> : 웹 사이트의 소개 및 정보
- <main>    : 웹 사이트의 메인항목
- <section> : 실제 문서 내용을 포함
- <article>   : section의 문서 내용 중 주제별로 그룹핑
- <nav>       : 사이트 메뉴
- <aside>    : 사이트의 양측면 ( 베너 광고, 목차, … )
- <footer>   : 사이트 하단에 회사 소개 및 저작권 정보 포함

### 11. 사용자 입력태그

1. **단일값 입력 ( text )** 
    - `<input type="text" name="username" maxlength="3” />`
2. **비밀번호 입력 ( password )**
    - `<input type="password" required  placeholder="비밀번호를 입력하세요. />`
3. **체크박스 ( checkbox )**
    - 여러개 선택 가능
    - checked : 처음부터 체크된 상태 가능
    
    ```
        사과 : <input type="checkbox" name="apple">
        바나나 : <input type="checkbox" name="banana"> <hr>
    ```
    
4. **라디오버튼**
    - 한개만 선택 가능
    - **name 값을 동일하게 지정해야 그룹핑이 되어 한개만 선택 가능하다.**
    - checked : 처음부터 체크된 상태 가능
    
    ```
        여자 : <input type="radio" name="gender" value="female" checked>
        남자 : <input type="radio" name="gender" value="male">
    ```
    
5. **이메일**
    - 반드시 @ 이메일 포맷을 지정해야 submit 할 수 있다.
    - `이메일 : <input type="email" [value="xxx@email.com](mailto:value=%22xxx@email.com)" />`
6. number, file, date, color 입력
    
    ```html
        나이 : <input type="number" name="number" step="2" min="10" max="50"><br>
        파일 : <input type="file" name="file" accept="image/png, image/jpeg"><br>
      날짜 : <input type="date" name="date"  min="2018-01-01" max="2018-12-31"><br>
        색상: <input type="color" name="color"><br>
    ```
    

1. select 태그
    
    ```html
        <select name="fruit">
        <option value="">과일을 선택하세요</option>
        <option value="apple">사과</option>
        <option value="banana">바나나</option>
        <option value="melon">멜론</option>
        </select>
    ```
    

1. 멀티값 입력 ( 텍스트 박스 )
    
    ```html
    <textarea name="content" rows="15" cols="15" readonly>홍길동</textarea>
    ```
    

### 12. 사용자 입력 데이터를 서버에 전달하는 방법

- **<form> 태그**
    - < form action="타겟( 서블릿 | JSP | HTML ) "> :  타겟 서버로 데이터를 전달하는 기능
    
    ```html
      <form action="sample01_head_title.html">
          이메일 : <input type="email" name="userid" placeholder="아이디(이메일)"> <br>
          비밀번호 : <input type="password"  name="password" placeholder="비밀번호"> <br> 
          <input type="submit" value="로그인">
          <input type="reset" value="취소">
        </form>
    ```
    
    ---
    
    - 클라이언트(웹 브라우저)에서 서벌 사용자 입력 데이터를 전달하는 2가지 방법
        1. **GET 방식 ( default )**
            
            : 사용자 입력데이터는 **URL에 query string 형식으로 전달**된다. 
            
            - `http://localhost:port/타겟?태그의name값=사용자입력값&태그의name값=사용자입력값`
                - `http://127.0.0.1:5500/sample01_head_title.html?userid=guhaa03%40nate.com&password=1234`
                - `userid=guhaa03%40nate.com&password=1234` 부분을 query string 이라고 부르고, query string은 URL에 포함되지 않는다.
            - payload 탭이 아니라 URL에서 전달된 사용자의 입력데이터를 확인할 수 있다.
            - 멱등성이 있다.
                
                <aside>
                💡
                
                멱등성 ?
                
                클라이언트에서 동일한 요청을 여러번 해도 서버에서 변경사항이  발생되지 않는다.
                
                </aside>
                
        2. **POST 방식**
            
            : 사용자 입력 데이터를 URL에 포함하지 않고 **body 에 숨겨서 전달**한다.
            
            - payload 탭을 확인하면 전달된 사용자의 입력데이터를 확인할 수 있다.
            - 웹 브라우저에서 POST 형식을 받아주지 않는 경우(요청방법이 일치X), 405 에러 발생
            - 멱등성이 없다.
                - POST는 새로운 데이터를 생성할 때 주로 사용되는 요청 방식이기 때문이다.
                - 동일한 요청을 반복할 떄 멱동성이 있으면 같은 데이터를 계속 insert 할 위험성이 있기에
        

### 13. image 보기

- `<img src = “이미지파일” alt=”대체 텍스트”>`
- `<img src="images/a.jpg" alt="첫번째 이미지" width="250" height="200">`

### 14. 화면 재사용

: 외부 html 파일을 이용해서 화면 처리

- < iframe src=”외부 html 파일”></iframe>
- `<iframe src="sample04_body11_image.html" frameborder="1" width="500" height="300">`

![image (8)](https://github.com/user-attachments/assets/50bbbfab-aad7-483b-b8fa-459e0d27680d)



### 15. 특수문자

: 기본적으로 html에서는 탭이나 스페이스바 등 적용되지 않는다.

- 공백 : &nbsp;
- < : &lt;
- > : &gt;
- “  : &quot;

```html
 <!-- 스페이스바 적용 안됨 -->
    hello                        world!! <br>
    hellp&nbsp;&nbsp;&nbsp;&nbsp;world!! <br>
    a &lt; b <br>
    a &gt; c
```

### 16. 경로

: 현재 html(css,js)에서 외부파일(html, css, js, image 등)을 참조할 때 위치(경로)를 알려주는 방법

- 풀 경로
    
    ```html
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <title>풀경로</title>
        <link
          rel="stylesheet"
          href="http://127.0.0.1:5500/01_html2/app1/test.css"
        />
      </head>
      <body>
        <img
          src="http://127.0.0.1:5500/01_html2/app1/images/a.jpg"
          alt="a.jpg"
          width="300"
          height="300"
        />
        <iframe
          src="http://127.0.0.1:5500/01_html2/app1/sample.html"
          frameborder="1"
        ></iframe>
        <p>ss</p>
        <form action="http://127.0.0.1:5500/01_html2/app1/sample.html">
          아이디 : <input type="text" />
          <button>전송</button>
        </form>
      </body>
      <script src="http://127.0.0.1:5500/01_html2/app1/test.js"></script>
    </html>
    ```
    
    - 경로 전체는 길기 때문에 주로 절대 경로나 상대 경로로 접근한다.
    
- **절대 경로**
    
    :  **반드시  /   로 시작한다.**  
    
    - ‘http://127.0.0.1:5500/‘ 를  /  로 치환
    
    ```html
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <title>절대경로</title>
        <link rel="stylesheet" href="/01_html2/app1/test.css" />
      </head>
      <body>
        <img
          src="/01_html2/app1/images/a.jpg"
          alt="a.jpg"
          width="300"
          height="300"
        />
        <iframe src="/01_html2/app1/sample.html" frameborder="1"></iframe>
        <p>ss</p>
        <form action="/01_html2/app1/sample.html">
          아이디 : <input type="text" />
          <button>전송</button>
        </form>
      </body>
      <script src="/01_html2/app1/test.js"></script>
    </html>
    ```
    

- **상대 경로**
    
    : 참조하는 곳의 위치를 상대로 . 이나 .. 으로 시작한다.
    
    - **.    : 현재 디렉토리**
    - **..   : 부모 디렉토리(상위)**
    
    ```html
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <title>상대경로</title>
        <link rel="stylesheet" href="../app1/test.css" />
      </head>
      <body>
        <img
          src="../app1/images/a.jpg"
          alt="a.jpg"
          width="300"
          height="300"
        />
        <iframe src="../app1/sample.html" frameborder="1"></iframe>
        <p>ss</p>
        <form action="../app1/sample.html">
          아이디 : <input type="text" />
          <button>전송</button>
        </form>
      </body>
      <script src="../app1/test.js"></script>
    </html>
    ```
