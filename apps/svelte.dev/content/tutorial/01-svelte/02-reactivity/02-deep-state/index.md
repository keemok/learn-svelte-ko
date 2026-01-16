---
title: 깊은 상태(Deep state)
---

이전 실습에서 본 것처럼, 상태는 재할당(reassignment)에 반응해요. 하지만 변경(mutation)에도 반응해요. 이걸 깊은 반응성(deep reactivity)이라고 불러요.

`numbers`를 반응형 배열로 만들어봐요:

```js
/// file: App.svelte
let numbers = +++$state([1, 2, 3, 4])+++;
```

이제 배열을 변경하면...

```js
/// file: App.svelte
function addNumber() {
	+++numbers[numbers.length] = numbers.length + 1;+++
}
```

...컴포넌트가 업데이트돼요. 또는 더 좋은 방법으로 배열에 `push`를 쓸 수도 있어요:

```js
/// file: App.svelte
function addNumber() {
	+++numbers.push(numbers.length + 1);+++
}
```

> [!NOTE] 깊은 반응성은 [프록시(Proxy)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy)를 사용해서 구현돼요. 프록시에 대한 변경은 원본 객체에 영향을 주지 않아요.
