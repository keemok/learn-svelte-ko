---
title: Spread props
---

이 실습에서 `App.svelte`는 `PackageInfo.svelte`가 필요로 하는 `name` prop을 전달하는 걸 깜빡했어요. 그래서 `<code>` 요소가 비어있고 npm 링크도 깨졌죠.

prop을 추가해서 고칠 수도 있어요...

```svelte
/// file: App.svelte
<PackageInfo
	+++name={pkg.name}+++
	version={pkg.version}
	description={pkg.description}
	website={pkg.website}
/>
```

...하지만 `pkg`의 속성들이 컴포넌트가 기대하는 props와 일치하기 때문에, 대신 컴포넌트에 'spread' 할 수 있어요:

```svelte
/// file: App.svelte
<PackageInfo +++{...pkg}+++ />
```

> [!NOTE] 반대로, `PackageInfo.svelte`에서는 rest 속성을 사용해서 컴포넌트에 전달된 모든 props를 포함하는 객체를 가져올 수 있어요...
>
> ```js
> let { name, ...stuff } = $props();
> ```
>
> ...또는 [구조 분해 할당(destructuring)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)을 완전히 건너뛸 수도 있어요:
>
> ```js
> let stuff = $props();
> ```
>
> ...이 경우 객체 경로로 속성에 접근할 수 있어요:
>
> ```js
> console.log(stuff.name, stuff.version, stuff.description, stuff.website);
> ```
