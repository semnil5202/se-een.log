# Permanent Redirect (301) vs Temporary Redirect (302)

301 영구 리다이렉트와 302 임시 리다이렉트의 차이점을 **SEO 측면**에서 서술한다.

## 설명

이 둘의 차이점은 사용자 입장에서 크게 다르지 않다. (캐시의 영향으로 인한 페이지 로딩 속도 차이는 있을 수 있다.)

### Permanent Redirect (301)

영구 리다이렉션은 말 그대로 사이트가 영구히 이전되었다는 뜻이다. 따라서 검색 엔진은 다음의 변경점이 생기게 된다.

- 기존 URL에 대한 SEO, URL 정보를 새로운 URL로 이전
- 새로운 URL에 대한 정보만 수집한다.
- 브라우저에서 기본적으로 캐싱이된다.

### Temporary Redirect (302)

임시 리다이렉션은 요청한 사이트가 임시로 이전되었는데 언제든 이전 URL로 돌아갈 수 있다는 뜻이다. 예를 들면, 사이트 점검 등의 상황에서 사용된다고 보면 되겠다.

- 기존 URL에 대한 SEO, URL 정보를 유지
- 기존 URL에 대한 정보를 수집한다. 컨텐츠만 새로운 URL에서 조회한다.
- Cache-control이나 Expire header를 명시해주어야 브라우저에서 캐싱이 된다.

## 참고 링크

- [301 vs 302 상태 코드 차이점 (SEO)](https://inpa.tistory.com/entry/HTTP-%F0%9F%8C%90-301-vs-302-%EC%83%81%ED%83%9C-%EC%BD%94%EB%93%9C-%EC%B0%A8%EC%9D%B4%EC%A0%90-%F0%9F%92%AF-%EC%99%84%EB%B2%BD-%EC%A0%95%EB%A6%AC)
