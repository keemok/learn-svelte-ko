---
title: 레이아웃 데이터
path: /blog
---

`+layout.svelte` 파일이 모든 자식 라우트에 대한 UI를 만드는 것처럼, `+layout.server.js` 파일은 모든 자식 라우트에 대한 데이터를 로드해요.

블로그 포스트 페이지에 '더 많은 포스트' 사이드바를 추가하고 싶다고 가정해봐요. `src/routes/blog/+page.server.js`에서처럼 `src/routes/blog/[slug]/+page.server.js`의 `load` 함수에서 `summaries`를 반환할 수도 있지만, 그건 반복적이에요.

대신, `src/routes/blog/+page.server.js`를 `src/routes/blog/+layout.server.js`로 이름을 바꿔봐요. `/blog` 라우트가 계속 작동하는 걸 주목하세요. `data.summaries`가 여전히 페이지에서 사용 가능해요.

이제 포스트 페이지의 레이아웃에 사이드바를 추가하세요:

```svelte
/// file: src/routes/blog/[slug]/+layout.svelte
<script>
	let { data, children } = $props();
</script>

<div class="layout">
	<main>
		{@render children()}
	</main>

+++	<aside>
		<h2>More posts</h2>
		<ul>
			{#each data.summaries as { slug, title }}
				<li>
					<a href="/blog/{slug}">{title}</a>
				</li>
			{/each}
		</ul>
	</aside>+++
</div>

<style>
	@media (min-width: 640px) {
		.layout {
			display: grid;
			gap: 2em;
			grid-template-columns: 1fr 16em;
		}
	}
</style>
```

레이아웃(과 그 아래의 모든 페이지)은 부모 `+layout.server.js`에서 `data.summaries`를 상속받아요.

한 포스트에서 다른 포스트로 이동할 때, 포스트 자체에 대한 데이터만 로드하면 돼요. 레이아웃 데이터는 여전히 유효하거든요. 더 알아보려면 [무효화](/docs/kit/load#Rerunning-load-functions)에 대한 문서를 참고하세요.
