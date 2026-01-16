---
title: 상태 검사하기
---

상태 값이 시간에 따라 어떻게 변하는지 추적할 수 있으면 유용해요.

`addNumber` 함수 안에 `console.log` 문을 추가했어요. 하지만 버튼을 클릭하고 콘솔 창을 열어보면(URL 바 오른쪽 버튼 사용) 경고와 함께 메시지를 복제할 수 없다는 메시지가 나타나요.

그 이유는 `numbers`가 반응형 [프록시(proxy)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy)이기 때문이에요. 몇 가지 방법이 있어요. 먼저 `$state.snapshot(...)`으로 상태의 비반응형 스냅샷을 만들 수 있어요:

```js
/// file: App.svelte
function addNumber() {
	numbers.push(numbers.length + 1);
	console.log(+++$state.snapshot(numbers)+++);
}
```

또는 `$inspect` 룬을 써서 상태가 변경될 때마다 자동으로 스냅샷을 로그로 남길 수 있어요. 이 코드는 프로덕션 빌드에서 자동으로 제거돼요:

```js
/// file: App.svelte
function addNumber() {
	numbers.push(numbers.length + 1);
	---console.log($state.snapshot(numbers));---
}

+++$inspect(numbers);+++
```

`$inspect(...).with(fn)`을 써서 정보가 표시되는 방식을 커스터마이즈할 수도 있어요. 예를 들어 `console.trace`를 쓰면 상태 변경이 어디서 시작됐는지 볼 수 있어요:

```js
/// file: App.svelte
$inspect(numbers)+++.with(console.trace)+++;
```
