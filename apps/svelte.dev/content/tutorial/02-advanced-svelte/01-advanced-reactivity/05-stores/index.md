---
title: 스토어(Stores)
---

Svelte 5에 룬(rune)이 도입되기 전에는, 스토어가 컴포넌트 외부의 반응형 상태를 다루는 관용적인 방법이었어요. 이제는 더 이상 그렇지 않지만, Svelte를 사용할 때(지금은 SvelteKit에서도) 여전히 스토어를 접하게 될 거예요. 그래서 사용법을 알아두는 게 좋아요.

> [!NOTE] 커스텀 스토어를 만드는 방법은 다루지 않을 거예요. 그건 [문서](/docs/svelte/stores)를 참고하세요.

[범용 반응성(universal reactivity)](universal-reactivity) 실습의 예제를 다시 살펴보되, 이번에는 스토어를 사용해서 공유 상태를 구현해봐요.

`shared.js`에서 현재 숫자인 `count`를 export하고 있어요. 이걸 writable 스토어로 바꿔봐요:

```js
/// file: shared.js
+++import { writable } from 'svelte/store';+++

export const count = +++writable(0)+++;
```

스토어의 값을 참조하려면 `$` 기호를 앞에 붙여요. `Counter.svelte`에서 `<button>` 안의 텍스트를 업데이트해서 더 이상 `[object Object]`라고 나오지 않게 하세요:

```svelte
/// file: Counter.svelte
<button onclick={() => {}}>
	clicks: {+++$count+++}
</button>
```

마지막으로 이벤트 핸들러를 추가하세요. writable 스토어이기 때문에 `set`이나 `update` 메서드를 써서 프로그래밍 방식으로 값을 업데이트할 수 있어요...

```js
count.update((n) => n + 1);
```

...하지만 컴포넌트 안에 있으니까 `$` 접두사를 계속 쓸 수 있어요:

```svelte
/// file: Counter.svelte
<button onclick={() => +++$count += 1+++}>
	clicks: {$count}
</button>
```
