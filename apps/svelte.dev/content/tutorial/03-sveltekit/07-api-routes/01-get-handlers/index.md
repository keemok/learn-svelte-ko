---
title: GET 핸들러
---

SvelteKit을 사용하면 페이지 이상의 것을 만들 수 있어요. HTTP 메서드에 해당하는 함수를 export하는 `+server.js` 파일을 추가해서 API 라우트도 만들 수 있어요: `GET`, `PUT`, `POST`, `PATCH`, `DELETE`.

이 앱은 버튼을 클릭하면 `/roll` API 라우트에서 데이터를 가져와요. `src/routes/roll/+server.js` 파일을 추가해서 그 라우트를 만드세요:

```js
/// file: src/routes/roll/+server.js
export function GET() {
	const number = Math.floor(Math.random() * 6) + 1;

	return new Response(number, {
		headers: {
			'Content-Type': 'application/json'
		}
	});
}
```

이제 버튼을 클릭하면 작동해요.

요청 핸들러는 [Response](https://developer.mozilla.org/en-US/docs/Web/API/Response/Response) 객체를 반환해야 해요. API 라우트에서 JSON을 반환하는 게 일반적이기 때문에, SvelteKit은 이런 응답을 생성하기 위한 편의 함수를 제공해요:

```js
/// file: src/routes/roll/+server.js
+++import { json } from '@sveltejs/kit';+++

export function GET() {
	const number = Math.floor(Math.random() * 6) + 1;

---	return new Response(number, {
		headers: {
			'Content-Type': 'application/json'
		}
	});---
+++	return json(number);+++
}
```
