---
title: 첫 번째 컴포넌트
---

Svelte에서 애플리케이션은 하나 이상의 _컴포넌트_ 로 이루어져요. 컴포넌트는 HTML, CSS, JavaScript를 한 곳에 모아놓은 재사용 가능한 코드 덩어리예요. `.svelte` 파일에 작성하면 돼요. 오른쪽 코드 에디터에 열려있는 `App.svelte` 파일이 바로 간단한 컴포넌트 예시예요.

## 데이터 추가하기

정적인 마크업만 보여주는 컴포넌트는 재미없죠. 데이터를 넣어봐요.

먼저 컴포넌트에 script 태그를 추가하고 `name` 변수를 만드세요:

```svelte
/// file: App.svelte
+++<script>
	let name = 'Svelte';
</script>+++

<h1>Hello world!</h1>
```

그다음 마크업에서 `name`을 참조할 수 있어요:

```svelte
/// file: App.svelte
<h1>Hello +++{name}+++!</h1>
```

중괄호 안에는 원하는 JavaScript 코드를 넣을 수 있어요. `name`을 `name.toUpperCase()`로 바꿔서 더 크게 인사해볼까요?

```svelte
/// file: App.svelte
<h1>Hello {name+++.toUpperCase()+++}!</h1>
```
