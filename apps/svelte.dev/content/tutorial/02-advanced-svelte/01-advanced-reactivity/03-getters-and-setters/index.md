---
title: Getter와 Setter
---

클래스는 데이터를 검증해야 할 때 특히 유용해요. 이 `Box` 클래스의 경우, 슬라이더가 허용하는 최대값을 넘어서 계속 커지면 안 되는데, 지금은 정확히 그렇게 되고 있어요.

`width`와 `height`를 getter와 setter로 바꿔서 고칠 수 있어요. 접근자(accessor)라고도 불리죠. 먼저 [프라이빗 속성](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Private_properties)으로 변환하세요:

```js
/// file: App.svelte
class Box {
	+++#width+++ = $state(0);
	+++#height+++ = $state(0);
	area = $derived(this.+++#width+++ * this.+++#height+++);

	constructor(width, height) {
		this.+++#width+++ = width;
		this.+++#height+++ = height;
	}

	// ...
}
```

그다음 getter와 setter를 만드세요:

```js
/// file: App.svelte
class Box {
	// ...

+++	get width() {
		return this.#width;
	}

	get height() {
		return this.#height;
	}

	set width(value) {
		this.#width = value;
	}

	set height(value) {
		this.#height = value;
	}+++

	embiggen(amount) {
		this.width += amount;
		this.height += amount;
	}
}
```

마지막으로 setter에 검증을 추가하세요:

```js
/// file: App.svelte
set width(value) {
	this.#width = +++Math.max(0, Math.min(MAX_SIZE, value));+++
}

set height(value) {
	this.#height = +++Math.max(0, Math.min(MAX_SIZE, value));+++
}
```

이제 range 입력의 `bind:value`를 통하든 `embiggen` 메서드를 통하든, 버튼을 아무리 세게 눌러도 박스 크기를 안전한 한계를 넘어 늘릴 수 없어요.
