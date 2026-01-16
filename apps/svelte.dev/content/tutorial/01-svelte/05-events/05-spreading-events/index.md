---
title: 이벤트 spread
---

이벤트 핸들러를 요소에 직접 [spread](spread-props)할 수도 있어요. 여기서는 `App.svelte`에 `onclick` 핸들러를 정의했어요. `BigRedButton.svelte`의 `<button>`에 props를 전달하기만 하면 돼요:

```svelte
/// file: BigRedButton.svelte
<button +++{...props}+++>
	Push
</button>
```
