---
title: 프리로딩
---

이 실습에서 `/slow-a`와 `/slow-b` 라우트는 둘 다 `load` 함수에 인위적인 지연이 있어서, 그것들로 탐색하는 데 오랜 시간이 걸려요.

항상 데이터를 더 빠르게 로드하게 만들 수는 없어요. 때로는 통제 밖이거든요. 하지만 SvelteKit은 탐색을 예측함으로써 탐색 속도를 높일 수 있어요. `<a>` 요소에 `data-sveltekit-preload-data` 속성이 있으면, SvelteKit은 사용자가 링크 위에 마우스를 올리자마자 (데스크톱에서) 또는 탭하자마자 (모바일에서) 탐색을 시작해요. 첫 번째 링크에 추가해보세요:

```svelte
/// file: src/routes/+layout.svelte
<nav>
	<a href="/">home</a>
	<a href="/slow-a" +++data-sveltekit-preload-data+++>slow-a</a>
	<a href="/slow-b">slow-b</a>
</nav>
```

이제 `/slow-a`로 탐색하는 게 눈에 띄게 빨라질 거예요. 호버나 탭에서 탐색을 시작하는 것 (`click` 이벤트가 등록되기를 기다리는 대신)이 큰 차이를 만들지 않는 것처럼 들릴 수 있지만, 실제로는 보통 200ms 이상을 절약해요. 느린 것과 빠른 것의 차이를 만들기에 충분해요.

개별 링크나 링크를 포함하는 요소에 속성을 넣을 수 있어요. 기본 프로젝트 템플릿은 `<body>` 요소에 속성을 포함해요:

```html
<body data-sveltekit-preload-data>
	%sveltekit.body%
</body>
```

속성에 다음 값 중 하나를 지정해서 동작을 더 커스터마이징할 수 있어요:

- `"hover"` (기본, 모바일에서 `"tap"`으로 폴백)
- `"tap"` — 탭에서만 프리로딩 시작
- `"off"` — 프리로딩 비활성화

`data-sveltekit-preload-data`를 사용하면 때로 거짓 양성이 발생할 수 있어요. 즉, 일어나지 않을 탐색을 예상해서 데이터를 로드하는 거죠. 바람직하지 않을 수 있어요. 대안으로, `data-sveltekit-preload-code`는 데이터를 즉시 로드하지 않고 주어진 라우트에 필요한 JavaScript를 프리로드할 수 있게 해줘요. 이 속성은 다음 값을 가질 수 있어요:

- `"eager"` — 탐색 후 페이지의 모든 것을 프리로드
- `"viewport"` — 뷰포트에 나타나는 모든 것을 프리로드
- `"hover"` (기본) — 위와 같이
- `"tap"` — 위와 같이
- `"off"` — 위와 같이

`$app/navigation`에서 import한 `preloadCode`와 `preloadData`로 프로그래밍 방식으로 프리로딩을 시작할 수도 있어요:

```js
import { preloadCode, preloadData } from '$app/navigation';

// /foo로 탐색하는 데 필요한 코드와 데이터를 프리로드
preloadData('/foo');

// /bar로 탐색하는 데 필요한 코드를 프리로드하지만, 데이터는 안 함
preloadCode('/bar');
```
