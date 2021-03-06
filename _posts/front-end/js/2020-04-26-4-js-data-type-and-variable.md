---
title:  "javascript 데이터 타입과 변수"
categories: 
  - js
tags:
  - javascript
  - front-end  
date: 2021-04-26
---
## javascript 데이터 타입과 변수

### 데이터 타입
ES6에서의 자바스크립트는 7개의 데이터 타입을 제공한다.   
6개의 원시 타입과 1개의 객체 타입으로 분류할 수 있다.   

![image](https://user-images.githubusercontent.com/49264011/116070960-35ba3d80-a6c8-11eb-9cbe-d4a77d7f4387.png)   

#### 1.숫자 타입
C나 JAVA의 경우 정수,실수를 구분해서 int, long, float, double 등 다양한 숫자타입을 제공한다.   
하지만 자바스크립트에서는 숫자(number) 타입 오직 한가지만 존재한다.
ECAMScript 사양에 따르면 64비트 부동소수점 형식을 따른다고 한다.   
이는 2진수, 8진수 등을 사용하지 못 한다는 것이 아니다. 입력을 해도 별도의 처리가 없으면 실수값으로 해석되서 참조된다는 뜻이다.
추가적으로 숫자타입에서는 3가지 특별한 표현값이 존재한다.
  1. Infinity : 양의 무한대
  2. -Infinity : 음의 무한대
  3. NaN : 산술 연산 불가(not-a-number)   

   물론 원시 데이터 숫자의 작업을 위해서 **Number**라는 래퍼객체가 존재한다.
   Number에는 isInter()같은 판별 함수나 toExponential() 지수 표기변환 함수가 있다.   

#### 2.문자열 타입
문자열 타입은 텍스트 데이터를 나타내는데 사용하는 값으로, 작은 따옴표, 큰 따옴표, 백틱(`)으로 텍스트를 감싸 사용한다. 일반적으로는 작은 따옴표를 쓴다고 한다.   
```js
var str = "string"; // 큰 따옴표
str = 'string';     // 작은 따옴표
str = `string`;     // 백틱(ES6 템플릿 리터럴)
```
자바 스크립트에서 문자열 타입은 **immutable** 하다.   
무슨뜻이냐면 변경 불가능하다는 뜻이다.   
아니, 변수 선언하고 계속 다른 문자열 넣으면 바뀌는데요?   
그렇지 않다. 바뀌는 것처럼 보이는 것 뿐이다.   
```js
var str = 'Hello';
str = 'world';
```
첫번째 줄이 실행되면 메모리에 Hello라는 문자열이 생성된다.   
그리고 두번째 줄이 실행되면 Hello가 world로 바뀌는게 아니라 메모리 어딘가에 world를 가르키는 주소가 생기고 str변수는 그 주소를 가르키게 되는 것이다.
   
자바스크립트에서 문자열은 배열처럼 인덱스를 통한 접근이 가능한데, 이런 특성을 가지는 데이터를 **유사배열**이라고 한다.   
물론 이런 경우에도 str[0] = 'P' 이런식으로 변경해도 반영되지않는다.(그리고 에러도 발생하지 않는다!..)   

#### 3.불리언 타입   
불리언(boolean)타입은 논리적인 참,거짓을 나타내는 true와 false 뿐이다.   
비어있는 문자열, null, undefined, 숫자 0은 false로 간주된다.

#### 4.undefined   
선언 이후 값을 할당하지 않은 변수는 undefined 값을 가진다.   
주로 선언은 되었지만 값을 할당하지 않은 변수나 존재하지 않는 객체의 프로퍼티에 접근할 경우 undefined가 반환된다.   
여기서 c라던지 다른 언어와 다른 재미있는 점은, 예전에 c언어 등의 배열을 할당하고 실행 할 때에 만약 배열의 길이가 4인데, 배열의 5번째 값을 참조하려고 하면 온갖 에러를 뱉어내며 실행이 멈추곤 했었다.   
하지만 자바스크립트는 종종 값을 할당하지 않은 경우에도 프로그램이 돌아가는 경우가 있다.   
물론 제대로 된 결과를 내지는 않겠지만, 이는 자바스크립트 엔진이 undefined로 무조건 초기화하기 때문이다.   
그래서 만약 개발자가 값이 없음을 표현하고자 하면 null을 할당하면 된다.

#### 5.null
null은 undefined과는 다르게 개발자가 의도적으로 변수에 값이 없음을 명시할때 사용된다.   
참고로 null은 typeof연산자로 연산하면 object, 객체라고 나온다. 따라서 일치 연산자인 ===을 사용해서 확인해줘야한다.   
#### 6.symbol   
심볼은 ES6에서 추가된 immutable한 원시 타입 값이다.   
주로 이름의 충돌 위험이 없는 객체의 유일키를 만들때 사용된다고 한다.   
Symbol 함수를 호출해서 생성하며, 이때 생성된 심볼 값은 다른 심볼값들과 다른 **유일한**심볼값이다.   
#### 7.객체 타입   
객체는 데이터와 그 데이터에 관련한 동작을 모두 포함할 수 있는 개념적 존재다.   
이름과 값을 가지는 프로퍼티, 그리고 동작에 관련된 메소드를 모두 포함할 수 있는 독립적 주체다.   
자바스크립트는 **객체**기반의 스크립트 언어로, 사실 자바스크립트를 이루고 있는 거의 모든것이 객체다. 원시 타입을 제외한 모든 배열, 함수 등 모든것이 객체이며, 객체는 **참조에 의한 전달**방식으로 전달된다.

##### *참조에 의한 전달(call by reference)이란?
언어에서 데이터를 전달하는 방법에는 '값에 의한 전달(call by value)'와 '참조에 의한 전달(call by reference)'로 크게 두가지 방법이 있다.   
먼저 값에 의한 전달은 인수로 전달되는 변수가 가지고 있는 값을 함수내의 매개변수에 복사하는 방식이다.   
무슨 말이냐 하면, a라는 변수의 값이 6이고 이걸 ten(a)이라는 함수에 넣을때 ten(a)은 a+10을 반환하는 함수라고 해보자. 그러면 ten(a)를 실행하게되면 우리는 16이라는 값을 얻게 된다. 하지만 그렇다고해서 a의 값이 16이 되는것은 아니다. a값은 여전히 6이다. 이렇게 값을 복사해서 완전히 넘겨 별개의 변수가 되어 기존의 변수에 영향을 미치지 않는 전달을 값에 의한 전달이라고 한다.   
   
   그러면 참조에 의한 전달은 무엇일까. 매개인수로 변수의 값을 전달하는게 아니라 해당 변수의 **주소값**을 전달하는 방식이다. 즉 매개변수로 전달된 값의 오리지널 주소값을 저장해서 불러와 사용하는것이다.   
   참조에 의한 전달방식으로 위의 행위를 똑같이 실행하게되면 ten(&a)는 16을 반환 할 것이고, a의 값도 16으로 변경되어있을 것이다.   

   이것이 값에 의한 전달과 참조에 의한 전달의 차이다.   

   
### 변수   
변수는 프로그램에서 데이터를 일정 기간동안 기억하며 사용할 때 각 데이터에 고유한 이름인 식별자를 명시한 것이다.   
자바스크립트에서 변수는 var, let, const 3가지 키워드를 사용해 선언하고 할당한다.   
뭐 다른언어에서 그러듯 자바스크립트에도 명명 규칙이 존재한다.   
하지면 여기서는 그런 일반적인 부분을 제외하고 자바스크립트의 특징을 써보려고 한다.   
ES5이전의 자바스크립트는 변수 선언이 var키워드로 이루어졌다.   
##### 1. 선언하고 값을 할당하지 않은 변수는 엔진에 의해 자동으로 undefined를 초기값으로 갖는다.   
##### 2. var을 통한 변수는 중복선언이 가능하다.   
##### 3. 동적타이핑, 자바스크립트는 변수의 타입지정을 별도로 하지않는다.   
값이 할당되는 과정에서 값을 판단하여 자동으로 타입이 결정된다.   
**즉, 같은 변수에 여러가지 타입을 할당할 수 있다.**
```js
   var foo;

   console.log(typeof foo);  // undefined

   foo = null;
   console.log(typeof foo);  // object

   foo = {};
   console.log(typeof foo);  // object

   foo = 3;
   console.log(typeof foo);  // number

   foo = 3.14;
   console.log(typeof foo);  // number

   foo = 'Hi';
   console.log(typeof foo);  // string

   foo = true;
   console.log(typeof foo);  // boolean
```   
##### 4.변수 호이스팅   
자바스크립트의 모든 선언문은 호이스팅된다.   
**호이스팅이란?**
var, function등 모든 선언문이 해당 Scope의 선두로 옮겨진 것처럼 동작하는 특성을 말한다.   
예전에 c언어에서 순차지향적인 언어의 실행에 있어서 main함수보다 다른 함수를 아래에 두려면 main함수 윗부분에 해당 함수의 선언을 해놔야 에러가 생기지 않는다는 것을 배웠었다. 그런데 이 자바스크립트라는 녀석은 이 행위가 해당 scope범위에서 맨위에 미리 선언을 해둔 것처럼 작동한다. 이것이 호이스팅이다.
```js
console.log(foo); // ① undefined
var foo = 123;
console.log(foo); // ② 123
{
  var foo = 456;
}
console.log(foo); // ③ 456
```

위의 예시를 통해 볼 수 있듯이, 1에서 변수 foo가 선언되지 않았지만 중단되지않고 undefined가 출력된다.. ??아니, 대체 선언한적도 없는데 어디서 선언은 됬단말인가? 바로 다음줄의 'var foo = 123;'에서다.   
변수는 **선언->초기화->할당**의 단계를 거치는 데, var로 선언된 변수는 선언과 초기화가 한번에 이루어진다. 변수가 등록되면서 동시에 메모리를 차지하고 undefined로 초기화가 된다.   
따라서 변수선언문 이전에 변수를 참조해도 undefined로 존재하고 있기때문에 에러를 발생하지 않고 undefined를 반환한다. 이런 현상을 호이스팅이라고 한다.   
   
이런 문제는 자바스크립트는 C계열 언어와 다르게 **블록 레벨 스코프(block-level scope)** 를 가지지 않고 **함수 레벨 스코프(function-level scope)** 를 갖기 때문이다.   
물론 ES6로 넘어오면서 let, const등의 키워드가 도입되서 블록 레벨의 스코프를 사용할 수 있게되었다..   
```md
- 함수 레벨 스코프(Function-level scope)
함수 내에서 선언된 변수는 함수 내에서만 유효하며 함수 외부에서는 참조할 수 없다. 즉, 함수 내부에서 선언한 변수는 지역 변수이며 함수 외부에서 선언한 변수는 모두 전역 변수이다.
- 블록 레벨 스코프(Block-level scope)
코드 블록 내에서 선언된 변수는 코드 블록 내에서만 유효하며 코드 블록 외부에서는 참조할 수 없다.
```
단순하게 미리 선언과 초기화만 이루어지면 다행인데, 문제는 이러한 함수레벨의 스코프때문에 변수들이 전역화 된다는 문제가 생긴다.   
for loop 반복문의 초기화식에서 사용한 변수를 반복문 외부나 전역에서 참조할 수 있다.   
그리고 중복선언이나 의도하지않은 변수의 전역화 등 여러가지 문제가 발생한다.
이런 특성들로 인한 사이드 이펙트 문제가 많아서 ES6부터는 let과 const가 도입되었다고 한다. [let과const](../1-js-let-and-const/)
