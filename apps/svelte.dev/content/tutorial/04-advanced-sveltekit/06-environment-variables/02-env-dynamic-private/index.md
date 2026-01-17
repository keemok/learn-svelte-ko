---
title: $env/dynamic/private
---

앱이 빌드될 때가 아니라 앱이 실행될 때 환경 변수의 값을 읽어야 하는 경우, `$env/static/private` 대신 `$env/dynamic/private`를 사용할 수 있어요:

```js
/// file: src/routes/+page.server.js
import { redirect, fail } from '@sveltejs/kit';
import { +++env+++ } from '$env/+++dynamic+++/private';

export function load({ cookies }) {
	if (cookies.get('allowed')) {
		redirect(307, '/welcome');
	}
}

export const actions = {
	default: async ({ request, cookies }) => {
		const data = await request.formData();

		if (data.get('passphrase') === +++env.+++PASSPHRASE) {
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
