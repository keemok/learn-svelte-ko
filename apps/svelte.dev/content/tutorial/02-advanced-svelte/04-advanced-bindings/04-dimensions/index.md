---
title: 크기
---

모든 요소에 `clientWidth`, `clientHeight`, `offsetWidth`, `offsetHeight` 바인딩을 추가할 수 있고, Svelte는 [`ResizeObserver`](https://developer.mozilla.org/en-US/docs/Web/API/ResizeObserver)를 사용해서 바인딩된 값을 업데이트해요:

```svelte
/// file: App.svelte
<div +++bind:clientWidth={w} bind:clientHeight={h}+++>
	<span style="font-size: {size}px" contenteditable>edit this text</span>
	<span class="size">{w} x {h}px</span>
</div>
```

이 바인딩들은 읽기 전용이에요. `w`와 `h`의 값을 변경해도 요소에 아무런 영향을 주지 않아요.

> [!NOTE] `display: inline` 요소는 너비나 높이가 없어요 (`<img>`나 `<canvas>` 같이 '고유' 크기가 있는 요소 제외). `ResizeObserver`로 관찰할 수도 없고요. 이런 요소들의 `display` 스타일을 `inline-block` 같은 다른 것으로 변경해야 해요.
