---
title: 인라인 핸들러
---

이벤트 핸들러를 인라인으로 선언할 수도 있어요:

```svelte
/// file: App.svelte
<script>
	let m = $state({ x: 0, y: 0 });

	---function onpointermove(event) {
		m.x = event.clientX;
		m.y = event.clientY;
	}---
</script>

<div
	onpointermove={+++(event) => {
		m.x = event.clientX;
		m.y = event.clientY;
	}+++}
>
	The pointer is at {m.x} x {m.y}
</div>
```
