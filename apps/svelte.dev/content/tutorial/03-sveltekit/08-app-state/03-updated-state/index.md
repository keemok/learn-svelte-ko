---
title: updated
---

`updated` 상태는 페이지가 처음 열린 이후 앱의 새 버전이 배포됐는지 여부에 따라 `true` 또는 `false`를 담고 있어요. 이게 작동하려면 `svelte.config.js`가 `kit.version.pollInterval`을 지정해야 해요.

```svelte
/// file: src/routes/+layout.svelte
<script>
	import { page, navigating, +++updated+++ } from '$app/state';
</script>
```

버전 변경은 프로덕션에서만 일어나고, 개발 중에는 일어나지 않아요. 그런 이유로 이 튜토리얼에서는 `updated.current`가 항상 `false`일 거예요.

`pollInterval`과 관계없이 `updated.check()`를 호출해서 수동으로 새 버전을 확인할 수 있어요.

```svelte
/// file: src/routes/+layout.svelte

+++{#if updated.current}+++
	<div class="toast">
		<p>
			A new version of the app is available

			<button onclick={() => location.reload()}>
				reload the page
			</button>
		</p>
	</div>
+++{/if}+++
```

> [!NOTE] SvelteKit 2.12 이전에는 이를 위해 `$app/stores`를 사용해야 했어요. 같은 정보를 담고 있는 `$updated` 스토어를 제공하죠. 현재 `$app/stores`를 사용하고 있다면, `$app/state`로 마이그레이션하는 걸 권장해요 (Svelte 5 필요).
