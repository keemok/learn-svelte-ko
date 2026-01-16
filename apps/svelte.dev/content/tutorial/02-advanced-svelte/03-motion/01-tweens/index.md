---
title: Tweened 값
---

값이 변경되고 있다는 걸 전달하는 좋은 방법은 모션(motion)을 사용하는 거예요. Svelte는 사용자 인터페이스에 모션을 추가하기 위한 클래스를 제공해요.

`svelte/motion`에서 `Tween` 클래스를 import하세요:

```svelte
/// file: App.svelte
<script>
	+++import { Tween } from 'svelte/motion';+++

	let progress = $state(0);
</script>
```

`progress`를 `Tween`의 인스턴스로 만드세요:

```svelte
/// file: App.svelte
<script>
	import { Tween } from 'svelte/motion';

	let progress = +++new Tween+++(0);
</script>
```

`Tween` 클래스는 쓰기 가능한 `target` 속성과 읽기 전용인 `current` 속성을 가지고 있어요. `<progress>` 요소를 업데이트하세요...

```svelte
<progress value={progress.+++current+++}></progress>
```

...그리고 각 이벤트 핸들러도:

```svelte
<button onclick={() => (progress.+++target+++ = 0)}>
	0%
</button>
```

버튼을 클릭하면 진행 바가 새 값으로 애니메이션돼요. 하지만 좀 로봇 같고 만족스럽지 않아요. 이징 함수를 추가해야 해요:

```svelte
/// file: App.svelte
<script>
	import { Tween } from 'svelte/motion';
	+++import { cubicOut } from 'svelte/easing';+++

	let progress = new Tween(0, +++{
		duration: 400,
		easing: cubicOut
	}+++);
</script>
```

> [!NOTE] `svelte/easing` 모듈에는 [Penner 이징 방정식](https://web.archive.org/web/20190805215728/http://robertpenner.com/easing/)이 들어있어요. 또는 `p`와 `t`가 모두 0과 1 사이의 값인 `p => t` 함수를 직접 제공할 수도 있어요.

`Tween`에 사용할 수 있는 전체 옵션:

- `delay` — 트윈이 시작되기 전 밀리초
- `duration` — 트윈의 지속 시간(밀리초) 또는 `(from, to) => milliseconds` 함수 (예를 들어 값의 변화가 클수록 더 긴 트윈을 지정할 수 있음)
- `easing` — `p => t` 함수
- `interpolate` — 임의의 값 사이를 보간하기 위한 커스텀 `(from, to) => t => value` 함수. 기본적으로 Svelte는 숫자, 날짜, 동일한 모양의 배열과 객체(숫자와 날짜 또는 다른 유효한 배열과 객체만 포함하는 경우) 사이를 보간해요. 색상 문자열이나 변환 행렬을 보간하려면 커스텀 인터폴레이터를 제공하세요.

`progress.target`에 직접 할당하는 대신 `progress.set(value, options)`를 호출할 수도 있어요. 이 경우 `options`가 기본값을 재정의해요. `set` 메서드는 트윈이 완료될 때 resolve되는 프로미스를 반환해요.
