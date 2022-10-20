## Sass 기본

1. npm 설치

1. 터미널에서 -y를 써서 질문 없이 기본세팅

```
npm init -y
```

1. node-sass 설치

```
npm i node-sass 
```

→ node_modules와 package-lock.json이 생성됨

→ git commit을 할 경우, node_modules와 package-lock.json 파일은 .gitignore파일안에 작성하여 git commit에서 제외시키기

1. package.json안 "scripts"부분에 밑에 내용을 작성하여 컴파일할 파일과 컴파일될 파일명을 작성

```jsx
"sass": "node-sass -w -r scss/input.scss src/output.css "
```

나의 프로젝트에서

```jsx
"sass": "node-sass -w -r scss/style.scss src/style.css "
```

1. sass 실행하는 소스입니다.

```
npm run sass 
```

## Sass 아키텍쳐

 Sass 프로젝트를 구성하는 방법중 가장 대중적인 방식은 7-1 패턴이다.

즉 7개의 폴더에 속한 파일들을 단 하나의 파일 통해서 사용한다는 뜻이다.

### 7-1 패턴이란?

7-1패턴이란 7개의 폴더와 하나의 파일을 의미한다.

```
sass/
|
|– abstracts/
|   |– _variables.scss    # Sass Variables
|   |– _mixins.scss       # Sass Mixins
|
|– vendors/
|   |– _bootstrap.scss    # Bootstrap
|
|– base/
|   |– _reset.scss        # Reset/normalize
|   |– _typography.scss   # Typography rules
|
|– layout/
|   |– _navigation.scss   # Navigation
|   |– _grid.scss         # Grid system
|   |– _header.scss       # Header
|   |– _footer.scss       # Footer
|   |– _sidebar.scss      # Sidebar
|   |– _forms.scss        # Forms
|
|– components/
|   |– _buttons.scss      # Buttons
|   |– _carousel.scss     # Carousel
|   |– _cover.scss        # Cover
|   |– _dropdown.scss     # Dropdown
|
|– pages/
|   |– _home.scss         # Home specific styles
|   |– _contact.scss      # Contact specific styles
|
|– themes/
|   |– _theme.scss        # Default theme
|   |– _admin.scss        # Admin theme
|
 – main.scss              # Main Sass input file
```

### 1. abstracts

abstracts 폴더는 프로젝트 전체에 사용되는 모든 Sass 도구와 도우미를 담고 있다.

ex) 모든 전역 변수, 함수, mixin 및 표시자

- _variables.scss
- _mixins.scss
- _functions.scss
- _placeholders.scss

### 2. vendors

프로젝트에서 사용하는 외부 라이브러리 및 프레임워크의 모든 CSS 파일을 담고 있다. 현재 프로젝트에서 사용하지 않는다.

- _bootstrap.scss
- _jquery-ui.scss
- _select2.scss

### 3. base

프로젝트의 상용구 코드를 담고 있다. 사이트 전반에 사용될 폰트, 디폴트 스타일이 해당된다. 

- _base.scss (HTML 요소 - html, body 등 디폴트)
- _reset.scss (브라우저 기본 CSS 초기화)
- _typography.scss (폰트)
- _animations.scss (@keyframes를 포함한 애니메이션)

### 4. layout

사이트 구조에 해당하는 레이아웃을 담고 있다.

- _grid.scss
- _header.scss
- _footer.scss
- _sidebar.scss
- _forms.scss
- _navigation.scss

### 5.  components

layout보다 더 작은 구성요소를 담고 있으며  사이트 내에서 재사용이 가능한 부분들을 의미한다.

Ex) button, slider, loader …

- _buttons.scss
- _media.scss
- _carousel.scss
- _thumbnails.scss

### 6. pages

페이지 고유의 스타일이 있는 경우 페이지 이름을 딴 파일을 만들어 사용한다.

- _home.scss
- _contact.scss

### 7. themes

대규모 사이트와 애플리케이션에는 다양한 모드의 테마를 사용하고는 하는데, 각 모드에 따라서 각기 다른 스타일을 지정하여 담아두는 곳이다.

- _theme.scss
- _admin.scss

### main.scss

위와 같이 각 폴더 기준에 따라 scss 파일들을 분류했다면, 이 모든 파일들을 단 하나의 파일로 모아서 사용한다. 해당 파일은 직접적으로 스타일을 정의하지 않고 단지 import만 담당하는 파일이다.

## 참고자료

[https://mine-it-record.tistory.com/594](https://mine-it-record.tistory.com/594)

[https://www.learnhowtoprogram.com/user-interfaces/building-layouts-preprocessors/7-1-sass-architecture](https://www.learnhowtoprogram.com/user-interfaces/building-layouts-preprocessors/7-1-sass-architecture)

[https://nykim.work/97](https://nykim.work/97)

[https://velog.io/@mangozoo20/Sass-SCSS-정리](https://velog.io/@mangozoo20/Sass-SCSS-%EC%A0%95%EB%A6%AC)
