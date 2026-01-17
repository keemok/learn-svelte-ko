---
title: 리다이렉트
---

`redirect` 메커니즘을 사용해서 한 페이지에서 다른 페이지로 리다이렉트할 수 있어요.

`src/routes/a/+page.server.js`에 새 `load` 함수를 만드세요:

```js
/// file: src/routes/a/+page.server.js
import { redirect } from '@sveltejs/kit';

export function load() {
	redirect(307, '/b');
}
```

이제 `/a`로 이동하면 바로 `/b`로 갈 거예요.

나중 챕터에서 논의할 `handle` 훅과 함께 `load` 함수, 폼 액션, API 라우트 안에서 `redirect(...)`를 할 수 있어요.

가장 일반적으로 사용할 상태 코드:

- `303` — 폼 액션에서, 성공적인 제출 후
- `307` — 임시 리다이렉트
- `308` — 영구 리다이렉트

> [!NOTE] `redirect(...)`는 `error(...)`처럼 던져져서, 리다이렉트 이후의 코드는 실행되지 않아요.
