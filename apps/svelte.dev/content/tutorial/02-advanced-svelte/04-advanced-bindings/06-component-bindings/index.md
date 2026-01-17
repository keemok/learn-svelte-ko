---
title: 컴포넌트 바인딩
---

DOM 요소의 속성에 바인딩할 수 있는 것처럼, 컴포넌트 props에도 바인딩할 수 있어요. 예를 들어, 이 `<Keypad>` 컴포넌트의 `value` prop에 폼 요소인 것처럼 바인딩할 수 있어요.

먼저, prop을 바인딩 가능(bindable)하다고 표시해야 해요. `Keypad.svelte` 안에서 `$props()` 선언을 업데이트해서 `$bindable` 룬을 사용하세요:

```js
/// file: Keypad.svelte
let { value +++= $bindable('')+++, onsubmit } = $props();
```

그다음 `App.svelte`에서 `bind:` 디렉티브를 추가하세요:

```svelte
/// file: App.svelte
<Keypad +++bind:value={pin}+++ {onsubmit} />
```

이제 사용자가 키패드와 상호작용하면, 부모 컴포넌트의 `pin` 값이 즉시 업데이트돼요.

> [!NOTE] 컴포넌트 바인딩은 아껴서 쓰세요. 너무 많이 사용하면 애플리케이션의 데이터 흐름을 추적하기 어려울 수 있어요. 특히 '단일 진실 공급원(single source of truth)'이 없는 경우에 그래요.
