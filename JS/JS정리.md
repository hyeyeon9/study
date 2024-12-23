# 1. JS(JavaScript) 개요

- java 언어와 무관하다.
- 서버에 저장하지만 웹브라우저에서 실행된다.
    - 웹 브라우저에는 2가지 엔진이 존재
        - html을 렌더링하는 엔진
        - JS 실행하는 엔진 ( 크롬 : v8 )
- 구글에서 V8엔진을 가진 서버를 만듦 : node.js

```
클라이언트 (웹브라우저)            서버(node.js)
         V8                             V8             
```

- 현재는 웹브라우저 및 서버(node.js)에서 JS를 실행할 수 있다.
- 표준화된 JS (2015년)
    - ECMAScript6
    - 표준화 안 된 JS는 ECMAScript5

---

# 2. JS 특징

- 인터프리터 언어 ( 컴파일 없이 한 줄 씩 실행된다. )
- 변수선언시 데이터 타입을 지정하지 않는다.
- 대소문자 구별
- 웹 브라우저 및 서버에서 실행
- html에 포함되어 JS가 실행된다.
- java 언어처럼 일반적인 프로그램언어가 가진 특징을 가진다.
    - 데이터 종류, 변수, 연산자, 제어문, 클래스, 함수
    - 주석문 :  // ,  /* … */
    - console 출력 : console.log(값)

---

# 3.  html에 js 설정

1) <head> 내에 <script> 설정

```
<head>
			 <script> 
			 // JS코드...
			 </script> 
</head>
```

2) <body> 내에 <script> 설정

```
<body>
			// html 태그
			 <script> 
			// JS코드...
			 </script> 
</body>
```

3) 외부파일로 설정 

- <head> 내에 <script>로 참조

```
<head>
			 <script src="test.js"> </script> 
</head>
```

---

# 4. 식별자 ( identifier )

: js 코드내의 단어의 개념

- 대소문자 구병
- 첫글자는 반드시 영문자 또는 _, $ 만 지정 가능
- 시스템 정의 식별자(예약어), 사용자 정의 식별자 사용
    - 변수명 : 모두 소문자 권장
    - 상수명 : 모두 대문자 권장
    - 함수명 : 모두 소문자 권장
    - 클래스명 : 첫글자 대문자

---

# 5. 데이터 종류

## 1) 기본 데이터형

- **수치 데이터** : 정수와 실수
    - Number 객체
      
- **문자 데이터** : 문자와 문자열 포함
    - String 객체
    - 홑따옴표/쌍따옴표 구분 X
      
- **논리 데이터** : 참/거짓
    - Boolean 객체 : true/false
    - false 로 처리되는 값
        - 0, “”, null, undefined, NaN
    - 주로 조건문 및 논리연산자에 사용
      
- **undefined** : 변수가 선언후 초기화 안 된 상태
    - Object 객체
      
- **null** : 변수 초기화 된 상태지만 값 없는 상태
    - Object 객체
      
- **NaN** : Not a Number
    - Number 객체
    - 일반적으로 숫자가 아닌 문자열을 수치형으로 변경할 때 발생할 수 있다.
        - 예 > “10”   ⇒   Number.parseInt(”10”)      ⇒   10
            
                   “민지” ⇒   ~~Number.parseInt(”민지”)~~   ⇒   NaN 발생
            


## 2) 참조 데이터형

- **배열** (객체)   :  [  값1, 값2, …  ]
- **JSON (**객체) :  JSON ( JavaScript Object Notation )
    - **{key : value} 형식** ⇒ `{ name: "홍길동", age: 10 }`
- **함수** (function) (객체) : 자바의 메서드 기능
    
    ```
    function 함수명(변수, ...){
    						// 문장
    						return 값;
    }
    ```
    
    - JS의 함수는 데이터로 처리된다.
    - 변수에 저장
    - 리턴값으로 사용
    - 함수 호출시 인자값으로사용
    - 위 3가지 특징을 갖는 함수(객체)를 일급객체(first-class)라 부른다.
        - 일급객체 언어 : JS, Python, 자바(람다)
        
- **클래스** (class) :
    
    ```
    class 클래스명 {
    		// 생성자
    		// 메서드
    }
    new 클래스명();
    ```
    
![image (2)](https://github.com/user-attachments/assets/70a5a71d-6e3a-44d8-ac92-297204506047)

    

---

# 6. **typeof 연산자**

: 데이터 타입을 확인

- `typeof new Cat()   // Cat object`
- `typeof 3.14   // number`

---

# 7. 변수 ( Variable )

: **데이터 저장**

## 1) JS 변수 특징

- **데이터형을 지정하지 않는다.**
    - 임의의 변수에 데이터타입을 제한하지 않기에 하나의 변수에 모든 데이터값을 저장할 수 있다.
    - 간편하지만 개발자 입장에서는 좋지 않음
        - 이를 해결하기 위해 타입스크립트 등장

## 2) 문법 2가지

1. **var 키워드** 
    - OLD 버전
    
    ```
    var 변수명;      // 변수선언, undefined 저장됨
    변수명 = 값;     // 변수 초기화
    var 변수명 = 값; // 변수 선언 및 초기화
    ```
    
    - 특징
        1. **변수 중복가능**
        2. **함수 스코프**를 따른다.
            - 함수에서 사용하는 {}안에서 선언한 것은 밖에서는 사용 불가
            - 함수 제외한 if, for 문 등의 {}는 상관없음
    
2. **let 키워드  (권장**)
    - ES6
    
    ```
    let 변수명;      // 변수선언, undefined 저장됨
    변수명 = 값;     // 변수 초기화
    let 변수명 = 값; // 변수 선언 및 초기화
    ```
    
    - 특징
        1. **변수 중복 불가능**
        2. **블럭 스코프**를 따른다.
            - 모든 {} 안에서 선언한 것은 밖에서 사용 불가

---

# 7. 기본형 변수 vs 참조형 변수

## 1) 기본형 변수

: 기본형 데이터를 저장하는 변수

- `let n = 10;`
- **call by value**
    - 값을 전달하기에 기존 변수에 다른 영향이 가지 않는다.

## 2) 참조형 변수

: 참조형 데이터를 저장하는 변수

- `let n2= [10,20,30];`
- **call by reference**
    - 값이 저장된 주소를 전달한다.
    - 따라서 값 변경등이 일어나면 기존의 변수에도 영향이 갈 수 있다.

---

# 8. 상수

: `const 상수명 = 값;`

- **값 변경 불가**
- **상수명 중복 불가**
- **블럭 스코프**를 따른다.
- Front-end 프레임워크 ( React.js (facebook), Vue.js, Angular (google) ) 에서 매우 자주 사용된다.

`주의할 점`

```jsx
// 상수 주의할 점
      const m = [10, 20, 30]; // m에는 배열의 주소가 저장되어 있음
      m[0] = 100; // 그래서 그 주소의 요소값은 변경 가능
      console.log(m);

      m = [100, 200, 300]; // m에 새로운 주소값을 넣었기에Assignment to constant variable 오류 발생 
      // console.log(m);
```

---
# 9. 연산자

- **산술연산자**
    - +
    - -
    - *
    - / : 소수점까지 출력
    - % : 나머지

⇒ 문자열로 된 숫자와의 연산이 가능하다. (  +  제외)

- **+ 로는 문자열로 합해진다.**

```jsx
      console.log("10" + 3); // 103
      console.log(Number.parseInt("10") + 3); // 13
      console.log("10"  -3); // 7
      console.log("10" * 3); // 30
      console.log("10" / 3); // 3.3333333333333335
      console.log("10" % 3); // 1
```

- **대입연산자**
    - =
    - +=
    - -=
    - *=
    - /=
    - %=

- **비교연산자**
    - a == b  |  a ! =  b
    - a > b  |  a >= b
    - a < b  | a <= b
    - **a === b**
        - **`값과 데이터 타입`까지 비교**, identical 연산자
        
        ```jsx
              console.log("10" == 10);  // true
              console.log("10" === 10); // false
        ```
        
        - **`undefined` 비교할 떄는 반드시 === 연산자를 사용**
        
        ```jsx
              let v = undefined;
              console.log(v == undefined); // true
              console.log(v === undefined); // true
        
              let v2 = null;
              console.log(v2 == undefined); // true
              console.log(v2 === undefined); // false
        ```
        
        - 실제값이 null일떄도 undefined와 == 비교를 하면 true 값이 나오기에 === 연산자를 사용해야 한다.
    - **a ! == b**
    
- **논리연산자**
    - && (and)
    - || (or)
    - ! (not)

⇒ JS 에서는 **true/false 가 아닌 임의의 값도 논리값으로 사용**될 수 있다.

- **`false`로 사용되는 5가지의 값**
    - 0,””, null, undefined, NaN

⇒ **A && B** :  중요 ( 리액트에서 자주 사용됨 )

- A가 참이면 B가 반환
- A가 거짓이면 A가 반환

```jsx
console.log(10 && "홍길동"); // 홍길동
console.log(0 && "홍길동");  // 0
```

**A || B**

- A 가 참이면 A 가 반환
- A 가 거짓이면 B 가 반환

**!A**

- A의 반대 반환 ( true ↔ false)

- **증감연산자**
    - ++n  : 전치 증가
    - n++  : 후치 증가
    - - - n  : 전치 감소
    - n - -  : 후치 감소
    
    ```jsx
          let n = 10;
          console.log(n++); // 10
          console.log(++n); // 12
    
          console.log(n--); // 12
          console.log(--n); //10
    
          let n2 = 10;
          let result = ++n2; // 11
          console.log(result, n2); // 11, 11
    
          let n3 = 10;
          let result2 = n3++; // 10
          console.log(result2, n3); // 10, 11
    ```
    

- 3항 연산자
    - (조건식) ? 참 : 거짓;
        
        `100 > 102 ? "O" : "X”`
        

---
# 10. 문장

## 실행문

- 순차문
- 제어문
    - **조건문  ( if문, if ~ else문, 다중 if문, switch문 )**
        
        ```jsx
              // 1. 단일if문
              if (3 > 2) {
                console.log("true");
              }
        
              console.log("=================");
        
              // 2. if ~ else 문
              if (3 > 20) {
                console.log("true");
              } else {
                console.log("false");
              }
        
              console.log("=================");
        
              // 3. 다중 if문
              let num = 90;
              let grade;
              if (num >= 90) {
                grade = "A";
              } else if (num >= 80) {
                grade = "B";
              } else {
                grade = "C";
              }
              console.log("학점 : ", grade);
        
              console.log("=================");
        
              // 동적으로 값 입력받기
              let num2 = prompt("점수입력");
              num2 = Number.parseInt(num2);
              let grade2;
              if (num2 >= 90) {
                grade2 = "A";
              } else if (num2 >= 80) {
                grade2 = "B";
              } else {
                grade2 = "C";
              }
              console.log("학점 : ", grade2);
              console.log("=================");
        
              // 4. switch문
              let x = "100";
              switch (
                x // 스위치문은 값과 데이터 타입을 같이 비교한다.
              ) {
                case 10:
                  console.log("10");
                  break;
                case 100: {
                  console.log("100");
                  break;
                }
                default:
                  console.log("default");
                  break;
              }
        ```
        
    - **반복문 ( for문, while문 , do ~ while문, foreach 문 )**
        
        ```jsx
              // 1. for문
              for (let i = 0; i < 5; i++) {
                console.log(i);
              }
              console.log("================");
              //2. while문
              let n = 0;
              while (n < 5) {
                n++;
              }
              console.log(n);
              console.log("================");
              // 3. do ~ while문
              let n2 = 1;
              do {
                n2++;
                console.log(n2);
              } while (n2 < 6);
        
              console.log("================");
              
              //4.breka, continue문
              let i = 0;
              for (i = 0; i < 5; i++) {
                if (i == 2) continue;
                if (i == 4) break;
                console.log(i);
              }
        ```
        

## 비실행문

- 주석문 : //, /* … */

---

