---
title: 페이지 데이터
path: /blog
---

핵심적으로 SvelteKit의 일은 세 가지로 요약돼요:

1. **라우팅** — 들어오는 요청과 매칭되는 라우트 파악하기
2. **로딩** — 라우트에 필요한 데이터 가져오기
3. **렌더링** — HTML 생성하기 (서버에서) 또는 DOM 업데이트하기 (브라우저에서)

라우팅과 렌더링이 어떻게 작동하는지 봤어요. 이제 중간 부분인 로딩에 대해 얘기해봐요.

앱의 모든 페이지는 `+page.svelte` 파일 옆에 `+page.server.js` 파일에서 `load` 함수를 선언할 수 있어요. 파일 이름이 시사하듯이, 이 모듈은 클라이언트 사이드 탐색을 포함해서 오직 서버에서만 실행돼요. `src/routes/blog/+page.server.js` 파일을 추가해서 `src/routes/blog/+page.svelte`의 하드코딩된 링크를 실제 블로그 포스트 데이터로 교체해봐요:

```js
/// file: src/routes/blog/+page.server.js
import { posts } from './data.js';

export function load() {
	return {
		summaries: posts.map((post) => ({
			slug: post.slug,
			title: post.title
		}))
	};
}
```

> [!NOTE] 튜토리얼을 위해 `src/routes/blog/data.js`에서 데이터를 import하고 있어요. 실제 앱에서는 데이터베이스나 CMS에서 데이터를 로드할 가능성이 높지만, 지금은 이렇게 할게요.

`data` prop을 통해 `src/routes/blog/+page.svelte`에서 이 데이터에 접근할 수 있어요:

```svelte
/// file: src/routes/blog/+page.svelte
+++<script>
	let { data } = $props();
</script>+++

<h1>blog</h1>

<ul>
---	<li><a href="/blog/one">one</a></li>
	<li><a href="/blog/two">two</a></li>
	<li><a href="/blog/three">three</a></li>---
+++	{#each data.summaries as { slug, title }}
		<li><a href="/blog/{slug}">{title}</a></li>
	{/each}+++
</ul>
```

이제 포스트 페이지에도 똑같이 해봐요:

```js
/// file: src/routes/blog/[slug]/+page.server.js
import { posts } from '../data.js';

export function load({ params }) {
	const post = posts.find((post) => post.slug === params.slug);

	return {
		post
	};
}
```

```svelte
/// file: src/routes/blog/[slug]/+page.svelte
+++<script>
	let { data } = $props();
</script>+++

---<h1>blog post</h1>---
+++<h1>{data.post.title}</h1>
<div>{@html data.post.content}</div>+++
```

마지막으로 처리해야 할 세부사항이 하나 있어요. 사용자가 `/blog/nope` 같은 유효하지 않은 경로를 방문할 수 있는데, 이 경우 404 페이지로 응답하고 싶어요:

```js
/// file: src/routes/blog/[slug]/+page.server.js
+++import { error } from '@sveltejs/kit';+++
import { posts } from '../data.js';

export function load({ params }) {
	const post = posts.find((post) => post.slug === params.slug);

	+++if (!post) error(404);+++

	return {
		post
	};
}
```

나중 챕터에서 에러 처리에 대해 더 배울 거예요.
