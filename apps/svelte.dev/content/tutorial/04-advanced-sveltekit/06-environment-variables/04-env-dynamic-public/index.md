---
title: $env/dynamic/public
---

[private 환경 변수](/tutorial/kit/env-static-private)처럼, 가능하면 정적 값을 사용하는 게 바람직하지만, 필요하다면 대신 동적 값을 사용할 수 있어요:

```svelte
/// file: src/routes/+page.svelte
<script>
	import { +++env+++ } from '$env/+++dynamic+++/public';
</script>

<main
	style:background={+++env.+++PUBLIC_THEME_BACKGROUND}
	style:color={+++env.+++PUBLIC_THEME_FOREGROUND}
>
	{+++env.+++PUBLIC_THEME_FOREGROUND} on {+++env.+++PUBLIC_THEME_BACKGROUND}
</main>
```
