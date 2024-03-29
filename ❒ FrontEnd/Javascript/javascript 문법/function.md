---
tags:
  - javascript
---
# 함수


## 함수 선언식 vs 함수 표현식

```jsx
<--- 함수 선언문 --->
function hello() {
 ///함수내용
} 

<--- 함수 표현식 --->
let hello = function () {
	///함수내용
} 
```

- 가급적 ‘함수 선언문’ 방식으로 쓰기
    - 가독성 good
    - 함수 선언하기 전에도 함수 활용 가능
    - 훨씬 유연한 형태로 사용 가능


## 함수 명시 방법 3가지 

```jsx
function a() {}   //1
const a = function () {}  //2
const a = () => {}    //3 이걸 요즘 제일 많이 쓴다구 한당.... 
```

    

### 화살표 함수 

```jsx
// 화살표(=>) 우측엔 표현식이 있음
let sum = (a, b) => a + b;

// 대괄호{ ... }를 사용하면 본문에 여러 줄의 코드를 작성할 수 있음. return문이 꼭 있어야 함.
let sum = (a, b) => {
  // ...
  return a + b;
}

// 인수가 없는 경우
let sayHi = () => alert("Hello");

// 인수가 하나인 경우
let double = n => n * 2;
```

 ** 주의점 

- 함수가 한줄이면 중괄호를 생략하는 습관을 들이자