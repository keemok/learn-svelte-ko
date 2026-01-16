# 🇰🇷 Svelte 공식 튜토리얼 한글 번역

이 저장소는 [Svelte 공식 사이트](https://svelte.dev)의 튜토리얼을 한글로 번역하는 프로젝트입니다.

> **원본 저장소**: [sveltejs/svelte.dev](https://github.com/sveltejs/svelte.dev)

## 🎯 프로젝트 목표

한국어 사용자들이 Svelte를 쉽게 학습할 수 있도록 공식 튜토리얼을 한글로 번역합니다.

## 📊 번역 진행 상황

### Part 1: Basic Svelte (01-svelte)
- [x] **Introduction** (소개) - 완료 ✅
  - [x] Welcome to Svelte (Svelte에 오신 것을 환영합니다)
  - [x] Your first component (첫 번째 컴포넌트)
  - [x] Dynamic attributes (동적 속성)
  - [x] Styling (스타일링)
  - [x] Nested components (중첩된 컴포넌트)
  - [x] HTML tags (HTML 태그)
- [x] **Reactivity** (반응성) - 완료 ✅
  - [x] State (상태)
  - [x] Deep state (깊은 상태)
  - [x] Derived state (파생 상태)
  - [x] Inspecting state (상태 검사하기)
  - [x] Effects (이펙트)
  - [x] Universal reactivity (범용 반응성)
- [x] **Props** - 완료 ✅
  - [x] Declaring props (Props 선언하기)
  - [x] Default values (기본값)
  - [x] Spread props (Spread props)
- [x] **Logic** (로직) - 완료 ✅
  - [x] If blocks (If 블록)
  - [x] Else blocks (Else 블록)
  - [x] Else-if blocks (Else-if 블록)
  - [x] Each blocks (Each 블록)
  - [x] Keyed each blocks (키가 있는 each 블록)
  - [x] Await blocks (Await 블록)
- [x] **Events** (이벤트) - 완료 ✅
  - [x] DOM events (DOM 이벤트)
  - [x] Inline handlers (인라인 핸들러)
  - [x] Capturing (캡처링)
  - [x] Component events (컴포넌트 이벤트)
  - [x] Spreading events (이벤트 spread)
- [x] **Bindings** (바인딩) - 완료 ✅
  - [x] Text inputs (텍스트 입력)
  - [x] Numeric inputs (숫자 입력)
  - [x] Checkbox inputs (체크박스 입력)
  - [x] Select bindings (Select 바인딩)
  - [x] Group inputs (그룹 입력)
  - [x] Multiple select bindings (다중 선택)
  - [x] Textarea inputs (Textarea 입력)
- [x] **Classes and styles** (클래스와 스타일) - 완료 ✅
  - [x] The class attribute (class 속성)
  - [x] The style directive (style 디렉티브)
  - [x] Component styles (컴포넌트 스타일)
- [x] **Attachments** (Attachment) - 완료 ✅
  - [x] The attach tag (attach 태그)
  - [x] Attachment factories (Attachment 팩토리)
- [x] **Transitions** (트랜지션) - 완료 ✅
  - [x] The transition directive (transition 디렉티브)
  - [x] Adding parameters (파라미터 추가하기)
  - [x] In and out (In과 out)
  - [x] Custom CSS transitions (커스텀 CSS 트랜지션)
  - [x] Custom JS transitions (커스텀 JS 트랜지션)
  - [x] Transition events (트랜지션 이벤트)
  - [x] Global transitions (전역 트랜지션)
  - [x] Key blocks (Key 블록)

### Part 2: Advanced Svelte (02-advanced-svelte)
- [x] **Advanced reactivity** (고급 반응성) - 완료 ✅
  - [x] Raw state (Raw 상태)
  - [x] Reactive classes (반응형 클래스)
  - [x] Getters and setters (Getter와 Setter)
  - [x] Reactive built-ins (반응형 내장 객체)
  - [x] Stores (스토어)
- [x] **Snippets** (Snippet) - 완료 ✅
  - [x] Snippets and render tags (Snippet과 render 태그)
  - [x] Passing snippets to components (컴포넌트에 snippet 전달하기)
  - [x] Implicit snippet props (암시적 snippet props)
- [ ] Motion
- [ ] Advanced bindings
- [ ] Advanced transitions
- [ ] Context
- [ ] Special elements
- [ ] Script module
- [ ] Next steps

### Part 3: Basic SvelteKit (03-sveltekit)
- [ ] 작업 예정

### Part 4: Advanced SvelteKit (04-advanced-sveltekit)
- [ ] 작업 예정

## 🚀 로컬 개발 환경 설정

### 1. pnpm 설치

#### Windows
**npm 사용 (권장):**
```bash
npm install -g pnpm
```

**PowerShell (관리자 권한):**
```powershell
iwr https://get.pnpm.io/install.ps1 -useb | iex
```

**Chocolatey:**
```bash
choco install pnpm
```

#### macOS/Linux
**npm 사용:**
```bash
npm install -g pnpm
```

**Homebrew (macOS):**
```bash
brew install pnpm
```

**curl (Linux/macOS):**
```bash
curl -fsSL https://get.pnpm.io/install.sh | sh -
```

설치 확인:
```bash
pnpm --version
```

### 2. 의존성 설치
```bash
cd C:\project\13.svelte_learn\learn-svelte-ko
pnpm install
```

### 3. svelte.dev 앱으로 이동
```bash
cd apps\svelte.dev
```

### 4. 문서 동기화 (처음 한 번만)
**PowerShell:**
```powershell
$env:USE_GIT="true"; pnpm sync-docs
```

**CMD:**
```cmd
set USE_GIT=true && pnpm sync-docs
```

**Git Bash:**
```bash
USE_GIT=true pnpm sync-docs
```

### 5. 개발 서버 실행
```bash
pnpm run dev
```

브라우저에서 `http://localhost:5173/tutorial/svelte/welcome-to-svelte` 접속

## 📁 튜토리얼 파일 위치

튜토리얼 컨텐츠는 다음 경로에 있습니다:
```
apps/svelte.dev/content/tutorial/
├── 01-svelte/              # Part 1: Basic Svelte
├── 02-advanced-svelte/     # Part 2: Advanced Svelte
├── 03-sveltekit/           # Part 3: Basic SvelteKit
└── 04-advanced-sveltekit/  # Part 4: Advanced SvelteKit
```

각 튜토리얼의 `index.md` 파일을 번역합니다.

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
- 존댓말을 사용합니다

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
