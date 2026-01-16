---
title: 범용 반응성(Universal reactivity)
---

이전 실습에서는 컴포넌트 안에서 룬을 써서 반응성을 추가했어요. 하지만 컴포넌트 밖에서도 룬을 쓸 수 있어요. 예를 들어 전역 상태를 공유할 때 쓸 수 있죠.

이 실습의 `<Counter>` 컴포넌트들은 모두 `shared.js`에서 `counter` 객체를 import하고 있어요. 하지만 일반 객체라서 버튼을 클릭해도 아무 일도 일어나지 않아요. 객체를 `$state(...)`로 감싸봐요:

```js
/// file: shared.js
export const counter = +++$state({+++
	count: 0
+++})+++;
```

에러가 나요. 일반 `.js` 파일에서는 룬을 쓸 수 없고, `.svelte.js` 파일에서만 쓸 수 있기 때문이에요. 고쳐봐요. 파일 이름을 `shared.svelte.js`로 바꾸세요.

그다음 `Counter.svelte`의 import 선언을 업데이트하세요:

```svelte
/// file: Counter.svelte
<script>
	import { counter } from './shared+++.svelte+++.js';
</script>
```

이제 어떤 버튼을 클릭하든 세 개 모두 동시에 업데이트돼요.

> [!NOTE] 선언이 (단순히 변경되는 게 아니라) 재할당되는 경우에는 모듈에서 `$state` 선언을 export할 수 없어요. import하는 쪽에서 그걸 알 방법이 없기 때문이에요.
