---
title: Else 블록
---

JavaScript처럼 `if` 블록에는 `else` 블록을 붙일 수 있어요:

```svelte
/// file: App.svelte
{#if count > 10}
	<p>{count} is greater than 10</p>
+++{:else}
	<p>{count} is between 0 and 10</p>+++
{/if}
```

`{#...}`는 블록을 열어요. `{/...}`는 블록을 닫아요. `{:...}`는 블록을 이어가요. 축하해요! 이제 Svelte가 HTML에 추가한 문법을 거의 다 배웠어요.
