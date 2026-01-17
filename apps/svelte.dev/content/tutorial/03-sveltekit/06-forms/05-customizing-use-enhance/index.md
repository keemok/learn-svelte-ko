---
title: use:enhance 커스터마이징하기
---

`use:enhance`를 사용하면 브라우저의 네이티브 동작을 에뮬레이트하는 것보다 더 나아갈 수 있어요. 콜백을 제공함으로써 **대기 상태**와 **낙관적 UI** 같은 것들을 추가할 수 있어요. 두 액션에 인위적인 지연을 추가해서 느린 네트워크를 시뮬레이션해봐요:

```js
/// file: src/routes/+page.server.js
export const actions = {
	create: async ({ cookies, request }) => {
		+++await new Promise((fulfil) => setTimeout(fulfil, 1000));+++
		...
	},

	delete: async ({ cookies, request }) => {
		+++await new Promise((fulfil) => setTimeout(fulfil, 1000));+++
		...
	}
};
```

항목을 만들거나 삭제하면 이제 UI가 업데이트되기까지 1초가 걸려서, 사용자가 뭔가 잘못했는지 궁금해해요. 이를 해결하기 위해 로컬 상태를 추가하세요...

```svelte
/// file: src/routes/+page.svelte
<script>
	import { fly, slide } from 'svelte/transition';
	import { enhance } from '$app/forms';

	let { data, form } = $props();

+++	let creating = $state(false);
	let deleting = $state([]);+++
</script>
```

...그리고 첫 번째 `use:enhance` 안에서 `creating`을 토글하세요:

```svelte
/// file: src/routes/+page.svelte
<form
	method="POST"
	action="?/create"
+++	use:enhance={() => {
		creating = true;

		return async ({ update }) => {
			await update();
			creating = false;
		};
	}}+++
>
	<label>
		add a todo:
		<input
			+++disabled={creating}+++
			name="description"
			value={form?.description ?? ''}
			autocomplete="off"
			required
		/>
	</label>
</form>
```

그러면 데이터를 저장하는 동안 메시지를 표시할 수 있어요:

```svelte
/// file: src/routes/+page.svelte
<ul class="todos">
	<!-- ... -->
</ul>

+++{#if creating}
	<span class="saving">saving...</span>
{/if}+++
```

삭제의 경우, 실제로 서버가 뭔가를 검증하기를 기다릴 필요가 없어요. 즉시 UI를 업데이트하면 돼요:

```svelte
/// file: src/routes/+page.svelte
<ul class="todos">
	{#each +++data.todos.filter((todo) => !deleting.includes(todo.id))+++ as todo (todo.id)}
		<li in:fly={{ y: 20 }} out:slide>
			<form
				method="POST"
				action="?/delete"
				+++use:enhance={() => {
					deleting = [...deleting, todo.id];
					return async ({ update }) => {
						await update();
						deleting = deleting.filter((id) => id !== todo.id);
					};
				}}+++
			>
				<input type="hidden" name="id" value={todo.id} />
				<button aria-label="Mark as complete">✔</button>

				{todo.description}
			</form>
		</li>
	{/each}
</ul>
```

> [!NOTE] `use:enhance`는 매우 커스터마이징 가능해요. 제출을 `cancel()` 하고, 리다이렉트를 처리하고, 폼이 리셋되는지 제어할 수 있어요. 자세한 내용은 [문서를 참고하세요](/docs/kit/$app-forms#enhance).
