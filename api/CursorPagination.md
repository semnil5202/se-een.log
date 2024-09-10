# Cursor Pagination

페이지네이션엔 크게 두 가지 방식이 있다.

- Offset-based Pagination
  - DB의 Offset 쿼리로 페이지 단위 요청 및 응답
- Cursor-based Pagination
  - 클라이언트가 가져간 마지막 row 순서상 다음 row의 n개를 요청 및 응답

## Offset-based Pagination의 문제점

- 페이지 간 요청 사이에 데이터 변화가 있는 경우 중복 데이터 노출

  - 활동이 활발한 커뮤니티에서 게시판 페이지를 오고 갈 때, 전 페이지에서 봤던 글을 현재 페이지에도 보는 경우를 생각하면 쉽다.

- RDBMS에서 Offset 쿼리의 성능 이슈

  - 쿼리의 모든 값을 조회하면서 순회하기에, row 수가 아주 많은 경우 offset 값이 올라갈수록 퍼포먼스는 이에 비례하여 떨어진다.

## Cursor-based Pagination의 동작 방식

Offset-based Pagination은 클라이언트가 원하는 데이터가 n번째에 있다는데 집중하는 반면, Cursor-based Pagination은 클라이언트가 원하는 데이터가 어떤 데이터의 n번째 있다는데 집중합니다.

**따라서 처음부터 n개의 row를 조회한 뒤 20개가 아니라 n번 row 다음부터 20개를 요청하는 식이다.**

> 개인적인 생각으론 Array와 Hash Map을 비교하는 것과 비슷하지 않을까 싶다.

## 결론

- 동일 요소 중복 노출이 큰 영향을 주지 않고, 빈번한 수정이 일어나지 않는다면 Offset-based Pagination도 괜찮다.
- Cursor-based Pagination이 거의 모든 경우에서 더 좋다.
