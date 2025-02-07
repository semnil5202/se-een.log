# Favicon

## 파비콘은 ico 확장자만 등록해야하는가?

png, jpg, jpeg 등의 포맷도 가능하나, ico를 권장한다.

모던 브라우저는 favicon 관련 link 태그가 없다면 기본적으로 `favicon.ico` 를 요청한다. 또한 `favicon.ico` 오래된 브라우저 (IE6 이하)와 하위 호환성을 고려할 수 있다.

따라서 favicon 404를 피하고 싶다면 `favicon.ico` 파일을 두는 것이 좋다.

배경 투명화는 ico 확장자도 이상없이 지원하므로, 배경 투명화를 위해 png 등의 확장자를 고려할 필요는 없다.

## 레퍼런스

스택오버플로우: https://stackoverflow.com/questions/1344122/favicon-png-vs-favicon-ico-why-should-i-use-png-instead-of-ico
