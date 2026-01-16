---
title: 파라미터 추가하기
---

트랜지션 함수는 파라미터를 받을 수 있어요. `fade` 트랜지션을 `fly`로 바꿔보세요...

```svelte
/// file: App.svelte
<script>
	import { +++fly+++ } from 'svelte/transition';

	let visible = $state(true);
</script>
```

...그리고 몇 가지 옵션과 함께 `<p>`에 적용하세요:

```svelte
/// file: App.svelte
<p transition:+++fly={{ y: 200, duration: 2000 }}+++>
	+++Flies+++ in and out
</p>
```

트랜지션이 역전 가능(reversible)하다는 걸 주목하세요. 트랜지션이 진행 중일 때 체크박스를 토글하면, 처음이나 끝이 아니라 현재 지점에서부터 전환돼요.
