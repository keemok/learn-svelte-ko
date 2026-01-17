---
title: 페이지 새로고침
---

일반적으로 SvelteKit은 페이지를 새로고침하지 않고 페이지 간 탐색해요. 이 실습에서 `/`와 `/about` 사이를 탐색하면 타이머가 계속 돌아가요.

드문 경우지만 이 동작을 비활성화하고 싶을 수 있어요. 개별 링크나 링크를 포함하는 요소에 `data-sveltekit-reload` 속성을 추가해서 그렇게 할 수 있어요:

```svelte
/// file: src/routes/+layout.svelte
<nav +++data-sveltekit-reload+++>
	<a href="/">home</a>
	<a href="/about">about</a>
</nav>
```

사용 가능한 링크 옵션과 그 값에 대한 더 많은 정보는 [링크 옵션 문서](/docs/kit/link-options)를 참고하세요.
