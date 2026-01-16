---
title: 파생 상태(Derived state)
---

다른 상태로부터 새로운 상태를 파생(derive)해야 할 때가 많아요. 이럴 때 `$derived` 룬을 쓰면 돼요:

```js
/// file: App.svelte
let numbers = $state([1, 2, 3, 4]);
+++let total = $derived(numbers.reduce((t, n) => t + n, 0));+++
```

이제 마크업에서 이걸 쓸 수 있어요:

```svelte
/// file: App.svelte
<p>{numbers.join(' + ')} = +++{total}+++</p>
```

`$derived` 선언 안의 표현식은 의존하고 있는 값(여기서는 `numbers`)이 업데이트될 때마다 다시 계산돼요.
