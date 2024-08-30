# z-index Stacking Context

쌓임 맥락(stacking context)은 사용자가 뷰포트를 바라보는 시점에서 가상의 Z축을 사용하여 HTML 요소를 3차원화한 개념이다. 대표적으로 z-index 속성이 있는데, z-index 속성은 다음의 규칙을 따른다.

- 일반적인 HTML 요소들은 읽히는 순서대로 (코드상 위에서 아래로) 쌓인다.
- position 속성이 있는 HTML 요소는 일반적인 HTML 요소보다 위에 읽히는 순서대로 쌓인다.
- z-index 속성이 있다면 z-index 값이 큰 HTML 요소가 위에 쌓이지만, 이는 부모 HTML 요소의 z-index를 기준으로 한다.

## 예시

```html
<div style="position: absolute; z-index: 10">element #2</div>

<div style="position: absolute; z-index: 1">
  <div style="position: absolute; z-index: 1000">element #5</div>
  <div style="position: absolute; z-index: 100">element #4</div>
  element #3
</div>

<div>element #1</div>
```

위와 같은 코드가 있다고 할 때, Z축의 관점에서 사용자가 보이는 순서대로 요소를 나열하면 `#2 - #5 - #4 - #3 - #1`이 된다.

#1은 마지막에 읽혔음에도 position static 이므로 가장 아래에 쌓이고, position absolute 요소들이 그 위에 쌓이게 된다. 여기서 #5와 #4가 #2보다 z-index 값은 크지만, 속한 부모 요소의 z-index 값(#3)이 #2보다 작기에, 최종적으로 #2가 가장 위에 쌓이게 된다.

#5와 #4는 #3에서의 z-index 값에 따른 우선 순위가 적용되며 #5 - #4 - #3 순으로 보이게된다.

## 참고 링크

- 제로초 블로그 z-index: https://www.zerocho.com/category/CSS/post/5a18b330e9c0ec001b08238e
- Stacking Context MDN: https://developer.mozilla.org/ko/docs/Web/CSS/CSS_positioned_layout/Understanding_z-index/Stacking_context
