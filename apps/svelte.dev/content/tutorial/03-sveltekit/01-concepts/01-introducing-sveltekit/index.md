---
title: SvelteKit이란?
---

Svelte가 컴포넌트 프레임워크인 반면, SvelteKit은 프로덕션 준비가 된 무언가를 만드는 까다로운 문제들을 해결하는 앱 프레임워크(또는 누구에게 물어보느냐에 따라 '메타프레임워크')예요:

- 라우팅
- 서버 사이드 렌더링
- 데이터 페칭
- 서비스 워커
- TypeScript 통합
- 프리렌더링
- 싱글 페이지 앱
- 라이브러리 패키징
- 최적화된 프로덕션 빌드
- 다양한 호스팅 프로바이더에 배포
- ...등등

SvelteKit 앱은 훌륭한 첫 로드 성능과 SEO 특성을 위해 기본적으로 서버 렌더링돼요 (전통적인 '멀티 페이지 앱' 또는 MPA처럼). 하지만 사용자가 탐색할 때 (서드파티 분석 코드 같은 것들을 포함해서) 모든 걸 덜컥거리며 다시 로드하는 걸 피하기 위해 클라이언트 사이드 탐색으로 전환할 수 있어요 (현대적인 '싱글 페이지 앱' 또는 SPA처럼). JavaScript가 실행되는 어디서나 실행될 수 있지만, 나중에 보겠지만 사용자가 JavaScript를 전혀 실행할 필요가 없을 수도 있어요.

복잡하게 들린다면 걱정하지 마세요. SvelteKit은 당신과 함께 성장하는 프레임워크예요! 간단하게 시작해서 필요할 때 새로운 기능을 추가하면 돼요.

## 프로젝트 구조

오른쪽 파일 트리 뷰어에서 SvelteKit이 프로젝트에서 찾길 기대하는 몇 가지 파일을 볼 수 있어요.

`package.json`은 이전에 Node.js를 다뤄봤다면 익숙할 거예요. `svelte`와 `@sveltejs/kit`를 포함한 프로젝트의 의존성들과, SvelteKit CLI와 상호작용하기 위한 다양한 `scripts`를 나열해요. (우리는 현재 하단 창에서 `npm run dev`를 실행하고 있어요.)

> [!NOTE] `"type": "module"`을 지정하고 있다는 걸 주목하세요. 이는 `.js` 파일들이 레거시 CommonJS 형식이 아니라 기본적으로 네이티브 JavaScript 모듈로 취급된다는 의미예요.

`svelte.config.js`는 프로젝트 설정을 포함해요. 지금은 이 파일에 대해 걱정할 필요 없지만, 궁금하다면 [문서를 방문하세요](/docs/kit/configuration).

`vite.config.js`는 [Vite](https://vitejs.dev/) 설정을 포함해요. SvelteKit은 Vite를 사용하기 때문에, 핫 모듈 교체, TypeScript 지원, 정적 에셋 처리 등과 같은 [Vite 기능](https://vitejs.dev/guide/features.html)을 사용할 수 있어요.

`src`는 앱의 소스 코드가 들어가는 곳이에요. `src/app.html`은 페이지 템플릿이고 (SvelteKit은 `%sveltekit.head%`와 `%sveltekit.body%`를 적절히 교체해요), `src/routes`는 앱의 [라우트](/tutorial/kit/pages)를 정의해요.

마지막으로 `static`은 앱이 배포될 때 포함되어야 하는 모든 에셋 (`favicon.png`나 `robots.txt` 같은)을 포함해요.
