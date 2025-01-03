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

---
# 6. selector

### **basic**

https://api.jquery.com/category/selectors/basic-css-selectors/

- [**All Selector (“*”)**](https://api.jquery.com/all-selector/)
- [**Class Selector (“.class”)**](https://api.jquery.com/class-selector/)
- [**Element Selector (“element”)**](https://api.jquery.com/element-selector/)
- [**ID Selector (“#id”)**](https://api.jquery.com/id-selector/)
- [**Multiple Selector (“selector1, selector2, selectorN”)**](https://api.jquery.com/multiple-selector/)

```jsx
 $(document).ready(function () { 
        $("*").css("color", "red");       // 전체
        $("p").css("color", "red");
        $("p, span").css("color", "red"); // 여러개
        $("#xxx").css("color", "red");    // id
        $(".yyy").css("color", "blue");   // class
    });
```

### **attribute**

https://api.jquery.com/category/selectors/attribute-selectors/

- [**Has Attribute Selector [name]**](https://api.jquery.com/has-attribute-selector/)
    
    ```jsx
    $(document).ready(function () {
            $("[class]").css("color", "red"); // 클래스 속성을 가지는 거
          });
    ```
    

- [**Attribute Equals Selector [name=”value”]**](https://api.jquery.com/attribute-equals-selector/)
    
    ```jsx
    $(document).ready(function () {
            $("[class]").css("color", "red"); // 클래스 속성을 가지는 거
          });
    ```
    

- [**Attribute Not Equal Selector [name!=”value”]**](https://api.jquery.com/attribute-not-equal-selector/)
    
    : value 값을 가지지 않는 요소 체크
    

- [**Attribute Starts With Selector [name^=”value”]**](https://api.jquery.com/attribute-starts-with-selector/)
    
     **:**  value로 시작되는지 확인
    
    ```jsx
    $(document).ready(function () {
           $("[href^= 'https']").css("color", "red");    // https로 시작
          });
    ```
    

- [**Attribute Ends With Selector [name$=”value”]**](https://api.jquery.com/attribute-ends-with-selector/)
    
    : 마지막이 value로 끝나는지 확인
    
    ```jsx
    $(document).ready(function () {
            $("[href$= 'net']").css("color", "blue");     // net으로 끝
          });
    ```
    

- [**Attribute Contains Selector [name*=”value”]**](https://api.jquery.com/attribute-contains-selector/)
    
    : value가 포함된 문자열이 있는지 확인
    
    ```jsx
    $(document).ready(function () {       
            $("[href*= 'naver']").css("color", "yellow"); // naver 포함
          });
    ```
    
- [**Attribute Contains Word Selector [name~=”value”]**](https://api.jquery.com/attribute-contains-word-selector/)
    
    : 공백으로 구분된 단어에  value가 있는지 확인
    
    ```jsx
    $(document).ready(function () {
            $("[href^= 'https']").css("color", "red");    // https로 시작
            $("[href$= 'net']").css("color", "blue");     // net으로 끝
            $("[href*= 'naver']").css("color", "yellow"); // naver 포함
          });
    ```
    

### **Hierarchy**

https://api.jquery.com/category/selectors/hierarchy-selectors/

- [**Child Selector (“parent > child”)**](https://api.jquery.com/child-selector/)
- [**Descendant Selector (“ancestor descendant”)**](https://api.jquery.com/descendant-selector/)
- [**Next Adjacent Selector (“prev + next”)**](https://api.jquery.com/next-adjacent-selector/)
- [**Next Siblings Selector (“prev ~ siblings”)**](https://api.jquery.com/next-siblings-selector/)

```jsx
      $(document).ready(function () {
        // div의 **자식**인 span
        $("div > span").css("color", "red");

        // div의 **자손**인 span  ( 자손은 자식을 포함한다.)
        $("div  span").css("color", "red");

        // class가 'yyy' 의 바로 뒤 <a> 태그 **형제 찾기**
        $(".yyy + a").css("font-size", "20px");

        // class가 'yyy' 의 바로 뒤 <a> 태그 **형제들 찾기**
        $(".yyy ~ a").css("font-size", "20px");
      });
```

### Basic filter

https://api.jquery.com/category/selectors/basic-filter-selectors/

: 대부분 DEPRECATED 됨

### Child filter

https://api.jquery.com/category/selectors/child-filter-selectors/

- [**:first-child Selector**](https://api.jquery.com/first-child-selector/)
    
    ```jsx
          $(document).ready(function () {
            // li 부모인 ul기준 첫번째 자식
            $("li:first-child").css("font-size", "30px");
           });
    ```
    
- [**:last-child Selector**](https://api.jquery.com/last-child-selector/)
    
    ```jsx
          $(document).ready(function () {
             // li 부모인 ul기준 마지막 자식
            $("li:last-child").css("color", "red");
           });
    ```
    
- [**:nth-child() Selector**](https://api.jquery.com/nth-child-selector/)
    
    ```jsx
          $(document).ready(function () {
            // li 부모인 ul기준 3번째 자식
            $("li:nth-child(3)").css("color", "orange");
    
            // li 부모인 ul기준 짝수번째 자식
            $("li:nth-child(2n)").css("font-size", "30px");
    
            // li 부모인 ul기준 홀수번째 자식
            $("li:nth-child(2n + 1)").css("font-size", "15px");
           });
    ```
    
- **only-child() Selector**
    
    ```jsx
          $(document).ready(function () {
            // li 부모인 ul기준 자식이 하나인 li 선택
            $("li:only-child").css("color", "purple");
          });
    ```
    

- [**:first-of-type Selector**](https://api.jquery.com/first-of-type-selector/)
    - **`first-type`**   vs    **`first-of-type`**
        
        ```html
        <!DOCTYPE html>
        <html lang="en">
          <head>
            <title>jquery - child filter2</title>
            <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.7.1/jquery.min.js"></script>
            <script>
              $(document).ready(function () {
                // i태그의 부모기준으로 첫번째 자식이 무주건 i태그여야 함
                // 여기서는 첫번째 자식이 span이기에 css 적용이 안됨
                $("i:first-child").css("color", "red");
        
                // i태그의 부모기준으로 첫번째 자식이 i태그가 아니더라도
                // i태그 중에서 첫번째인 i태그면 찾아줌
                // 여기서는 span이 첫번째 자식이지만, i태그중 첫번째인 Hello1에 css 적용됨
                $("i:first-of-type").css("font-size", "30px");
              });
            </script>
          </head>
          <body>
            <p>
              <span>Hello</span>
              <i>Hello1</i>
              <i>Hello2</i>
              <i>Hello3</i>
            </p>
          </body>
        </html>
        ```
        

### **Content Filter**

https://api.jquery.com/category/selectors/content-filter-selector/

- [**:contains() Selector**](https://api.jquery.com/contains-selector/)
    
    ```jsx
          $(document).ready(function () {
            // $(":contains('John')").css("color", "red");
            // $("span:contains('John')").css("color", "red");
    
            // 지정한 태그에서 특정 문자를 가지는지 확인(대소문자 구분함)
            $("div:contains('John')").css("color", "red");
          });
    ```
    
- [**:empty Selector**](https://api.jquery.com/empty-selector/)
    
    ```jsx
            // 자식이 없는 요소 반환
            $("td:empty")
                        .css("background-color", "Yellow")
                        .text("빈 요소!");
    ```
    
- [**:has() Selector**](https://api.jquery.com/has-selector/)
    
    ```jsx
            // 특정 태그를 포함하는 요소 반환
            $("div:has(span)").css("font-size", "30px");
    ```
    
- [**:parent Selector**](https://api.jquery.com/parent-selector/)
    
    ```jsx
            // 자식이 있는 요소 반환
            $("td:parent").css("background-color", "tomato");
    ```
    

- 전체실습 코드
    
    ```jsx
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <title>jquery - content filter</title>
        <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.7.1/jquery.min.js"></script>
        <script>
          $(document).ready(function () {
            $(":contains('John')").css("color", "red");
    
            $("span:contains('John')").css("color", "red");
    
            // 지정한 태그에서 특정 문자를 가지는지 확인(대소문자 구분함)
            $("div:contains('John')").css("color", "red");
    
            // 특정 태그를 포함하는 요소 반환
            $("div:has(span)").css("font-size", "30px");
    
            // 자식이 있는 요소 반환
            $("td:parent").css("background-color", "tomato");
    
            // 자식이 없는 요소 반환
            $("td:empty").css("background-color", "Yellow").text("빈 요소!");
          });
        </script>
      </head>
      <body>
        <span>John Happy</span>
        <span>john Happy2</span>
        <div>
          <span>John Happy3</span>
        </div>
        <div>John Resig</div>
        <div>George Martin</div>
        <div>Malcom John Sinclair</div>
        <div>J. Ohn</div>
        <hr />
        <table border="1">
          <tr>
            <td>TD #0</td>
            <td></td>
          </tr>
          <tr>
            <td>TD #2</td>
            <td></td>
          </tr>
          <tr>
            <td></td>
            <td>TD#5</td>
          </tr>
        </table>
      </body>
    </html>
    
    ```
    

### Form

https://api.jquery.com/category/selectors/form-selectors/

- [**:button Selector**](https://api.jquery.com/button-selector/)
    - **버튼  /  text(), html() 메서드**
    
    ```jsx
    <script>
          $(document).ready(function () {
            var btn = $(":button"); // 변수로 받을 수 있다.
            // 모든 버튼을 반환하기에 하나씩 접근하기 위해서는 인덱스로 접근
    
            // btn은 jquery 객체, btn[0]은 js객체
            // jquery의 text 메서드
            console.log($(btn[0]).text()); // OK
    
            // 한번에 출룍 가능하다
            console.log(btn.text()); // OKOK2
    
            // 하나씩 작업하기 위해서는 인덱스로 접근하고 jquery로 감싸야함
            $(btn[1]).text("OK버튼2");
            console.log($(btn[1]).text()); // OK버튼2
    
            // innerHTML은 jquery의 html() 메서드를 사용
            console.log($(":button").html()); // OK
          });
     </script>
     
      <body>
        <button>OK</button>
        <button>OK2</button>
      </body>
    ```
    

- [**:checkbox Selector**](https://api.jquery.com/checkbox-selector/)

- [**:checked Selector**](https://api.jquery.com/checked-selector/)
    - **checked 속성  /  val() 메서드**
    
    ```jsx
    <script>
    $(document).ready(function () {
            **var chk = $(":input:checked");** // 배열로 반환
            console.log(chk); // jquery 객체
    
            // js객체의 value값 얻기
            **console.log(chk[0].value); // apple**
    
            // jquery객체의 value값 얻기 => **val() 메서드 사용**
            **console.log($(chk[1]).val()); // peach**
     })
     </script>
     <body>
        사과:<input type="checkbox" checked value="apple" /> 
        복숭아:<input
          type="checkbox"
          checked
          value="peach"
        />
        바나나:<input type="checkbox" value="banana" />
      </body>
    ```
    

- [**:disabled Selector**](https://api.jquery.com/disabled-selector/)
- [**:enabled Selector**](https://api.jquery.com/enabled-selector/)
- [**:file Selector**](https://api.jquery.com/file-selector/)
- [**:focus Selector**](https://api.jquery.com/focus-selector/)
- [**:image Selector**](https://api.jquery.com/image-selector/)
- [**:input Selector**](https://api.jquery.com/input-selector/)
- [**:password Selector**](https://api.jquery.com/password-selector/)
- [**:radio Selector**](https://api.jquery.com/radio-selector/)
- [**:reset Selector**](https://api.jquery.com/reset-selector/)
- [**:selected Selector**](https://api.jquery.com/selected-selector/)
- [**:submit Selector**](https://api.jquery.com/submit-selector/)
- [**:text Selector**](https://api.jquery.com/text-selector/)

---
# **7. Traversing**

https://api.jquery.com/category/traversing/

: 앞에서 배운 selectors는 DOM에서 1차로 필터링하는 방법이고,  **Traversing은 2차 필터링하는 방법**이다.

### **1) Filtering**

https://api.jquery.com/category/traversing/filtering/

- [**.eq(idx)](https://api.jquery.com/eq/)**
    
    : *명시된 인덱스의 요소를 찾아줌*
    
    `$("li").eq(1).css("color", "red");`
    
- [**.even()**](https://api.jquery.com/even/)
    
    : *인덱스 0부터 시작해서 짝수번째 요소 반환*
    
    `$("li").even().css("color", "yellow");`
    
- [**.filter(selector|function)](https://api.jquery.com/filter/)**
    
    : *1차 필러팅 이후 셀렉터 조건에 맞는 요소 반환*
    
    ```jsx
          $(document).ready(function () {
            // 2. .filter(selector|function) : selector에 해당되는 요소를 찾아줌
            $("li").filter(".xxx").css("font-size", "30px");
    
            // 2-1. .filter
            $("li")
              .filter(function (idx, ele) {
                // ele는 js객체
                console.log(idx, ele); // li태그 하나씩 출력됨
                return idx % 2 === 0; // 0부터 시작하여 짝수번째
              })
              .css("background-color", "tomato")
          });
    ```
    
- [**.not(selector|function)**](https://api.jquery.com/not/)
    
    : *1차 필터링 이후 셀렉터 조건에 맞지 않는 요소 반환*
    
    `$("li").not(".xxx").css("font-size", "10px");`
    
- [**.first()**](https://api.jquery.com/first/)
    
    : *1차 필터링 이후 첫번째 요소 반환*
    
     `$("li").first().css("color", "pink");`
    
- [**.last()**](https://api.jquery.com/last/)
    
    : *1차 필터랑 이후 마지막 요소 반환*
    
- [**.has(selector)**](https://api.jquery.com/has/)
    
    : *지정된 셀렉터를 포함하는 요소 반환*
    
    `$("li").has("span").css("color", "red");`
    
- [**.is(selector|function)**](https://api.jquery.com/is/)
    
    : 지정된 셀렉터를 포함하는 요소가 있으면 true, 없으면 false
    
    ```jsx
            $("ul").on("click", function (e) {
              var target = $(event.target);
              if (target.is("li")) {
                target.css("background-color", "red");
              }
            });
    
            var result = $("li").is("[class]");
            console.log(result); // true
    ```
    
- [**.slice( start [, end ] )**](https://api.jquery.com/slice/)
    
    : *start부터 end-1까지의 요소를 반환*
    
    `$("li").slice(2,5).css("font-size", "30px");`
    
- [**.map( callback )**](https://api.jquery.com/map/)
    
    : *1차 필터링 이후의 요소들을 가공해서  반환*
    
    ```jsx
            var a = $(":checkbox")
              .map(function () {
                return this.id; // this는 1차 필터링 객체이다.
              })
              .get() // 베열안의 값을 get()메서드를 통해서 가져온다. => 배열로 나옴
              .join(" ");
            console.log(a); // two four six eight
    
            var result = $("li")
              .map(function (idx, ele) {
                return ele.innerText.toLowerCase();
              })
              .get();
            console.log(result); // ['aaa', 'aa', 'bb', 'cc', 'dd', 'ee', 'aaa', 'a', 'b', 'c', 'd', 'e', 'f']
    
            var result2 = $("li")
              .map(function (idx, ele) {
                console.log($(ele)); // jquery 객체
                console.log($(this)); // console.log($(ele));와 똑같은 결과
                return $(ele).text().toLowerCase();
              })
              .get()
              .join(" ");
            console.log(result2); // aaa aa bb cc dd ee aaa a b c d e f
    ```
    

### **2) Tree Traversal**

https://api.jquery.com/category/traversing/tree-traversal/

- [**.children( [ selector ] )**](https://api.jquery.com/children/)
    
    : selector가 있을 수도 없을 수도 있다. 없는 경우 모든 자식요소를 찾고, 있는 경우 셀렉터에 일치하는 자식요소를 찾는다.
    
     `$("div").children().css("color", "red");`
    
     `$("div").children("p").css("font-size", "30px");`
    
- [**.find( selector )**](https://api.jquery.com/find/)
    
    : selector가 필수이다. 셀렉터에 일치하는 자식, 자손 요소를 찾는다.
    
     `$("div").find("span").css("font-size", "30px");`
    
- [**.parent( [ selector ] )**](https://api.jquery.com/parent/)
    
    : 셀럭터에 일치하는 부모 요소를 찾는다. 셀렉터가 없는 경우에는 모든 부모요소를 찾는다.
    
     `$("span").parent().attr("class", "yyy"); *// attr(속성명, 속성값)*`
    
    `$("span").parent("p").attr("class", "yyy"); *// 부모 중 p태그 요소만 찾음*`
    
- [**.parents( [selector ] )**](https://api.jquery.com/parents/)
    
    : 조상요소까지 찾는다.
    
    `$("span").parents().attr("class", "yyy"); *// body, html까지*`
    
    `$("span").parents("body").attr("class", "classs"); *// body에만*`
    
- [**.next( [selector ] )**](https://api.jquery.com/next/)
    
    : 형제요소를 찾는다.
    
     `$("li:first").next().css("color", "blue"); ;// li중 첫번째 요소의 바로 다음 형제요소 하나를 반환`
    
- [**.nextAll( [selector ] )**](https://api.jquery.com/nextAll/)
    
    : 모든 형제들을 찾는다.
    
    `$("li:first").nextAll().css("color", "red"); //  li중 첫번째 요소 뒤의 모든 형제들을 반환`
    
- [**.prev( [selector ] )**](https://api.jquery.com/prev/)
    
    : 바로 앞 형제를 찾는다.
    
    `$("li").prev().css("color", "blue");`
    
    `$("li").prev(".xxx").css("font-size", "30px");`
    
- [**.prevAll( [selector ] )**](https://api.jquery.com/prevAll/)
    
    : 앞 형제들 모두 찾는다.
    
    `$("li:last").prevAll().css("color", "red"); *// li 마지막 요소 앞의 모든 형제들 반환*`
    
- [**.siblings( [selector ] )**](https://api.jquery.com/siblings/)
    
    : 1차 필터링 이후의 바로 앞/뒤 형제들을 찾는다.
    
     `$("li.xxx").siblings().css("color", "red");`
  
