---
title: handleError
---

`handleError` 훅을 사용하면 예상치 못한 에러를 가로채고 Slack 채널에 핑을 보내거나 에러 로깅 서비스에 데이터를 보내는 것 같은 동작을 트리거할 수 있어요.

[이전 실습](error-basics)에서 기억하겠지만, 에러가 `@sveltejs/kit`의 `error` 헬퍼로 만들어지지 않았다면 예상치 못한 에러예요. 일반적으로 앱에서 뭔가 고쳐야 한다는 의미죠. 기본 동작은 에러를 로그하는 거예요:

```js
/// file: src/hooks.server.js
export function handleError({ event, error }) {
	console.error(error.stack);
}
```

`/the-bad-place`로 이동하면 실제로 볼 수 있어요. 에러 페이지가 표시되고, 터미널을 열면 (URL 바 오른쪽 버튼 사용) `src/routes/the-bad-place/+page.server.js`의 메시지를 볼 수 있어요.

사용자에게 에러 메시지를 보여주지 않는다는 걸 주목하세요. 에러 메시지가 민감한 정보를 포함할 수 있기 때문이에요. 좋게는 사용자를 혼란스럽게 하고, 나쁘게는 악당들에게 도움이 될 수 있죠. 대신, 앱에서 사용 가능한 에러 객체 — `+error.svelte` 페이지의 `page.error` 또는 `src/error.html` 폴백의 `%sveltekit.error%`로 표현되는 — 는 그냥 이거예요:

<!-- prettier-ignore-start -->
```js
{
	message: 'Internal Error' // 또는 404의 경우 'Not Found'
}
```
<!-- prettier-ignore-end -->

때로는 이 객체를 커스터마이징하고 싶을 수 있어요. 그렇게 하려면 `handleError`에서 객체를 반환할 수 있어요:

```js
/// file: src/hooks.server.js
export function handleError({ event, error }) {
	console.error(error.stack);

	return {
		message: 'everything is fine',
		code: 'JEREMYBEARIMY'
	};
}
```

이제 커스텀 에러 페이지에서 `message` 외의 속성을 참조할 수 있어요. `src/routes/+error.svelte`를 만드세요:

```svelte
/// file: src/routes/+error.svelte
<script>
	import { page } from '$app/state';
</script>

<h1>{page.status}</h1>
<p>{page.error.message}</p>
<p>error code: {page.error.code}</p>
```
