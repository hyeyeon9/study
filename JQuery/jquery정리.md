# 1. 개요

https://jquery.com/

 : **javascript의 라이브러리**로서 javascript를 wrap한 기능

- 훨씬 쉽게 Js 처리 가능
- 풍부한 기능 제공
- *.js 파일로 구성

---

# 2. 설치방법 2가지

1. **로컬에 다운로드**
    - compressed, production version (압축 버전)
        - 용량을 최소화한 버전
        - 엔터, 들여쓰기 등의 작업을 제외시키고 한줄로 작성됨
        - jquery-3.7.1.min.js  ( 86k )
    - uncompressed development version
        - 용량을 비최소화
        - 엔터, 들여쓰기 등 지원
        - jquery-3.7.1. js  ( 279k )
    - small version (slim version)
        - ajax , effects 제외
        
2. **원격에 링크 ( CDN : Content Delivery Network )**
    - 구글 CDN
        
        **`<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.7.1/jquery.min.js"></script>`**
        

---

# 3. JS 객체  vs  jQuery 객체

### jQuery 문법

**: `jQuery(식별자)` ,** 별칭으로 **`$(식별자)`** 형태를 자주 사용한다.

- JS 객체
    - document, this, window,  …
- jQuery 객체
    - `$(document), $(this), $(window), …`
    - jquery에서 사용하는 속성과 메서드는 따로 존재한다.
        - 예 > `$(document).ready();`

### 실습

- 로컬에 다운 ( jquery-3.7.1. js )

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>jquery 설치1 - 다운로드</title>
    **<script src="jquery-3.7.1.js"></script>**
    <script>
      console.log("JS 객체: ", document);
      // JS 객체:  #document
      
      console.log("JQuery 객체: ", **$(document)**);
      // JQuery 객체:  **jQuery.fn.init {0: document, length: 1}**
    </script>
  </head>
  <body></body>
</html>
```

- CDN

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>jquery 설치1 - 다운로드</title>
    **<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.7.1/jquery.min.js"></script>
    <script>**
      console.log("JS 객체: ", document);
      // JS 객체:  #document
      console.log("JQuery 객체: ", $(document));
      // JQuery 객체:  ce.fn.init
    </script>
  </head>
  <body></body>
</html>
```

---

# 4. DOM 선택하는 방법

### js 방법

: `document.querySelector(”css선택자”);`

### jquery  방법

: **`$(”css 선택자”)`**

- 예 > `$(”div”), $(”.class”), $(”#id > span”)`

---

## 5. ready 메서드

https://api.jquery.com/ready/#ready-handler

: **DOM이 준비된 이후에 함수를 실행시키기 위해 사용하는 메서드**이다.
``` HTML
$( document ).ready(function() {  
					// Handler for .ready() called.
					});
```
``` javascript
       console.log($("p")); 
      // e.fn.init {length: 0, prevObject: ce.fn.init}

      $(document).ready(function () {
        console.log("ready 안에서 호출");
        console.log($("p")); 
        // ce.fn.init {0: p, 1: p, length: 2, prevObject: ce.fn.init}
      });
```
