---
title: POST 핸들러
---

`POST` 같이 데이터를 변경하는 핸들러도 추가할 수 있어요. 대부분의 경우 [폼 액션](the-form-element)을 대신 사용해야 해요. 더 적은 코드를 작성하게 되고, JavaScript 없이도 작동해서 더 탄력적이거든요.

'add a todo' `<input>`의 `keydown` 이벤트 핸들러 안에서 서버에 데이터를 POST해봐요:

```svelte
/// file: src/routes/+page.svelte
<input
	type="text"
	autocomplete="off"
	onkeydown={async (e) => {
		if (e.key !== 'Enter') return;

		const input = e.currentTarget;
		const description = input.value;

+++		const response = await fetch('/todo', {
			method: 'POST',
			body: JSON.stringify({ description }),
			headers: {
				'Content-Type': 'application/json'
			}
		});+++

		input.value = '';
	}}
/>
```

여기서 우리는 사용자의 쿠키에서 `userid`를 사용해서 `/todo` API 라우트에 JSON을 POST하고, 응답으로 새로 생성된 할 일의 `id`를 받아요.

`src/lib/server/database.js`의 `createTodo`를 호출하는 `POST` 핸들러가 있는 `src/routes/todo/+server.js` 파일을 추가해서 `/todo` 라우트를 만드세요:

```js
/// file: src/routes/todo/+server.js
import { json } from '@sveltejs/kit';
import * as database from '$lib/server/database.js';

export async function POST({ request, cookies }) {
	const { description } = await request.json();

	const userid = cookies.get('userid');
	const { id } = await database.createTodo({ userid, description });

	return json({ id }, { status: 201 });
}
```

`load` 함수와 폼 액션처럼, `request`는 표준 [Request](https://developer.mozilla.org/en-US/docs/Web/API/Request) 객체예요. `await request.json()`은 이벤트 핸들러에서 POST한 데이터를 반환해요.

우리는 [201 Created](https://http.dog/201) 상태와 데이터베이스에 새로 생성된 할 일의 `id`로 응답을 반환하고 있어요. 이벤트 핸들러로 돌아가서, 이걸 사용해서 페이지를 업데이트할 수 있어요:

```svelte
/// file: src/routes/+page.svelte
<input
	type="text"
	autocomplete="off"
	onkeydown={async (e) => {
		if (e.key !== 'Enter') return;

		const input = e.currentTarget;
		const description = input.value;

		const response = await fetch('/todo', {
			method: 'POST',
			body: JSON.stringify({ description }),
			headers: {
				'Content-Type': 'application/json'
			}
		});

+++		const { id } = await response.json();

		const todos = [...data.todos, {
			id,
			description
		}];

		data = { ...data, todos };+++

		input.value = '';
	}}
/>
```

> [!NOTE] 페이지를 새로고침해서 얻을 수 있는 것과 같은 결과를 얻을 수 있는 방식으로만 `data`를 업데이트해야 해요. `data` prop은 깊게(deeply) 반응형이 아니기 때문에 교체해야 해요. `data.todos = todos` 같은 변경은 재렌더링을 일으키지 않아요.
