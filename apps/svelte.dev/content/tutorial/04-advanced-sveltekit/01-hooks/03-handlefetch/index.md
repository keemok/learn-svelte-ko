---
title: handleFetch
---

`event` 객체는 표준 [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)처럼 동작하지만 슈퍼파워를 가진 `fetch` 메서드를 가지고 있어요:

- 들어오는 요청의 `cookie`와 `authorization` 헤더를 상속받기 때문에 서버에서 인증된 요청을 만드는 데 사용할 수 있어요
- 서버에서 상대 요청을 만들 수 있어요 (일반적으로 서버 컨텍스트에서 사용될 때 `fetch`는 origin이 있는 URL이 필요해요)
- 내부 요청 (예: `+server.js` 라우트)은 서버에서 실행될 때 HTTP 호출의 오버헤드 없이 핸들러 함수로 직접 가요

동작은 기본적으로 이렇게 생긴 `handleFetch` 훅으로 수정할 수 있어요:

```js
/// file: src/hooks.server.js
export async function handleFetch({ event, request, fetch }) {
	return await fetch(request);
}
```

예를 들어, `src/routes/a/+server.js`에 대한 요청에 대신 `src/routes/b/+server.js`의 응답으로 응답할 수 있어요:

```js
/// file: src/hooks.server.js
export async function handleFetch({ event, request, fetch }) {
+++	const url = new URL(request.url);
	if (url.pathname === '/a') {
		return await fetch('/b');
	}+++

	return await fetch(request);
}
```

나중에 [범용 `load` 함수](universal-load-functions)를 다룰 때 `event.fetch`가 브라우저에서도 호출될 수 있다는 걸 볼 거예요. 그 시나리오에서는 브라우저에서 `https://api.yourapp.com` 같은 공개 URL에 대한 요청이 있을 때, 서버에서 실행될 때 내부 URL로 리다이렉트되어야 하는 경우 (API 서버와 공개 인터넷 사이의 프록시와 로드 밸런서를 우회해서) `handleFetch`가 유용해요.
