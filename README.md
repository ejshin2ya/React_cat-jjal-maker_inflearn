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

## 12강. 스타일링

> Html과 다른점

- class가 아니라 className으로 작성
- html에서 onclick 사용법
  `onclick="sayHi()"`
- react에서 onclick 사용법
  `react : onClick={sayHi}`
- jsx 문법에서는 onClick에서 c를 대문자사용하며, sayHi를 String 형태가 아닌 자바스크립트 그대로 넘겨야 한다.

> inline-sytle 작성법

- {{}} 중괄호를 두번 사용해서 한번 더 object를 만들어준다.
- 원하는 태그에 style을 사용해서 key와 value값을 만드는데, value값은 String 형태로 만들어준다.
  `<img src={props.img} style={{ width: "150px"}}/>`

> 최근 react 개발시 많이 사용하는 style 방법

- https://emotion.sh/docs/introduction 페이지에 나와있는 것처럼 styled 형태를 많이 사용한다고 한다.
- 개발자마다 추구하는 방법이 다른데, class-name을 잘알고 있는 경우 사용하기 좋은 페이지 https://tailwindcss.com/

## 13강. 이벤트 다루기

> 이벤트 핸들러 사용하기

- 이벤트 핸들러 이름은 handle ~ Click, handle ~ MouseOver 형태가 관례이며 카멜 케이스로 작성한다.(띄어쓰기를 대문자로 구분, 낙타 혹처럼 생겨서 카멜케이스라고함)
- return 작성 전에 function으로 이벤트 핸들러를 만들어준다.
- 하트 버튼 클릭시 이벤트 발생 : `onClick={handleHeartClick}`
- 하트 위에 마우스 지나갈때 이벤트 발생 : `onMouseOver={handleHeartMouseOver}`

```
   const MainCard = ({ img }) => {
        function handleHeartClick() {
          console.log("하트 눌렀음");
        }
        function handleHeartMouseOver() {
          console.log("하트 스쳐 지나감");
        }
        return (
          <div className="main-card">
            <img src={img} alt="고양이" width="400" />
            <button
              onClick={handleHeartClick}
              onMouseOver={handleHeartMouseOver}
            >
              🤍
            </button>
          </div>
        );
      };
```

> From 태그에서 이벤트 발생시 처리방법

- form에서는 onSubmit을 사용하여 이벤트 핸들러 사용
  `onSubmit={handleFormSubmit}`
- form에서 onSumit 이벤트 발생시에는 브라우저가 리프레쉬되는 기본동작이 발생한다.
- 이러한 기본동작을 막기 위해서는 자바스크립트 문법인 event.preventDefault() 함수를 작성해줘야한다.
- form 태그의 submit의 첫번째 인자로 event가 들어오고 evnet로 prevent하면 기본동작을 막을 수 있다.

```
 const Form = () => {
        function handleFormSubmit(event) {
          console.log("폼 전송됨");
          event.preventDefault();
        }
        return (
          <form onSubmit={handleFormSubmit}>
            <input
              type="text"
              name="name"
              placeholder="영어 대사를 입력해주세요"
            />
            <button type="submit">생성</button>
          </form>
        );
      };
```

## 14. useState로 상태 만들기

> useState() 사용방법

- useState(초기값) 함수안에 초기값을 넣어준다.
- useState()를 이용하면 상태값을 변수에 바로 담아서 사용할 수 있다.
- counterState라는 변수에 useState를 이용해서 초기값을 1로 설정해주었다.
  ` const counterState = React.useState(1);`
- useState()는 첫번째 인자와 두번째 인자를 가지고 있다. 위에서 만들었던 counterState의 값은 1이면서, 두가지 인자값을 가지게 된다.
- 첫번째 인자인 counter는 counterState 자체의 값을 가지고 있고, 두번째 인자인setCounter는 변경된 상태값을 가지게 된다.

```const counter= counterState[0];
    const setCounter = counterState[1];
```

> 자바스크립트 문법으로 useState 바꾸면

- 위에서는 3줄을 사용했지만, 변수에 바로 counter와 setCounter를 담아서 사용하면 1줄로 사용할 수 있다.

```const[ counter, setCounter] = React.useState(1);

```

- form 태그의 submit이 발생할때마다 변수의 값이 1이 증가하도록 만들어주었다.

```setCounter(counter+1);

```

- 최종 코드

```
 const Form = () => {
        const [counter, setCounter] = React.useState(1);

        console.log("카운터", counter);

        function handleFormSubmit(event) {
          event.preventDefault();
          console.log("폼 전송됨");

          setCounter(counter + 1);
        }

        return (
          <form onSubmit={handleFormSubmit}>
            <input
              type="text"
              name="name"
              placeholder="영어 대사를 입력해주세요"
            />
            <button type="submit">생성</button>
          </form>
        );
      };
```

## 15강. 상태 끌어올리기

> HandleFromSubmit 상태 끌어올리기(lifting state up)란?

- 상태를 부모 컴포넌트에서 선언하도록 바꾸고, 부모에서 만들어진 상태를 자식 컴포넌트에 props로 넘겨준다.

- 자식 컴포넌트인 Form에 있던 상태를 부모 컴포넌트 App에서 선언하도록 변경했다.
- Form에서 handleFormSubmit 함수를 실행하기 위해서 props를 통해서 필요한 값을 받았다.

```
 const Form = ({ handleFormSubmit }) => {
        return (
          <form onSubmit={handleFormSubmit}>
            <input
              type="text"
              name="name"
              placeholder="영어 대사를 입력해주세요"
            />
            <button type="submit">생성</button>
          </form>
        );
      };
```

- 부모 컴포넌트(App)에서 자식 컴포넌트(Form)으로 handleFormSubmit을 props로 넘겨주었다.
- App을 컴포넌트 화살표함수로 함들어준 후, 상태를 선언했다.

```
  const App = () => {
        const [counter, setCounter] = React.useState(1);

        console.log("카운터", counter);

        function handleFormSubmit(event) {
          event.preventDefault();
          console.log("폼 전송됨");

          setCounter(counter + 1);
        }

        return (
          <div>
            <Title>{counter}번째 고양이 가라사대</Title>
            <Form handleFormSubmit={handleFormSubmit} />
            <MainCard img="https://cataas.com/cat/60b73094e04e18001194a309/says/react" />
            <Favorites />
          </div>
        );
      };
```
