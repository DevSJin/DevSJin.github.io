---
title:  "[JavaScript] parseInt()와 Number()의 차이"
permalink: /categories/js/parseIntvsNumber
author_profile: true
categories:
  - 자바스크립트
tags:
  - 직무면접
  - 자바스크립트
toc: true
toc_label: "목차"
toc_icon: "bookmark"
last_modified_at: 2023-02-01
toc_sticky: true
---

​	최근 JS로 알고리즘 문제를 풀다가 문자열을 숫자로 변경할 경우가 생기면 parseInt나 Number중 그때그때 끌리는 것을 번갈아가면서 썼다. 그러다가 문득 이 두가지의 차이점은 무엇일까? 라는 생각이 들어 직접 콘솔을 찍어보면서 발생하는 차이점들을 글로 정리해 보겠다.



##### 1. 일반적인 수로 이루어진 문자열과 앞이 0으로 반복되는 경우

```js
let strNum1 = '1234'
let strNum2 = '00001234'

console.log(parseInt(strNum1)) // 1234
console.log(Number(strNum1)) // 1234

console.log(parseInt(strNum2)) // 1234
console.log(Number(strNum2)) // 1234

//위의 경우 모두 숫자로 잘 변환되는 것을 볼 수 있다.
```



##### 2. 숫자 + 문자열로 이루어진 경우

```js
let strNum1 = '1994년생'

console.log(parseInt(strNum1)) // 1994
console.log(Number(strNum1)) // NaN
```

parseInt()의 경우, 해당 문자열에서 정수만 파싱해서 보여주는 반면, Number는 NaN로 나오는 것을 볼 수 있었다. 



##### 3. 문자열 + 숫자는?

```js
let strNum1 = '넘버7'
let strNum2 = '넘버7넘버'
let strNum3 = '7.7넘버7넘버'

console.log(parseInt(strNum1)) // NaN
console.log(Number(strNum1)) // NaN

console.log(parseInt(strNum2)) // NaN
console.log(Number(strNum2)) // NaN

console.log(parseInt(strNum3)) // 7
console.log(Number(strNum3)) // NaN
```

parseInt도 진짜 문자 사이에 있는 숫자까지는 파싱해주지 못했고, 앞부분이 소수일 경우에는 정수만 파싱해주었다.



##### 4. 소수점은?

```js
let strNum1 = '123.456789'

console.log(parseInt(strNum1)) // 123
console.log(Number(strNum1)) // 123.456789
```

당연한 얘기겠지만 parseInt()는 정수부분만을 파싱해서 보여줬다. Number은 숫자 모든 숫자타입을 포함하기 때문에 소수까지 파싱해주었다.



위 실험을 정리해보면,

`parseInt()`는 문자열 안에서 숫자가 먼저 시작될 경우, 해당 숫자(물론 정수로)를 다 파싱해줄 수 있고

`Number()`은 **문자열 전체가 숫자일때만** 소수점까지 숫자타입으로 가져올 수 있다는것이다.

사실 알고리즘 문제에서는 두가지를 크게 구분할 필요까진 없을 것 같지만, 개인적인 호기심에 몇가지 실험을 진행해 보았다. 앞으로 개발하면서 꾸준히 사용하다 보면 더 잘 구분할 수 있을 것이라 생각한다.
