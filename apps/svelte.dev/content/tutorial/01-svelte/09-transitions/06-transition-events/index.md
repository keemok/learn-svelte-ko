---
title: 트랜지션 이벤트
---

트랜지션이 시작되고 끝날 때를 아는 게 유용할 수 있어요. Svelte는 다른 DOM 이벤트처럼 들을 수 있는 이벤트를 디스패치해요:

```svelte
/// file: App.svelte
<p
	transition:fly={{ y: 200, duration: 2000 }}
+++	onintrostart={() => status = 'intro started'}
	onoutrostart={() => status = 'outro started'}
	onintroend={() => status = 'intro ended'}
	onoutroend={() => status = 'outro ended'}+++
>
	Flies in and out
</p>
```
