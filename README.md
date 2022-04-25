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

## 컴포넌트가 뭔가요?

> 컴포넌트란?

- 프로그래밍에 있어 재사용이 가능한 각각의 독립된 모듈
- 컴포넌트 함수는 대문자로 시작한다.

* app에서 컴포넌트를 사용할 때는 {}중괄호가 아닌 <> 이것을 사용해준다.

```
const app = (
        <div>
          <Title>1번째 고양이 가라사대</Title>
          <Title>2번째 고양이 가라사대</Title>
          {form}
          <MainCard />
          <Favorites />
        </div>
      );
```

- Title을 2번 사용하고 싶을 때 컴포넌트을 만들어서 사용할 수 있다.
- 컴포넌트를 만들 때 값을 전달하고 싶을 때는 props를 사용

> > 화살표 함수를 사용해서 컴포넌트를 생성한 경우.

```
      const Title = (props) => {
        return <h1>{props.children}</h1>;
      };
```

- app에서 Title을 태그로 사용하여 글씨를 작성한 경우
  `<Title>1번째 고양이 가라사대</Title>`
- props는 children으로 값을 받아오기 때문에 {props.children}으로 작성해준다.

> > 일반 함수를 사용하여 컴포넌트를 생성한 경우.

```
      function CatItem(props) {
        return (
          <li>
            <img src={props.img} />
          </li>
        );
      }
```

- Favorites 함수가 CatItem을 컴포넌트로 사용하고 있다.
- CatItem에 이미지 값을 전달하기 위해 props를 사용했다.
- Favorites에서 CatItem을 컴포넌트로 사용할 때 `CatItem img=""` 형태로 작성해서 img값을 props로 넘기며, CatItem에서 값을 꺼내 쓸때는 props.img해서 사용한다.

```
      function Favorites() {
        //대문자로 시작
        return (
          <ul class="favorites">
            <CatItem img="https://cataas.com//cat/5e9970351b7a400011744233/says/inflearn" />
            <CatItem img="https://cataas.com/cat/595f280b557291a9750ebf65/says/JavaScript" />
          </ul>
        );
```

- 컴포넌트 함수 작성시 retrun과 중괄호를 제거하고 작성도 가능하며 바로 리턴해주는 것과 같다.

```
const Form = () => (
        <form>
          <input
            type="text"
            name="name"
            placeholder="영어 대사를 입력해주세요"
          />
          <button type="submit">생성</button>
        </form>
      );
```

> ES6 +디스트럭처링 문법 적용 전과 후

- 문제 상황 : app에서 MainCard 컴포넌트를 사용하고 있고 재사용을 위해 img 주소 값을 props로 컴포넌트에 전달하여 사용하려고 한다.

- 문법 적용 전

```
      const MainCard = (props) => {
        return (
          <div class="main-card">
            <img src={props.img} alt="고양이" width="400" />
            <button>🤍</button>
          </div>
        );
      };
```

- 문법 적용 후
- props를 중괄호를 사용해서 받아오면 img로 바로 사용이 가능하다.

```
      const MainCard = ({ img }) => {
        return (
          <div class="main-card">
            <img src={img} alt="고양이" width="400" />
            <button>🤍</button>
          </div>
        );
      };
```
