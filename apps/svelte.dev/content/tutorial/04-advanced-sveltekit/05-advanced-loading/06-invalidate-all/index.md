---
title: invalidateAll
path: /Europe/London
---

마지막으로 핵 옵션이 있어요. `invalidateAll()`이에요. 이것은 무엇에 의존하는지와 관계없이 현재 페이지의 모든 `load` 함수를 무차별적으로 다시 실행해요.

이전 실습의 `src/routes/[...timezone]/+page.svelte`를 업데이트하세요:

```svelte
/// file: src/routes/[...timezone]/+page.svelte
<script>
	import { onMount } from 'svelte';
	import { +++invalidateAll+++ } from '$app/navigation';

	let { data } = $props();

	onMount(() => {
		const interval = setInterval(() => {
			+++invalidateAll();+++
		}, 1000);

		return () => {
			clearInterval(interval);
		};
	});
</script>
```

`src/routes/+layout.js`의 `depends` 호출은 더 이상 필요하지 않아요:

```js
/// file: src/routes/+layout.js
export async function load(---{ depends }---) {
	---depends('data:now');---

	return {
		now: Date.now()
	};
}
```

> [!NOTE] `invalidate(() => true)`와 `invalidateAll`은 같지 않아요. `invalidateAll`은 `url` 의존성이 없는 `load` 함수도 다시 실행하는데, `invalidate(() => true)`는 그렇지 않아요.
