---
title: <svelte:boundary>
---

에러가 앱을 망가진 상태로 두는 걸 방지하려면, `<svelte:boundary>` 요소를 사용해서 에러 경계(error boundary) 안에 에러를 담을 수 있어요.

이 예제에서 `<FlakyComponent>`에는 버그가 있어요. 버튼을 클릭하면 `mouse`가 `null`로 설정되는데, 템플릿의 `{mouse.x}`와 `{mouse.y}` 표현식이 렌더링에 실패한다는 의미죠.

이상적인 세상에서는 그냥 버그를 고치면 돼요. 하지만 항상 그럴 수 있는 건 아니에요. 때로는 컴포넌트가 다른 사람 것이고, 때로는 예상치 못한 것에 대비해야 할 때도 있죠. `<FlakyComponent />`를 `<svelte:boundary>`로 감싸는 것부터 시작하세요:

```svelte
<!--- file: App.svelte --->
+++<svelte:boundary>+++
	<FlakyComponent />
+++</svelte:boundary>+++
```

지금까지는 아무것도 바뀌지 않았어요. 경계가 핸들러를 지정하지 않았거든요. 에러가 발생했을 때 표시할 UI를 제공하기 위해 `failed` [snippet](snippets-and-render-tags)을 추가하세요:

```svelte
<!--- file: App.svelte --->
<svelte:boundary>
	<FlakyComponent />

+++	{#snippet failed(error)}
		<p>Oops! {error.message}</p>
	{/snippet}+++
</svelte:boundary>
```

이제 버튼을 클릭하면 경계의 내용이 snippet으로 대체돼요. `failed`에 전달되는 두 번째 인자를 사용해서 리셋을 시도할 수 있어요:

```svelte
<!--- file: App.svelte --->
<svelte:boundary>
	<FlakyComponent />

	{#snippet failed(error+++, reset+++)}
		<p>Oops! {error.message}</p>
		+++<button onclick={reset}>Reset</button>+++
	{/snippet}
</svelte:boundary>
```

`onerror` 핸들러도 지정할 수 있어요. `failed` snippet에 전달된 것과 같은 인자로 호출돼요:

```svelte
<!--- file: App.svelte --->
<svelte:boundary +++onerror={(e) => console.error(e)}+++>
	<FlakyComponent />

	{#snippet failed(error, reset)}
		<p>Oops! {error.message}</p>
		<button onclick={reset}>Reset</button>
	{/snippet}
</svelte:boundary>
```

이건 에러에 대한 정보를 리포팅 서비스에 보내거나, 에러 경계 자체 밖에 UI를 추가하는 데 유용해요.
