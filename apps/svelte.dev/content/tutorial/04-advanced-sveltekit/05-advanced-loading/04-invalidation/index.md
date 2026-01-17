---
title: 무효화
path: /Europe/London
---

사용자가 한 페이지에서 다른 페이지로 탐색할 때, SvelteKit은 뭔가 변경됐다고 생각하는 경우에만 `load` 함수를 호출해요.

이 예제에서 타임존 간 탐색은 `params.timezone`이 무효하기 때문에 `src/routes/[...timezone]/+page.js`의 `load` 함수가 다시 실행되게 해요. 하지만 `src/routes/+layout.js`의 `load` 함수는 다시 실행되지 않아요. SvelteKit이 관련된 한 탐색에 의해 무효화되지 않았거든요.

URL을 받아서 그것에 의존하는 모든 `load` 함수를 다시 실행하는 [`invalidate(...)`](/docs/kit/$app-navigation#invalidate) 함수를 사용해서 수동으로 무효화함으로써 고칠 수 있어요. `src/routes/+layout.js`의 `load` 함수가 `fetch('/api/now')`를 호출하기 때문에, `/api/now`에 의존해요.

`src/routes/[...timezone]/+page.svelte`에서 1초에 한 번 `invalidate('/api/now')`를 호출하는 `onMount` 콜백을 추가하세요:

```svelte
/// file: src/routes/[...timezone]/+page.svelte
<script>
	+++import { onMount } from 'svelte';+++
	+++import { invalidate } from '$app/navigation';+++

	let { data } = $props();

+++	onMount(() => {
		const interval = setInterval(() => {
			invalidate('/api/now');
		}, 1000);

		return () => {
			clearInterval(interval);
		};
	});+++
</script>

<h1>
	{new Intl.DateTimeFormat([], {
		timeStyle: 'full',
		timeZone: data.timezone
	}).format(new Date(data.now))}
</h1>
```

> [!NOTE] 특정 URL이 아닌 패턴에 기반해서 무효화하고 싶은 경우, `invalidate`에 함수를 전달할 수도 있어요.
