---
title: 기본
---

SvelteKit에는 두 가지 유형의 에러가 있어요. 예상된(expected) 에러와 예상치 못한(unexpected) 에러예요.

예상된 에러는 `src/routes/expected/+page.server.js`에서처럼 `@sveltejs/kit`의 [`error`](/docs/kit/@sveltejs-kit#error) 헬퍼를 통해 던져진 에러예요:

```js
/// file: src/routes/expected/+page.server.js
import { error } from '@sveltejs/kit';

export function load() {
	error(420, 'Enhance your calm');
}
```

`src/routes/unexpected/+page.server.js`의 에러 같은 다른 모든 에러는 예상치 못한 것으로 취급돼요:

```js
/// file: src/routes/unexpected/+page.server.js
export function load() {
	throw new Error('Kaboom!');
}
```

예상된 에러를 던질 때, SvelteKit에게 "걱정 마, 나는 내가 여기서 뭘 하고 있는지 알아"라고 말하는 거예요. 반대로 예상치 못한 에러는 앱의 버그로 간주돼요. 예상치 못한 에러가 던져지면 메시지와 스택 트레이스가 콘솔에 기록돼요.

> [!NOTE] 나중 챕터에서 `handleError` 훅을 사용해서 커스텀 에러 처리를 추가하는 방법을 배울 거예요.

이 앱의 링크를 클릭하면 중요한 차이를 알아차릴 거예요. 예상된 에러 메시지는 사용자에게 표시되지만, 예상치 못한 에러 메시지는 검열되고 일반적인 'Internal Error' 메시지와 500 상태 코드로 대체돼요. 에러 메시지가 민감한 데이터를 포함할 수 있기 때문이에요.
