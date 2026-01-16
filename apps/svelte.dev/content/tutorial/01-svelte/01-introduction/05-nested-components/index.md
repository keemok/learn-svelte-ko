---
title: 중첩된 컴포넌트
---

앱 전체를 하나의 컴포넌트에 다 넣기는 불가능하죠. 다른 파일에서 컴포넌트를 가져와서(import) 마크업에 넣을 수 있어요.

`App.svelte` 맨 위에 `<script>` 태그를 추가하고 `Nested.svelte`를 import 하세요...

```svelte
/// file: App.svelte
+++<script>
	import Nested from './Nested.svelte';
</script>+++
```

...그리고 `<Nested />` 컴포넌트를 넣어주세요:

```svelte
/// file: App.svelte
<p>This is a paragraph.</p>
+++<Nested />+++
```

`Nested.svelte`에도 `<p>` 요소가 있는데, `App.svelte`의 스타일이 적용되지 않는 걸 확인해보세요.

> [!NOTE] 컴포넌트 이름은 HTML 요소와 구분하기 위해 대문자로 시작해요.
