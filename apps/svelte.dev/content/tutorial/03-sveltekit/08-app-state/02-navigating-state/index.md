---
title: navigating
---

`navigating` 객체는 현재 탐색을 나타내요. 링크 클릭, 뒤로/앞으로 탐색, 프로그래밍 방식의 `goto` 때문에 탐색이 시작되면, `navigating`의 값은 다음 속성들을 가진 객체가 돼요:

- `from`과 `to` — `params`, `route`, `url` 속성을 가진 객체
- `type` — 탐색 타입, 예: `link`, `popstate` 또는 `goto`

> [!NOTE] 완전한 타입 정보는 [`Navigation`](/docs/kit/@sveltejs-kit#Navigation) 문서를 방문하세요.

오래 실행되는 탐색에 대한 로딩 표시기를 보여주는 데 사용할 수 있어요. 이 실습에서 `src/routes/+page.server.js`와 `src/routes/about/+page.server.js` 모두 인위적인 지연이 있어요. `src/routes/+layout.svelte` 안에서 `navigating` 객체를 import하고 네비게이션 바에 메시지를 추가하세요:

```svelte
/// file: src/routes/+layout.svelte
<script>
	import { page, +++navigating+++ } from '$app/state';

	let { children } = $props();
</script>

<nav>
	<a href="/" aria-current={page.url.pathname === '/'}>
		home
	</a>

	<a href="/about" aria-current={page.url.pathname === '/about'}>
		about
	</a>

+++	{#if navigating.to}
		navigating to {navigating.to.url.pathname}
	{/if}+++
</nav>

{@render children()}
```

> [!NOTE] SvelteKit 2.12 이전에는 이를 위해 `$app/stores`를 사용해야 했어요. 같은 정보를 담고 있는 `$navigating` 스토어를 제공하죠. 현재 `$app/stores`를 사용하고 있다면, `$app/state`로 마이그레이션하는 걸 권장해요 (Svelte 5 필요).
