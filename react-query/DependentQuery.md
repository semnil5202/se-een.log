# Dependent Query

현재의 쿼리가 이전의 다른 쿼리에 의존적인 경우 사용한다. `enabled` 옵션을 활용하여 만들어 볼 수 있다.

## 문제 상황

아래 코드 블록처럼 `useRelayQuestionQuery`가 이전 쿼리의 `useMyMeetingsQuery`에 의존적인 상황이다. myMeetings 값이 보장되어야 `useRelayQuestionQuery`의 실행이 가능한 상황.

```ts
const { myMeetings } = useMyMeetingsQuery();
const { questions } = useRelayQuestionListQuery(
  myMeetings?.meetingIds[0] || NULL_ID
);
```

위 코드 블록을 실행하면 첫 fetch에선 `useRelayQuestionQuery`의 요청이 실패하고, 두 번째 fetch에서 정상적으로 데이터를 받아온다. 따라서 이런 경우는 아래와 같이 `useRelayQuestionQuery`를 수정해볼 수 있겠다.

## 해결 방법

아래와 같이 `enabled` 옵션으로 meetingId 값이 보장되었을 경우에만 `useRelayQuestionQuery`를 실행하도록 한다.

```ts
export const useRelayQuestionListQuery = (meetingId: number) => {
  const { data, ...rest } = useQuery({
    queryKey: [RELAY_QUESTION_LIST_QUERY_KEY, meetingId],
    queryFn: () => {
      return _getRelayQuestionList(meetingId);
    },
    // ✅
    enabled: !!meetingId,
  });

  return { questions: data, ...rest };
};
```

다만 이런 경우, 예시로 쓴 코드 블록에선 `useRelayQuestionQuery`의 인자 값의 타입을 강제해야 하는 불편함이 있다.

```ts
const { myMeetings } = useMyMeetingsQuery();
const { questions } = useRelayQuestionListQuery(
  // ✅
  myMeetings?.meetingIds[0]!
);
```

## 참고 링크

- 공식 문서: https://tanstack.com/query/v5/docs/framework/react/guides/dependent-queries
