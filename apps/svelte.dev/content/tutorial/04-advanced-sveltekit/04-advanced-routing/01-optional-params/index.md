---
title: 선택적 파라미터
---

[라우팅](/tutorial/kit/pages)의 첫 챕터에서 [동적 파라미터](/tutorial/kit/params)로 라우트를 만드는 방법을 배웠어요.

때로는 파라미터를 선택적으로 만드는 게 유용해요. 고전적인 예는 경로명을 사용해서 로케일을 결정하는 경우예요. `/fr/...`, `/de/...` 등이지만, 기본 로케일도 갖고 싶을 때죠.

그렇게 하려면 이중 대괄호를 사용해요. `[lang]` 디렉토리를 `[[lang]]`으로 이름을 바꾸세요.

이제 앱이 빌드에 실패해요. `src/routes/+page.svelte`와 `src/routes/[[lang]]/+page.svelte` 둘 다 `/`와 매칭될 거거든요. `src/routes/+page.svelte`를 삭제하세요. (에러 페이지에서 복구하려면 앱을 새로고침해야 할 수도 있어요).

마지막으로 `src/routes/[[lang]]/+page.server.js`를 편집해서 기본 로케일을 지정하세요:

```js
/// file: src/routes/[[lang]]/+page.server.js
const greetings = {
	en: 'hello!',
	de: 'hallo!',
	fr: 'bonjour!'
};

export function load({ params }) {
	return {
		greeting: greetings[params.lang +++?? 'en'+++]
	};
}
```
