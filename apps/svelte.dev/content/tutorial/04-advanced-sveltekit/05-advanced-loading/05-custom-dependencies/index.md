---
title: 커스텀 의존성
path: /Europe/London
---

`load` 함수 안에서 `fetch(url)`을 호출하면 `url`이 의존성으로 등록돼요. 때로는 `fetch`를 사용하는 게 적절하지 않은데, 그런 경우 [`depends(url)`](/docs/kit/load#Rerunning-load-functions-Manual-invalidation) 함수로 수동으로 의존성을 지정할 수 있어요.

`[a-z]+:` 패턴으로 시작하는 모든 문자열은 유효한 URL이기 때문에, `data:now` 같은 커스텀 무효화 키를 만들 수 있어요.

`src/routes/+layout.js`를 업데이트해서 `fetch` 호출을 하는 대신 값을 직접 반환하고, `depends`를 추가하세요:

```js
/// file: src/routes/+layout.js
export async function load({ +++depends+++ }) {
	+++depends('data:now');+++

	return {
		now: +++Date.now()+++
	};
}
```

이제 `src/routes/[...timezone]/+page.svelte`의 `invalidate` 호출을 업데이트하세요:

```svelte
/// file: src/routes/[...timezone]/+page.svelte
<script>
	import { onMount } from 'svelte';
	import { invalidate } from '$app/navigation';

	let { data } = $props();

	onMount(() => {
		const interval = setInterval(() => {
			invalidate(+++'data:now'+++);
		}, 1000);

		return () => {
			clearInterval(interval);
		};
	});
</script>
```
