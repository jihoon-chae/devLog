바벨공식 사이트

[https://babeljs.io/](https://babeljs.io/)

바벨

→ 브라우저가 호환가능한 자바스크립트로 변환해준다!

[ES6 Modules 문법 소개 글](https://joshua1988.github.io/es6-online-book/modules.html)

## **import & export 기본 문법**

모듈화 기능을 사용하기 위한 기본적인 import, export 문법을 보겠습니다.

먼저 export 문법입니다.

```jsx
export 변수, 함수
```

다른 파일에서 가져다 쓸 변수나 함수의 앞에 `export` 라는 키워드를 붙입니다. 익스포트된 파일은 임포트로 불러와 사용할 수 있습니다.

import 문법을 보겠습니다.

```jsx
import { 불러올 변수 또는 함수 이름 } from '파일 경로';
```

익스포트된 변수나 함수를 `{}`에 선언한 뒤 해당 파일이 있는 경로를 적어줍니다.

## ****import & export 기본 예제****

배운 문법을 바탕으로 간단한 예제를 살펴보겠습니다.

```jsx
// math.js
export var pi = 3.14;
```

```jsx
// app.js
import { pi } from './math.js';

console.log(pi); // 3.14
```

위 코드는 `math.js`라는 파일에서 `pi`를 익스포트하고 `app.js` 파일에서 임포트하여 콘솔에 출력하는 코드입니다. 만약 변수가 아니라 함수를 내보내고 싶다면 아래와 같이 코딩할 수 있습니다.

```jsx
// math.js
export var pi = 3.14;
export function sum(a, b) {
  return a + b;
}

```

```jsx
// app.js
import { sum } from './math.js';

sum(10, 20); // 30
```

위 코드는 `math.js`에 두 숫자의 합을 구하는 `sum()` 함수를 익스포트 한 뒤 `app.js`에서 임포트하여 사용한 코드입니다.

## ES6 modules 실습

[실습 폴더 주소](https://github.com/joshua1988/LearnWebpack/tree/master/es6-modules)

네트워크 탭에서 확인해 보면 index.html과 main.bundle.js 이 두 파일만 전달됨(웹소켓은 제외하고)

```jsx
// index.html
...
<script src="build/main.bundle.js"></script>
```

![스크린샷 2022-10-18 오후 6.48.33.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f39ebb36-9268-4f2c-b5a5-e27ed93b70f0/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-10-18_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_6.48.33.png)

네트워크 탭에서 main.bundle.js를 들어가 보면 아래처럼 난독화 되어있음

```jsx
!function(e){var t={};function r(n){if(t[n])return t[n].exports;var o=t[n]={i:n,l:!1,exports:{}};return e[n].call(o.exports,o,o.exports,r),o.l=!0,o.exports}r.m=e,r.c=t,r.d=function(e,t,n){r.o(e,t)||Object.defineProperty(e,t,{enumerable:!0,get:n})},r.r=function(e){"undefined"!=typeof Symbol&&Symbol.toStringTag&&Object.defineProperty(e,Symbol.toStringTag,{value:"Module"}),Object.defineProperty(e,"__esModule",{value:!0})},r.t=function(e,t){if(1&t&&(e=r(e)),8&t)return e;if(4&t&&"object"==typeof e&&e&&e.__esModule)return e;var n=Object.create(null);if(r.r(n),Object.defineProperty(n,"default",{enumerable:!0,value:e}),2&t&&"string"!=typeof e)for(var o in e)r.d(n,o,function(t){return e[t]}.bind(null,o));return n},r.n=function(e){var t=e&&e.__esModule?function(){return e.default}:function(){return e};return r.d(t,"a",t),t},r.o=function(e,t){return Object.prototype.hasOwnProperty.call(e,t)},r.p="",r(r.s=0)}([function(e,t,r){"use strict";r.r(t),console.log("10 + 20 = ",10+20)}]);
//# sourceMappingURL=main.bundle.js.map
```

sourcemap → 빌드한 결과물과 빌드되기전 결과물을 연결해줌
