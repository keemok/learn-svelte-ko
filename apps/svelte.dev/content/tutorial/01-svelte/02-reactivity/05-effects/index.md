---
title: 이펙트(Effects)
---

지금까지 상태 관점에서 반응성에 대해 얘기했어요. 하지만 이건 절반만 본 거예요. 상태는 뭔가가 그것에 반응할 때만 반응형이에요. 그렇지 않으면 그냥 반짝이는 변수일 뿐이죠.

반응하는 것을 이펙트(effect)라고 불러요. 이미 이펙트를 접해봤어요. Svelte가 상태 변경에 반응해서 DOM을 업데이트하기 위해 만드는 이펙트 말이에요. `$effect` 룬으로 직접 만들 수도 있어요.

> [!NOTE] 대부분의 경우 만들 필요가 없어요. `$effect`는 자주 쓰는 것보다는 탈출구로 생각하는 게 좋아요. [이벤트 핸들러](dom-events)에 사이드 이펙트를 넣을 수 있다면 거의 항상 그게 더 나아요.

`setInterval`을 써서 컴포넌트가 마운트된 지 얼마나 됐는지 추적한다고 해봐요. 이펙트를 만들어봐요:

```svelte
/// file: App.svelte
<script>
	let elapsed = $state(0);
	let interval = $state(1000);

+++	$effect(() => {
		setInterval(() => {
			elapsed += 1;
		}, interval);
	});+++
</script>
```

'speed up' 버튼을 몇 번 클릭해보세요. `interval`이 작아질 때마다 `setInterval`을 호출하기 때문에 `elapsed`가 더 빨리 증가하는 걸 볼 수 있어요.

그다음 'slow down' 버튼을 클릭하면... 음, 작동하지 않아요. 이펙트가 업데이트될 때 기존 interval을 정리하지 않았기 때문이에요. 정리 함수를 반환해서 고칠 수 있어요:

```js
/// file: App.svelte
$effect(() => {
	+++const id =+++ setInterval(() => {
		elapsed += 1;
	}, interval);

+++	return () => {
		clearInterval(id);
	};+++
});
```

정리 함수는 `interval`이 변경될 때 이펙트 함수가 다시 실행되기 직전에 호출되고, 컴포넌트가 소멸될 때도 호출돼요.

이펙트 함수가 실행될 때 어떤 상태도 읽지 않으면, 컴포넌트가 마운트될 때 딱 한 번만 실행돼요.

> [!NOTE] 이펙트는 서버 사이드 렌더링 중에는 실행되지 않아요.
