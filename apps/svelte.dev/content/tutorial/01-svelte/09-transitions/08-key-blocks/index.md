---
title: Key 블록
---

Key 블록은 표현식의 값이 변경될 때 내용을 파괴하고 다시 생성해요. 요소가 DOM에 들어오거나 나갈 때만이 아니라 값이 변경될 때마다 트랜지션을 재생하고 싶을 때 유용해요.

예를 들어, 여기서는 로딩 메시지(즉, `i`)가 변경될 때마다 `transition.js`의 `typewriter` 트랜지션을 재생하고 싶어요. `<p>` 요소를 key 블록으로 감싸세요:

```svelte
/// file: App.svelte
+++{#key i}+++
	<p in:typewriter={{ speed: 10 }}>
		{messages[i] || ''}
	</p>
+++{/key}+++
```
