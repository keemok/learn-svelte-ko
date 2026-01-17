---
title: 미디어 요소
---

`<audio>`와 `<video>` 요소의 속성에 바인딩할 수 있어서, 예를 들어 `AudioPlayer.svelte` 같은 커스텀 플레이어 UI를 쉽게 만들 수 있어요.

먼저, 바인딩과 함께 `<audio>` 요소를 추가하세요 (`src`, `duration`, `paused`에는 단축 표기법을 쓸 거예요):

```svelte
/// file: AudioPlayer.svelte
<div class={['player', { paused }]}>
+++	<audio
		{src}
		bind:currentTime={time}
		bind:duration
		bind:paused
	></audio>+++

	<button
		class="play"
		aria-label={paused ? 'play' : 'pause'}
	></button>
```

다음으로, `paused`를 토글하는 이벤트 핸들러를 `<button>`에 추가하세요:

```svelte
/// file: AudioPlayer.svelte
<button
	class="play"
	aria-label={paused ? 'play' : 'pause'}
	+++onclick={() => paused = !paused}+++
></button>
```

이제 오디오 플레이어에 기본 기능이 생겼어요. 슬라이더를 드래그해서 트랙의 특정 부분으로 이동하는 기능을 추가해봐요. 슬라이더의 `pointerdown` 핸들러 안에 `seek` 함수가 있는데, 여기서 `time`을 업데이트할 수 있어요:

```js
/// file: AudioPlayer.svelte
function seek(e) {
	const { left, width } = div.getBoundingClientRect();

	let p = (e.clientX - left) / width;
	if (p < 0) p = 0;
	if (p > 1) p = 1;

	+++time = p * duration;+++
}
```

트랙이 끝나면 친절하게 되감아주세요:

```svelte
/// file: AudioPlayer.svelte
<audio
	{src}
	bind:currentTime={time}
	bind:duration
	bind:paused
+++	onended={() => {
		time = 0;
	}}+++
></audio>
```

`<audio>`와 `<video>`의 전체 바인딩 세트는 다음과 같아요. 7개의 읽기 전용 바인딩...

- `duration` — 총 길이(초)
- `buffered` — `{start, end}` 객체의 배열
- `seekable` — 위와 동일
- `played` — 위와 동일
- `seeking` — boolean
- `ended` — boolean
- `readyState` — 0과 4 사이의 숫자(포함)

...그리고 5개의 양방향 바인딩:

- `currentTime` — 재생 헤드의 현재 위치(초)
- `playbackRate` — 속도 높이기 또는 낮추기 (`1`이 '정상')
- `paused` — 이건 설명이 필요 없죠
- `volume` — 0과 1 사이의 값
- `muted` — true가 음소거인 boolean 값

비디오에는 추가로 읽기 전용 `videoWidth`와 `videoHeight` 바인딩이 있어요.
