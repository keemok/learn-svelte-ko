---
title: 쿠키 읽고 쓰기
---

[`setHeaders`](headers) 함수는 `Set-Cookie` 헤더와 함께 사용할 수 없어요. 대신 `cookies` API를 사용해야 해요.

`load` 함수에서 `cookies.get(name, options)`로 쿠키를 읽을 수 있어요:

```js
/// file: src/routes/+page.server.js
export function load(+++{ cookies }+++) {
	+++const visited = cookies.get('visited');+++

	return {
		visited: visited === 'true'
	};
}
```

쿠키를 설정하려면 `cookies.set(name, value, options)`를 사용하세요. 쿠키를 설정할 때 `path`를 명시적으로 구성하는 게 강력히 권장돼요. 브라우저의 기본 동작이 다소 쓸모없게도 현재 경로의 부모에 쿠키를 설정하거든요.

```js
/// file: src/routes/+page.server.js
export function load({ cookies }) {
	const visited = cookies.get('visited');

	+++cookies.set('visited', 'true', { path: '/' });+++

	return {
		visited: visited === 'true'
	};
}
```

이제 iframe을 새로고침하면 `Hello stranger!`가 `Hello friend!`로 바뀌어요.

`cookies.set(name, ...)`을 호출하면 `Set-Cookie` 헤더가 작성되지만, 쿠키의 내부 맵도 업데이트돼요. 즉, 같은 요청 동안 이후에 `cookies.get(name)`을 호출하면 업데이트된 값이 반환돼요. 내부적으로 `cookies` API는 인기 있는 `cookie` 패키지를 사용해요. `cookies.get`과 `cookies.set`에 전달된 옵션은 `cookie` [문서](https://github.com/jshttp/cookie#api)의 `parse`와 `serialize` 옵션에 해당해요. SvelteKit은 쿠키를 더 안전하게 만들기 위해 다음 기본값을 설정해요:

```js
{
	httpOnly: true,
	secure: true,
	sameSite: 'lax'
}
```
