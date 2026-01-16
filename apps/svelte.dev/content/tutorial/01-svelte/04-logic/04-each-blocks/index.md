---
title: Each 블록
---

사용자 인터페이스를 만들다 보면 데이터 리스트를 다룰 일이 많아요. 이 실습에서는 `<button>` 마크업을 여러 번 반복했어요. 매번 색상을 바꿨지만, 아직 추가할 게 더 있죠.

힘들게 복사, 붙여넣기, 수정하는 대신에, 첫 번째 버튼만 남기고 나머지는 지운 다음 `each` 블록을 쓸 수 있어요:

```svelte
/// file: App.svelte
<div>
	+++{#each colors as color}+++
		<button
			style="background: red"
			aria-label="red"
			aria-current={selected === 'red'}
			onclick={() => selected = 'red'}
		></button>
	+++{/each}+++
</div>
```

> [!NOTE] 표현식(여기서는 `colors`)은 반복 가능한(iterable) 객체나 배열 같은 객체면 뭐든 돼요. 즉, [`Array.from`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from)과 작동하는 것이면 다 가능해요.

이제 `"red"` 자리에 `color` 변수를 써야 해요:

```svelte
/// file: App.svelte
<div>
	{#each colors as color}
		<button
			style="background: +++{color}+++"
			aria-label=+++{color}+++
			aria-current={selected === +++color+++}
			onclick={() => selected = +++color+++}
		></button>
	{/each}
</div>
```

두 번째 인자로 현재 인덱스를 가져올 수도 있어요:

```svelte
/// file: App.svelte
<div>
	{#each colors as color, +++i}+++
		<button
			style="background: {color}"
			aria-label={color}
			aria-current={selected === color}
			onclick={() => selected = color}
		>+++{i + 1}+++</button>
	{/each}
</div>
```
