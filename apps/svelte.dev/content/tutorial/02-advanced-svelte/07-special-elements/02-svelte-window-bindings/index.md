---
title: <svelte:window> 바인딩
---

`scrollY` 같은 `window`의 특정 속성에도 바인딩할 수 있어요:

```svelte
/// file: App.svelte
<svelte:window +++bind:scrollY={y}+++ />
```

바인딩할 수 있는 속성 목록은 다음과 같아요:

- `innerWidth`
- `innerHeight`
- `outerWidth`
- `outerHeight`
- `scrollX`
- `scrollY`
- `online` — `window.navigator.onLine`의 별칭

`scrollX`와 `scrollY`를 제외한 모든 속성은 읽기 전용이에요.
