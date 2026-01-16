---
title: 스프링(Springs)
---

`Spring` 클래스는 `Tween`의 대안으로, 자주 변경되는 값에 더 잘 작동하는 경우가 많아요.

이 예제에는 마우스를 따라가는 원이 있고, 두 개의 값이 있어요. 원의 좌표와 크기죠. 스프링으로 변환해봐요:

```svelte
/// file: App.svelte
<script>
	+++import { Spring } from 'svelte/motion+++';

	let coords = +++new Spring+++({ x: 50, y: 50 });
	let size = +++new Spring+++(10);
</script>
```

`Tween`처럼 스프링도 쓰기 가능한 `target` 속성과 읽기 전용인 `current` 속성을 가지고 있어요. 이벤트 핸들러를 업데이트하세요...

```svelte
<svg
	onmousemove={(e) => {
		coords.+++target+++ = { x: e.clientX, y: e.clientY };
	}}
	onmousedown={() => (size.+++target+++ = 30)}
	onmouseup={() => (size.+++target+++ = 10)}
	role="presentation"
>
```

...그리고 `<circle>` 속성도:

```svelte
<circle
	cx={coords.+++current+++.x}
	cy={coords.+++current+++.y}
	r={size.+++current+++}
></circle>
```

두 스프링 모두 기본 `stiffness`와 `damping` 값을 가지고 있어요. 스프링의, 음... 스프링다움을 제어하죠. 우리만의 초기값을 지정할 수 있어요:

```js
/// file: App.svelte
let coords = new Spring({ x: 50, y: 50 }, +++{
	stiffness: 0.1,
	damping: 0.25
}+++);
```

마우스를 이리저리 흔들어보고, 슬라이더를 드래그해서 스프링의 동작에 어떤 영향을 주는지 느껴보세요. 스프링이 여전히 움직이는 동안에도 값을 조정할 수 있다는 걸 알아차리세요.
