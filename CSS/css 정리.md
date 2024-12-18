# CSS

# 1. CSS (Cascading StyleSheet)

## 1) 역할

: HTML에 시각적 표현을 지정해서 스타일 관리

## 2) 버전

- css1 : 1996년
- css2 : 1998년
- css3 : 현재까지 계속 개발중 ( 표준화 버전)

<hr>

# 2. html에 css 적용하는 방법

## 1) 인라인 스타일

: html의 시작태그의 style 속성을 이용해서 스타일 적용

- `<p style=”color:red” > Hello </p>`

## 2) 내부 스타일

: <head> 태그 안의 <style> 태그에서 css를 지정하는 방법

```html
<head>
	<style>
			p{
				color : red;
			}
	</style>
</head>		
```

- 태그 이름(전역), id값( #id ), class이름( .class )으로 특정 태그를 지정해서 css를 적용할 수 있다는 점

## 3) 외부 스타일

: html 파일 외부에 *.css 형식의 파일을 작성해 css 지정하는 방법으로, html에서 css 파일을 참조해서 사용한다.

- 같은 *.css 파일을 사용하는 여러 html 페이지는 맨 처음 요청한 페이지에서 다운로드 받아서 웹 브라우저 캐시 메모리에 저장된 *.css 파일을 재사용해서 참조한다.
- `<link rel=”stylesheet”  href=”test.css” >`

## 4) 우선순위

       인라인 스타일    >    내부 스타일    >     외부 스타일

<hr>

# 3. CSS 선수 내용

## 1) Cascading

: DOM 트리의 상위에서 정의한 스타일이 하위 요소로 전달되는 개념이다. 자식 요소 입장에서 여러 스타일이 중복 적용될 수도 있다. 하위에서 스타일 재정의로 해결 가능

## 2) 명시도 ( Specificity )

https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity

:  선택자마다 우선순위가 있다. 같은 명시도를 가지면 나중에 정의한 선택자가 적용된다. 

- 우선순위  :   인라인   >   id   >   class, 속성명    >   태그
- !important
    - 권장하지 않음
    - 명시도의 우선순위를 다 무시하고 가장 최우선 순위를 가진다.
    - `color: red !important;`
- 선택자를 결합해서 구체적으로 지정할 수록 명시도가 올라간다.
    
    ```html
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <title>명시도</title>
        <style>
          h1 {
            color: red;
          }
           /* blue가 적용됨 */
          #xxx > h1 {
            color: blue;
          }
        </style>
      </head>
      <body>
        <div id="xxx">
          <h1>Hello</h1>
        </div>
      </body>
    </html>
    ```
    
<hr>

# 4. 선택자

## 1) 전체 선택자

: * 로 html의 모든 요소들을 선택한다.

- 

## 2) 태그 선택자

: 태그명으로 표현한다. 

- 같은 태그인 요소들에 전체 적용된다.
- 명시도 : (0, 0, 1)
- `div {  color: blue; }`

## 3) id 선택자

: 태그에 id 속성을 지정하고, #id값 으로 표현한다. 

- 태그마다 유일한 id를 지정해서 요소들을 식별한다.
- 명시도 : (1, 0, 0)

## 4) class 선택자

: 태그의 class 속성을 지정하고, .class값 으로 표현한다. 한번에 여러값으로 class를 지정할 수 있고, 중복값도 가능하다.

- `<li class="select xxx">A3</li>`
- .xxx : 클래스명이 xxx인 태그를 찾음
- p.xxx : p태그이고 클래스명이 xxx인 태그를 찾음
- p .xxx : p태그 자식에서 클래스명이 xxx인 태그를 찾음
- 명시도 : (0, 1, 0)

## 5) 계층구조

### - 자식

- 부모태그  >  자식태그
    
    :  부모태그를 먼저 찾고, 부모 바로 아래의 자식태그를 찾는다. 
    
    - 자손이 아니라 자식까지만 찾아준다. ( 1레벨 )

### - 자손

- 부모태그  자식태그
    
    : 공백으로 자손을 표현한다.
    
    - 자손은 자식까지 포함한다. ( 2레벨 )]

### - 형제

- 선택자 + 형제태그
    
    : 인접한 바로 뒤 형제만 참조한다.
    
    - .xxx + p

### - 형제들 (sibilings)

- 선택자 ~ 형제태그
    
    : 인접한 요소 뒤의 모든 형제들을 참조한다.
    
    - .xxx ~ p

### - 속성

- 속성명으로 찾기
    
    : [속성명] , 태그[속성명]
    
    - a[href] { color : red; }

- 속성값으로 찾기
    
    : [속성명=”속성값”],  태그[속성명=”속성값”]
    
    - [class=”xxx”] { color : red; }

- 특정 속성값으로 시작하는 요소 찾기
    
    : [속성명 ^= ”속성값”],  태그[속성명 ^= ”속성값”]
    
    - a[href ^= ”https”]{ color : red; }

- 특정 속성값으로 끝나는 요소 찾기
    
    : [속성명 $= ”속성값”],  태그[속성명 $= ”속성값”]
    
    - a[href $= ”net”]{ color : red; }

- 특정값을 포함하는 요소 찾기
    
    : [속성명 *= ”속성값”],  태그[속성명 *= ”속성값”]
    
    - a[href *= ”www”]{ color : red; }


<hr>

# 5. 의사코드 ( pseudo code )

: html의 시멘틱 태그처럼 이름안에 기능이 내포되어 있는 선택자

## 1) 의사 클래스 ( pseudo class )

- :클래스명
    - :first-child

- a태그의 link 관련 의사 클래스
    
    방문전 (기본: blue)     :   a:link { color:red; }
    
    방문후 (기본: purple) :    a:visted { color:green; }
    
    마우스오버                 :    a:hover{ color:yellow; }     
    
    누르고 있을떄 (기본: red) : a:active{ color:blue; }\
    

- 자식 선택하는 의사 클래스 ( 지정된 선택자의 부모 기준)
    - :first-child : 태그의 부모를 찾고 그 부모의 첫번째 자식을 찾음 ( 위치상 첫번째 )
        - first-of-type() : 태그의 부모를 찾고 그 부모에서 태그 별 첫번째 자식을 찾음 ( 태그별 첫번째 )
    - :last-child :  태그의 부모를 찾고 그 부모의 마지막 자식을 찾음
    - :only-child :  태그의 부모를 찾고 그 부모의 유일한 자식을 찾음
        - :empty : 자식이 없는 태그를 참조
    - :nth-child(n) : n번째 자식을 찾음

- 사용자 입력 태그에서 사용하는 의사 클래스
    - :focus
        - input:focus { }
    - :blur
        - focus 반대
    - :checked
        - 체크박스 및 select 태그에서 값을 선택했을 때
    - :enabled / :disabled
        - 활성화 / 비활성화

## 2) 의사 요소 ( pseudo elements )

: 의사 클래스는 태그 전체에 스타일이 적용되고 의사 요소는 부분적으로 스타일이 적용된다.

- ::요소
    - ::first-line
        - 문단의 첫줄
        - `p::first-line {color: red;}`
    - ::first-letter
        - 텍스트의 첫글자
        - `p::first-letter { color: blue;}`
    
- 특정요소에 컨텐츠(문자열, image..) 삽입
    
    : 무조건 content 속성을 지정해야된다. 
    
    - ::before { content : 값 | url(’이미지경로’) }
    - *::after { content : 값 | url(’이미지경로’) }*

---

# 6. Box 모델

## 1) 개요

: css(html)에서 모든 요소는 box로 관리한다.

## 2) 구성요소
![image](https://github.com/user-attachments/assets/02ccdfdd-22f2-4dbe-95f9-4186781e90d2)
### - content

: 실질적 내용 ( 텍스트, 이미지, .. )

### - padding

: 패딩은 content의 안쪽 여백 (top, bottom, left, right)

### - border

: 보더는 content를 감싸는 테두리 ( 색상, 굵기, 여부, 선의종류 )

### - margin

: 마진은 content 비낕쪽 여백 (top, bottom, left, right)

- body에 기본적으로 margin : 8px 로 되어 있음.

## 3) 블럭레벨 vs 인라인레벨

1. 블럭레벨
    - 웹 브라우저의 전체 너비를 차지하기에, 다음 요소는 새로운 라인에 추가된다.
    - 크롬 브라우저의 개발자도구(f12)로 확인하면 width와 height값을 확인할 수 있다.
    - 명시적으로 width, height를 지정할 수 있다.
2. 인라인레벨
    - 자신의 content 크기만큼 너비를 차지하기에, 다음 요소는 5같은 라인에 추가된다.
    - 크롬 브라우저의 개발자도구(f12)로 확인하면 width와 height가 auto로 보인다.
    - width와 height를 명시적으로 지정해도 적용되지 않는다.

## 4) width 와 height

: Box 모델에서의 content의 너비와 높이를 의미한다.

- 문법
    
    : width | height : 절대값(px)
    
      width | height : 상대값(%, rem)
    
    - 상대값은 부모의 너비, 높이를 기준으로 한다.
    - 1rem(1em) = 16px
    - position 속성에 따라 기준이 달라질 수 있다.

---

# 7. box-sizing 속성

: 요소의 너비와 높이를 계산하는 방식이다.

## content-box

- 기본(디폴트) 속성
- padding, border 의 값이 지정된 width와 height에 추가되어 실제 박스 크기가  설정된다.
- 따라서 실제 너비와 높이는 지정한 값보다 커질 수 도 있다.
    - 최종 width = 지정한 width + padding + border

## border-box

- 지정한 width와 height는 고정되고, 그 안에서 padding과 border가 포함되어 그려진다.
- 패딩과 보더를 지정해도 박스 크기는 고정되기에 박스 크기가 변경될 위험성이 없다.

---

# 8. margin

## 1) 기능

: **요소(content)의 테두리(border) 바깥쪽 여백**을 제어한다 .

- px와 % 지정 가능

## 2) 문법

- 개별적으로 4개 위치 지정
    
    `margin-top : 10px, margin-right : 10px, margin-bottom : 10px, margin-left : 10px`
    
- 축약 표현
    - 개별위치 4개 모두 지정
        
        `margin : 10px 10px 10px 10px /* (top right bottom left */`
        
    - 개별위치 3개 지정
        
        `margin : 10px 10px 10px /* top right|left bottom */`
        
    - 개별위치 2개 지정
        
        `margin : 10px 10px  /*(top|bottom right|left*/` 
        
    - 1개 지정
        
        `margin : 10px  /*(top|bottom|right|left*/` 
        

## 3) margin의 상쇄

: **인접한 box의 margin은** 서로 겹쳐질 수 있는데 이때 하나로 합쳐서 margin이 만들어지는 것이 아니고 **큰 크기의 margin으로 대체된다.**

```
      width: 100px;
      margin: auto;
      background-color: red;
```

```css
 #x1 {
      margin: 20px 10px;
    }
 #x2 {
      margin: 50px 10px;
    }
```

- x1과 x1 사이의 마진은 70px가 아니라 50px이다.

## 4) 중앙정렬 ( 수평으로 가운데 정렬 )

: `margin: auto;`

- 반드시 **블럭레벨**이면서 **width 값을 가져야** 적용이 된다.

---

# 9. Padding

## 1) 기능

: **요소(content) 내용과 테두리(border) 사이의 여백**을 제어한다.

## 2) 문법

- 개별적으로 4개 위치 지정
    
    `padding-top : 10px, padding-right : 10px, padding-bottom : 10px, padding-left : 10px`
    
- 축약 표현
    - 개별위치 4개 모두 지정
        
        `padding: 10px 10px 10px 10px /* (top right bottom left */`
        
    - 개별위치 3개 지정
        
        `padding: 10px 10px 10px /* top right|left bottom */`
        
    - 개별위치 2개 지정
        
        `padding: 10px 10px  /*(top|bottom right|left*/` 
        
    - 1개 지정
        
        `padding: 10px  /*(top|bottom|right|left*/` 
        
---

# 10. border ( 테두리 )

## 1) 기능

: margin과 padding 사이의 테두리

- 3가지 속성을 이용해서 스타일 지정이 가능하다.
    
    - width : border 두께
    
    - style : border 스타일 ( 실선, 점선, .. )
    
    - color : border 색상
    

## 2) 문법1 - 개별

- width
    
    `border-top-width : 5px`
    
- style
    
    `border-top-style : soild | dotted | dashed..`
    
- color
    
    `border-color : red;`
    

## 3) 문법2 - 개별 축약 지정

- width
    
    `border-width: top right bottom left` 
    
    `border-width: top right|left bottom` 
    
    `border-width: top|bottom`  
    
    `right|left` 
    
    `border-width: top|right|bottom|left` 
    
- style
    
    `border-style : top right bottom left` 
    
    `border-style : top right|left bottom` 
    
    `border-style : top|bottom  right|left` 
    
    `border-style : top|right|bottom|left` 
    
- color
    
    `border-color : red`
    
    `border-color: blue yellow red purple;`
    

## 4) 문법 - width + style + color

- `border: width style color;`

## 5) border-radius 속성

: box의 boder를 둥글게 설정할 떄 사용하는 속성으로, 값이 클수록 동글해진다.

- `border-radius : 50%  // 원`
- `border-radius : 10px`

---

# 11. 요소배치

## 1)  display

- display : block           :   블럭 레벨로 배치
- display : inline           :   인라인 레벨로 배치
- display:  inline-block :   인라인-블럭 레벨 ( 인라인레벨 + width + height)
- diplay : none              :   화면 레더링 방지, 영역유지 안됨

## 2) position

: position의 top, right, bottom, left 속성을 이용해서 요소의 실제 위치를 바꿀 수 있다.

- **position : static (기본)**
    - 블럭레벨은 세로 배치, 인라인 레벨은 가로 배치, left와 top이 8px 마진을 가진다.
    - **top, right, bottom, left 속성을 지정해도 적용되지 않는다**. 따라서 static이 아닌 다른 값으로 지정해야 4가지 속성을 사용할 수 있다.
    
    ```css
    /***top, right, bottom, left 속성을 지정해도 적용되지 않는다***/
    position: static;
    top: 300px;
    left: 300px;
    ```
    
- **position : relative**
    - 기준 위치는 ‘positon : static’ 일 때의 위치
    - **top, right, bottom, left 속성을 지정할 수 있다.**
- **position : absolute**
    - 부모 요소와 같이 사용된다.
    - 기준 위치는 부모요소이다.
        - **부모가 position:relative**   :  자식 요소 기준은 부모가 된다.
        - 부모에 positon 속성 X ( position : static )  : 자식 요소 기준은 뷰포트( 웹 브라우저)가 된다.
- **position : fixed**
    - **기준은 웹브라우저 화면( 뷰포트 : viewport ) 이다.**
    - **top, right, bottom, left 속성을 지정할 수 있다.**
    - **스크롤 해도 위치가 고정**된다.
- position : sticky
    - 최근에 추가된 기능, 지원여부를 확인해야 한다
        - https://caniuse.com/
    - 평시에는 static 으로 동작되고 특정 임계값을 만나면 fixed 로 동작
        
        ```css
        /*top이 40px이 되면 fixed 됨.*/
        positon : sticky;
        top : 40px; 
        ```
        

## 3) z-index

: z축으로 요소를 배치할 수 있도록 하는 속성으로, 요소들이 겹쳐보이지 않도록 할 떄 주로 사용한다.

- position : fixed  absolute 속성으로 요소가 겹쳐 보이는 경우가 생긴다.

## 1) 문법

- z-index : auto | 값
    - 디폴트는 auto이고 0을 준 것과 동일하다.
    - 값이 작을수록 밑에 배치된다.
        - 아래에 있는 요소를 위로 배치하고 샆으면 위 요소의 z-index보다 크게 값을 지정하면 된다.
        

---

# 12. 배경

## 1) 배경색

- `background-color: 색상`

## 2) 배경 이미지

- `backgorund-image : url(”경로”)`
- x축 및 y축으로 반복적으로 이미지가 출력된다.
- 배경색과 같이 사용가능

## 3) 배경 이미지 반복 제어

- `background-repeat : repeat-x | repeate-y | repeat(디폴트) | no-repeat`

## 4) 배경 이미지 크기

 `background-size : auto(기본값) | px | contain | cover`

- background-size : 30px 50px (너비, 높이)
- **background-size : contain**
    - 이미지를 보여주는 **컨테이너 사이즈에 맞춰서** 보여준다. 화면을 작게하거나 크게하면 컨테이너 사이즈에 맞춰서 자동적으로 조절된다.  단 일정 크기에서만 움직인다.
    - **이미지 전체를 확인**할 수 있다.
- **background-size : cover**
    - **이미지 비율**을 관리하기에 이미지 **전체가 바로 나오지 않을 수 있다.**
    - 화면이 커지면 비례해서 이미지가 커져서  잘려보이거나 화면이 작아지면 일정 부분까지 작아져서 잘려보일 수 있다.

## 5) 배경 이미지 위치

- `background-position : x축( px | % );`
- `background-position : x축( px | % )  y축( px | % );`
- `background-position : bottom 10px  right 20px;`
    - top, right, bottom, left 지정가능하다.

## 6) 배경 이미지 스크롤 여부

- `backgrond-attachment : scroll(기본) | fixed`

---

# 13. 크기단위 (unit)

## 1) 단위 종류

- px   (c, inch)
- %
- rem (em)
- vw ,vh

## 2) 적용 css 속성

- width/height        : %, vw, vh
- font-size               :  rem
- margin/padding   :  %,  rem
- border                  :  px
- position (top/right/bottom/left)  :  %

## 3) 단위 종류 2가지

### 절대 단위

: px만 사용하기로 한다.

### 상대 단위

- **%**
    - 기본적으로 부모 기준이고, position에 따라 기준이 달라진다.
        - position : static     : top/right/bottom/left 지정 불가
        - position : relative   : top/right/bottom/left  지정 가능, 기준은 static으로 지정했을 때의 기본 문서대열
        - position : fixed        : top/right/bottom/left  지정 가능, 기준은 뷰포트
        - position : absolute   : top/right/bottom/left 지정 가능, 부모가 relative로 지정되었으면 기준은 부모고 아닌 경우는 뷰포트 이다.
    - max - width 속성
        - % 를 사용하면 화면크기가 커짐에 따라 이미지가 계속 커질 수도 있다.
- **vw, vh**  (  vw: viewport width,    vh: viewport height )
    - 기준은 뷰포트
    - 사용하지 않는 경우
        
        ```css
        <div>
        	<h1>  <== position: fixed;  width:50%
        ```
        
    - 사용하는 경우
        
        ```css
        <div>
        	<h1>  <==  width:50vw
        ```
        
- **rem (em)**
    - 글꼴에서 주로 사용
    - 1rem(1em) = 16px  ( 16px는 웹 브라우저에 설정된 기본글꼴크기)
    - em
        - 부모요소의 em값을 상속해서 글꼴크기가 정해진다.
    - rem ( root em )
        - root인 html(body)를 상속해서 글꼴크기가 정해진다.


---

# 14. 색상

## 1) 영단어 표기

- color : red | blue | yellow …

## 2) 16진수 ( 0 ~ 15 )

- #RRGGBB  (6비트),   #RGB  (3비트)
- #FFFFFF  (흰색)
- #000000 (검정)

## 3) 10진수 ( 0 ~ 255 ) + rgb (r,g,b)

- rgb(0 ~ 255, 0 ~ 255, 0 ~ 255)
- rgb(225,255,255) : 흰색
- rgb(0,0,0) : 검정색

## 4) 투명도 (alpha)

- rgb(0 ~ 255, 0 ~ 255, 0 ~ 255, 0 ~ 1)
- 0: 완전투명, 1 : 완전불투명
- 예 > color : rgba(0, 0, 0, 0.00-004)

```css
    #x1 {
      color: red;
    }
    #x2 {
      color: #019201;
    }
    #x3 {
      color: rgb(22, 21, 100);
    }
    #x4 {
      color: rgba(23, 55, 200, 0.1);
    }
```


---

# 15. visibility  속성

: 요소를 보이거나 안 보이게 설정 할 수 있다.

- visibility  : visibile(기본)
    
                   : hidden     ⇒  요소가 안보이게  
    
              : collapse   ⇒  <table>을 안보이게
    
- hidden은 요소가 안 보이더라도 영역유지 O
- collapse는 <table> 렌더링을 방지 ( 안보이게 )하고, 영역유지 X
- display: none도 영역유지 X


---

# 16. 투명도 (opacity) 속성

: 요소의 투명도를 제어하는 속성이다.

- opacity :  0 ~ 1 값
    - 0 : 완전투명
    - 1 : 완전불투명


---

# 17. 글꼴(font)

## 1) font-style

- font-style : normal | italic | …

## 2) font-weight

- font-weight : bold | bolder | lighter |100 ~ 900

## 3) font-size

- font-size : rem | px

## 4) font-family

- font-family : 값1, 값2, 값3, …
- 값 종류 3가지
    - generic family
        
        : 실제 글꼴들의 카데고리로서 글꼴들이 가지는 특별한 주요 특징들을 가진다
        
        - serif, sans-serif, monospace(고정폭), ….
    - font family
        
        : generic family에 속하는 실제 글꼴을 의미한다.
        
        - serif : Times New Roman, Geogia
        - sans-serif : consolas

- 크롬 브라우저에서 글꼴 확인 방법
    
    : 설정 > 모양 > 글꼴 맞춤 설정에 가면 아래와 같이 설정되어 있다.
    
    **표준 글꼴 : Malgun Gothic**   <=  font family 
    
    Serif: Batang                         <=  generic family 
    
    Sans-serif : Malgun Gothic   <=  generic family 
    

- 웹 브라우저가 글꼴을 결정하는 방법 2가지
    - font-family 속성을 명시적으로 지정하지  않는 경우
        
        : 웹 브라우저에서 기본으로 설정된 글꼴을 이용해서 렌더링 된다. 따라서 표준 글꼴 ( Malgun Gothic)으로 렌더링 
        
    
    - font-family 속성을 명시적으로 지정하지  않는 경우
        - generic family 만 지정한 경우
            
            ```css
             font-family: serif;
                 /* serif 카테고리에서 기본으로 설정된 폰트를 사용한다 */
                }
            ```
            
        - font family 지정한 경우
            
            ```html
                  font-family:'Times New Roman', Times, serif
                  /* serif카데고리의 폰트들을 사용한다. */
                  /* 'Times New Roman'이 있으면 이걸 사용하고, 없으면 'Times'사용한다는 의미*/
            ```
            

## 5) 축약 표현

- `font: italic bold 2rem 'Times New Roman', Georgia, sans-serif;`


---

# 18. 구글폰트

https://fonts.google.com/

- 웹 폰트라고 부른다.
- 로컬에 글꼴이 없어도 링크를 통해 가져와 사용할 수 있다.
- [구글 폰트](https://fonts.google.com/) > 원하는 폰트 선택 > Get Font 클릭 > Get embed code > 복사해서 사용


---

# 19. text 관련 속성

## 1) color : 색상

- `color : 값;`

## 2) text-align :  수평 정렬

- `text-align : center | left | right | justify (양쪽)`

## 3) text-decoration : 밑줄 및 취소선

- `text-decoration : underline | overline | line-through (취소선)`

## 4) text-indent  : 첫 라인 들여쓰기

- `text-indent : 10px;`

## 5) line-height : 줄 간격

- `line-height: 2;`
- font-size : 16px 값에 비례해서 적용

  ---
  # 20. Flex Box 모델

## 1) 개념

: Flex Box를 이용하면 **매우 쉽게 레이아웃 및 수직/수평 정렬, 요소 순서(ordering), 동적 사이징이 가능**하다.

## 2) 구성요소 2가지

- 부모(flex Container)와 부모안의 자식요소(flex item)로 구성된다. flex를 사용하기 위해서는 반드시 **부모 컨테이너**가 필요하고, 부모에 flex를 지정하면 **자식요소에 영향을 주는 것**이다.
1. **flex Container**
    - **`display : flex;`**
    - 정렬의 **기본 배치는 가로 정렬**이다. **flex-direction 속성**으로 변경 가능하다.
        - **`flex-direction: column;`  : 세로 정렬**
            - 세로 정렬시 자식의 width 중 가장 큰 width 기준으로 맞춰진다.
        - **`flex-direction: row;` : 가로 정렬**
            - 가로 정렬시 자식요소 중 가장 큰 height를 기준으로 맞춰진다.
2. **flex item**
    - item의 부모 Container에서 **display:flex** 를 지정해 정렬되는 요소를 의미한다.
    - **order, align-self, flow-grow** 속성을 지정할 수 있다.

## 3) Flex Box 속성 ( Container )

### flex-direction

: flex  정렬 기준을 변경할 수 있다.

- **`flex-direction: column;`  : 세로 정렬**
- **`flex-direction: row;` : 가로 정렬**
- **`flex-direction: row-reverse;` : 가로 반대로 ( 오 → 왼)**
- **`flex-direction: column-reverse;` : 세로 반대로 ( 아래 → 위 )**

### flex-wrap

: 화면 크기를 줄였을 떄 **item이 다음줄로 넘겨가도록** 하는 속성

- `flex-wrap: wrap;`
- `flex-wrap:nowrap;` ( 디폴트 )
- `flex-wrap:wrap-reverse;` : 하단 기준으로 wrap

### flex-flow

:flex-direction과 flex-wrap 한번에 표현하는 속성

- `flex-flow : row warp;`

### justify-content

: **주축에 대한 정렬** 

- `justify-content : center | flex-start | flex-end | space-around | space-between | space-evenly`
    - center
    - flex-start
    - flex-end
    - space-around
    - space-between
    - space-evenly
    

### align-items

: **교차축에 대한 정렬**

- align-items: center | flex-start| flex-end | stretch(기본) | baseline
    - stretch : item을 늘려서 컨테이너에 꽉 채운다. ( width나 height )
    - center : 원래 값을 가지고 중앙정렬
    - flex-start : 요소의 위쪽 테두리를 맞춰서 정렬
    - flex-end : 요소의 아래 테두리에 맞줘서 정렬
    - baseline :item 안의 content의 위치에 맞춰서 정렬

### align-content

: justify-content와 align-items 합성 기능

- wrap 항목에서만 적용된다.
- `align-content: center | flex-start | flex-end | stretch(기본) | space-around | space-between | space-evenly`

## 4) Flex Box 속성 (item)

### order

: 기본적으로는 코드에 명시된 순서로 표현되지만 **order 속성을 사용하면 순서를 변경할 수 있다.**

- `order : 0; ( 0이 기본값 )`
- -1(앞)  0 (기본)  1(뒤)

### align-self

: Container에서 설정된 **align-items 속성을 재정의**할 수 있다.

- `align-self : center | flex-start | flex-end | stretch(기본) | baseline`

### flow-grow

: 화면을 크게할 때 **item이 커지는 비율을 관리**하는 방법

- flow-grow : 0 (0이 기본값)
- 예 >
    - `flow-grow : 1` 로 지정하면 flow-grow : 0인 요소들은 자신의 너비만큼 차지하고, 나머지 영역을 flow-grow:1이 차지한다.
    - `flow-grow : 1` , `flow-grow : 3` 로 지정하면 flow-grow : 0 인 요소들은 자신의 너비만큼 차지하고, 나머지를 **flow-grow : 1 은 1/4를 차지, flow-grow : 3 은 3/4를 차지**한다.

### flow-shrink

: 화면을 작게할 떄 **item의 작아지는 비율을 관리**하는 방법

- flow-shrink : 1 (1이 기본값)
- flow-shrink : 0  ⇒ 크기변경이 안 됨

### flow-basis

: item의 기본 크기 설정 용도로, **기존에 지정한 width, height를 flex-basis 지정값으로 덮어쓴다.**

- flex-basis : auto | px | %

- 동작방식

- 주축이 row인 경우 ( width 고려)
    
    flex-basis : auto   ⇒ 기존의 width를 사용
    
    flex-basis: 100px  ⇒ 기존 width : 50px 가 아니라 100px를 사용
    
- 주축이 column 인 경우 ( height 고려)
    
    flex-basis : auto     ⇒ 기존의 height 를 사용
    
    flex-basis: 100px    ⇒ 기존 height : 50px 가 아니라 100px를 사용
    

---

# 21. Grid 모델

: **grid는 2차원인 행/열 같이 제어가 가능**하다.

## 2) 구성요소 2가지

: 반드시 부모에 display:grid 를 지정해야 한다. 실행결과는 행으로 추가된다. ( 세로나열 )

- Grid Container
- Grid item

## 3) Grid 속성 (Container)

### grid-auto-flow

- item 배치
- `grid-auto-flow : row(기본) | column;`

### grid-template-columns

- 열을 생성
- `grid-template-columns : 값1 값2 값3 값4`
    - 예 > `grid-template-columns : 20px 20px 20px 20px`
    - `grid-template-columns : repeat(4, 20px)`
    - `grid-template-columns : 20px 30px 1fr 2fr`
        - fr : fraction이고 나머지 여백을 비율로 계산

### grid-template-rows

- 행을 생성
- `grid-template-rows : 값1 값2 값3`
    - 예 > `grid-template-rows: 130px 240px 125px 200px;`
    - `grid-template-rows: 25% 25% 250px auto;`

### 행/열 만들기

```html
      grid-template-rows: 120px 1fr 250px;
      grid-template-columns: 1fr 2fr;
```

### item 간 gap 지정

- `row-gap: 10px;`       : 행 간격
- `column-gap: 10px;`  : 열 간격
- `gap: 10px 10px;`      : 행/열 간격

### 정렬

- 셀 안에서의 item 정렬
    - x축 정렬 : **`justify-items** : center | flex-start …`
    - y축 정렬 : **`align-items** : center | flex-start …`

- container 정렬
    - x축 정렬 : **`justify-content** : center | flex-start …`
    - y축 정렬 : **`align-content** : center | flex-start …`

## 4) Grid 속성 (item)

### 셀 안에서의 item 정렬 재정의

- x축 정렬 : **`justify-self**: center | flex-start …`
- y축 정렬 : **`align-self**: center | flex-start …`

### item을 원하는 위치에 정렬 - 위치 번호 이용

- `grid-column-start: 시작값(번호);`
- `grid-column-end: 값(번호);`
    - `grid-column: 시작값(번호)/값(번호);`  :  축약 표현
- `grid-row-start: 시작값(번호);`
- `grid-row-end: 값(번호);`
    - `grid-row: 시작값(번호)/값(번호);`  :  축약 표현

### item을 원하는 위치에 정렬 - 갯수 이용

- `grid-column-start: 값;`
- `grid-column-end: span n(갯수) ;`
    - `grid-column: 값/span n(갯수);`  :  축약 표현
- `grid-row-start: 값;`
- `grid-row-end: span n(갯수);`
    - `grid-row: 값/span n(갯수);`  :  축약 표현

### item을 원하는 위치에 정렬 - 셀 이름 이용

![image (1)](https://github.com/user-attachments/assets/09a1141d-f85b-4506-aedb-d59ba824950e)


```css
container {
		 grid-template-areas:
        "header header header1 header2"
        "main1 main main main"
        "footer footer footer4 footer4";
}
.item-1 {
      background: red;
      grid-area: main1; /*main1 위치에 정렬*/
    }
    
.item-2 {
      background: blue;
      grid-area: main; /*main 위치에 정렬 == 3개의 셀*/
    }
```

---

# 22. media 쿼리

: 반응형 웹을 구축할 때 사용하는 방법

### *반응형 웹

: 현재 대부분 모바일 기기를 사용하기애 개발자는 하나의 웹 페이지를 일반 PC에서도 잘 보여주고 모바일 기기에서도 잘 보여질 수 있도록 구축해야된다. 이떄 반응형 웹을 사용한다.

- 방법1 : 디바이스마다 html을 따로 만듦
- 방법2 : 하나의 html을 만들어서 **화면의 크기에 따라 레이아웃을 변경시키는 방법**. 이것이 **반응형 웹**이고 **media 쿼리를 이용**해서 구축할 수 있다.

### 문법
```css
/* 화면이 700px보다 같거나 작을떄의 css */
@media screen (max-width : 700px) {
				...
}
```
```css
 body {
      background-color: yellow;
    }

 @media screen and (max-width: 700px) {
      body {
        background-color: tomato;
      }
    }
 `` 
