---
title: 커스텀 CSS 트랜지션
---

`svelte/transition` 모듈에는 몇 가지 내장 트랜지션이 있지만, 직접 만드는 것도 아주 쉬워요. 예를 들어, `fade` 트랜지션의 소스는 이래요:

```js
function fade(node, { delay = 0, duration = 400 }) {
	const o = +getComputedStyle(node).opacity;

	return {
		delay,
		duration,
		css: (t) => `opacity: ${t * o}`
	};
}
```

함수는 두 개의 인자를 받아요. 트랜지션이 적용될 노드와 전달된 파라미터들이죠. 그리고 다음 속성들을 가질 수 있는 트랜지션 객체를 반환해요:

- `delay` — 트랜지션이 시작되기 전 밀리초
- `duration` — 트랜지션의 길이(밀리초)
- `easing` — `p => t` 이징 함수 ([tweening](/tutorial/svelte/tweens) 챕터 참고)
- `css` — `(t, u) => css` 함수, 여기서 `u === 1 - t`
- `tick` — 노드에 어떤 효과를 주는 `(t, u) => {...}` 함수

`t` 값은 intro의 시작이나 outro의 끝에서 `0`이고, intro의 끝이나 outro의 시작에서 `1`이에요.

대부분의 경우 `tick` 속성이 아니라 `css` 속성을 반환해야 해요. CSS 애니메이션은 가능한 한 끊김을 방지하기 위해 메인 스레드 밖에서 실행되거든요. Svelte는 트랜지션을 '시뮬레이션'하고 CSS 애니메이션을 구성한 다음 실행하게 해요.

예를 들어, `fade` 트랜지션은 대략 이런 CSS 애니메이션을 생성해요:

<!-- prettier-ignore-start -->
```css
0% { opacity: 0 }
10% { opacity: 0.1 }
20% { opacity: 0.2 }
/* ... */
100% { opacity: 1 }
```
<!-- prettier-ignore-end -->

하지만 훨씬 더 창의적일 수 있어요. 진짜 화려한 걸 만들어봐요:

```svelte
/// file: App.svelte
<script>
	import { fade } from 'svelte/transition';
	+++import { elasticOut } from 'svelte/easing';+++

	let visible = $state(true);

	function spin(node, { duration }) {
		return {
			duration,
			css: (t, u) => +++{
				const eased = elasticOut(t);

				return `
					transform: scale(${eased}) rotate(${eased * 1080}deg);
					color: hsl(
						${Math.trunc(t * 360)},
						${Math.min(100, 1000 * u)}%,
						${Math.min(50, 500 * u)}%
					);`
			}+++
		};
	}
</script>
```

기억하세요: 큰 힘에는 큰 책임이 따라요.
