---
title: 부모 데이터 사용하기
---

[레이아웃 데이터](/tutorial/kit/layout-data) 소개에서 봤듯이, `+page.svelte`와 `+layout.svelte` 컴포넌트는 부모 `load` 함수에서 반환된 모든 것에 접근할 수 있어요.

때때로 `load` 함수 자체가 부모로부터 데이터에 접근하는 게 유용해요. `await parent()`로 할 수 있어요.

어떻게 작동하는지 보여주기 위해, 다른 `load` 함수에서 나온 두 숫자를 합산할 거예요. 먼저, `src/routes/+layout.server.js`에서 데이터를 반환하세요:

```js
/// file: src/routes/+layout.server.js
export function load() {
	return { +++a: 1+++ };
}
```

그런 다음, `src/routes/sum/+layout.js`에서 그 데이터를 얻으세요:

```js
/// file: src/routes/sum/+layout.js
export async function load(+++{ parent }+++) {
	+++const { a } = await parent();+++
	return { +++b: a + 1+++ };
}
```

> [!NOTE] [범용](/tutorial/kit/universal-load-functions) `load` 함수가 부모 서버 `load` 함수에서 데이터를 얻을 수 있다는 걸 주목하세요. 역은 참이 아니에요. 서버 load 함수는 다른 서버 load 함수로부터만 부모 데이터를 얻을 수 있어요.

마지막으로 `src/routes/sum/+page.js`에서 두 `load` 함수로부터 부모 데이터를 얻으세요:

```js
/// file: src/routes/sum/+page.js
export async function load(+++{ parent }+++) {
	+++const { a, b } = await parent();+++
	return { +++c: a + b+++ };
}
```

> [!NOTE] `await parent()`를 사용할 때 폭포수(waterfall)를 도입하지 않도록 주의하세요. 부모 데이터에 의존하지 않는 다른 데이터를 `fetch`할 수 있다면, 그걸 먼저 하세요.
