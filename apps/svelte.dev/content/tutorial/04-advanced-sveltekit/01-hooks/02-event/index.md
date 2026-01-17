---
title: RequestEvent 객체
---

`handle`에 전달된 `event` 객체는 `+server.js` 파일의 [API 라우트](get-handlers), `+page.server.js` 파일의 [폼 액션](the-form-element), `+page.server.js`와 `+layout.server.js`의 `load` 함수에 전달되는 것과 같은 객체예요. [`RequestEvent`](/docs/kit/@sveltejs-kit#RequestEvent)의 인스턴스죠.

이미 만난 것들을 포함해서 많은 유용한 속성과 메서드를 담고 있어요:

- `cookies` — [cookies API](cookies)
- `fetch` — 추가 능력을 가진 표준 [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
- `getClientAddress()` — 클라이언트의 IP 주소를 가져오는 함수
- `isDataRequest` — 클라이언트 사이드 탐색 중 브라우저가 페이지의 데이터를 요청하면 `true`, 페이지/라우트가 직접 요청되면 `false`
- `locals` — 임의의 데이터를 넣을 곳
- `params` — 라우트 파라미터
- `request` — [Request](https://developer.mozilla.org/en-US/docs/Web/API/Request) 객체
- `route` — 매칭된 라우트를 나타내는 `id` 속성을 가진 객체
- `setHeaders(...)` — 응답에 [HTTP 헤더를 설정](headers)하는 함수
- `url` — 현재 요청을 나타내는 [URL](https://developer.mozilla.org/en-US/docs/Web/API/URL) 객체

유용한 패턴은 `handle`에서 `event.locals`에 데이터를 추가해서 이후 `load` 함수에서 읽을 수 있게 하는 거예요:

```js
/// file: src/hooks.server.js
export async function handle({ event, resolve }) {
	+++event.locals.answer = 42;+++
	return await resolve(event);
}
```

```js
/// file: src/routes/+page.server.js
export function load(+++event+++) {
	return {
		message: `the answer is ${+++event.locals.answer+++}`
	};
}
```
