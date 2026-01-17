---
title: This
---

특별한 `bind:this` 디렉티브를 사용해서 컴포넌트의 요소에 대한 읽기 전용 바인딩을 얻을 수 있어요.

이 실습의 `$effect`는 캔버스 컨텍스트를 생성하려고 하지만, `canvas`가 `undefined`예요. 컴포넌트의 최상위 수준에서 선언하는 것부터 시작하세요...

```svelte
/// file: App.svelte
<script>
	import { paint } from './gradient.js';

	+++let canvas;+++

	$effect(() => {
		// ...
	});
</script>
```

...그다음 `<canvas>` 요소에 디렉티브를 추가하세요:

```svelte
/// file: App.svelte
<canvas +++bind:this={canvas}+++ width={32} height={32}></canvas>
```

`canvas`의 값은 컴포넌트가 마운트될 때까지 `undefined`로 남아있다는 걸 주목하세요. 즉, `$effect`가 실행될 때까지는 접근할 수 없어요.
