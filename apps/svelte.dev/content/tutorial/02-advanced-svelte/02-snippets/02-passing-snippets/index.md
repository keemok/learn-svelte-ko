---
title: 컴포넌트에 snippet 전달하기
---

Snippet은 함수처럼 단순한 값이기 때문에, props로 컴포넌트에 전달할 수 있어요.

이 `<FilteredList>` 컴포넌트를 봐요. 전달받은 `data`를 필터링하는 게 역할이지만, 그 데이터가 어떻게 렌더링되어야 하는지에 대해서는 의견이 없어요. 그건 부모 컴포넌트의 책임이죠.

이미 몇 가지 snippet이 정의돼 있어요. `<FilteredList>`에 전달하는 것부터 시작해봐요:

```svelte
/// file: App.svelte
<FilteredList
	data={colors}
	field="name"
	+++{header}+++
	+++{row}+++
></FilteredList>
```

그다음 반대편에서 `header`와 `row`를 props로 선언하세요:

```svelte
/// file: FilteredList.svelte
<script>
	let { data, field, +++header, row+++ } = $props();

	// ...
</script>
```

마지막으로, 플레이스홀더 콘텐츠를 render 태그로 바꾸세요:

```svelte
/// file: FilteredList.svelte
<div class="header">
	+++{@render header()}+++
</div>

<div class="content">
	{#each filtered as d}
		+++{@render row(d)}+++
	{/each}
</div>
```

이제 `MistyRose`나 `PeachPuff`의 16진수 코드를 외울 필요가 없어요.
