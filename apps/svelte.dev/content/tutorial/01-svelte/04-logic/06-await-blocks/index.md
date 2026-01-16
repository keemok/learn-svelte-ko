---
title: Await 블록
---

대부분의 웹 애플리케이션은 언젠가 비동기 데이터를 다뤄야 해요. Svelte는 마크업에서 [프로미스(promise)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)의 값을 직접 기다릴(await) 수 있게 해줘요:

```svelte
/// file: App.svelte
+++{#await promise}+++
	<p>...rolling</p>
+++{:then number}
	<p>you rolled a {number}!</p>
{:catch error}
	<p style="color: red">{error.message}</p>
{/await}+++
```

> [!NOTE] 가장 최근의 `promise`만 고려되기 때문에 경쟁 상태(race condition)를 걱정할 필요가 없어요.

프로미스가 거부(reject)되지 않는다는 걸 안다면 `catch` 블록을 생략할 수 있어요. 프로미스가 해결(resolve)될 때까지 아무것도 보여주고 싶지 않다면 첫 번째 블록도 생략할 수 있어요:

```svelte
{#await promise then number}
	<p>you rolled a {number}!</p>
{/await}
```
