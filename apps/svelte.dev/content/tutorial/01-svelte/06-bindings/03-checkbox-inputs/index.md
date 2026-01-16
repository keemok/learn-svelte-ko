---
title: 체크박스 입력
---

체크박스는 상태를 토글할 때 사용해요. `input.value` 대신 `input.checked`에 바인딩하면 돼요:

```svelte
/// file: App.svelte
<input type="checkbox" +++bind:+++checked={yes}>
```
