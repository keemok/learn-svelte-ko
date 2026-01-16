---
title: Textarea 입력
---

`<textarea>` 요소는 Svelte에서 텍스트 입력과 비슷하게 작동해요. `bind:value`를 쓰면 돼요:

```svelte
/// file: App.svelte
<textarea +++bind:value=+++{value}></textarea>
```

이런 경우처럼 이름이 일치하면 단축 표기법도 쓸 수 있어요:

```svelte
/// file: App.svelte
<textarea +++bind:value+++></textarea>
```

이건 `<textarea>` 바인딩뿐만 아니라 모든 바인딩에 적용돼요.
