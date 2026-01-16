---
title: In과 out
---

`transition` 디렉티브 대신, 요소는 `in`이나 `out` 디렉티브를 가질 수 있어요. 둘 다 함께 쓸 수도 있고요. `fly`와 함께 `fade`를 import하세요...

```js
/// file: App.svelte
import { +++fade+++, fly } from 'svelte/transition';
```

...그다음 `transition` 디렉티브를 `in`과 `out` 디렉티브로 분리하세요:

```svelte
/// file: App.svelte
<p +++in+++:fly={{ y: 200, duration: 2000 }} +++out:fade+++>
	Flies in, +++fades out+++
</p>
```

이 경우에는 트랜지션이 역전되지 않아요.
