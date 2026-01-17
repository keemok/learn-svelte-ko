---
title: $env/static/private
---

환경 변수 — API 키와 데이터베이스 자격 증명 같은 — 는 `.env` 파일에 추가될 수 있고, 애플리케이션에서 사용 가능하게 될 거예요.

> [!NOTE] `.env.local`이나 `.env.[mode]` 파일도 사용할 수 있어요. 더 많은 정보는 [Vite 문서](https://vitejs.dev/guide/env-and-mode.html#env-files)를 참고하세요. 민감한 정보를 포함하는 파일은 `.gitignore` 파일에 추가하세요!
>
> `process.env`의 환경 변수도 `$env/static/private`를 통해 사용 가능해요.

이 실습에서는 환경 변수를 사용해서 올바른 암호를 아는 경우 사용자가 웹사이트에 들어갈 수 있게 하고 싶어요.

먼저, `.env`에 새 환경 변수를 추가하세요:

```env
/// file: .env
PASSPHRASE=+++"open sesame"+++
```

`src/routes/+page.server.js`를 여세요. `$env/static/private`에서 `PASSPHRASE`를 import하고 [폼 액션](/tutorial/kit/the-form-element) 안에서 사용하세요:

```js
/// file: src/routes/+page.server.js
import { redirect, fail } from '@sveltejs/kit';
+++import { PASSPHRASE } from '$env/static/private';+++

export function load({ cookies }) {
	if (cookies.get('allowed')) {
		redirect(307, '/welcome');
	}
}

export const actions = {
	default: async ({ request, cookies }) => {
		const data = await request.formData();

		if (data.get('passphrase') === +++PASSPHRASE+++) {
			cookies.set('allowed', 'true', {
				path: '/'
			});

			redirect(303, '/welcome');
		}

		return fail(403, {
			incorrect: true
		});
	}
};
```

이제 웹사이트는 올바른 암호를 아는 누구나 접근할 수 있어요.

## 비밀 유지하기

민감한 데이터가 실수로 브라우저로 전송되지 않는 게 중요해요. 해커와 악당이 쉽게 훔칠 수 있거든요.

SvelteKit은 이런 일이 일어나는 걸 쉽게 방지해요. `src/routes/+page.svelte`에 `PASSPHRASE`를 import하려고 하면 어떤 일이 일어나는지 주목하세요:

```svelte
/// file: src/routes/+page.svelte
<script>
	+++import { PASSPHRASE } from '$env/static/private';+++
	let { form } = $props();
</script>
```

에러 오버레이가 나타나서 `$env/static/private`를 클라이언트 사이드 코드로 import할 수 없다고 알려줘요. 서버 모듈에서만 import할 수 있어요:

- `+page.server.js`
- `+layout.server.js`
- `+server.js`
- `.server.js`로 끝나는 모든 모듈
- `src/lib/server` 안의 모든 모듈

결과적으로 이 모듈들은 다른 서버 모듈에서만 import될 수 있어요.

## 정적 vs 동적

`$env/static/private`의 `static`은 이 값들이 빌드 타임에 알려져 있고 정적으로 대체될 수 있다는 걸 나타내요. 이것은 유용한 최적화를 가능하게 해요:

```js
import { FEATURE_FLAG_X } from '$env/static/private';

if (FEATURE_FLAG_X === 'enabled') {
	// FEATURE_FLAG_X가 활성화되지 않으면
	// 여기의 코드는 빌드 출력에서 제거될 거예요
}
```

경우에 따라 동적인 환경 변수를 참조해야 할 수 있어요. 다시 말해, 앱을 실행할 때까지 알려지지 않은 것들이죠. 다음 실습에서 이 경우를 다룰 거예요.
