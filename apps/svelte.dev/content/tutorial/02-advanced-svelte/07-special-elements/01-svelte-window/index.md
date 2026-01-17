---
title: <svelte:window>
---

모든 DOM 요소에 이벤트 리스너를 추가할 수 있는 것처럼, `<svelte:window>`로 `window` 객체에도 이벤트 리스너를 추가할 수 있어요.

이미 `onkeydown` 함수가 선언돼 있어요. 이제 연결만 하면 돼요:

```svelte
/// file: App.svelte
<svelte:window +++{onkeydown}+++ />
```
