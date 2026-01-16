---
title: Attachment 팩토리
---

종종 attachment가 일부 매개변수나 컴포넌트 상태에 의존해야 할 때가 있어요. 이런 경우에는 [attachment 팩토리](/docs/svelte/@attach#Attachment-factories)를 쓸 수 있어요. attachment를 반환하는 함수죠.

이 실습에서는 [`Tippy.js`](https://atomiks.github.io/tippyjs/) 라이브러리를 사용해서 `<button>`에 툴팁을 추가하려고 해요. attachment는 이미 `{@attach tooltip}`으로 연결돼 있지만, 버튼에 마우스를 올리거나(또는 키보드로 포커스하면) 툴팁에 내용이 없어요.

먼저, 간단한 attachment를 attachment를 반환하는 팩토리 함수로 변환해야 해요.

```js
/// file: App.svelte
function tooltip(---node---) {
+++	return (node) => {+++
		const tooltip = tippy(node);
		return tooltip.destroy;
+++	};+++
}
```

다음으로, 팩토리가 Tippy에 전달하려는 옵션(여기서는 `content`만)을 받아야 해요:

```js
/// file: App.svelte
function tooltip(+++content+++) {
	return (node) => {
		const tooltip = tippy(node+++, { content }+++);
		return tooltip.destroy;
	};
}
```

> [!NOTE] `tooltip(content)` 표현식은 이펙트 안에서 실행되기 때문에, content가 변경될 때마다 attachment가 파괴되고 다시 생성돼요.

마지막으로, `{@attach}` 태그에서 attachment 팩토리를 호출하고 `content` 인자를 전달해야 해요:

```svelte
/// file: App.svelte
<button {@attach tooltip+++(content)+++}>
	Hover me
</button>
```
