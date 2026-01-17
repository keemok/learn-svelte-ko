---
title: 헤더 설정하기
---

`load` 함수 안에서 (나중에 배울 [폼 액션](the-form-element), [훅](handle), [API 라우트](get-handlers)에서도) `setHeaders` 함수에 접근할 수 있어요. 놀랍지 않게도 응답에 헤더를 설정하는 데 사용할 수 있어요.

가장 일반적으로는 [`Cache-Control`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control) 응답 헤더로 캐싱 동작을 커스터마이징하는 데 사용하지만, 이 튜토리얼을 위해 덜 권장되고 더 극적인 것을 해볼게요:

```js
/// file: src/routes/+page.server.js
export function load(+++{ setHeaders }+++) {
+++	setHeaders({
		'Content-Type': 'text/plain'
	});+++
}
```

(효과를 보려면 iframe을 새로고침해야 할 수도 있어요.)
