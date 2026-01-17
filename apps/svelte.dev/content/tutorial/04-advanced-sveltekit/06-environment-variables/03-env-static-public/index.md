---
title: $env/static/public
---

일부 환경 변수는 브라우저에 안전하게 노출될 수 있어요. 이것들은 `PUBLIC_` 접두사로 private 환경 변수와 구별돼요.

`.env`의 두 public 환경 변수에 값을 추가하세요:

```env
/// file: .env
PUBLIC_THEME_BACKGROUND=+++"steelblue"+++
PUBLIC_THEME_FOREGROUND=+++"bisque"+++
```

그런 다음, `src/routes/+page.svelte`에 import하세요:

```svelte
/// file: src/routes/+page.svelte
<script>
---	const PUBLIC_THEME_BACKGROUND = 'white';
	const PUBLIC_THEME_FOREGROUND = 'black';---
+++	import {
		PUBLIC_THEME_BACKGROUND,
		PUBLIC_THEME_FOREGROUND
	} from '$env/static/public';+++
</script>
```
