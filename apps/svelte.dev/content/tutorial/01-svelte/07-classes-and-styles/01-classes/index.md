---
title: class 속성
---

다른 속성처럼 JavaScript 속성으로 클래스를 지정할 수 있어요. 여기서 카드에 `flipped` 클래스를 추가할 수 있어요:

```svelte
/// file: App.svelte
<button
	class="card {+++flipped ? 'flipped' : ''+++}"
	onclick={() => flipped = !flipped}
>
```

예상대로 작동해요. 카드를 클릭하면 뒤집히죠.

하지만 더 깔끔하게 만들 수 있어요. 특정 조건에 따라 클래스를 추가하거나 제거하는 건 UI 개발에서 매우 흔한 패턴이라서, Svelte는 [clsx](https://github.com/lukeed/clsx)를 통해 문자열로 변환되는 객체나 배열을 전달할 수 있게 해줘요.

```svelte
/// file: App.svelte
<button
	+++class={["card", { flipped }]}+++
	onclick={() => flipped = !flipped}
>
```

이건 '항상 `card` 클래스를 추가하고, `flipped`가 truthy일 때마다 `flipped` 클래스를 추가한다'는 의미예요.

조건부 클래스를 결합하는 더 많은 예시는 [`class` 문서](/docs/svelte/class)를 참고하세요.
