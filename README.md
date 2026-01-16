# 🇰🇷 Svelte 공식 튜토리얼 한글 번역

이 저장소는 [Svelte 공식 사이트](https://svelte.dev)의 튜토리얼을 한글로 번역하는 프로젝트입니다.

> **원본 저장소**: [sveltejs/svelte.dev](https://github.com/sveltejs/svelte.dev)

## 🎯 프로젝트 목표

한국어 사용자들이 Svelte를 쉽게 학습할 수 있도록 공식 튜토리얼을 한글로 번역합니다.

## 📊 번역 진행 상황

### Part 1: Basic Svelte
- [ ] Introduction
- [ ] Reactivity
- [ ] Props
- [ ] Logic
- [ ] Events
- [ ] Bindings
- [ ] Lifecycle
- [ ] Stores
- [ ] Motion
- [ ] Transitions
- [ ] Actions
- [ ] Classes and styles
- [ ] Component composition
- [ ] Context API
- [ ] Special elements

### Part 2: Advanced Svelte
- [ ] Advanced reactivity
- [ ] Advanced bindings
- [ ] Advanced transitions
- [ ] Advanced actions

### Part 3: Basic SvelteKit
- [ ] Introduction
- [ ] Routing
- [ ] Loading data
- [ ] Headers and cookies
- [ ] Shared modules
- [ ] Forms
- [ ] API routes
- [ ] Stores
- [ ] Errors and redirects
- [ ] Advanced routing
- [ ] Advanced loading
- [ ] Environment variables

## 🚀 로컬 개발 환경 설정
```bash
# 의존성 설치
pnpm install

# svelte.dev 앱으로 이동
cd apps/svelte.dev

# 문서 동기화 (처음 한 번만)
USE_GIT=true pnpm sync-docs

# 개발 서버 실행
pnpm run dev
```

## 📁 튜토리얼 파일 위치

튜토리얼 컨텐츠는 다음 경로에 있습니다:
```
apps/svelte.dev/content/tutorial/
├── part1-basic-svelte/
├── part2-advanced-svelte/
└── part3-basic-sveltekit/
```

각 튜토리얼은 `README.md` 파일을 번역하면 됩니다.

## 🤝 기여 방법

1. 이슈를 생성하여 번역할 파트를 선택합니다
2. 브랜치를 생성합니다: `git checkout -b translate/part-name`
3. 번역 작업을 진행합니다
4. 커밋하고 푸시합니다
5. Pull Request를 생성합니다

## 📝 번역 가이드

- 기술 용어는 원어를 병기합니다 (예: 컴포넌트(component))
- 코드 주석도 한글로 번역합니다
- 자연스러운 한국어 표현을 사용합니다

## 📜 라이선스

이 프로젝트는 원본 저장소와 동일한 라이선스를 따릅니다.

---

# 원본 README

# svelte.dev

This is the repository behind [svelte.dev](https://svelte.dev), the official Svelte site, and the related packages that it relies on.

## Documentation PRs

If you're creating a documentation PR, make sure you're targeting the right repository. More specifically, changes to content within `apps/svelte.dev/content/docs` are synced from other repositories, and documentation changes within those folder should therefore be made in those repositories:

- `docs/svelte` -> https://github.com/sveltejs/svelte
- `docs/kit` -> https://github.com/sveltejs/kit
- `docs/cli` -> https://github.com/sveltejs/cli

The tutorial, blog and examples are maintained within this repository.

## Setup

```
pnpm install
cd apps/svelte.dev
USE_GIT=true pnpm sync-docs
pnpm run dev
```
