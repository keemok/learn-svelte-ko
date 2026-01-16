---
title: 반응형 내장 객체
---

Svelte는 JavaScript 내장 객체 대신 사용할 수 있는 여러 반응형 클래스를 제공해요. `Map`, `Set`, `Date`, `URL`, `URLSearchParams` 같은 거죠.

이 실습에서 `$state(new Date())`를 써서 `date`를 선언하고 `setInterval` 안에서 재할당할 수도 있어요. 하지만 더 좋은 방법은 [`svelte/reactivity`](/docs/svelte/svelte-reactivity)의 `SvelteDate`를 쓰는 거예요:

```svelte
/// file: App.svelte
<script>
	+++import { SvelteDate } from 'svelte/reactivity';+++

	let date = new +++SvelteDate();+++

	// ...
</script>
```
