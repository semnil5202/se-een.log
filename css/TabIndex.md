# Tab Index

Tab 키를 사용하는 연속적인 키보드 탐색에서 어느 순서에 위치할지 지정하는 속성이다.

## 명세를 바탕으로 속성 살펴보기

[HTML4 명세](https://www.w3.org/TR/html401/interact/forms.html#h-17.11.1)에는 다음과 같이 되어있다.

- 할당할 수 있는 값은 0부터 32767 사이의 숫자여야하며, 만약 값 앞에 0이 붙어있다면 브라우저는 이를 무시해야한다.
- 탐색 순서는 작은 수에서 큰 수로 향한다. 값은 연속되지 않아도 된다.
- disabled 속성이 사용되어 있다면 탭 속성에 관여하지 않는다.

[HTML5 명세](https://html.spec.whatwg.org/multipage/interaction.html#sequential-focus-navigation-and-the-tabindex-attribute)에는 다음과 같이 되어있다.

- tabindex 값이 음의 정수라면 요소에 초점이 도달하지 않도록 한다.

따라서 HTML5로 넘어오면서 음수 값을 사용할 수 있도록 스펙이 추가되었다.

## 정리

- `tabindex="1"`

  - 문서 안에서 가장 먼저 초점을 받는다. 자연스러운 마크업 순서를 거스를 수 있을수도 있기 때문에 주의해서 사용해야 한다.

- `tabindex="0"`
  키보드 초점을 받을 수 없는 div, span과 같은 요소도 초점을 받을 수 있도록 만들어 준다. 초점을 받는 순서는 자연스러운 마크업 순서를 따른다.

- `tabindex="-1"`
  키보드 초점을 받을 수 있는 요소도 초점을 받을 수 없도록 만들어 준다.

## 참고 링크

- 참고 블로그: https://naradesign.github.io/tabindex.html
