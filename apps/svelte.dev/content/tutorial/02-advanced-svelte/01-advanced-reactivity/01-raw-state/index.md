---
title: Raw 상태
---

이전 실습에서 상태가 [깊은 반응성(deeply reactive)](deep-state)을 가진다는 걸 배웠어요. 예를 들어 객체의 속성을 변경하거나 배열에 push하면 UI가 업데이트되죠. 이건 읽기와 쓰기를 가로채는 [프록시(proxy)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy)를 생성해서 작동해요.

가끔은 그게 원하는 게 아닐 때가 있어요. 개별 속성을 변경하지 않거나, 참조 동등성(referential equality)을 유지하는 게 중요하다면, 대신 raw 상태를 쓸 수 있어요.

이 예제에서는 Svelte의 꾸준히 상승하는 주가 차트가 있어요. 새 데이터가 들어올 때 차트가 업데이트되길 원하는데, `data`를 상태로 만들어서 달성할 수 있어요...

```js
/// file: App.svelte
let data = +++$state(poll())+++;
```

...하지만 몇 밀리초 후에 버려질 거라면 깊은 반응성을 만들 필요가 없어요. 대신 `$state.raw`를 쓰세요:

```js
/// file: App.svelte
let data = +++$state.raw(poll())+++;
```

> [!NOTE] Raw 상태를 변경해도 직접적인 효과가 없어요. 일반적으로 비반응형 상태를 변경하는 건 강력히 권장되지 않아요.
