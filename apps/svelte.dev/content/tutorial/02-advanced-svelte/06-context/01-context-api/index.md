---
title: setContext와 getContext
---

Context API는 컴포넌트들이 props로 데이터와 함수를 전달하거나 많은 이벤트를 디스패치하지 않고도 서로 '대화'할 수 있는 메커니즘을 제공해요. 고급 기능이지만 유용하죠. 이 실습에서는 context API를 사용해서 생성 미술의 선구자 중 한 명인 George Nees의 [Schotter](https://collections.vam.ac.uk/item/O221321/schotter-print-nees-georg/)를 재현할 거예요.

`Canvas.svelte` 안에는 캔버스에 항목을 추가하는 `addItem` 함수가 있어요. `setContext`로 `<Square>` 같은 `<Canvas>` 내부의 컴포넌트에서 사용할 수 있게 만들 수 있어요:

```js
/// file: Canvas.svelte
+++import { setContext } from 'svelte';+++
import { SvelteSet } from 'svelte/reactivity';

let { width = 100, height = 100, children } = $props();

let canvas;
let items = new SvelteSet();

+++setContext('canvas', { addItem });+++

function addItem(fn) {
	$effect(() => {
		items.add(fn);
		return () => items.delete(fn);
	});
}
```

자식 컴포넌트 안에서는 이제 `getContext`로 context를 가져올 수 있어요:

```js
/// file: Square.svelte
+++import { getContext } from 'svelte';+++

let { x, y, size, rotate } = $props();

+++getContext('canvas').addItem(draw);+++
```

지금까지는... 지루해요. 그리드에 무작위성을 추가해봐요:

```svelte
/// file: App.svelte
<div class="container">
	<Canvas width={800} height={1200}>
		{#each Array(12) as _, c}
			{#each Array(22) as _, r}
				<Square
					x={180 + c * 40+++ + jitter(r * 2)+++}
					y={180 + r * 40+++ + jitter(r * 2)+++}
					size={40}
					+++rotate={jitter(r * 0.05)}+++
				/>
			{/each}
		{/each}
	</Canvas>
</div>
```

`setContext`와 `getContext`는 컴포넌트 초기화 중에 호출되어야 해요. 그래야 context가 올바르게 바인딩될 수 있거든요. 키(이 경우 `'canvas'`)는 원하는 무엇이든 될 수 있어요. 문자열이 아닌 것도 가능하고, 누가 context에 접근할 수 있는지 제어하는 데 유용해요.

> [!NOTE] Context 객체는 반응형 상태를 포함해서 무엇이든 포함할 수 있어요. 이를 통해 시간이 지남에 따라 변경되는 값을 자식 컴포넌트에 전달할 수 있어요:
>
> ```js
> // 부모 컴포넌트에서
> import { setContext } from 'svelte';
>
> let context = $state({...});
> setContext('my-context', context);
> ```
>
> ```js
> // 자식 컴포넌트에서
> import { getContext } from 'svelte';
>
> const context = getContext('my-context');
> ```
