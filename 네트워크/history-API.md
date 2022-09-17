### history API

history API는 브라우저에서 제공하는 주소 API를 사용해 주소를 변경합니다.

history API의 필요성은 주소가 바뀌지 않는 싱글 페이지 애플리케이션(SPA)에서 나타납니다. 이 API는 기존 history 객체(`window.history`)를 그대로 활용합니다. 따라서 자바스크립트로 뒤로가기(`history.back()`)와 앞으로 가기(`history.forward()`), 지정한 위치로 가기(`history.go(인덱스)`)를 모두 사용할 수 있습니다. 

주소 내역은 하나의 목록으로 뒤로가기, 앞으로가기는 목록 안에서 이동하는 것입니다. 따라서 목록에 새로운 주소를 추가하면 페이지를 이동한 셈이 됩니다. 목록에 주소를 추가하기 위한 메소드가 HTML5에서 생겼습니다.

바로 `history.pushState()` 와 `history.replaceState()` 입니다.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>History API</title>
  </head>
  <body>
    <div id="state">
    <button id="pushState-login">pushState 로그인</button>
    <button id="pushState-home">pushState 홈</button>
    <button id="pushState-profile">pushState 프로필</button>
  </div>

  <div id="state2">
    <button id="replaceState-login">replaceState 로그인</button>
    <button id="replaceState-home">replaceState 홈</button>
    <button id="replaceState-profile">replaceState 프로필</button>
  </div>
  </body>
</html>
```

```jsx
document.querySelector("#pushState-login").addEventListener("click", function () {
        history.pushState({ data: "로그인" }, "title을 login로", "/login");
      });

      document.querySelector("#pushState-home").addEventListener("click", function () {
        history.pushState({ data: "홈" }, "title을 home로", "/home");
      });

      document.querySelector("#pushState-profile").addEventListener("click", function () {
        history.pushState({ data: "프로필" }, "title을 profile로", "/profile");
      });

      

      document.querySelector("#replaceState-login").addEventListener("click", function () {
        history.replaceState({ data: "로그인" }, "title을 login로", "/login");
      });

      document.querySelector("#replaceState-home").addEventListener("click", function () {
        history.replaceState({ data: "홈" }, "title을 home로", "/home");
      });

      document.querySelector("#replaceState-profile").addEventListener("click", function () {
        history.replaceState({ data: "프로필" }, "title을 profile로", "/profile");
      });

      window.addEventListener("popstate", function () {
        console.log("popstate", history.state);
        document.querySelector("#state").innerHTML = JSON.stringify(
          history.state
        );
      });

      window.addEventListener('popstate', function () {
        console.log('popstate', history.state);
        document.querySelector('#state2').innerHTML = JSON.stringify(history.state);
      });
```

첫 번째 인자는 바뀐 주소와 함께 저장할 데이터 객체이고, 두 번째 인자는 바꿀 제목, 세 번째 인자는 바꿀 주소입니다.

```jsx
history.pushState({데이터 객체}, 바꿀 제목, 바꿀 주소)
history.replaceState({데이터 객체}, 바꿀 제목, 바꿀 주소)
```

주소와 함께 데이터도 저장할 수 있기 때문에 매우 유용합니다. 이 데이터에 바뀔 페이지의 정보들을 담아두고 클라이언트에서 정보를 활용해 새로운 페이지를 렌더링하면 됩니다. 정보는 `history.state`로 접근할 수 있습니다.

두 번째 인자는 제목인데 브라우저에서 아직 제목 바꾸는 것까지는 구현하지 않았습니다. 그냥 빈 문자열을 넣어 두는 정도로 하시면 됩니다.

세 번째 인자는 바뀔 주소입니다. 

`pushState`의 경우

초기주소

```jsx
http://127.0.0.1:5501/index.html
```

로그인 버튼 > 홈버튼 > 프로필버튼을 차례로 클릭할 경우 다음과 같이 주소가 차례로 변경 되고 뒤로가기 버튼이 활성화 됩니다.

 

```jsx
http://127.0.0.1:5501/login // 1

http://127.0.0.1:5501/home // 2

http://127.0.0.1:5501/profile // 3
```

이 상태에서 뒤로가기 버튼을 클릭시 다음의 주소로 변경됩니다.

```jsx
http://127.0.0.1:5501/home
```

뒤로가기 번튼을 한번 더 클릭시 다음의 주소로 변경됩니다.

```jsx
http://127.0.0.1:5501/login
```

`pushState`는 주소 목록에 새로운 주소를 추가합니다. 따라서  `/index.html`을 이전 주소로 두고 `/login` ,`/home` , `/profile` 을 차례로 추가한 것입니다. 이전의 주소가 남아 있기 때문에 뒤로가기를 통해 `/profile` →  `/home` → `/login` 으로 되돌아 갈 수 있습니다.

하지만 `replaceState` 이전 주소를 없애고 바꿀 주소를 넣습니다. /index.html이라는 주소 기록을 지우고 `/login` ,`/home` , `/profile` 를 추가하는 것입니다. 따라서 `/profile` 에서 뒤로가기를 통해서 `/home` 이나 `/login` 에 접근할 수 없습니다.

### 참고자료

[history push와 replace의 차이](https://medium.com/w-bs-log/history-push%EC%99%80-replace%EC%9D%98-%EC%B0%A8%EC%9D%B4-ed5f2f7db7dc)

[[TIL_개발일기_210317] history.push()와 history.replace()의 차이점](https://dolphinsarah.tistory.com/17)

[[Next.js] Router.push와 Router.replace의 차이](https://soft91.tistory.com/97)

[ZeroCho Blog](https://www.zerocho.com/category/HTML&DOM/post/599d2fb635814200189fe1a7)
