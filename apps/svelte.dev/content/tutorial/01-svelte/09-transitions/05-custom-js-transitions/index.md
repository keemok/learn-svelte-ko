---
title: 커스텀 JS 트랜지션
---

일반적으로 트랜지션에는 가능한 한 CSS를 사용해야 하지만, 타자기 효과처럼 JavaScript 없이는 달성할 수 없는 효과도 있어요:

```js
/// file: App.svelte
function typewriter(node, { speed = 1 }) {
	const valid = node.childNodes.length === 1 && node.childNodes[0].nodeType === Node.TEXT_NODE;

	if (!valid) {
		throw new Error(`This transition only works on elements with a single text node child`);
	}

	+++const text = node.textContent;
	const duration = text.length / (speed * 0.01);

	return {
		duration,
		tick: (t) => {
			const i = Math.trunc(text.length * t);
			node.textContent = text.slice(0, i);
		}
	};+++
}
```
