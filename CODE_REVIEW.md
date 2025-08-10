# 1번 리뷰

- 범위 : styles/main.css | 5 ~ 20 line (:root 부분)

- 전체 개요
  CSS 변수로 색상, 패딩, 폰트 크기, 카드 스타일 등 기본 스타일 값들을 정의하였습니다.

- 기능 내용

  1. `--padding`은 화면을 키웠을 때 컨텐츠의 너비가 1280px를 넘지 않고, 최소 4rem로 유지하게 위해 `max(4rem, calc((100% - 1280px) / 2))`로 작성하였습니다.
  2. `-fs-heading-md-fluid`에는 `clamp(x, y, z)`를 이용하여 x에는 모바일 버전의 heading 사이즈와, z에는 데스크톱 버전의 사이즈를 넣었습니다. y값에는 개발자 도구에서 사이즈를 봐가면서 적절해 보이는 값으로 설정했습니다.

- 기타 (모르겠는 부분)

1. padding에 `max()` 함수를 사용하는 방식이 적절한지, 제 의도대로 잘 작성한건지 궁금합니다.
2. `clamp()` 함수의 중간값(y) 설정 기준과 좋은 값을 찾는 방법에 대해 조언 부탁드립니다.

# 2번 리뷰

- 범위 : styles/main.css | 80 ~ 87 line (.text-container 부분)

섹션마다 반복적으로 사용되는 구조인 '제목-설명' 구조를 `.text-container`로 묶어서 사용하였는데, 완전히 동일하게 생기진 않아서 이런식으로 큰 틀만 먼저 정하고 `.section-banner .text-container {...}` 이런식으로 선택자로 지정해서 수정했는데 적절한지.. 다른 방법이 있는지 알고 싶습니다. 이런 선택자를 많이 사용하는 것이 옳은지..

# 3번 리뷰

- 범위 :
  styles/main.css | 365 ~ 415 line,
  styles/mobile.css | 209 ~ 224 line
  (.article-subscribe form 부분)

.article-subscribe form(이메일 입력) 부분
mobile screen에서 'subscribe'버튼이 분리되는 구조로 바껴서, 이걸 어떻게 해결하는 것이 적절한지, 지금은 좀 꾸역꾸역 한 느낌이 있어서.. (깔끔하지 않은 느낌..)

# 4번 리뷰

- 범위 : styles/main.css | 499 ~ 553 line (footer 부분)

footer의 display를 어떻게 설정해야 하는지 모르겠습니다..
지금은 footer에 flex를 주고, footer-links 에 position: absolute를 줬는데, 적절한 방법인지? 아니면 grid라든지 다른 방법이 더 나을지..

# 5번 리뷰

- 범위 : index.html | 131 ~ 158 line (article 태그 부분)

`aside` 태그에서 `article` 태그로 수정했는데 `article` 태그의 사용이 적절한지

# 그외 질문

css 파일을 더 분리해야 하는지? 지금은 main.css 파일에 주석으로 구분해 놨는데, 파일 자체로 분리해야 하는지.. 분리한다면 파일의 적정 개수? 분리 기준.. 등이 궁금합니다. 찾아보기 힘들어짐..
