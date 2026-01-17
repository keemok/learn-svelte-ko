---
title: <svelte:element>
---

어떤 요소를 렌더링해야 할지 미리 알 수 없을 때가 있어요. 긴 `{#if ...}` 블록 목록을 갖는 대신...

```svelte
/// file: App.svelte
{#if selected === 'h1'}
	<h1>I'm a <code>&lt;h1&gt;</code> element</h1>
{:else}
	<p>TODO others</p>
{/if}
```

...`<svelte:element>`를 쓸 수 있어요:

```svelte
/// file: App.svelte
+++<svelte:element this={selected}>
	I'm a <code>&lt;{selected}&gt;</code> element
</svelte:element>+++
```

`this` 값은 어떤 문자열이든 될 수 있고, falsy 값도 가능해요. falsy면 아무 요소도 렌더링되지 않아요.
