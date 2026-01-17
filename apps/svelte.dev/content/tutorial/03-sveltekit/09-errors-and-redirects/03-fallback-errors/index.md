---
title: 폴백 에러
---

상황이 정말 잘못되면 — 루트 레이아웃 데이터를 로드하는 동안 또는 에러 페이지를 렌더링하는 동안 에러가 발생하면 — SvelteKit은 정적 에러 페이지로 폴백해요.

실제로 보려면 새 `src/routes/+layout.server.js` 파일을 추가하세요:

```js
/// file: src/routes/+layout.server.js
export function load() {
	throw new Error('yikes');
}
```

폴백 에러 페이지를 커스터마이징할 수 있어요. `src/error.html` 파일을 만드세요:

```html
/// file: src/error.html
<h1>Game over</h1>
<p>Code %sveltekit.status%</p>
<p>%sveltekit.error.message%</p>
```

이 파일은 다음을 포함할 수 있어요:

- `%sveltekit.status%` — HTTP 상태 코드
- `%sveltekit.error.message%` — 에러 메시지
