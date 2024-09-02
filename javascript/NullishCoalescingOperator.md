# Nullish Coalescing Operator

널 병합 연산자 (??) 는 왼쪽 피연산자가 null 또는 undefined일 때 오른쪽 피연산자를 반환하고, 그렇지않
으면 왼쪽 피연산자를 반환하는 논리 연산자이다.

## Or Operator와 차이

개인적으로 논리적 OR (||) 연산자와 혼용해서 사용하는 경우가 적지 않게 있었다고 생각한다. OR 연산자 역시
왼쪽 피연산자의 값이 falsy 한 경우 오른쪽 피연산자 값을 반환하는 특성이 있기 떄문이다.

하지만 falsy한 것과 null 또는 undefined 한 것에서 널 병합 연산자와 논리 연산자와의 차이가 있다.

```ts
const result = 0 || 'hello'; // hello

const result = 0 ?? 'hello'; // 0
```

자바스크립트는 `null, undefined, 0, ''` 등 falsy한 값이 여러 개가 있다. 검증하고자 하는 목적이 falsy
한 값을 파악하는 것인지, 예기치 않은 null 또는 undefined를 식별하고자 하는 것인지 생각해서 연산자를
선택해서 적용할 필요가 있다.
