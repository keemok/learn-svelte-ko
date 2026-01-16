---
title: Select 바인딩
---

`<select>` 요소에도 `bind:value`를 쓸 수 있어요:

```svelte
/// file: App.svelte
<select
    +++bind:+++value={selected}
    onchange={() => answer = ''}
>
```

`<option>` 값들이 문자열이 아니라 객체인 걸 주목하세요. Svelte는 상관없어요.

> [!NOTE] `selected`의 초기값을 설정하지 않았기 때문에, 바인딩이 자동으로 기본값(리스트의 첫 번째)으로 설정해요. 하지만 조심하세요. 바인딩이 초기화될 때까지 `selected`는 undefined 상태라서, 템플릿에서 `selected.id` 같은 걸 무작정 참조할 수 없어요.
