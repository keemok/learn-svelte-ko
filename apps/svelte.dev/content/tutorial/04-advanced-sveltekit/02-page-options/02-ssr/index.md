---
title: ssr
---

서버 사이드 렌더링(SSR)은 서버에서 HTML을 생성하는 프로세스예요. SvelteKit이 기본적으로 하는 일이죠. 성능과 [복원력](https://kryogenix.org/code/browser/everyonehasjs.html)에 중요하고, 검색 엔진 최적화(SEO)에 매우 유익해요. 일부 검색 엔진은 JavaScript로 브라우저에서 렌더링되는 콘텐츠를 인덱싱할 수 있지만, 덜 빈번하고 신뢰할 수 없게 일어나요.

그렇긴 하지만, 일부 컴포넌트는 서버에서 렌더링될 수 없어요. 아마도 `window` 같은 브라우저 전역에 즉시 접근할 수 있기를 기대하기 때문이죠. 가능하다면 그 컴포넌트들을 서버에서 렌더링될 수 있도록 변경해야 하지만, 그럴 수 없다면 SSR을 비활성화할 수 있어요:

```js
/// file: src/routes/+page.server.js
export const ssr = false;
```

> [!NOTE] 루트 `+layout.server.js` 안에서 `ssr`을 `false`로 설정하면 전체 앱이 효과적으로 싱글 페이지 앱(SPA)이 돼요.
