---
title: 코드 공유하기
---

지금까지 본 모든 예제에서 `<script>` 블록은 각 컴포넌트 인스턴스가 초기화될 때 실행되는 코드를 포함하고 있어요. 대부분의 컴포넌트에서는 그게 필요한 전부예요.

아주 가끔씩 개별 컴포넌트 인스턴스 밖에서 코드를 실행해야 할 때가 있어요. 예를 들어, [이전 실습](media-elements)의 커스텀 오디오 플레이어로 돌아가보면, 네 개의 트랙을 동시에 재생할 수 있어요. 하나를 재생하면 다른 것들이 멈추는 게 더 나을 거예요.

`<script module>` 블록을 선언해서 할 수 있어요. 안에 포함된 코드는 컴포넌트가 인스턴스화될 때가 아니라 모듈이 처음 평가될 때 한 번 실행돼요. `AudioPlayer.svelte`의 맨 위에 이걸 배치하세요 (이건 별도의 script 태그라는 걸 주목하세요):

```svelte
/// file: AudioPlayer.svelte
+++<script module>
	let current;
</script>+++
```

이제 컴포넌트들이 상태 관리 없이 서로 '대화'할 수 있어요:

```svelte
/// file: AudioPlayer.svelte
<audio
	src={src}
	bind:currentTime={time}
	bind:duration
	bind:paused
+++	onplay={(e) => {
		const audio = e.currentTarget;

		if (audio !== current) {
			current?.pause();
			current = audio;
		}
	}}+++
	onended={() => {
		time = 0;
	}}
/>
```
