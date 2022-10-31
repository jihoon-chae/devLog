## **리액트에서 왜 번들러를 사용할까?**

- `create-react-app`은 내장 라이브러리가 많아서 규모가 커지면 성능 문제가 발생한다! 따라서 웹팩으로 필요한 라이브러리만 설치할 수 있어야 한다.
- React는 원하는 라이브러리만 골라서 사용한다는 자유도가 높지만 많은 부가 라이브러리를 설치해야 한다는 부담이 있다.
- 따라서 이번 프로젝트에서 `create-react-app`의 많은 라이브러리 목록을 줄이고자 Webpack을 설치해 필요한 것들만 설정하여 개발하게 되었다.

- **리액트에 꼭 필요한 라이브러리**
    - react, react-dom
    - babel - 자바스크립트 컴파일러로 JSX를 JS로 변환하여 번들링해준다.
    - css-loader - css를 적용하게 해준다.
- **리액트에 도움되는 라이브러리**
    - eslint - JS 에러 방지위한 린터
    - prettier - 코드형식 통일성 맞추는 툴

## 프로젝트**에서 Webpack 적용하기**

1. package.json 생성

`npm init -y`

1. react 관련 라이브러리 설치

`npm install -D react react-dom`

1. 아래 명령어로 해당 폴더에 webpack 관련 라이브러리 설치

```jsx
npm install -D webpack webpack-cli webpack-dev-server html-webpack-plugin mini-css-extract-plugin
```

`webpack-cli` : 터미널에서 웹팩 명령어 실행 가능하게 해준다.

`webpack-dev-server` : 파일 변경사항 실시간으로 빌드하는 개발 서버 구동 (dev 서버)

`html-webpack-plugin` : html 파일에 번들링 된 js 파일을 삽입한다.

→ 설치 결과는 package.json에서 확인할 수 있다.

1. babel 관련 라이브러리 설치

```jsx
npm install -D babel-loader @babel/cli @babel/core @babel/preset-env @babel/preset-react
```

`babel-loader` : `babel.config.js` 또는 `.babelrc` 바벨 설정 파일을 읽어 해당 설정에 맞게 변환

`@babel/cli` : 터미널에서 바벨명령어 사용가능하도록 CLI 제공

`@babel/core` : babel의 핵심기능을 포함해서 반드시 설치해야 함

`@babel/preset-env` : es6, es7 버전을 지정안해도 babel이 자동 탐지

`@babel/preset-react` : 리액트(JSX)를 js로 인식가능

1. 로더 라이브러리 설치 (babel, css, sass)

```jsx
npm install -D css-loader babel-loader sass-loader file-loader
```

`css-loader` : CSS를 JS파일 내에서 불러올 수 있게 하기

`sass-loader` : .scss 파일을 JS 파일 내에서 불러올 수 있게 하기

`style-loader` : CSS를 style 태그 안에 담기 → `MiniCssExtractPlugin` 으로 대체

`file-loader` : .jpg, png 등의 파일 확장자 불러올 수 있도록 하기

1. webpack.config.js 생성

```jsx
var path = require("path");
var MiniCssExtractPlugin = require("mini-css-extract-plugin");
const HtmlWebPackPlugin = require("html-webpack-plugin");

module.exports = {
  mode: "development",
  entry: "./src/index.js", // 웹팩을 실행할 진입점으로 src폴더 내부의 index.js로 설정하겠다.
  output: {
    filename: "bundle.js", // 빌드할때마다 파일에 고유 값을 붙여줌 -> 내용 변했을때를 구분하기 위해서 chunkhash 사용함(별도의 새로고침없이)
    path: path.resolve(__dirname, "build"), // 웹팩의 결과물을 담는 파일로 build 폴더 내부의 bundle.js로 설정하겠다.
    assetModuleFilename: "assets/[name][ext]?[hash]", // images라는 폴더를 생성하고 내부에 해당 파일 생성
  },
  module: {
    // loader
    rules: [
      {
        test: /\.scss$/, // 모든 .scss 파일을 대상으로 함
        use: [
          { loader: MiniCssExtractPlugin.loader },
          "css-loader",
          "sass-loader",
        ], // style 태그 대신 css파일로 만들어줌
      },
      {
        test: /\.(js|jsx)$/,
        loader: "babel-loader",
        exclude: /node_modules/, // 노드모듈은 제외하겠다.
        options: { presets: ["@babel/env", "@babel/preset-react"] },
      },
      {
        test: /\.(png|jpg|jpeg|gif|svg)$/,
        type: "asset/resource", // file-loader 대신 사용
      },
    ],
  },
  devServer: {
    port: 9000, // dev 서버의 포트를 9000으로 하겠다.
  },
  plugins: [
    new MiniCssExtractPlugin(),
    new HtmlWebPackPlugin({
      template: "index.html",
    }),
  ],
};
```

 

1. 폴더에 `index.html` 파일을 생성하고 아래 내용 추가

```jsx
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title></title>
</head>
<body>
    <div id="root"></div>
</body></html></body>
</html>
```

1. 프로젝트 루트 레벨에 `src` 폴더를 생성하고 그 안에 `index.js` 파일 생성(`App.jsx` import 해오기)

```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App.jsx";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

1. `index.js` 와 동일한 경로에 `App.jsx` 파일 생성(`Home.jsx` import 해오기)

```jsx
import React from "react";
import Home from "./pages/home/Home.jsx";

function App() {
  return (
    <>
      <Home />
    </>
  );
}

export default App;
```

1. `Home.jsx`에서 .scss 파일과 이미지 import로 연결하기

```jsx
import React from "react";
import "./home.scss";

import "../../../src/assets/logo-cutout.png";
import "../../../src/assets/icon/icon-post-list-off2.png";
...

export default function Home() {
  return (
    <>
      <div id="app">
        {/* header   */}
        <header>
       ...
        </header>

        {/* main  */}
        <main>
         ...
        </main>

        {/* footer  */}
        <footer class="company-container">
       ...
        </footer>
      </div>
    </>
  );
}
```

## 참고자료

[https://juni-official.tistory.com/158](https://juni-official.tistory.com/158)

[https://berkbach.com/웹팩-webpack-과-바벨-babel-을-이용한-react-개발-환경-구성하기-fb87d0027766](https://berkbach.com/%EC%9B%B9%ED%8C%A9-webpack-%EA%B3%BC-%EB%B0%94%EB%B2%A8-babel-%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%9C-react-%EA%B0%9C%EB%B0%9C-%ED%99%98%EA%B2%BD-%EA%B5%AC%EC%84%B1%ED%95%98%EA%B8%B0-fb87d0027766)

[https://joshua1988.github.io/webpack-guide/guide.html](https://joshua1988.github.io/webpack-guide/guide.html)

[https://bravenamme.github.io/2020/02/12/what-is-babel/](https://bravenamme.github.io/2020/02/12/what-is-babel/) 

[https://velog.io/@juno7803/React-React에서-SVG-활용하기](https://velog.io/@juno7803/React-React%EC%97%90%EC%84%9C-SVG-%ED%99%9C%EC%9A%A9%ED%95%98%EA%B8%B0)

[https://agal.tistory.com/68](https://agal.tistory.com/68)
