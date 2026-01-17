---
title: 지연된 트랜지션
---

Svelte의 트랜지션 엔진에서 특히 강력한 기능은 트랜지션을 지연(defer)시켜서 여러 요소 간에 조정할 수 있다는 거예요.

이 한 쌍의 할 일 목록을 봐요. 할 일을 토글하면 반대편 목록으로 보내져요. 현실에서 객체는 그렇게 작동하지 않아요. 다른 곳에서 사라지고 다시 나타나는 대신, 일련의 중간 위치를 거쳐 이동하죠. 모션을 사용하면 사용자가 앱에서 무슨 일이 일어나고 있는지 이해하는 데 큰 도움이 돼요.

`transition.js`에 있는 `crossfade` 함수를 사용해서 이 효과를 달성할 수 있어요. 이 함수는 `send`와 `receive`라는 한 쌍의 트랜지션을 생성해요. 요소가 '전송(send)'될 때, 대응하는 '수신(receive)'되는 요소를 찾아서 요소를 상대방의 위치로 변환하고 페이드 아웃하는 트랜지션을 생성해요. 요소가 '수신'될 때는 반대로 일어나요. 상대방이 없으면 `fallback` 트랜지션이 사용돼요.

`TodoList.svelte`를 열어보세요. 먼저 transition.js에서 `send`와 `receive` 트랜지션을 import하세요:

```svelte
/// file: TodoList.svelte
<script>
	+++import { send, receive } from './transition.js';+++

	let { todos, remove } = $props();
</script>
```

그다음 `<li>` 요소에 추가하되, `todo.id` 속성을 요소를 매칭하기 위한 키로 사용하세요:

```svelte
/// file: TodoList.svelte
<li
	class={{ done: todo.done }}
	+++in:receive={{ key: todo.id }}+++
	+++out:send={{ key: todo.id }}+++
>
```

이제 항목을 토글하면 새 위치로 부드럽게 이동해요. 트랜지션되지 않는 항목들은 여전히 어색하게 튀어요. 다음 실습에서 고칠 수 있어요.
