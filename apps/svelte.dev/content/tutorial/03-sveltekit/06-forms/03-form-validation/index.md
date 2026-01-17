---
title: 검증
---

사용자는 장난스러운 무리라서, 기회가 주어지면 온갖 말도 안 되는 데이터를 제출할 거예요. 그들이 혼란을 일으키지 못하도록 폼 데이터를 검증하는 게 중요해요.

첫 번째 방어선은 브라우저의 [내장 폼 검증](https://developer.mozilla.org/en-US/docs/Learn/Forms/Form_validation#using_built-in_form_validation)이에요. 예를 들어 `<input>`을 필수로 표시하기 쉽게 만들어주죠:

```svelte
/// file: src/routes/+page.svelte
<form method="POST" action="?/create">
	<label>
		add a todo
		<input
			name="description"
			autocomplete="off"
			+++required+++
		/>
	</label>
</form>
```

`<input>`이 비어있는 동안 Enter를 쳐보세요.

이런 종류의 검증은 유용하지만 불충분해요. 일부 검증 규칙(예: 고유성)은 `<input>` 속성으로 표현할 수 없고, 어쨌든 사용자가 엘리트 해커라면 브라우저의 개발자 도구를 사용해서 속성을 간단히 삭제할 수 있어요. 이런 종류의 장난질을 방지하려면 항상 서버 사이드 검증을 사용해야 해요.

`src/lib/server/database.js`에서 설명이 존재하고 고유한지 검증하세요:

```js
/// file: src/lib/server/database.js
export function createTodo(userid, description) {
+++	if (description === '') {
		throw new Error('todo must have a description');
	}+++

	const todos = db.get(userid);

+++	if (todos.find((todo) => todo.description === description)) {
		throw new Error('todos must be unique');
	}+++

	todos.push({
		id: crypto.randomUUID(),
		description,
		done: false
	});
}
```

중복된 할 일을 제출해보세요. 이런! SvelteKit이 우리를 불친절하게 보이는 에러 페이지로 데려가요. 서버에서는 'todos must be unique' 에러를 보지만, SvelteKit은 예상치 못한 에러 메시지를 사용자로부터 숨겨요. 종종 민감한 데이터를 포함하거든요.

같은 페이지에 머물면서 무엇이 잘못됐는지 표시해서 사용자가 고칠 수 있게 하는 게 훨씬 나아요. 이를 위해 `fail` 함수를 사용해서 적절한 HTTP 상태 코드와 함께 액션에서 데이터를 반환할 수 있어요:

```js
/// file: src/routes/+page.server.js
+++import { fail } from '@sveltejs/kit';+++
import * as db from '$lib/server/database.js';

export function load({ cookies }) {...}

export const actions = {
	create: async ({ cookies, request }) => {
		const data = await request.formData();

+++		try {+++
			db.createTodo(cookies.get('userid'), data.get('description'));
+++		} catch (error) {
			return fail(422, {
				description: data.get('description'),
				error: error.message
			});
		}+++
	}
```

`src/routes/+page.svelte`에서 `form` prop을 통해 반환된 값에 접근할 수 있어요. 이건 폼 제출 후에만 채워져요:

```svelte
/// file: src/routes/+page.svelte
<script>
	let { data, +++form+++ } = $props();
</script>

<div class="centered">
	<h1>todos</h1>

	+++{#if form?.error}
		<p class="error">{form.error}</p>
	{/if}+++

	<form method="POST" action="?/create">
		<label>
			add a todo:
			<input
				name="description"
				+++value={form?.description ?? ''}+++
				autocomplete="off"
				required
			/>
		</label>
	</form>
```

> [!NOTE] `fail`로 감싸지 않고 액션에서 데이터를 반환할 수도 있어요. 예를 들어 데이터가 저장됐을 때 'success!' 메시지를 보여주기 위해요. 그러면 `form` prop을 통해 사용 가능해요.
