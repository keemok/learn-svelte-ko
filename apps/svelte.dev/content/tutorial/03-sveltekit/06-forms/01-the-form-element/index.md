---
title: <form> 요소
---

[데이터 로딩](page-data) 챕터에서 서버에서 브라우저로 데이터를 가져오는 방법을 봤어요. 때로는 반대 방향으로 데이터를 보내야 하는데, 그때 데이터를 제출하는 웹 플랫폼의 방법인 `<form>`이 등장해요.

할 일 앱을 만들어봐요. `src/lib/server/database.js`에 이미 인메모리 데이터베이스가 설정돼 있고, `src/routes/+page.server.js`의 `load` 함수는 [`cookies`](/docs/kit/load#Cookies) API를 사용해서 사용자별 할 일 목록을 가질 수 있지만, 새 할 일을 만들기 위한 `<form>`을 추가해야 해요:

```svelte
/// file: src/routes/+page.svelte
<h1>todos</h1>

+++<form method="POST">
	<label>
		add a todo:
		<input
			name="description"
			autocomplete="off"
		/>
	</label>
</form>+++

<ul class="todos">
```

`<input>`에 뭔가 입력하고 Enter를 치면, 브라우저가 현재 페이지로 POST 요청을 만들어요 (`method="POST"` 속성 때문에). 하지만 POST 요청을 처리할 서버 사이드 액션(action)을 만들지 않았기 때문에 에러가 발생해요. 지금 만들어봐요:

```js
/// file: src/routes/+page.server.js
import * as db from '$lib/server/database.js';

export function load({ cookies }) {
	// ...
}

+++export const actions = {
	default: async ({ cookies, request }) => {
		const data = await request.formData();
		db.createTodo(cookies.get('userid'), data.get('description'));
	}
};+++
```

`request`는 표준 [Request](https://developer.mozilla.org/en-US/docs/Web/API/Request) 객체예요. `await request.formData()`는 [`FormData`](https://developer.mozilla.org/en-US/docs/Web/API/FormData) 인스턴스를 반환해요.

Enter를 치면 데이터베이스가 업데이트되고 페이지가 새 데이터로 새로고침돼요.

`fetch` 코드나 그런 걸 전혀 작성하지 않았다는 걸 주목하세요. 데이터가 자동으로 업데이트돼요. 그리고 `<form>` 요소를 사용하고 있기 때문에, 이 앱은 JavaScript가 비활성화되거나 사용 불가능해도 작동해요.
