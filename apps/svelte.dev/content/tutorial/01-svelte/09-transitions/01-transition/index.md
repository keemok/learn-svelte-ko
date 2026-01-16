---
title: transition 디렉티브
---

요소가 DOM에 들어오고 나갈 때 부드럽게 전환되도록 하면 더 매력적인 사용자 인터페이스를 만들 수 있어요. Svelte는 `transition` 디렉티브로 이걸 아주 쉽게 만들어줘요.

먼저 `svelte/transition`에서 `fade` 함수를 import하세요...

```svelte
/// file: App.svelte
<script>
	+++import { fade } from 'svelte/transition';+++

	let visible = $state(true);
</script>
```

...그다음 `<p>` 요소에 추가하세요:

```svelte
/// file: App.svelte
<p +++transition:fade+++>
	Fades in and out
</p>
```
