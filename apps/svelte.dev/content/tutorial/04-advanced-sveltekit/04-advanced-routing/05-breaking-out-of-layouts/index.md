---
title: 레이아웃에서 벗어나기
editing_constraints:
  { 'create': ['/src/routes/a/b/c/+page@b.svelte', '/src/routes/a/b/c/+page@a.svelte'] }
---

일반적으로 페이지는 위의 모든 레이아웃을 상속받아요. 즉, `src/routes/a/b/c/+page.svelte`는 네 개의 레이아웃을 상속받아요:

- `src/routes/+layout.svelte`
- `src/routes/a/+layout.svelte`
- `src/routes/a/b/+layout.svelte`
- `src/routes/a/b/c/+layout.svelte`

때때로 현재 레이아웃 계층에서 벗어나는 게 유용해요. '재설정'할 부모 세그먼트의 이름 뒤에 `@` 기호를 추가해서 그렇게 할 수 있어요. 예를 들어 `+page@b.svelte`는 `/a/b/c`를 `src/routes/a/b/+layout.svelte` 안에 넣을 거고, `+page@a.svelte`는 `src/routes/a/+layout.svelte` 안에 넣을 거예요.

`+page@.svelte`로 이름을 바꿔서 루트 레이아웃까지 완전히 재설정해봐요.

> [!NOTE] 루트 레이아웃은 앱의 모든 페이지에 적용돼요. 거기서 벗어날 수 없어요.
