---
title: 동적 속성
---

중괄호로 텍스트를 제어할 수 있는 것처럼, 요소의 속성도 제어할 수 있어요.

이미지에 `src` 속성이 빠져있네요. 추가해봐요:

```svelte
/// file: App.svelte
<img +++src={src}+++ />
```

훨씬 좋아졌어요. 하지만 에디터에서 `<img>`에 마우스를 올려보면 Svelte가 경고를 띄워요:

```
`<img>` element should have an alt attribute
```

웹 앱을 만들 때는 시각 장애나 신체적 제약이 있는 사람, 성능이 낮은 기기를 쓰는 사람, 인터넷이 느린 환경의 사람 등 다양한 사용자가 모두 사용할 수 있게 만드는 게 중요해요. 접근성(Accessibility, a11y)을 완벽하게 구현하기가 쉽지는 않지만, Svelte는 접근성이 떨어지는 마크업을 작성하면 경고를 띄워서 도와줘요.

지금 경우에는 스크린 리더를 쓰는 분들이나 인터넷이 느려서 이미지를 못 불러오는 분들을 위한 `alt` 속성이 빠져있어요. 추가해봐요:

```svelte
/// file: App.svelte
<img src={src} +++alt="A man dances."+++ />
```

속성 안에서도 중괄호를 쓸 수 있어요. `"{name} dances."`로 바꿔보세요. `<script>` 블록에 `name` 변수를 선언하는 걸 잊지 마세요.

## 속성 단축 표기법

`src={src}`처럼 속성 이름과 값이 같은 경우가 종종 있어요. Svelte는 이럴 때 쓸 수 있는 편리한 단축 표기법을 제공해요:

```svelte
/// file: App.svelte
<img +++{src}+++ alt="{name} dances." />
```
