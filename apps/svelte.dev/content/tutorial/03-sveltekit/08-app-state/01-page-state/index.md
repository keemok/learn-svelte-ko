---
title: page
---

SvelteKit은 `$app/state` 모듈을 통해 세 개의 읽기 전용 상태 객체를 사용 가능하게 만들어요. `page`, `navigating`, `updated`예요. 가장 자주 사용할 것은 현재 페이지에 대한 정보를 제공하는 [`page`](/docs/kit/@sveltejs-kit#Page)예요:

- `url` — 현재 페이지의 [URL](https://developer.mozilla.org/en-US/docs/Web/API/URL)
- `params` — 현재 페이지의 [파라미터](params)
- `route` — 현재 라우트를 나타내는 `id` 속성을 가진 객체
- `status` — 현재 페이지의 HTTP 상태 코드
- `error` — 현재 페이지의 에러 객체 (있다면) ([나중](error-basics) [실습](handleerror)에서 에러 처리에 대해 더 배울 거예요)
- `data` — 현재 페이지의 데이터, 모든 `load` 함수의 반환 값을 결합한 것
- `form` — [폼 액션](the-form-element)에서 반환된 데이터

이 속성들 각각은 내부적으로 `$state.raw`를 사용해서 반응형이에요. 다음은 `page.url.pathname`을 사용하는 예제예요:

```svelte
/// file: src/routes/+layout.svelte
<script>
	+++import { page } from '$app/state';+++

	let { children } = $props();
</script>

<nav>
	<a href="/" +++aria-current={page.url.pathname === '/'}+++>
		home
	</a>

	<a href="/about" +++aria-current={page.url.pathname === '/about'}+++>
		about
	</a>
</nav>

{@render children()}
```

> [!NOTE] SvelteKit 2.12 이전에는 이를 위해 `$app/stores`를 사용해야 했어요. 같은 정보를 담고 있는 `$page` 스토어를 제공하죠. 현재 `$app/stores`를 사용하고 있다면, `$app/state`로 마이그레이션하는 걸 권장해요 (Svelte 5 필요).
