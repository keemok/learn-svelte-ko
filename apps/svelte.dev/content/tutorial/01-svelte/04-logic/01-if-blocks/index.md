---
title: If 블록
---

HTML에는 조건문이나 반복문 같은 로직을 표현하는 방법이 없어요. Svelte에는 있죠.

조건부로 마크업을 렌더링하려면 `if` 블록으로 감싸면 돼요. `count`가 `10`보다 클 때 나타나는 텍스트를 추가해봐요:

```svelte
/// file: App.svelte
<button onclick={increment}>
	Clicked {count}
	{count === 1 ? 'time' : 'times'}
</button>

+++{#if count > 10}
	<p>{count} is greater than 10</p>
{/if}+++
```

시도해보세요. 컴포넌트를 업데이트하고 버튼을 몇 번 클릭해봐요.
