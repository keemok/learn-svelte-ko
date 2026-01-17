---
title: 범용 load 함수
---

[데이터 로딩](page-data)의 이전 섹션에서 `+page.server.js`와 `+layout.server.js` 파일을 사용해서 서버에서 데이터를 로드했어요. 데이터베이스에서 직접 데이터를 가져오거나 쿠키를 읽는 것 같은 일을 해야 하는 경우 매우 편리해요.

때로는 클라이언트 사이드 탐색을 할 때 서버에서 데이터를 로드하는 게 말이 안 될 수 있어요. 예를 들어:

- 외부 API에서 데이터를 로드하는 경우
- 사용 가능하면 인메모리 데이터를 사용하고 싶은 경우
- 튀어나옴(pop-in)을 피하기 위해 이미지가 프리로드될 때까지 탐색을 지연하고 싶은 경우
- `load`에서 직렬화될 수 없는 것(SvelteKit은 [devalue](https://github.com/Rich-Harris/devalue)를 사용해서 서버 데이터를 JSON으로 바꿔요)을 반환해야 하는 경우, 예를 들어 컴포넌트나 스토어

이 실습에서는 후자의 경우를 다뤄요. `src/routes/red/+page.server.js`, `src/routes/green/+page.server.js`, `src/routes/blue/+page.server.js`의 서버 `load` 함수는 데이터처럼 직렬화될 수 없는 `component` 생성자를 반환해요. `/red`, `/green` 또는 `/blue`로 이동하면 터미널에서 'Data returned from `load` ... is not serializable' 에러를 볼 거예요.

서버 `load` 함수를 범용 `load` 함수로 바꾸려면 각 `+page.server.js` 파일을 `+page.js`로 이름을 바꾸세요. 이제 함수는 서버 사이드 렌더링 중에 서버에서 실행되지만, 앱이 하이드레이트되거나 사용자가 클라이언트 사이드 탐색을 수행할 때 브라우저에서도 실행될 거예요.

이제 이 `load` 함수에서 반환된 `component`를 `src/routes/+layout.svelte`에서 다른 값처럼 사용할 수 있어요:

```svelte
/// file: src/routes/+layout.svelte
<nav
	class={[page.data.color && 'has-color']}
	style:background={page.data.color ?? 'var(--bg-2)'}
>
	<a href="/">home</a>
	<a href="/red">red</a>
	<a href="/green">green</a>
	<a href="/blue">blue</a>

+++	{#if page.data.component}
		<page.data.component />
	{/if}+++
</nav>
```

서버 `load` 함수와 범용 `load` 함수의 차이점과 언제 어떤 것을 사용할지에 대해 더 배우려면 [문서](/docs/kit/load#Universal-vs-server)를 읽어보세요.
