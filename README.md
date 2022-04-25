## 리액트가 왜 좋은가요?

> 리액트 1분 내로 추가하기

- 리액트 공식문서 : https://ko.reactjs.org/docs/add-react-to-a-website.html#add-react-in-one-minute
- 리액트 스크립트를 body태그 안에 붙여넣어서 빠르게 사용 가능

> babel 이란?

- 모든 브라우저가 자바스크립트 언어를 지원하지 않고 ES6이상의 최신 문법이 작동하지 않는 이슈를 해결해주는 자바스크립트 트랜스파일러이다.
- 보통 컴파일은 인간이 작성한 소스코드를 컴퓨터가 이해할 수 있도록 바꿔주는 과정을 의미하는데 여기서는 어떤 실행환경에서도 돌아갈 수 있도록 해주는 것을 의미합니다.

```
    <script
      src="https://unpkg.com/react@17/umd/react.development.js"
      crossorigin
    ></script>
    <script
      src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"
      crossorigin
    ></script>
    <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
    <script type="text/babel">
```

> 중괄호 사용 {}

- 중괄호를 사용하면 자바스크립트 문법을 react 안에서도 사용할 수 있다.
- 삼항연산자, 함수, 여러가지 변수 등을 중괄호 안에 담아서 사용가능
- catItem이라는 자바스크립트 문법의 변수를 favorites의 변수 안에서 사용하기 위해 {catItem}의 형태로 중괄호 안에 넣어서 사용했다.

```
      const catItem = (
        <li>
          <img src="https://cataas.com/cat/60b73094e04e18001194a309/says/react" />
        </li>
      );
      const favorites =
        (
          <ul class="favorites">
            {catItem}
            {catItem}
            {catItem}
          </ul>
        );
```

> 리액트에서는 최상위 태그 하나만 사용가능

- 여러가지 변수를 한번에 담아내고 싶을 때는 div 태그를 이용해서 최상위 태그를 하나로 만들어 준다.

```
      const app = (
        <div>
          {title}
          {form}
          {mainCard}
          {favorites}
        </div>
      );
      const 여기다가그려 = document.querySelector("#app");

      ReactDOM.render(app, 여기다가그려);
```
