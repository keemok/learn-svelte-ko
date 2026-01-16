---
title: 캡처링
---

일반적으로 이벤트 핸들러는 [버블링(bubbling)](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Event_bubbling) 단계에서 실행돼요. 이 예제에서 `<input>`에 뭔가 입력해보면 무슨 일이 일어나는지 보세요. 이벤트가 타깃에서 document로 '버블링'되면서 안쪽 핸들러가 먼저 실행되고, 그다음 바깥쪽 핸들러가 실행돼요.

때로는 핸들러가 캡처(capture) 단계에서 실행되길 원할 때가 있어요. 이벤트 이름 끝에 `capture`를 붙이면 돼요:

```svelte
/// file: App.svelte
<div onkeydown+++capture+++={(e) => alert(`<div> ${e.key}`)} role="presentation">
	<input onkeydown+++capture+++={(e) => alert(`<input> ${e.key}`)} />
</div>
```

이제 순서가 반대가 돼요. 특정 이벤트에 캡처링과 논캡처링 핸들러가 둘 다 있으면, 캡처링 핸들러가 먼저 실행돼요.
