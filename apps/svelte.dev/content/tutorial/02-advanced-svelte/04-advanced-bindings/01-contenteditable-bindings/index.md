---
title: Contenteditable 바인딩
---

`contenteditable` 속성을 가진 요소는 `textContent`와 `innerHTML` 바인딩을 지원해요:

```svelte
/// file: App.svelte
<div +++bind:innerHTML={html}+++ contenteditable></div>
```
