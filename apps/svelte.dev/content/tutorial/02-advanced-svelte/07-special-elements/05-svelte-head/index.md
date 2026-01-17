---
title: <svelte:head>
---

`<svelte:head>` 요소를 사용하면 문서의 `<head>` 안에 요소를 삽입할 수 있어요. 좋은 SEO에 중요한 `<title>`이나 `<meta>` 태그 같은 것들에 유용해요.

이 튜토리얼의 맥락에서는 그런 걸 보여주기가 꽤 어려우니까, 다른 목적으로 사용할게요. 스타일시트를 로드하는 거죠.

```svelte
/// file: App.svelte
<script>
	const themes = ['margaritaville', 'retrowave', 'spaaaaace', 'halloween'];
	let selected = $state(themes[0]);
</script>

+++<svelte:head>
	<link rel="stylesheet" href="/tutorial/stylesheets/{selected}.css" />
</svelte:head>+++

<h1>Welcome to my site!</h1>
```

> [!NOTE] 서버 사이드 렌더링(SSR) 모드에서 `<svelte:head>`의 내용은 나머지 HTML과 별도로 반환돼요.
