---
title: 다중 선택
---

`<select>` 요소는 `multiple` 속성을 가질 수 있어요. 이 경우 단일 값을 선택하는 대신 배열을 채워요.

체크박스를 `<select multiple>`로 바꿔보세요:

```svelte
/// file: App.svelte
<h2>Flavours</h2>

+++<select multiple bind:value={flavours}>+++
	{#each ['cookies and cream', 'mint choc chip', 'raspberry ripple'] as flavour}
+++		<option>{flavour}</option>+++
	{/each}
+++</select>+++
```

`<option>`의 `value` 속성을 생략할 수 있다는 걸 주목하세요. 값이 요소의 내용과 동일하니까요.

> [!NOTE] 여러 옵션을 선택하려면 `control` 키(MacOS에서는 `command` 키)를 누른 채로 하세요.
