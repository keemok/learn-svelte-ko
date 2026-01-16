---
title: DOM 이벤트
---

이미 간단히 봤듯이, `on<name>` 함수로 요소의 모든 DOM 이벤트(click이나 [pointermove](https://developer.mozilla.org/en-US/docs/Web/API/Element/pointermove_event) 같은)를 들을 수 있어요:

```svelte
/// file: App.svelte
<div +++onpointermove={onpointermove}+++>
	The pointer is at {Math.round(m.x)} x {Math.round(m.y)}
</div>
```

다른 속성처럼 이름과 값이 일치하면 단축 표기법을 쓸 수 있어요:

```svelte
/// file: App.svelte
<div +++{onpointermove}+++>
	The pointer is at {Math.round(m.x)} x {Math.round(m.y)}
</div>
```
