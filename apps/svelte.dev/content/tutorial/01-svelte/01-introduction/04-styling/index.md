---
title: 스타일링
---

HTML처럼 컴포넌트에도 `<style>` 태그를 넣을 수 있어요. `<p>` 요소에 스타일을 적용해봐요:

```svelte
/// file: App.svelte
<p>This is a paragraph.</p>

<style>
+++	p {
		color: goldenrod;
		font-family: 'Comic Sans MS', cursive;
		font-size: 2em;
	}+++
</style>
```

중요한 건 이 스타일 규칙이 이 컴포넌트 안에서만 적용된다는 거예요. 다음 단계에서 보겠지만, 앱의 다른 곳에 있는 `<p>` 요소에는 영향을 주지 않아요.
