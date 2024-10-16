# getInitialProps d

각 페이지 접속 (또는 전환) 시 서버 또는 클라이언트 측에서 수행할 작업을 명시할 수 있는 함수이다. [현재는 Legacy API로 분류되어 있으며](https://nextjs.org/docs/pages/api-reference/functions/get-initial-props) 상황에 맞게 아래의 것들을 사용할 것을 권장하고 있다.

- getStaticProps: 빌드 타임에서 정적 사이트 생성 시
- getStaticPaths: 빌드 타임에서 동적 라우팅에 따른 페이지 경로를 지정
- getServerSideProps: 매 요청시마다 데이터 페칭 등의 작업을 수행

## 사용 방법

\_app.js 에서 다음과 같이 사용해볼 수 있다.

```ts
export default function APP({ Component, pageProps }: AppProps) {}

App.getInitialProps = async ({ Component, ctx }: AppContext) => {
  const pageProps = {};

  return {
    pageProps,
  };
};
```

### 커스터마이징

getInitialProps는 페이지/최상위 파일에서만 사용할 수 있으며 중첩된 구성 요소에서는 사용할 수 없다는 특징이 있다. 하지만 아래와 같이 커스터마이징을 하면 최종 결과를 pageProps에 담을 수 있다. 무엇을 담을 수 있는지는 [여기서 확인하자.](https://nextjs.org/docs/pages/api-reference/functions/get-initial-props#context-object)

```ts
App.getInitialProps = async ({ Component, ctx }: AppContext) => {
  let pageGetInitialProps = {};

  if (Component.getInitialProps) {
    pageGetInitialProps = await Component.getInitialProps(ctx);
  }

  return {
    pageProps: {
      // App ctx 전개
      ...pageGetInitialProps,
    },
  };
};
```

### 서버사이드 사이클

- Next Server가 GET 요청을 받는다.
- 요청에 맞는 Page를 찾는다.
- \_app.js의 getInitialProps가 있다면 실행한다.
- Page Component의 getInitialProps가 있다면 실행한다. pageProps들을 받아온다.
- \_document.js의 getInitialProps가 있다면 실행한다. pageProps들을 받아온다.
- 모든 props들을 구성하고, \_app.js > page Component 순서로 rendering.
- 모든 Content를 구성하고 \_document.js를 실행하여 html 형태로 출력한다.

### 알아둬야할 점

- getInitialProps에서 반환된 데이터는 서버 렌더링 시 직렬화된다. 따라서 Map, Set을 사용하지 않는 일반 객체인지 확인할 것.
- getInitialProps는 최초 페이지 로드의 경우에만 서버에서 실행된다. 이후 `next/link`, `next/router`를 사용하여 다른 경로로 이동할 때는 클라이언트에서도 실행된다.
  - 단, \_app.js 이후에 탐색 중인 페이지에서 getServerSideProps를 사용하면 getInitialProps도 서버에서 실행된다.
- getInitialProps를 사용하면 자동 정적 페이지 최적화 (Automatic Static Optimization)를 [지원할 수 없다.](https://velog.io/@suyeon9456/getInitialProps-vs-getServerSideProps) 따라서, 각 페이지 특성에 맞게 getStaticProps, getStaticPaths, getServerSideProps을 사용하는게 좋다.

## 참고 링크

- 공식 문서: https://nextjs.org/docs/pages/api-reference/functions/get-initial-props
- Next js 구동방식 과 getInitialProps: https://velog.io/@cyranocoding/Next-js-%EA%B5%AC%EB%8F%99%EB%B0%A9%EC%8B%9D-%EA%B3%BC-getInitialProps
- getInitialProps vs getServerSideProps: https://velog.io/@suyeon9456/getInitialProps-vs-getServerSideProps
