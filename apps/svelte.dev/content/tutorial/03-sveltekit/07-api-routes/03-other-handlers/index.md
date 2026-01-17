---
title: 다른 핸들러
---

비슷하게, 다른 HTTP 동사에 대한 핸들러도 추가할 수 있어요. `src/lib/server/database.js`의 `toggleTodo`와 `deleteTodo` 함수를 사용해서 할 일을 토글하고 제거하는 `PUT`과 `DELETE` 핸들러가 있는 `src/routes/todo/[id]/+server.js` 파일을 만들어서 `/todo/[id]` 라우트를 추가하세요:

```js
/// file: src/routes/todo/[id]/+server.js
import * as database from '$lib/server/database.js';

export async function PUT({ params, request, cookies }) {
	const { done } = await request.json();
	const userid = cookies.get('userid');

	await database.toggleTodo({ userid, id: params.id, done });
	return new Response(null, { status: 204 });
}

export async function DELETE({ params, cookies }) {
	const userid = cookies.get('userid');

	await database.deleteTodo({ userid, id: params.id });
	return new Response(null, { status: 204 });
}
```

브라우저에 실제 데이터를 반환할 필요가 없기 때문에, [204 No Content](https://http.dog/204) 상태의 빈 [Response](https://developer.mozilla.org/en-US/docs/Web/API/Response)를 반환하고 있어요.

이제 이벤트 핸들러 안에서 이 엔드포인트와 상호작용할 수 있어요:

```svelte
/// file: src/routes/+page.svelte
<label>
	<input
		type="checkbox"
		checked={todo.done}
		onchange={async (e) => {
			const done = e.currentTarget.checked;

+++			await fetch(`/todo/${todo.id}`, {
				method: 'PUT',
				body: JSON.stringify({ done }),
				headers: {
					'Content-Type': 'application/json'
				}
			});+++
		}}
	/>
	<span>{todo.description}</span>
	<button
		aria-label="Mark as complete"
		onclick={async (e) => {
+++			await fetch(`/todo/${todo.id}`, {
				method: 'DELETE'
			});

			const todos = data.todos.filter((t) => t !== todo);

			data = { ...data, todos };+++
		}}
	></button>
</label>
```
