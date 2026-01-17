---
title: 애니메이션
---

[이전 챕터](/tutorial/svelte/deferred-transitions)에서 지연된 트랜지션을 사용해서 요소가 한 할 일 목록에서 다른 목록으로 이동할 때 모션의 환상을 만들었어요.

환상을 완성하려면, 트랜지션되지 않는 요소에도 모션을 적용해야 해요. 이를 위해 `animate` 디렉티브를 사용해요.

먼저, `TodoList.svelte`에 `svelte/animate`에서 `flip` 함수를 import하세요. flip은 ['First, Last, Invert, Play'](https://aerotwist.com/blog/flip-your-animations/)를 의미해요:

```svelte
/// file: TodoList.svelte
<script>
	+++import { flip } from 'svelte/animate';+++
	import { send, receive } from './transition.js';

	let { todos, remove } = $props();
</script>
```

그다음 `<li>` 요소에 추가하세요:

```svelte
/// file: TodoList.svelte
<li
	class={{ done: todo.done }}
	in:receive={{ key: todo.id }}
	out:send={{ key: todo.id }}
	+++animate:flip+++
>
```

이 경우 움직임이 좀 느리니까, `duration` 파라미터를 추가할 수 있어요:

```svelte
/// file: TodoList.svelte
<li
	class={{ done: todo.done }}
	in:receive={{ key: todo.id }}
	out:send={{ key: todo.id }}
	animate:flip+++={{ duration: 200 }}+++
>
```

> [!NOTE] `duration`은 `d => milliseconds` 함수일 수도 있어요. 여기서 `d`는 요소가 이동해야 하는 픽셀 수예요.

모든 트랜지션과 애니메이션이 JavaScript가 아닌 CSS로 적용되고 있다는 걸 주목하세요. 즉, 메인 스레드를 차단하지 않아요(또는 차단당하지도 않아요).
