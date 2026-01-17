---
title: <svelte:document>
---

`<svelte:document>` 요소를 사용하면 `document`에서 발생하는 이벤트를 들을 수 있어요. `window`에서 발생하지 않는 `selectionchange` 같은 이벤트에 유용해요.

`<svelte:document>` 태그에 `onselectionchange` 핸들러를 추가하세요:

```svelte
/// file: App.svelte
<svelte:document +++{onselectionchange}+++ />
```

> [!NOTE] 이 요소에서는 `mouseenter`와 `mouseleave` 핸들러를 피하세요. 모든 브라우저에서 `document`에 이 이벤트들이 발생하지는 않거든요. 대신 `<svelte:body>`를 사용하세요.
