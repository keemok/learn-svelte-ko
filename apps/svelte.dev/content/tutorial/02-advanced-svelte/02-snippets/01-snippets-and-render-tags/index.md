---
title: Snippet과 render 태그
---

Snippet을 사용하면 별도의 파일로 추출하지 않고도 컴포넌트 내에서 콘텐츠를 재사용할 수 있어요.

이 실습에서는 유니코드 이스케이프 시퀀스와 HTML 엔티티와 함께 [삼원색(세 마리 원숭이)](https://en.wikipedia.org/wiki/Three_wise_monkeys) 표를 만들고 있어요. 지금까지는 원숭이가 하나뿐이에요.

물론 마크업을 복제할 수도 있어요. 또는 `{ emoji, description }` 객체 배열을 만들어서 `{#each ...}` 블록에 전달할 수도 있고요. 하지만 더 깔끔한 해결책은 마크업을 재사용 가능한 블록으로 캡슐화하는 거예요.

먼저 snippet을 선언하세요:

```svelte
/// file: App.svelte
+++{#snippet monkey()}+++
	<tr>
		<td>{emoji}</td>
		<td>{description}</td>
		<td>\u{emoji.charCodeAt(0).toString(16)}\u{emoji.charCodeAt(1).toString(16)}</td>
		<td>&amp#{emoji.codePointAt(0)}</td>
	</tr>
+++{/snippet}+++
```

원숭이는 렌더링하기 전까지는 더 이상 보이지 않아요. 렌더링해봐요:

```svelte
/// file: App.svelte
<tbody>
	{#snippet monkey()}...{/snippet}

	+++{@render monkey()}+++
</tbody>
```

나머지 원숭이들에도 snippet을 사용하려면, snippet에 데이터를 전달해야 해요. Snippet은 0개 이상의 파라미터를 가질 수 있어요:

```svelte
/// file: App.svelte
<tbody>
	+++{#snippet monkey(emoji, description)}...{/snippet}+++

	+++{@render monkey('🙈', 'see no evil')}+++
</tbody>
```

> [!NOTE] 원한다면 구조 분해 파라미터(destructured parameters)도 쓸 수 있어요.

나머지 원숭이들을 추가하세요:

- `'🙈', 'see no evil'`
- `'🙉', 'hear no evil'`
- `'🙊', 'speak no evil'`

마지막으로, 더 이상 필요 없는 `<script>` 블록을 삭제하세요:

```svelte
/// file: App.svelte
---<script>
	let emoji = '🙈';
	let description = 'see no evil';
</script>---
```

> [!NOTE] Snippet은 컴포넌트 어디에나 선언할 수 있지만, 함수처럼 같은 '스코프'나 자식 스코프의 render 태그에서만 볼 수 있어요.
