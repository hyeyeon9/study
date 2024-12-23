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

# 11. 객체종류

## 데이터 관련 객체

### **문자열 객체 ( String )**

https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String

- **`문자열 속성 및 메서드`**
    - **문자열 길이 : lenght 속성**
        
        ```jsx
        let s = "HeLLO";
        
        console.log("1. 문자열 길이 : ", s.length); // 5
        ```
        
    - **문자열 연결 : concat()**
        
        ```jsx
         console.log("3. 문자열 연결 : ", s.concat("!!!")); // HeLLO!!!
         console.log("3. 문자열 연결 : ", s.concat("!!", "~~~")); // HeLLO!!~~~
        ```
        
    - **특정 문자 얻기 : charAt()**
        
        ```jsx
        console.log("2. 특정 문자 얻기 : ", s.charAt(0)); // H
        ```
        
    - **특정 문자 위치 얻기 : indexOf()**
        
        ```jsx
        console.log("4. 특정 문자 위치 얻기: ", s.indexOf("e")); // 1
              console.log("4. 특정 문자 위치 얻기: ", s.indexOf("a")); // 없으면 -1
        ```
        
    - **부분열 :  substring(start, end)  / substr( start, len )**
        
        ```jsx
        console.log("5. 부분열 ", s.substring(0, 4)); //  start, end  //  HeLL
              console.log("5. 부분열 ", s.substr(0, 4)); // start, len // HeLL
        ```
        
    - **소문자 / 대문자 : toLowerCase() / toUpperCase()**
        
        ```jsx
        console.log("6. 소문자 ", s.toLowerCase()); // hello
        console.log("7. 대문자 ", s.toUpperCase());
        
        ```
        
    - **특정값 시작여부 / 종료여부 : startsWith()  /  endsWith()**
        
        ```jsx
        console.log("8. 특정값 시작여부 ", s.startsWith("H")); //  true
              console.log("9. 특정값 종료여부 ", s.endsWith("a")); // false
              console.log("9. 특정값 종료여부 ", s.endsWith("l", 4)); // 문자열 4개(HeLl)의 종료가 l인지 확인 => false
        
        ```
        
    - **특정값 포함 여부 : includes()**
        
        ```jsx
        console.log("10. 특정값 포함 여부 : ", s.includes("e")); // true
        ```
        
    - **치환 :  replace()  /  replaceAll()**
        
        ```jsx
          console.log("11. 치환 : ", s.replace("H", "h")); // heLlO
              console.log("11. 치환 ALL : ", s.replaceAll("L", "l")); // HellO
        ```
        
    - **공백제거 : trim()  /  trimStart()  /  trimEnd()**
        
        ```jsx
         let s2 = "      world     ";
              console.log("12. 공백제거(양쪽) : ", s2.trim()); // world
              console.log("12. 공백제거(왼쪽) : ", s2.trimStart()); // world
              console.log("12. 공백제거(오른쪽) : ", s2.trimEnd()); //        world
        
              console.log("12. 공백제거후 길이 :", s2.trim().length); // 5
        ```
        
    - **구분자로 분리 : split()**
        
        ```jsx
         let s3 = "홍길동/이순신/유관순";
              let result_arr = s3.split("/");
              console.log("13. 구분자로 분리 : ", result_arr, result_arr[0]); // (3) ['홍길동', '이순신', '유관순']0: "홍길동"1: "이순신"2: "유관순"length: 3[[Prototype]]: Array(0) 홍길동
        ```
        
    - **문자열 반복 : repeat()**
        
        ```jsx
        let s4 = "hello";
              console.log("14.문자열 반복 : ", s4.repeat(2)); //hellohello
        ```
        
    - **문자열 길이만큼 채우기 : padStart() /  padEnd()**
        
        ```jsx
        let s5 = "홍길동";
              console.log("15. LPAD : ", s5.padStart(10, "*")); // *******홍길동
              console.log("16. RPAD : ", s5.padEnd(10, "*")); // 홍길동*******
        ```
        
    - **이스케이프 문자**
        
        ```jsx
              // aaa"bbb
              console.log("aaa'bbb"); // aaa'bbb
              console.log("aaa\tbbb"); // aaa	bbb
              console.log("aaa\nbbb"); // aaa
              // bbb
              console.log("aaa\\nbbb"); // aaa\nbbb
        ```
        

### **수치 객체 ( Number )**

https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Number

- **`수치 속성 및 메서드`**
    - **최대값 / 최소값  :  MAX_VALUE / MIN_VALUE**
        
        ```jsx
         // 1. 수치 데이터 생성 방벙
              let n = 100;
              let n2 = Number(100);
              let n3 = new Number(100);
        
              console.log(n, n2, n3); // 100 100 Number {100}
        
              // 속성 및 메서드
              console.log("1. 최대값 : ", Number.MAX_VALUE); // 1.7976931348623157e+308
              console.log("2. 최소값 : ", Number.MIN_VALUE); // 5e-324
        ```
        
    - **문자열로 변경  :  toString()**
        
        ```jsx
         let n4 = 10;
              console.log("3. 문자열로 변경(10진수) : ", n4.toString()); // 10
              console.log("3. 문자열로 변경(2진수) : ", n4.toString(2)); // 1010
              console.log("3. 문자열로 변경(8진수) : ", n4.toString(8)); // 12
              console.log("3. 문자열로 변경(16진수) : ", n4.toString(16)); // a
        ```
        
    - **문자열로 고정 소수점 표기법  :  toFixed()**
        
        ```jsx
         let n5 = 3.141586;
              console.log("4. 문자열로 고정 소수점 표기법 : ", n5.toFixed()); //  3
              console.log("4. 문자열로 고정 소수점 표기법 : ", n5.toFixed(2)); // 3.14
              console.log("4. 문자열로 고정 소수점 표기법 : ", n5.toFixed(4)); // 3.1416 => 반올림됨
        ```
        
    - **NaN 여부  :  isNaN()**
        
        ```jsx
              console.log("5. NaN 이냐 : ", Number.isNaN(NaN)); // true
              console.log("5. NaN 이냐 : ", Number.isNaN(null)); // false
              console.log("5. NaN 이냐 : ", Number.isNaN(undefined)); // false
              console.log("5. NaN 이냐 : ", Number.isNaN("홍길동")); // false
              console.log("5. NaN 이냐 : ", Number.isNaN(10)); // false
        
        ```
        
    - **정수 여부  :  isInteger()**
        
        ```jsx
                   console.log("6. 정수인가? :  ", Number.isInteger(NaN)); //  false
              console.log("6. 정수인가? :  ", Number.isInteger(null)); //  false
              console.log("6. 정수인가? :  ", Number.isInteger(undefined)); //  false
              console.log("6. 정수인가? :  ", Number.isInteger(10)); // true
              console.log("6. 정수인가? :  ", Number.isInteger(3.14)); //  false
              console.log("6. 정수인가? :  ", Number.isInteger(-10)); // true
              console.log("6. 정수인가? :  ", Number.isInteger("10")); //  false
        ```
        
    - **문자열을 정수/실수로 변환   :  parseInt()  /   parseFloat()**
        
        ```jsx
        // "10" -> 10
              console.log("7. 문자열을 정수로 반환 : ", Number.parseInt("10") + 10); // 20
        
              // "3.14" -> 3.14
              console.log("8. 문자열을 실수로 반환 : ", Number.parseFloat("3.14") + 10); //  13.14
        ```
        

### **날짜 객체 ( Date )**

https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Date

- **`날짜 생성 및 메서드`**
    - **날짜 데이터 생성**
        
        ```jsx
          // 날짜 데이터 생성 방법
              let d = new Date(); // 객체로 반환
              let d2 = Date(); // 문자열
              let d3 = Date.now();
              console.log(d); // Thu Dec 19 2024 14:17:44 GMT+0900 (한국 표준시)
              console.log(d2); // Thu Dec 19 2024 14:17:44 GMT+0900 (한국 표준시)
              console.log(d3); // 1970/0101/00:00:00 ~ 현재시간 까지 시간을 밀리세컨즈로 반환 : 1734585505861
        ```
        
    - **toString()**
        
        ```jsx
         console.log("1. toString() : ", d.toString()); // Thu Dec 19 2024 14:23:08 GMT+0900 (한국 표준시)
              console.log("2. toDateString() : ", d.toDateString()); // Thu Dec 19 2024
              console.log("3. toISOString() : ", d.toISOString()); // 2024-12-19T05:22:57.377Z
              console.log("3. toISOString() : ", d.toISOString().slice(0, 10)); //  2024-12-19
        ```
        
    - **날짜 및 시간 데이터 얻기**
        
        ```jsx
         console.log("4. getFullYear()", d.getFullYear()); //2024
              console.log("5. getMonth() :", d.getMonth() + 1); // 12
              console.log("6. getDate() : ", d.getDate()); // 19
              console.log("7. getMinutes() : ", d.getMinutes()); // 36
        ```
        

### **Boolean 객체**

https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Boolean

```jsx
      // 불린 객체 생성 방법

      // false로 처리되는 값
      let b1 = new Boolean(0); // 객체가 나옴
      let b2 = Boolean("");
      let b3 = Boolean(null);
      let b4 = Boolean(undefined);
      let b5 = Boolean(NaN);
      console.log(b1, b1.valueOf(), b1.toString()); // Boolean {false} false 'false'
      console.log(b2, b3, b4, b5); // false false false false

      if (b1.toString()) {
        // 문자열이 들어가기에 false 아님
        console.log("AAA"); //AAA
      }

      if (b1.valueOf()) {
        // false 임
        console.log("BBB");
      }

      // true 처리되는 값
      let v = Boolean(10);
      let v2 = Boolean("aaa");
      let v3 = Boolean([]);
      let v4 = Boolean({});
      console.log(v, v2, v3, v4); // true true true true
```

### **배열 객체 ( Array )**

https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array

- 자바의 ArrayList와 유사하다.
- 배열의 크기 변경이 가능하고, 저장되는 데이터 타입 무관
- **`배열 메서드`**
    - **map 함수**
        
        : 배열 안의 요소들을 가공할 떄 사용하는 함수
        
        ```jsx
              let y = ["hello", "world", "happy"];
              let result4 = y.map((item, index, array) => {
                return item.toUpperCase();
              });
              console.log(result4);  // ['HELLO', 'WORLD', 'HAPPY']
        ```
        
    - **filter 함수**
        
        : 배열 안의 요소들 중 조건에 일치하는 값을 찾을 때 사용하는 함수
        
        ```jsx
        let x2 = [10, 11, 20, 21, 30, 31];
              let result3 = x2.filter((ele, index, array) => {
                return ele % 2 == 0; // 짝수인 값만 반환
              });
              console.log("짝수만 : ", result3); // [10, 20, 30] => 배열로 반환됨
        ```
        
    - **split 함수**
        
        : 문자열을 구분자 기준으로 나누어 배열로 반환하는 함수
        
        ```jsx
         let y3 = "hello World !!";
         console.log(y3.split(" ")); // ['hello', 'World', '!!']
        ```
        
    - **join 함수**
        
        : 배열 안의 값들을 하나의 문자열로 합치는 함수
        
        - 구분자를 지정해서 합칠 수 있다.
        
        ```jsx
        let y2 = ["hello", 2, "happy"];
        let result5 = y2.join(" "); // 구분자 공백하나 지정함
        console.log(result5); // hello 2 happy
        ```
        
    - **fill 함수**
        
        : 배열값들을 지정한 값으로 변경(채우기)하는 함수
        
        ```jsx
        let y4 = [1, 2, 3, 4, 5];
        console.log(y4.fill(100)); // [100, 100, 100, 100, 100]
        console.log(y4.fill(99, 2)); // (채울값, 시작인덱스)  [100, 100, 99, 99, 99]
        console.log(y4.fill(88, 0, 3)); // (채울값, 시작인덱스, 끝인덱스)  [88, 88, 88, 99, 99]
        ```
        
    - **Array.from()**
        
        : 배열이 아닌 것을 배열로 만들어 반환
        
        ```jsx
         console.log("8. Arrray.from() ");
              let y6 = "hello";
              console.log(Array.from(y6)); // ['h', 'e', 'l', 'l', 'o']
        
              let result6 = Array.from(y6, (s) => {
                return s.toUpperCase(); // y6 요소들을 한번씩 순회함
              });
              console.log(result6); // ['H', 'E', 'L', 'L', 'O']
        ```
        
    - **Arrray.isArray()**
        
        : 배열인지 아닌지 boolean값으로 반환
        
        ```jsx
        console.log("9. 배열인지 여부 : Arrray.isArray(배열) ");
        console.log(Array.isArray([1, 2, 3])); // true
        console.log(Array.isArray([])); // true
        console.log(Array.isArray("AAA")); // false
        ```
        
    - **spread 연산자**
        
        : `let x = [ …배열 ];`
        
        ```jsx
        let x = [10, 20, 30];
        
              // 1. 배열값 복사
              let copy_x = [...x];
              copy_x[0] = 100;
              console.log(copy_x); // [100, 20, 30]
        
              // 2. 기본배열에 값 추가
              let x2 = [10, 20, 30];
              let new_x2 = [0, ...x2, 40, 50];
              console.log(new_x2); //[0, 10, 20, 30, 40, 50]
        
              // 3. 배열 연결
              let x3 = [10, 20, 30];
              let x4 = [100, 200, 300];
              let result = [...x3, ...x4];
              console.log(result); // [10, 20, 30, 100, 200, 300]
        
              //4. 문자열 --> 배열로 변경
              console.log([..."hello"]); // ['h', 'e', 'l', 'l', 'o']
        ```
        
