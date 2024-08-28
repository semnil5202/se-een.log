# Redirect

Server Components, Route Handlers, Server Actions 환경에서 사용자의 URL을 리다이렉트 하기 위해 사용한다.

## 적용 사례

특정 페이지에서 사용자의 상태에 따라, 다른 URL로 리다이렉트가 필요로 했다. 최초에는 아래의 코드처럼 useEffect로 처리했다.

```ts
// 중략..
const { personStatus } = usePersonStatusQuery(personId);
const router = useRouter();

useEffect(() => {
  if (personStatus === 'signed') router.push('/somewhere');
}, [personStatus]);

// 중략..
```

이는 화면상에서 리다이렉트 전의 페이지가 잠깐 보였다가, 리다이렉트가 진행된다. 따라서 사용자 입장에서 의도치 않은 동작이 행해졌다고 오해할 수 있는 여지가 있다고 판단했다.

### Server Components, getServerSideProps에서 리다이렉트 수행

위 코드를 보면, usePersonStatusQuery는 서버에서 preFetching 후 personStatus에 따라서, 미리 리다이렉트를 진행할 수 있다.

```ts
// in Server Component
import { redirect } from 'next/navigation';

// 중략..

const getServerSide = async (personId) => {
  try {
    const cookie = cookies();
    const personStatus = await usePersonStatusPrefetch(personId, cookie);

    if (personStatus === 'signed') redirect('/somewhere');
  } catch (e) {
    console.error(e);
  }
};
```

### redirect 에러 발생

위 코드는 personStatus의 데이터는 정상적으로 받아오지만, redirect 쪽에서 에러가 발생한다. next.js 공식 문서에 가보면 redirect는 try-catch 문에 포함시키지 말라는 내용이 있다.

> In Server Actions and Route Handlers, redirect should be called after the try/catch block.

따라서 다음과 같이 수정해주면 정상적으로 동작한다.

```ts
const getServerSide = async (personId) => {
  let personStatus = null;

  try {
    const cookie = cookies();
    const personStatusResponse = await usePersonStatusPrefetch(
      personId,
      cookie
    );

    personStatus = personStatusResponse;
  } catch (e) {
    console.error(e);
  }

  if (personStatus === 'signed') redirect('/somewhere');
};
```

## 참고 링크

- 공식 문서: https://nextjs.org/docs/app/api-reference/functions/redirect
