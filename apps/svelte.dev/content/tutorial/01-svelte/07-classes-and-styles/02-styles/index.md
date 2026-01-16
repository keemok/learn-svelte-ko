---
title: style 디렉티브
---

`class`처럼 인라인 `style` 속성도 그대로 작성할 수 있어요. Svelte는 사실 멋진 기능이 추가된 HTML일 뿐이거든요:

```svelte
/// file: App.svelte
<button
	class="card"
	+++style="transform: {flipped ? 'rotateY(0)' : ''}; --bg-1: palegoldenrod; --bg-2: black; --bg-3: goldenrod"+++
	onclick={() => flipped = !flipped}
>
```

스타일이 많아지면 좀 지저분해 보이기 시작해요. `style:` 디렉티브를 써서 정리할 수 있어요:

```svelte
/// file: App.svelte
<button
	class="card"
+++	style:transform={flipped ? 'rotateY(0)' : ''}
	style:--bg-1="palegoldenrod"
	style:--bg-2="black"
	style:--bg-3="goldenrod"+++
	onclick={() => flipped = !flipped}
>
```
