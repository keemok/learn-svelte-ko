---
title: Export
---

`module` script 블록에서 export된 것은 모듈 자체의 export가 돼요. `pauseAll` 함수를 export해봐요:

```svelte
/// file: AudioPlayer.svelte
<script module>
	let current;

+++	export function pauseAll() {
		current?.pause();
	}+++
</script>
```

이제 `App.svelte`에서 `pauseAll`을 import할 수 있어요...

```svelte
/// file: App.svelte
<script>
	import AudioPlayer, +++{ pauseAll }+++ from './AudioPlayer.svelte';
	import { tracks } from './tracks.js';
</script>
```

...그리고 이벤트 핸들러에서 사용할 수 있어요:

```svelte
/// file: App.svelte
<div class="centered">
	{#each tracks as track}
		<AudioPlayer {...track} />
	{/each}

+++	<button onclick={pauseAll}>
		pause all
	</button>+++
</div>
```

> [!NOTE] 기본 export는 가질 수 없어요. 컴포넌트 자체가 기본 export이거든요.
