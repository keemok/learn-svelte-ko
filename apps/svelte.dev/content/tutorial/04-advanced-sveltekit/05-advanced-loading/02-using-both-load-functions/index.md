---
title: 두 load 함수 함께 사용하기
---

때때로 서버 load 함수와 범용 load 함수를 함께 사용해야 할 수 있어요. 예를 들어, 서버에서 데이터를 반환해야 하지만, 서버 데이터로 직렬화될 수 없는 값도 반환해야 할 수 있어요.

이 예제에서는 `src/routes/+page.server.js`에서 얻은 데이터가 `cool`인지 아닌지에 따라 `load`에서 다른 컴포넌트를 반환하고 싶어요.

`data` 속성을 통해 `src/routes/+page.js`에서 서버 데이터에 접근할 수 있어요:

```js
/// file: src/routes/+page.js
export async function load(+++{ data }+++) {
	const module = +++data.cool+++
		? await import('./CoolComponent.svelte')
		: await import('./BoringComponent.svelte');

	return {
		component: module.default,
		message: +++data.message+++
	};
}
```

> [!NOTE] 데이터가 병합되지 않는다는 걸 주목하세요. 범용 `load` 함수에서 명시적으로 `message`를 반환해야 해요.
