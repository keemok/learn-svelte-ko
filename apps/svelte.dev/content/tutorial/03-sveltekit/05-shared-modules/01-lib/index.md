---
title: $lib 별칭
---

SvelteKit은 디렉토리 기반 라우팅을 사용하기 때문에, 모듈과 컴포넌트를 사용하는 라우트 옆에 배치하기 쉬워요. 좋은 경험 법칙은 '코드를 사용되는 곳 가까이에 두기'예요.

때로는 코드가 여러 곳에서 사용돼요. 이런 경우 `../../../../`로 import에 접두사를 붙일 필요 없이 모든 라우트에서 접근할 수 있는 곳에 두는 게 유용해요. SvelteKit에서 그 장소는 `src/lib` 디렉토리예요. 이 디렉토리 안의 모든 것은 `$lib` 별칭을 통해 `src`의 모든 모듈에서 접근할 수 있어요.

이 실습의 두 `+page.svelte` 파일 모두 `src/lib/message.js`를 import해요. 하지만 `/a/deeply/nested/route`로 이동하면 앱이 망가져요. 접두사를 잘못 지정했거든요. 대신 `$lib/message.js`를 사용하도록 업데이트하세요:

```svelte
/// file: src/routes/a/deeply/nested/route/+page.svelte
<script>
	import { message } from +++'$lib/message.js'+++;
</script>

<h1>a deeply nested route</h1>
<p>{message}</p>
```

`src/routes/+page.svelte`에도 똑같이 해주세요:

```svelte
/// file: src/routes/+page.svelte
<script>
	import { message } from +++'$lib/message.js'+++;
</script>

<h1>home</h1>
<p>{message}</p>
```
