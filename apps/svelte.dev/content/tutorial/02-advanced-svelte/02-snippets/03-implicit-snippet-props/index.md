---
title: 암시적 snippet props
---

작성 편의를 위해, 컴포넌트 내부에 직접 선언된 snippet은 해당 컴포넌트의 props가 돼요. `header`와 `row` snippet을 `<FilteredList>` 안으로 옮겨봐요:

```svelte
/// file: App.svelte
<FilteredList
	data={colors}
	field="name"
	{header}
	{row}
>
	+++{#snippet header()}...{/snippet}+++

	+++{#snippet row(d)}...{/snippet}+++
</FilteredList>

---{#snippet header()}...{/snippet}---

---{#snippet row(d)}...{/snippet}---
```

이제 명시적 props에서 제거할 수 있어요:

```svelte
/// file: App.svelte
<FilteredList data={colors} field="name" ---{header} {row}--->
	{#snippet header()}...{/snippet}

	{#snippet row(d)}...{/snippet}
</FilteredList>
```

선언된 snippet의 일부가 아닌 컴포넌트 내부의 모든 콘텐츠는 특별한 `children` snippet이 돼요. `header`는 파라미터가 없으니까, 블록 태그를 제거해서 `children`으로 바꿀 수 있어요...

```svelte
/// file: App.svelte
---{#snippet header()}---
<header>
	<span class="color"></span>
	<span class="name">name</span>
	<span class="hex">hex</span>
	<span class="rgb">rgb</span>
	<span class="hsl">hsl</span>
</header>
---{/snippet}---
```

...그리고 반대편에서 `header` prop을 `children`으로 이름을 바꾸세요:

```svelte
/// file: FilteredList.svelte
<script>
	let { data, field, +++children+++, row } = $props();

	// ...
</script>
```

```svelte
/// file: FilteredList.svelte
<div class="header">
	+++{@render children()}+++
</div>
```
