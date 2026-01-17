---
title: 레이아웃
---

앱의 다른 라우트들이 종종 공통 UI를 공유할 거예요. 각 `+page.svelte` 컴포넌트에서 반복하는 대신, 같은 디렉토리의 모든 라우트에 적용되는 `+layout.svelte` 컴포넌트를 사용할 수 있어요.

이 앱에는 두 개의 라우트가 있어요. 같은 내비게이션 UI를 포함하는 `src/routes/+page.svelte`와 `src/routes/about/+page.svelte`죠. 새 파일 `src/routes/+layout.svelte`를 만들어봐요...

```
src/routes/
├ about/
│ └ +page.svelte
+++├ +layout.svelte+++
└ +page.svelte
```

...그리고 중복된 내용을 `+page.svelte` 파일들에서 새 `+layout.svelte` 파일로 옮기세요. `{@render children()}` 태그는 페이지 콘텐츠가 렌더링될 곳이에요:

```svelte
/// file: src/routes/+layout.svelte
<script>
	let { children } = $props();
</script>

<nav>
	<a href="/">home</a>
	<a href="/about">about</a>
</nav>

{@render children()}
```

`+layout.svelte` 파일은 형제 `+page.svelte`(존재한다면)를 포함해서 모든 자식 라우트에 적용돼요. 레이아웃을 임의의 깊이로 중첩할 수 있어요.
