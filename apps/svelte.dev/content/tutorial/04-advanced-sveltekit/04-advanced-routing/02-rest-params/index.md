---
title: 나머지 파라미터
path: /how
focus: /src/routes/[path]/+page.svelte
---

알 수 없는 수의 경로 세그먼트와 매칭하려면 `[...rest]` 파라미터를 사용하세요. [JavaScript의 나머지 파라미터](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)와 닮아서 그렇게 이름 붙여졌어요.

`src/routes/[path]`를 `src/routes/[...path]`로 이름을 바꾸세요. 이제 라우트가 모든 경로와 매칭돼요.

> [!NOTE] 다른 더 구체적인 라우트가 먼저 테스트되기 때문에, 나머지 파라미터는 '모두 잡는(catch-all)' 라우트로 유용해요. 예를 들어, `/categories/...` 안의 페이지에 대한 커스텀 404 페이지가 필요하다면, 다음 파일들을 추가할 수 있어요:
>
> ```tree
> src/routes/
> ├ categories/
> │ ├ animal/
> │ ├ mineral/
> │ ├ vegetable/
> +++│ ├ [...catchall]/
> │ │ ├ +error.svelte
> │ │ └ +page.server.js+++
> ```
>
> `+page.server.js` 파일 안에서 `load` 안에 `error(404)`를 넣으세요.

나머지 파라미터는 끝에 갈 필요가 없어요. `/items/[...path]/edit`나 `/items/[...path].json` 같은 라우트는 완전히 유효해요.
