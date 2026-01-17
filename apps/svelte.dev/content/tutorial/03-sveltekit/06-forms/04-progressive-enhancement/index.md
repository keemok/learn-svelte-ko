---
title: 점진적 향상
---

`<form>`을 사용하고 있기 때문에, 사용자가 JavaScript를 가지고 있지 않아도 앱이 작동해요 ([여러분이 생각하는 것보다 더 자주 일어나요](https://kryogenix.org/code/browser/everyonehasjs.html)). 그건 좋은 일이에요. 앱이 탄력적이라는 의미거든요.

대부분의 경우 사용자는 JavaScript를 가지고 있어요. 그런 경우 SvelteKit이 클라이언트 사이드 라우팅을 사용해서 `<a>` 요소를 점진적으로 향상시키는 것처럼 경험을 점진적으로 향상시킬 수 있어요.

`$app/forms`에서 `enhance` 함수를 import하세요...

```svelte
/// file: src/routes/+page.svelte
<script>
	+++import { enhance } from '$app/forms';+++

	let { data, form } = $props();
</script>
```

...그리고 `<form>` 요소에 `use:enhance` 디렉티브를 추가하세요:

```svelte
/// file: src/routes/+page.svelte
<form method="POST" action="?/create" +++use:enhance+++>
```

```svelte
/// file: src/routes/+page.svelte
<form method="POST" action="?/delete" +++use:enhance+++>
```

그게 전부예요! 이제 JavaScript가 활성화되면 `use:enhance`가 전체 페이지 새로고침을 제외하고 브라우저 네이티브 동작을 에뮬레이트해요. 다음을 수행해요:

- `form` prop 업데이트
- 성공 응답 시 모든 데이터 무효화해서 `load` 함수가 다시 실행되게 함
- 리다이렉트 응답 시 새 페이지로 이동
- 에러 발생 시 가장 가까운 에러 페이지 렌더링

이제 페이지를 새로고침하는 대신 업데이트하기 때문에, 트랜지션 같은 것들로 멋지게 꾸밀 수 있어요:

```svelte
/// file: src/routes/+page.svelte
<script>
	+++import { fly, slide } from 'svelte/transition';+++
	import { enhance } from '$app/forms';

	let { data, form } = $props();
</script>
```

```svelte
/// file: src/routes/+page.svelte
<li +++in:fly={{ y: 20 }} out:slide+++>...</li>
```
