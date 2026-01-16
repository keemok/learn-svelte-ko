---
title: 상태(State)
---

Svelte의 핵심은 강력한 반응성(reactivity) 시스템이에요. 이걸로 애플리케이션의 상태(state)와 DOM을 동기화할 수 있어요. 예를 들어 이벤트에 반응해서 화면을 업데이트하는 식이죠.

`count` 선언을 `$state(...)`로 감싸서 반응형으로 만들어봐요:

```js
/// file: App.svelte
let count = +++$state(0)+++;
```

이걸 룬(rune)이라고 불러요. Svelte에게 `count`가 일반 변수가 아니라고 알려주는 거예요. 룬은 함수처럼 보이지만 함수가 아니에요. Svelte를 쓸 때는 언어의 일부분이 돼요.

이제 `increment` 함수만 구현하면 끝이에요:

```js
/// file: App.svelte
function increment() {
	+++count += 1;+++
}
```
