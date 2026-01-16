---
title: 컴포넌트 스타일
---

자식 컴포넌트 내부의 스타일에 영향을 줘야 할 때가 많아요. 이 박스들을 빨강, 초록, 파랑으로 만들고 싶다고 해봐요.

한 가지 방법은 `:global` CSS 수정자를 쓰는 거예요. 다른 컴포넌트 내부의 요소를 무차별적으로 타겟팅할 수 있어요:

```svelte
/// file: App.svelte
<style>
	.boxes :global(.box:nth-child(1)) {
		background-color: red;
	}

	.boxes :global(.box:nth-child(2)) {
		background-color: green;
	}

	.boxes :global(.box:nth-child(3)) {
		background-color: blue;
	}
</style>
```

하지만 이렇게 하지 말아야 할 이유가 많아요. 우선 엄청 장황해요. 또 취약해요. `Box.svelte`의 구현 세부사항이 바뀌면 선택자가 망가질 수 있어요.

무엇보다도 무례해요. 컴포넌트는 어떤 변수를 props로 노출할지 결정하는 것처럼, 어떤 스타일을 '외부'에서 제어할 수 있을지 스스로 결정할 수 있어야 해요. `:global`은 탈출구로 써야 해요. 최후의 수단이죠.

`Box.svelte` 안에서 `background-color`를 [CSS 커스텀 속성](https://developer.mozilla.org/en-US/docs/Web/CSS/--*)으로 결정되도록 바꿔봐요:

```svelte
/// file: Box.svelte
<style>
	.box {
		width: 5em;
		height: 5em;
		border-radius: 0.5em;
		margin: 0 0 1em 0;
		background-color: +++var(--color, #ddd)+++;
	}
</style>
```

부모 요소(`<div class="boxes">` 같은)가 `--color` 값을 설정할 수 있지만, 개별 컴포넌트에도 설정할 수 있어요:

```svelte
/// file: App.svelte
<div class="boxes">
	<Box +++--color="red"+++ />
	<Box +++--color="green"+++ />
	<Box +++--color="blue"+++ />
</div>
```

값은 다른 속성처럼 동적일 수 있어요.

> [!NOTE] 이 기능은 필요할 때 각 컴포넌트를 `display: contents`가 적용된 요소로 감싸고, 거기에 커스텀 속성을 적용하는 방식으로 작동해요. 요소를 검사하면 이런 마크업을 볼 수 있어요:
>
> ```svelte
> <svelte-css-wrapper style="display: contents; --color: red;">
> 	<!-- contents -->
> </svelte-css-wrapper>
> ```
>
> `display: contents` 때문에 레이아웃에는 영향을 주지 않지만, 추가된 요소가 `.parent > .child` 같은 선택자에 영향을 줄 수 있어요.
