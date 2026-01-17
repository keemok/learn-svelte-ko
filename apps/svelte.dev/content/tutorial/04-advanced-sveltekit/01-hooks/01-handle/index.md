---
title: handle
---

SvelteKit은 여러 훅(hook)을 제공해요. 프레임워크의 기본 동작을 가로채고 재정의하는 방법이죠.

가장 기본적인 훅은 `src/hooks.server.js`에 있는 `handle`이에요. `event` 객체와 `resolve` 함수를 받고 [`Response`](https://developer.mozilla.org/en-US/docs/Web/API/Response)를 반환해요.

`resolve`는 마법이 일어나는 곳이에요. SvelteKit은 들어오는 요청 URL을 앱의 라우트와 매칭하고, 관련 코드(`+page.server.js`와 `+page.svelte` 파일 등)를 import하고, 라우트에 필요한 데이터를 로드하고, 응답을 생성해요.

기본 `handle` 훅은 이렇게 생겼어요:

```js
/// file: src/hooks.server.js
export async function handle({ event, resolve }) {
	return await resolve(event);
}
```

([API 라우트](get-handlers)가 아닌) 페이지의 경우, `transformPageChunk`로 생성된 HTML을 수정할 수 있어요:

```js
/// file: src/hooks.server.js
export async function handle({ event, resolve }) {
	return await resolve(event, {
+++		transformPageChunk: ({ html }) => html.replace(
			'<body',
			'<body style="color: hotpink"'
		)+++
	});
}
```

완전히 새로운 라우트도 만들 수 있어요:

```js
/// file: src/hooks.server.js
export async function handle({ event, resolve }) {
+++	if (event.url.pathname === '/ping') {
		return new Response('pong');
	}+++

	return await resolve(event, {
		transformPageChunk: ({ html }) => html.replace(
			'<body',
			'<body style="color: hotpink"'
		)
	});
}
```
