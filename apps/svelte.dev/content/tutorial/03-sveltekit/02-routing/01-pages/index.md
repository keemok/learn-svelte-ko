---
title: 페이지
---

SvelteKit은 파일시스템 기반 라우팅을 사용해요. 즉, 앱의 라우트(다시 말해, 사용자가 특정 URL로 이동할 때 앱이 무엇을 해야 하는지)가 코드베이스의 디렉토리로 정의된다는 의미예요.

`src/routes` 안의 모든 `+page.svelte` 파일은 앱에 페이지를 만들어요. 이 앱에는 현재 하나의 페이지가 있어요. `/`에 매핑되는 `src/routes/+page.svelte`죠. `/about`으로 이동하면 404 Not Found 에러가 보일 거예요.

고쳐봐요. 두 번째 페이지 `src/routes/about/+page.svelte`를 추가하고, `src/routes/+page.svelte`의 내용을 복사한 다음 업데이트하세요:

```svelte
/// file: src/routes/about/+page.svelte
<nav>
	<a href="/">home</a>
	<a href="/about">about</a>
</nav>

<h1>+++about+++</h1>
<p>this is the +++about+++ page.</p>
```

이제 `/`와 `/about` 사이를 탐색할 수 있어요.

> [!NOTE] 전통적인 멀티 페이지 앱과 달리, `/about`으로 이동했다가 돌아오면 싱글 페이지 앱처럼 현재 페이지의 내용이 업데이트돼요. 이렇게 양쪽의 장점을 모두 얻을 수 있어요. 빠른 서버 렌더링 시작과 즉각적인 탐색이죠. (이 동작은 [설정할 수 있어요](/docs/kit/page-options).)
