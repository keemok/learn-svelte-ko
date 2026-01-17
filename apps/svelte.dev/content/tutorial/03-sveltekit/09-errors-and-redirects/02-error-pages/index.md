---
title: 에러 페이지
---

`load` 함수 안에서 뭔가 잘못되면, SvelteKit은 에러 페이지를 렌더링해요.

기본 에러 페이지는 다소 밋밋해요. `src/routes/+error.svelte` 컴포넌트를 만들어서 커스터마이징할 수 있어요:

```svelte
/// file: src/routes/+error.svelte
<script>
	import { page } from '$app/state';
	import { emojis } from './emojis.js';
</script>

<h1>{page.status} {page.error.message}</h1>
<span style="font-size: 10em">
	{emojis[page.status] ?? emojis[500]}
</span>
```

`+error.svelte` 컴포넌트가 루트 `+layout.svelte` 안에 렌더링된다는 걸 주목하세요. 더 세밀한 `+error.svelte` 경계를 만들 수 있어요:

```svelte
/// file: src/routes/expected/+error.svelte
<h1>this error was expected</h1>
```

이 컴포넌트는 `/expected`에 대해 렌더링될 거예요. 반면 루트 `src/routes/+error.svelte` 페이지는 발생하는 다른 모든 에러에 대해 렌더링될 거예요.
