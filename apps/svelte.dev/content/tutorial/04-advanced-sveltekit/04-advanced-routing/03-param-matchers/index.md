---
title: 파라미터 매처
path: /colors/ff3e00
---

라우터가 유효하지 않은 입력과 매칭되는 것을 방지하려면 매처(matcher)를 지정할 수 있어요. 예를 들어, `/colors/[value]` 같은 라우트가 `/colors/ff3e00` 같은 16진수 값과는 매칭되지만 `/colors/octarine` 같은 명명된 색상이나 다른 임의의 입력과는 매칭되지 않기를 원할 수 있어요.

먼저, `src/params/hex.js`라는 새 파일을 만들고 `match` 함수를 export하세요:

```js
/// file: src/params/hex.js
export function match(value) {
	return /^[0-9a-f]{6}$/.test(value);
}
```

그러면, 새 매처를 사용하려면 `src/routes/colors/[color]`를 `src/routes/colors/[color=hex]`로 이름을 바꾸세요.

이제 누군가 그 라우트로 탐색할 때마다 SvelteKit은 `color`가 유효한 `hex` 값인지 확인할 거예요. 아니라면 SvelteKit은 다른 라우트와 매칭을 시도하고, 결국 404를 반환할 거예요.

> [!NOTE] 매처는 서버와 브라우저 둘 다에서 실행돼요.
