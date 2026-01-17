---
title: 이름이 있는 폼 액션
---

실제로 단일 액션만 있는 페이지는 꽤 드물어요. 대부분의 경우 페이지에 여러 액션이 필요해요. 이 앱에서 할 일을 만드는 것만으로는 충분하지 않아요. 완료되면 삭제하고 싶거든요.

`default` 액션을 이름이 있는 `create`와 `delete` 액션으로 교체하는 것부터 시작해요:

```js
/// file: src/routes/+page.server.js
export const actions = {
	+++create+++: async ({ cookies, request }) => {
		const data = await request.formData();
		db.createTodo(cookies.get('userid'), data.get('description'));
	}+++,+++

+++	delete: async ({ cookies, request }) => {
		const data = await request.formData();
		db.deleteTodo(cookies.get('userid'), data.get('id'));
	}+++
};
```

> [!NOTE] 기본 액션은 이름이 있는 액션과 공존할 수 없어요.

`<form>` 요소는 `<a>` 요소의 `href` 속성과 비슷한 선택적 `action` 속성을 가지고 있어요. 기존 폼을 업데이트해서 새 `create` 액션을 가리키도록 하세요:

```svelte
/// file: src/routes/+page.svelte
<form method="POST" +++action="?/create"+++>
	<label>
		add a todo:
		<input
			name="description"
			autocomplete="off"
		/>
	</label>
</form>
```

> [!NOTE] `action` 속성은 어떤 URL이든 될 수 있어요. 액션이 다른 페이지에 정의돼 있다면 `/todos?/create` 같은 걸 가질 수도 있어요. 액션이 이 페이지에 있으니까 경로명을 완전히 생략할 수 있고, 그래서 앞에 `?` 문자가 있어요.

다음으로, 각 할 일에 대한 폼을 만들고 싶어요. 고유하게 식별하는 숨겨진 `<input>`과 함께요:

```svelte
/// file: src/routes/+page.svelte
<ul class="todos">
	{#each data.todos as todo (todo.id)}
		<li>
+++			<form method="POST" action="?/delete">
				<input type="hidden" name="id" value={todo.id} />
				<span>{todo.description}</span>
				<button aria-label="Mark as complete"></button>
			</form>+++
		</li>
	{/each}
</ul>
```
