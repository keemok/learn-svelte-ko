---
title: attach 태그
---

Attachment는 본질적으로 요소 수준의 생명주기 함수예요. 이런 것들에 유용해요:

- 서드파티 라이브러리와 인터페이싱
- 지연 로드되는 이미지
- 툴팁
- 커스텀 이벤트 핸들러 추가

이 앱에서는 `<canvas>`에 낙서할 수 있고, 메뉴를 통해 색상과 브러시 크기를 바꿀 수 있어요. 하지만 메뉴를 열고 Tab 키로 옵션들을 순환하다 보면, 포커스가 모달 안에 갇혀(trapped) 있지 않다는 걸 알게 될 거예요.

attachment로 이걸 고칠 수 있어요. `attachments.svelte.js`에서 `trapFocus`를 import하세요...

```svelte
/// file: App.svelte
<script>
	import Canvas from './Canvas.svelte';
	+++import { trapFocus } from './attachments.svelte.js';+++

	const colors = ['red', 'orange', 'yellow', 'green', 'blue', 'indigo', 'violet', 'white', 'black'];

	let selected = $state(colors[0]);
	let size = $state(10);
	let showMenu = $state(true);
</script>
```

...그다음 `{@attach}` 태그로 메뉴에 추가하세요:

```svelte
/// file: App.svelte
<div class="menu" +++{@attach trapFocus}+++>
```

`attachments.svelte.js`의 `trapFocus` 함수를 살펴봐요. attachment 함수는 노드가 DOM에 마운트될 때 `node`(여기서는 `<div class="menu">`)와 함께 호출돼요. Attachment는 [이펙트(effect)](effects) 안에서 실행되기 때문에, 함수 내부에서 읽는 상태가 변경될 때마다 다시 실행돼요.

먼저, Tab 키 입력을 가로채는 이벤트 리스너를 추가해야 해요:

```js
/// file: attachments.svelte.js
focusable()[0]?.focus();
+++const off = on(node, 'keydown', handleKeydown);+++
```

> [!NOTE] [`on`](/docs/svelte/svelte-events#on)은 <a href="/docs/svelte/basic-markup#Events-Event-delegation">이벤트 위임</a>을 사용하는 `addEventListener`의 래퍼예요. 핸들러를 제거하는 함수를 반환해요.

둘째로, 노드가 언마운트될 때 정리 작업을 해야 해요. 이벤트 리스너를 제거하고, 요소가 마운트되기 전에 있던 곳으로 포커스를 복원하는 거죠. 이펙트처럼 attachment도 teardown 함수를 반환할 수 있어요. 이 함수는 attachment가 다시 실행되기 직전이나 요소가 DOM에서 제거된 후에 실행돼요:

```js
/// file: attachments.svelte.js
focusable()[0]?.focus();
const off = on(node, 'keydown', handleKeydown);

+++return () => {
	off();
	previous?.focus();
};+++
```

이제 메뉴를 열면 Tab 키로 옵션들을 순환할 수 있어요.
