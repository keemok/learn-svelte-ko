---
title: 숫자 입력
---

DOM에서는 모든 입력 값이 문자열이에요. 숫자 입력(`type="number"`나 `type="range"`)을 다룰 때는 불편해요. 사용하기 전에 `input.value`를 강제 변환해야 하거든요.

`bind:value`를 쓰면 Svelte가 알아서 처리해줘요:

```svelte
/// file: App.svelte
<label>
	<input type="number" +++bind:+++value={a} min="0" max="10" />
	<input type="range" +++bind:+++value={a} min="0" max="10" />
</label>

<label>
	<input type="number" +++bind:+++value={b} min="0" max="10" />
	<input type="range" +++bind:+++value={b} min="0" max="10" />
</label>
```
