---
title: 그룹 입력
---

같은 값과 관련된 여러 개의 `type="radio"`나 `type="checkbox"` 입력이 있다면, `value` 속성과 함께 `bind:group`을 쓸 수 있어요. 같은 그룹의 라디오 입력은 상호 배타적이고, 같은 그룹의 체크박스 입력은 선택된 값들의 배열을 만들어요.

라디오 입력에 `bind:group={scoops}`를 추가하세요...

```svelte
/// file: App.svelte
<input
	type="radio"
	name="scoops"
	value={number}
	+++bind:group={scoops}+++
/>
```

...그리고 체크박스 입력에 `bind:group={flavours}`를 추가하세요:

```svelte
/// file: App.svelte
<input
	type="checkbox"
	name="flavours"
	value={flavour}
	+++bind:group={flavours}+++
/>
```
