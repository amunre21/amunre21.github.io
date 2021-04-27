---
title:  "javascript let과 const"
categories: 
  - js
tags:
  - javascript
  - front-end  
date: 2021-04-26
---
## javascript let과 const

ES5까지 변수를 선언하는 유일한 방법은 var키워드였고, var은 함수 레벨 스코프여서 변수의 전역화 및 호이스팅 문제 등이 있었다.   
전역화된 변수는 어디서 사용되고 사이드 이펙트를 일으킬지 모르기 때문에...   
ES6에서는 var의 단점을 보완하기위해 let과 const가 도입되었다.   
### 1. let   
##### 1.1 let은 함수 레벨 스코프가 아닌 블록 레벨 스코프를 따른다.   
```md
- 함수 레벨 스코프(Function-level scope)
함수 내에서 선언된 변수는 함수 내에서만 유효하며 함수 외부에서는 참조할 수 없다. 즉, 함수 내부에서 선언한 변수는 지역 변수이며 함수 외부에서 선언한 변수는 모두 전역 변수이다.
- 블록 레벨 스코프(Block-level scope)
코드 블록 내에서 선언된 변수는 코드 블록 내에서만 유효하며 코드 블록 외부에서는 참조할 수 없다.(ex. function, if, for, while...)
```   
```js
var foo = 123; // 전역 변수
console.log(foo); // 123
{
  var foo = 456; // 전역 변수
}
console.log(foo); // 456
```
```js
let foo = 123; // 전역 변수
{
  let foo = 456; // 지역 변수
  let bar = 456; // 지역 변수
}
console.log(foo); // 123
console.log(bar); // ReferenceError: bar is not defined
```   
위와 아래는 각각 var과 let을 활용한 변수 선언 및 값 할당에 따른 결과다.   
var의 경우에는 함수 레벨 스코프를 따르기때문에 foo가 456의 값을 가지게 되었지만,   
let의 경우에는 foo가 블록내에서 456으로 값이 지정되었음에도 불구하고 블록을 나와서 출력되었기 때문에 이전에 선언한 foo = 123의 값이 나타나게 되었다. 그리고 bar는 선언되지 않은 변수 취급을 받았다.   
##### 1.2 변수 중복 선언 금지   
var에서는 동일한 이름의 변수를 중복해서 선언할 수 있다고 했다. 하지만 let은 동일한 이름의 변수는 중복선언 할 수 없으며, 선언시 문법에러가 발생하게 된다.   
```js
var foo = 123;
var foo = 456;  // 중복 선언 허용

let bar = 123;
let bar = 456;  // Uncaught SyntaxError: Identifier 'bar' has already been declared
```   
##### 1.3 호이스팅   
[데이터타입과 변수](../4-js-data-type-and-variable/#4변수-호이스팅) 에서도 설명했듯이, 자바스크립트의 모든 선언문은 호이스팅된다.   
즉 선언을 어딘가에 해두면 선언 이전에 해당 변수를 참조하더라 해도 undefined로 생각하고 에러가 발생하지 않는 것이다.   
하지만 let은 이러한 호이스팅이 발생하지 않는 것처럼 **'동작'** 한다.   
```js
console.log(bar); // Error: Uncaught ReferenceError: bar is not defined
let bar;
```   
위에 링크로 걸어놓은 내용에서도 설명했듯이, 변수는 **선언-초기화-할당**의 3단계를 거친다.   
<img src = "https://user-images.githubusercontent.com/49264011/116253226-3ed00b00-a7ab-11eb-9f07-2e83e289ed17.png" width="600px">   
var의 경우에는 이렇게 선언과 초기화가 동시에 이루어져서 선언 단계에서 스코프에 해당 변수 식별자를 등록하면서 자바스크립트 엔진이 undefined로 변수 초기화도 시켜준다.   
이러면 실제 코드상에서 선언부분 이전에 변수를 참조해도 에러가 발생하지는 않는것이다.   
   
   <img src = "https://user-images.githubusercontent.com/49264011/116253698-a5edbf80-a7ab-11eb-9d70-3a4c38851438.png" width="600px">   
   
let의 경우에는 선언 단계와 초기화 단계를 분리해서 진행한다.   
런타임 이전에 자바스크립트 엔진에 의해 암묵적으로 선언단계가 먼저 실행은 되지만 그 이후에는 초기화 지점(변수 선언부)까지 일시적 사각지대(TDZ)에 놓여 초기화는 이뤄지지 않는다.   
따라서 만약 변수선언 이전에 참조하려고 하면 참조 에러가 뜰 것이다.   
```js
let foo = 1; // 전역 변수
{
  console.log(foo); // ReferenceError: foo is not defined
  let foo = 2; // 지역 변수
}
```   
이렇게 말이다.   

##### 1.4 전역 객체로서의 let   
var과는 다르게 전역변수로 선언한 let 은 **전역객체**의 프로퍼티로 참조할 수 없다.   
전역객체란 window 를 말한다.
```js
let foo = 123; // 전역변수
console.log(window.foo); // undefined

```   
이렇게 let 변수는 전역객체의 프로퍼티로는 참조가 불가능하다.   
위에서 말 했듯이, 함수 레벨스코프가 아닌 블록 레벨 스코프가 적용되있기 때문에 보이지 않지만 존재하는 개념적인 블록 내에 존재하게 된다.   

### 2. const  
const도 let과 동일하게 블록 레벨 스코프를 갖는다.    

##### 2.1 const의 선언   
```js
const FOO = 123;
FOO = 456; // TypeError: Assignment to constant variable.
```   
const는 let과 다르게 선언과 동시에 할당을 해줘야한다. 그렇지 않으면 문법 에러가 발생한다.   
그리고 재할당이 가능한 let에 비해 const는 재할당이 금지된다.   
```js
const obj = { foo: 123 };
obj = { bar: 456 }; // TypeError: Assignment to constant variable.
```   
객체도 마찬가지로 금지된다.   

##### 2.2 상수   
const는 블록 범위의 상수다.   
상수는 주로 가독성과 유지보수의 편의를 위해 사용되는 편이다.   
```js
// 10이 뭘 의미하는지 최초 개발자만 알 수 있다..
if (rows > 10) {
}

// 고정된 값을 상수로 두어 가독성이 좋고 유지보수에 용이하다.
const MAXROWS = 10;
if (rows > MAXROWS) {
}
```   
이런식으로 사용된다.   

##### 2.3 const의 객체   
앞서 const의 객체도 재할당이 금지된다고 서술했다.   
하지만 const의 객체의 **프로퍼티**는 추가,삭제 및 변경을 할 수 있다.   
```js
const user = { name: 'Lee' };

// const 변수는 재할당이 금지된다.
// user = {}; // TypeError: Assignment to constant variable.

// 객체의 내용은 변경할 수 있다.
user.name = 'Kim';

console.log(user); // { name: 'Kim' }
```   
이렇게 가능하다.   
따라서 객체 타입 변수 선언에는 가급적 const를 사용하는 것이 좋다.   
만약 명시적으로 객체 타입 변수의 주소값을 변경해야하는 경우라면 let을 사용해야 한다.   

### 3. var vs. let vs. const   
그러면 어떤경우에 var, let 그리고 const를 써야할까?   
- 일단, ES6 이후 버전을 사용하고 있다면 var은 사용하지 않는 것이 좋다.
- 재할당이 필요한 변수의 경우에만 let을 사용한다.   
- 변경이 필요없는 원시 값과 객체는 const키워드를 사용한다.   
차후에 변경이 필요하게 되면 그때 const를 let으로 변경해도 되므로 일단 const 사용을 지향한다.   
   
