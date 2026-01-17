---
title: trailingSlash
---

`/foo`와 `/foo/` 같은 두 URL은 같아 보일 수 있지만, 실제로는 달라요. `./bar` 같은 상대 URL은 첫 번째 경우 `/bar`로 해석되고 두 번째 경우 `/foo/bar`로 해석될 거예요. 그리고 검색 엔진은 이들을 별도 항목으로 취급해서 SEO를 해칠 거예요.

간단히 말해, 후행 슬래시에 대해 느슨하게 구는 건 나쁜 생각이에요. 기본적으로 SvelteKit은 후행 슬래시를 제거해요. `/foo/`에 대한 요청이 `/foo`로 리다이렉트되는 거죠.

대신 후행 슬래시가 항상 존재하도록 하려면 `trailingSlash` 옵션을 그에 맞게 지정할 수 있어요:

```js
/// file: src/routes/always/+page.server.js
export const trailingSlash = 'always';
```

두 경우를 모두 수용하려면 (권장하지 않아요!) `'ignore'`를 사용하세요:

```js
/// file: src/routes/ignore/+page.server.js
export const trailingSlash = 'ignore';
```

기본값은 `'never'`예요.

후행 슬래시가 적용되는지 여부는 사전 렌더링에 영향을 미쳐요. `/always/` 같은 URL은 디스크에 `always/index.html`로 저장되는 반면 `/never` 같은 URL은 `never.html`로 저장돼요.
