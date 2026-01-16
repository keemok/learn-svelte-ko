---
title: Props 선언하기
---

지금까지는 내부 상태(internal state)만 다뤘어요. 즉, 값이 특정 컴포넌트 안에서만 접근 가능했죠.

실제 애플리케이션에서는 한 컴포넌트에서 자식 컴포넌트로 데이터를 전달해야 해요. 이럴 때 속성(properties), 줄여서 'props'를 선언해야 해요. Svelte에서는 `$props` 룬으로 이걸 해요. `Nested.svelte` 컴포넌트를 수정해봐요:

```svelte
/// file: Nested.svelte
<script>
	let { answer } = +++$props()+++;
</script>
```
