---
title: 라우트 그룹
---

[라우팅 소개](/tutorial/kit/layouts)에서 봤듯이, 레이아웃은 다른 라우트 간 UI와 데이터 로딩 로직을 공유하는 방법이에요.

때로는 라우트에 영향을 주지 않고 레이아웃을 사용하는 게 유용해요. 예를 들어, `/app`과 `/account` 라우트는 인증 뒤에 있어야 하지만 `/about` 페이지는 세상에 열려 있어야 할 수 있어요. 괄호 안의 디렉토리인 라우트 그룹(route group)으로 이렇게 할 수 있어요.

`account`를 `(authed)/account`로 이름을 바꾼 다음 `app`을 `(authed)/app`으로 이름을 바꿔서 `(authed)` 그룹을 만드세요.

이제 `src/routes/(authed)/+layout.server.js`를 만들어서 이 라우트에 대한 접근을 제어할 수 있어요:

```js
/// file: src/routes/(authed)/+layout.server.js
import { redirect } from '@sveltejs/kit';

export function load({ cookies, url }) {
	if (!cookies.get('logged_in')) {
		redirect(303, `/login?redirectTo=${url.pathname}`);
	}
}
```

이 페이지들을 방문하려고 하면 `/login` 라우트로 리다이렉트될 거예요. `src/routes/login/+page.server.js`에 `logged_in` 쿠키를 설정하는 폼 액션이 있어요.

`src/routes/(authed)/+layout.svelte` 파일을 추가해서 이 두 라우트에 UI를 추가할 수도 있어요:

```svelte
/// file: src/routes/(authed)/+layout.svelte
<script>
	let { children } = $props();
</script>

{@render children()}

<form method="POST" action="/logout">
	<button>log out</button>
</form>
```
