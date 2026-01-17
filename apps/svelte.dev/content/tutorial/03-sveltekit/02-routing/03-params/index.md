---
title: 라우트 파라미터
path: /blog
---

동적 파라미터를 가진 라우트를 만들려면, 유효한 변수명 주위에 대괄호를 사용하세요. 예를 들어, `src/routes/blog/[slug]/+page.svelte` 같은 파일은 `/blog/one`, `/blog/two`, `/blog/three` 등과 매칭되는 라우트를 만들어요.

그 파일을 만들어봐요:

```svelte
/// file: src/routes/blog/[slug]/+page.svelte
<h1>blog post</h1>
```

이제 `/blog` 페이지에서 개별 블로그 포스트로 이동할 수 있어요. 다음 챕터에서는 콘텐츠를 로드하는 방법을 볼 거예요.

> [!NOTE] 여러 라우트 파라미터가 하나의 URL 세그먼트 안에 나타날 수 있어요. 최소한 하나의 정적 문자로 구분되기만 하면 돼요. `foo/[bar]x[baz]`는 `[bar]`와 `[baz]`가 동적 파라미터인 유효한 라우트예요.
