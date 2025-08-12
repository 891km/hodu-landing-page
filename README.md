# 호두의 랜딩 페이지

#### 프로젝트 소개

- 본 프로젝트는 ‘호두의 랜딩 페이지’를 주제로 한 웹페이지 구현을 목표로 제작되었습니다.

- 데스크톱 환경을 우선으로 설계하였으며, 미디어 쿼리를 활용해 모바일 화면까지 최적화된 반응형 레이아웃을 구현하였습니다.

- 시멘틱 마크업과 접근성, SEO 등 웹 품질 요소를 고려하여 제작하였습니다.

#### 관련 링크

- **[[배포 URL 🔗]](https://891km.github.io/hodu-landing-page/)**

- **[[시연 영상 🎞️]](#)**

#### 작성자 및 개발자

- 김민주

<br>

## 요구사항 명세

| 번호 | 요구사항 내용                                       | 비고        |
| ---- | --------------------------------------------------- | ----------- |
| 1    | 피그마를 참고하여 페이지 구현                       | 디자인 준수 |
| 2    | 시멘틱, 반응형, 접근성, SEO, CSS 네이밍 방법론 고려 | 품질 기준   |
| 3    | 모바일 화면 고려하여 구현                           | 반응형 적용 |
| 4    | 스크롤 시 헤더 고정 구현                            | 기능 구현   |
| 5    | 구독하기 모달창 퍼블리싱 후 화면에서 숨김 처리      | 기능 데모   |

<br>

## 프로젝트 구조

```
📂
├─ .gitignore
├─ index.html
├─ README.md
├─assets
│  ├─icons
│  └─images
└─styles
    ├─ main.css
    ├─ mobile.css
    └─ reset.css
```

<br>

## 주요 고려 사항

### 1. 반응형 최적화

#### 1-1. CSS 변수를 통한 반응형 관리

- 화면을 키웠을 때 컨텐츠의 너비가 1280px를 넘지 않고, 최소 4rem로 유지하게 위해 `padding`에 `max ()` 함수를 사용하였습니다.

- `clamp ()` 함수를 사용하여 `font-size`와 `border-radius`가 뷰포트에 따라 유동적으로 적용되도록 하였습니다.

- 공통적으로 사용되는 값들을 CSS 변수로 지정하여 스타일 통일을 유지하고, 관리 효율성을 높였습니다.

  ```css
  :root {
    /* padding */
    --padding: max(4rem, calc((100% - 1280px) / 2));

    /* font-size */
    --fs-heading-lg-fluid: clamp(2.4rem, 4.8vw, 4.8rem);
    --fs-heading-md-fluid: clamp(2.4rem, 2.4vw, 3.6rem);
    --fs-body-md: 1.6rem;
    --fs-body-sm: 1.4rem;
    --fs-body-caption: 1.2rem;

    /* card style */
    --card-radius: clamp(1.8rem, 3vw, 3rem);
    --card-shadow: 1rem 1rem 3rem 0 rgba(0, 0, 0, 0.25);
  }
  ```

  #### 1-2. 자연스러운 레이아웃 변화

  - flex로 화면 너비에 따라 자연스럽게 바뀌게 함
  - 모바일 미디어 쿼리와 이어지게 함

### 2. 접근성 고려

#### 2-1. download 버튼의 툴팁

- 'download' 버튼에 `::after` 가상요소를 이용하여 버튼의 역할과 다운로드 파일명을 명시하는 툴팁 스타일링을 추가하였습니다.
  ![툴팁이 추가된 버튼 이미지](https://github.com/user-attachments/assets/cabf0129-d5f0-4940-8481-5f285ae7d51b)

#### 2-2. 포커스 스타일

- 입력 필드와 버튼 요소에 명도가 높은 컬러를 사용하여 '포커스 스타일'을 적용하여 사용자가 쉽게 인지할 수 있도록 하였습니다.

  ```css
  input:focus,
  :is(button, a):focus-visible {
    outline: 0.4rem solid #ff4000;
    outline-offset: 0.1rem;
  }
  ```

### 3. 이미지 최적화

- `<picture>` 태그를 사용해 `webp` 형식의 이미지와 미디어 쿼리에 따라 크기가 다른 이미지가 로드되도록 구현했습니다.

  ```html
  <picture>
    <source srcset="./assets/images/intro-cat-1280px.webp" type="image/webp" />
    <source
      srcset="./assets/images/intro-cat-768px.webp"
      media="screen and (max-width: 768px)"
      type="image/webp"
    />
    <img
      src="./assets/images/intro-cat.jpg"
      alt="배를 드러내고 누워있는 고양이 호두"
    />
  </picture>
  ```

### 4. 스타일링 컴포넌트화

- 공통 클래스를 부여해 반복되는 ‘제목-설명’ 구조에 기본 스타일을 적용하고, 섹션별 개별 스타일은 선택자를 사용하여 덮어썼습니다.
- `.text-container`로 기본 틀을 설정하고, 섹션별 차이를 위해 `.section-banner .text-container {...}` 같은 형태의 선택자를 사용하여 개별 스타일을 추가 및 변경하였습니다.

  ```css
  .text-container {
    text-align: left;
    display: flex;
    flex-direction: column;
    justify-content: start;
    align-items: start;
    gap: 4rem 0;
  }

  .section-banner .text-container {
    flex: 1 1 auto;
    min-width: 45rem;
    padding-top: 20rem;
  }
  ```

### 5. 스크롤바 스타일링

- 이미지 리스트의 가로 스크롤바가 hover 했을 때만 보이도록 하였습니다.
- 스크롤바의 스타일링을 통해 디자인 통일감을 주었습니다.
- 크로스 브라우징을 위한 추가의 스크롤바 코드를 넣었습니다.

  ```css
  /* for standard */
  .section-skills .image-list {
    scrollbar-width: auto;
    scrollbar-color: transparent transparent;
  }

  .section-skills .image-list:hover {
    scrollbar-color: #d976524c transparent;
  }

  /* for legacy */
  .section-skills .image-list::-webkit-scrollbar {
    width: 0.6rem;
    height: 1.2rem;
    background-color: transparent;
  }

  .section-skills .image-list::-webkit-scrollbar-thumb {
    background-color: transparent;
  }

  .section-skills .image-list:hover::-webkit-scrollbar-thumb {
    background-color: #d976524c;
    border-radius: 0.4rem;
  }
  ```

<br>

## 에러와 에러 해결

### 1. 반응형 레이아웃 조정

#### 1-1. 문제 정의

- 입력폼과 버튼 요소로 구성된 `form` 요소에서 데스크톱에서는 가로로 배치되고, 모바일 미디어 쿼리에서 버튼이 아래로 분리되게 배치해야 하는 문제가 있었습니다.

#### 1-2. 문제 해결

- `<input>` 태그를 `<div>` 태그로 감싸 `::before`를 이용하여 이메일 아이콘을 추가하여 레이아웃 관리에 용이하게끔 html 구조를 수정하였습니다.
- 데스크톱 화면에서는 `form`에 `display: flex`를 주어 한 줄로 배치하였습니다.
- 모바일 화면에서는 `flex-direction: column;`으로 수정하고, 기존 `form`에 적용했던 배경 스타일링을 `.input-wrapper`로 옮겨 버튼이 분리되는 것처럼 보이게 하였습니다.

  ```html
  <form action="#" method="post">
    <!-- ::before을 통해 이메일 아이콘 추가 -->
    <div class="input-wrapper">
      <input
        type="email"
        name="email"
        placeholder="Enter your e-mail address"
      />
    </div>
    <button
      class="btn"
      id="btn-open-modal"
      type="button"
      aria-label="블로그 구독 신청하기"
    >
      Subscribe
    </button>
  </form>
  ```

### 2. dialog와 display

#### 2-1. 문제 정의

- 요소의 가운데 정렬을 위해 `<dialog>` 태그에 `display: flex`를 적용했더니 dialog가 닫히지 않는 문제가 있었습니다.

#### 2-2. 문제 해결

- `<dialog>` 태그에는 `display` 속성을 제거하고, 하위 요소에 `display: flex`와 `margin` 속성을 적용하여 수정하였습니다.

<br />
