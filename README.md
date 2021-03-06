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

## 16강. useState 퀴즈 풀이

> 생성 버튼을 누르면 MainCard 고양이 사진을 CAT2로 변경

1. useState 만들기

- CAT1 사진을 기본값으로 가지고 있는 useState를 만든다.
  `const [mainCat, setMainCat] = React.useState(CAT1);`

2. MainCard 자식 컴포넌트에 props로 useState의 첫번째 인자값 mainCat을 입력해준다.
   ` <MainCard img={mainCat} />`

3. form 전송시 이벤트가 발생하는 handleFormSubmit에 변화된 두번째 인자값 setMainCat(CAT2)를 입력해준다.

```
        function handleFormSubmit(event) {
          event.preventDefault();
          console.log("폼 전송됨");

          setCounter(counter + 1);
          setMainCat(CAT2);
        }
```

## 17강. 리스트

> map 사용법

- map은 리스트에 담긴 값들을 반복문으로 출력할 때 사용한다.
- {배열.map((배열의 개별값을 담을 변수명) => (
  값들을 출력하는 코드
  ))}
- CAT 사진 3개를 가져와서 cats 배열을 만든 후, map을 사용하여 CatItem에 이미지 주소를 props로 넘겨주었다.

```
 function Favorites() {
        const CAT1 =
          "https://cataas.com/cat/60b73094e04e18001194a309/says/react";
        const CAT2 =
          "https://cataas.com//cat/5e9970351b7a400011744233/says/inflearn";
        const CAT3 =
          "https://cataas.com/cat/595f280b557291a9750ebf65/says/JavaScript";

        const cats = [CAT2, CAT3];
        return (
          <ul className="favorites">
            {cats.map((cat) => (
              <CatItem img={cat} key={cat} />
            ))}
          </ul>
        );
      }
```

## 18강. 배웠던 개념 조합해서 기능 추가(상태, props, 이벤트, 리스트)

> 하트 버튼 누르면 고양이 사진이 추가되도록 구현해보기

1. MainCard 컴포넌트 안에 들어있던 handleHeartClick() 함수를 부모 컴포넌트 App으로 끌어올리기

2. handleHeartClick() 함수를 자식 컴포넌트 MainCard에 props로 전달한다.

3. Favorites 컴포넌트를 동적으로 만들기 위해 useState() 변수에 담아낸다.

4. useState()초기값에 CAT1, CAT2 배열을 넣고, 하트를 누르면 CAT3가 추가되도록 하기 위해서 setFavorites([...favorites, CAT3]) 형태로 작성해준다.
   ...은 기존의 배열을 펼쳐주는 자바스크립트 문법을 사용한다.

```
 function Favorites({ favorites }) {
        return (
          <ul className="favorites">
            {favorites.map((cat) => (
              <CatItem img={cat} key={cat} />
            ))}
          </ul>
        );
      }

      const MainCard = ({ img, handleHeartClick }) => {
        return (
          <div className="main-card">
            <img src={img} alt="고양이" width="400" />
            <button onClick={handleHeartClick}>🤍</button>
          </div>
        );
      };

      const App = () => {
        const CAT1 =
          "https://cataas.com/cat/60b73094e04e18001194a309/says/react";
        const CAT2 =
          "https://cataas.com//cat/5e9970351b7a400011744233/says/inflearn";
        const CAT3 =
          "https://cataas.com/cat/595f280b557291a9750ebf65/says/JavaScript";

        const [counter, setCounter] = React.useState(1);
        const [mainCat, setMainCat] = React.useState(CAT1);
        const [favorites, setFavorites] = React.useState([CAT1, CAT2]);

        console.log("카운터", counter);

        function handleFormSubmit(event) {
          event.preventDefault();
          console.log("폼 전송됨");

          setCounter(counter + 1);
          setMainCat(CAT2);
        }

        function handleHeartClick() {
          console.log("하트 눌렀음");
          setFavorites([...favorites, CAT3]);
        }

        return (
          <div>
            <Title>{counter}번째 고양이 가라사대</Title>
            <Form handleFormSubmit={handleFormSubmit} />
            <MainCard img={mainCat} handleHeartClick={handleHeartClick} />
            <Favorites favorites={favorites} />
          </div>
        );
      };
```

## 19강. 폼 다루기

> 사용자가 form input 창에 소문자 입력시 자동으로 대문자로 입력되도록 제어

1. form 컴포넌트를 찾아서 동적인 상태로 만들어주는 useState() 변수를 만든다.

2. useState()의 초기값은 빈 스트링으로 설정하고, 첫번째 인자값은 value, 두번째 인자값은 setValue라는 이름으로 만들어준다.

3. form 태그 안에 onChange라는 내장함수를 이용해서 input창에 값이 입력되는 것을 인지하는 handleInputChange 이벤트 함수를 만들어준다.

4. handleInputChange 이벤트를 console.log로 찍어보면 input 창에 입력한 값이 target.value안에 들어있는것을 확인할 수 있다.

5. handleInputChange 이벤트 함수가 발생될때마다(사용자가 input창에 입력을 할때마다) 입력값을 대문자로 바꿔주는 함수 toUpperCase()와 setValue를 사용하여 소문자를 대문자로 동적으로 바꿔준다.

6. 최종적으로 handleInputChange(e) 이벤트 함수에 setValue(e.target.value.toUpperCase());를 추가하여 동적으로 바꿔준다. 하지만 실제 input창에는 값이 변화하지 않고 내부적으로 변화한다.

7. 이를 해결해주기 위해 form 태그 내장함수인 value에 우리가 만든 useState의 첫번째인자값인 value를 입력해준다. valus={value}

8. 최종 코드

```
 const Form = ({ handleFormSubmit }) => {
        const [value, setValue] = React.useState("");
        function handleInputChange(e) {
          console.log(e.target.value.toUpperCase());
          setValue(e.target.value.toUpperCase());
        }
        return (
          <form onSubmit={handleFormSubmit}>
            <input
              type="text"
              name="name"
              placeholder="영어 대사를 입력해주세요"
              value={value}
              onChange={handleInputChange}
            />
            <button type="submit">생성</button>
          </form>
        );
      };
```

## 20강. 폼 검증하기 (Form validation)

> 영어대사가 아닌 한글입력시 한글은 입력할 수 없습니다라는 텍스트 보여주고, 빈값을 입력 후 생성버튼 입력시 빈값으로는 생성할 수 없습니다라는 에러메세지 띄워보기

1. 값이 한글인지 아닌지 검증하는 함수 만들기

`const includesHangul = (text) => /[ㄱ-ㅎ|ㅏ-ㅣ|가-힣]/i.test(text);`

2. handleInputChange 함수가 실행될 때(input창에 사용자가 값을 입력할 때) 입력된 값(e.target.value)가 한글인지 아닌지를 확인하기 위해 includesHangul(e.target.value) 콘솔창에 찍어보면 한글이 입력되면 true, 영어가 입력되면 false가 나오는 것을 알 수 있다.

3. 한글이 입력되면 true값이 나오는걸 이용해서 조건문과 setState()함수를 사용해서 동적으로 만들어준다. 초기값은 빈 스트링이고 첫번째 인자값은 errorMessage, 두번째 인자값은 setErrorMessage를 갖는 useState를 만들어준다.
   `const [errorMessage, setErrorMessage] = React.useState("");`

- 한글이 입력되면 한글은 입력할 수 없습니다라는 상태값을 setErrorMessage를 이용해서 동적으로 만들어준다.

```
 function handleInputChange(e) {
          const userValue = e.target.value;

          setErrorMessage("");

          if (includesHangul(userValue)) {
            setErrorMessage("한글은 입력할 수 없습니다.");
          }
          setValue(userValue.toUpperCase());
        }
```

4. 위에서 만든 동적인 errorMessage 값을 화면에 보여주기 위해 form 태그 안에 p태그를 만들어서 에러 메세지를 보여준다.
   `<p style={{ color: "red" }}>{errorMessage}</p>`

5. 빈값이 입력되어 생성버튼을 눌렀을때 "빈값으로 만들 수 없습니다"라는 메세지를 보여주기 위해 기존에 만들었던 handleFormSubmit(e) 함수를 사용한다.
   App 부모 컴포넌트에서 handleFormSubmit을 받아오던 prop은 지워주고, form 컴포넌트 안에 새로 handleFormSubmit 함수를 만들어준다.

6. 조건문과 useSatate()함수를 이용하여 value값이 빈 문자열일때 setErrorMessage("빈 값으로 만들 수 없습니다.")라는 동적인 문구를 보여줍니다.

7. 빈문자열이 아닐때 else를 사용하여 setErrorMessage를 빈문자열로 만들어줄 수도 있지만 애초에 setErrorMessage("")로 작성하면 else를 적을 필요가 없다.

```
        function handleFormSubmit(e) {
          e.preventDefault();
          setErrorMessage("");
          if (value === "") {
            setErrorMessage("빈 값으로 만들 수 없습니다.");
          }
        }
```

8. 최종 코드

```
      const Form = () => {
        const [value, setValue] = React.useState("");
        const includesHangul = (text) => /[ㄱ-ㅎ|ㅏ-ㅣ|가-힣]/i.test(text);
        const [errorMessage, setErrorMessage] = React.useState("");

        function handleInputChange(e) {
          const userValue = e.target.value;

          setErrorMessage("");

          if (includesHangul(userValue)) {
            setErrorMessage("한글은 입력할 수 없습니다.");
          }
          setValue(userValue.toUpperCase());
        }

        function handleFormSubmit(e) {
          e.preventDefault();
          setErrorMessage("");
          if (value === "") {
            setErrorMessage("빈 값으로 만들 수 없습니다.");
          }
        }

        return (
          <form onSubmit={handleFormSubmit}>
            <input
              type="text"
              name="name"
              placeholder="영어 대사를 입력해주세요"
              value={value}
              onChange={handleInputChange}
            />
            <button type="submit">생성</button>
            <p style={{ color: "red" }}>{errorMessage}</p>
          </form>
        );
      };
```

## 21. 코드 정리하기

1. console.log() 지워주기(test용)
2. 이벤트 핸들러 컨벤션(규칙)에 맞게 prop 이름 지어주기

- handle이 들어간 함수를 prop으로 보낼때는 on이라는 접두어를 붙여서 이름을 지어준다.

- handleHeartClick() 함수를 MainCard자식 컴포넌트에 prop으로 보내줄때,
  handleHeartClick={handleHeartClick}이라고 적은 부분을
  onHeartClick={handleHeartClick}으로 바꿔주었다.
  ```
  <MainCard img={mainCat} onHeartClick={handleHeartClick} />
  ```

3. handleFormSubmit() 함수를 App컴포넌트와 form 컴포넌트에서 중복해서 사용하고 있는 것을 합쳐준다.
   form이 submit될 때 app컴포넌트에서는 고양이사진과 숫자를 바꿔주는 기능을 하고, form컴포넌트에서는 빈값이 입력되어 submit될때 에러메세지를 띄워주는 기능을 하고 있다. app컴포넌트에서의 handleFormSubmit()함수를 기능구현에 맞는 이름 updateMainCat()으로 바꿔주고, 이 함수를 prop으로 form컴포넌트로 넘겨준다. form 컴포넌트의 handleFormSubmit() 함수 내부에 updateMainCat()을 적어준다.

- form 컴포넌트의 handleFormSubmit()함수

```
        function handleFormSubmit(e) {
          e.preventDefault();
          setErrorMessage("");
          if (value === "") {
            setErrorMessage("빈 값으로 만들 수 없습니다.");
            return;
          }
          updateMainCat();
        }
```

- app 컴포넌트의 updateMainCat()함수와 prop으로 넘겨주는 코드

```
        function updateMainCat() {
          setMainCat(CAT2);
          setCounter(counter + 1);
        }

        return (
          <div>
            <Title>{counter}번째 고양이 가라사대</Title>
            <Form updateMainCat={updateMainCat} />
            <MainCard img={mainCat} onHeartClick={handleHeartClick} />
            <Favorites favorites={favorites} />
          </div>
        );
```

4. 함수실행시 동작 우선순위에 따라 위치 바꿔준다.

- 고양이 사진 보여주는 것이 숫자 바꾸는 것보다 기능 구현에 있어 우선순위가 높다.

```
        function updateMainCat() {
          setMainCat(CAT2);
          setCounter(counter + 1);
        }
```

5. return으로 함수가 추가 실행되지 않도록 막아주기

- 빈값이 입력되었을 때, updateMainCat()이 실행되지 않도록 return을 적어준다.

```
        function handleFormSubmit(e) {
          e.preventDefault();
          setErrorMessage("");
          if (value === "") {
            setErrorMessage("빈 값으로 만들 수 없습니다.");
            return;
          }
          updateMainCat();
        }
```

## 22. 로컬스토리지에 데이터 싱크하기

> 영어대사를 입력 후 생성 버튼 클릭시 증가한 숫자를 저장하는 방법으로 localStorage를 사용

1. 로컬스토리지에 데이터 저장하기

- setItem 사용
- counter라는 키값으로 nextCounter자리에 있는 값이 들어간다.

```
localStroage.setItem("counter", nextCounter);
```

2. 로컬스토리지의 데이터 가져오기

- getItem 사용
- 로컬스토리지에 있는 데이터는 String 타입으로 꺼내지기 때문에 int 타입이 필요할때는 Number를 이용하여 숫자로 변환

```
 Number(localStorage.getItem("counter"))
```

## 23. 로컬스토리지에 데이터 싱크하기2

> JSON.stringify()

- 웹 서버로 데이터를 보낼 때 데이터는 문자열이여야 하며, JSON.stringify()를 사용해서 javascript 객체를 문자열로 변환할 수 있다.

> JSON.parse()

- 웹 서버에 보내진 문자열 데이터를 가져올때, JSON.parse()를 사용해서 문자열을 javascript 객체로 변환할 수 있다.

> localStorage에 데이터를 저장하고 꺼내오는 함수

```
const jsonLocalStorage = {
        setItem: (key, value) => {
          localStorage.setItem(key, JSON.stringify(value));
        },
        getItem: (key) => {
          return JSON.parse(localStorage.getItem(key));
        },
      };
```

> 좋아요 버튼을 누르면, 해당 사진이 아래 화면에 추가되어 생성되게 하려면?

1. 기존 컴포넌트의 역할을 살펴보면, MainCard 컴포넌트에 있는 좋아요를 눌렀을 때, favorites 컴포넌트에서 map 반복문을 돌면서 CatItem 컴포넌트를 이용해서 고양이 사진들을 화면에 그려준다.

2. App 컴포넌트에 handleHeartClick() 이라는 함수가 있고, 이 함수를 MainCard 컴포넌트에 props로 전달해주고 있다.

3. handleHeartClick()이라는 함수 안에 "favorites"키 값으로 현재 찜한 사진 상태값 favorites 배열과, 현재 메인 사진 상태값 mainCat을 배열로 담아서 JSON.stringify(localStorage.setItem("favorites", [...favorites, mainCat]))하여 데이터를 저장한다.

```
 function handleHeartClick() {
          const nextFavorites = [...favorites, mainCat];
          setFavorites(nextFavorites);
          jsonLocalStorage.setItem("favorites", nextFavorites);
        }
```

4. JSON.parse(localStrage.getItem("favorites"))해서 JSON 문자열로 저장된 찜한 사진을 자바스크립트 객체로 꺼내온다. 처음에 찜한사진이 아무것도 없을 때는 빈배열을 꺼내올 수 있도록 or연산을 사용하여 빈배열이 꺼내지도록 한다.

```const [favorites, setFavorites] = React.useState(
          jsonLocalStorage.getItem("favorites") || []
        );
```

## 25. 지금까지 배운 개념 정리1(JSX, 바벨, 컴포넌트, 스타일링, 이벤트)

> JSX란?

- JavaScript + XML
- javaScript에 HTML 태그를 끼얹은 문법이다.
- HTML 태그 안에선 중괄호({})를 사용해서 JS를 쓸 수 있다.

```
const count=1;
const title = <h1>{count}번째 고양이</h1>
```

- 위 title 변수에 담은 h1 태그는 리액트 엘리먼트라고 부른다.

> Babel 이란?

- 최신 문법을 브라우저가 이해할 수 있는 JavaScript로 통역
- 브라우저는 JSX를 이해하지 못한다.
- Babel이라는 통역사로 JSX => JavaScript

* jsx : `const title=<h1>안녕</h1>`
* 브라우저 : 뭐라고?
* Bavel : `const title=React.createElement('h1', null, '안녕')` 이래요.
* 브라우저 : 아하!

> 리액트 코드 브라우저에 그리기

- 빈 HTML 공간에 React 때려박기
- HTML
  `<div id="app"></div>`

- React

```const target = document.querySelector("#app")
  const myButton=<button>버튼</button>

  ReactDOM.render(myButton, target)
```

> 컴포넌트

- 여기저기 재사용 가능한 UI코드 조각
- props는 properties의 약자로 속성들을 의미한다.

```
<Card emoji={dog} title="멍멍" />
<Card emoji={cat} title="야옹" />

function Card(props){
  return(
    <div>
      {props.emoji}
      <h2>{props.title}</h2>
    </div>
  )
}
```

> 스타일링

- 리액트에 CSS 끼얹기
- CSS 클래스 : className
- 인라인 스타일링 : style={{스타일속성 : 스타일값}}

* 인라인 스타일링할때 두번쨰 속성값 스타일값은 "스트링"의 형태로 작성

```
<div className = "danger">위험</div>
<div style={{color:"red"}}>위험</div>
```

> 이벤트

- 사용자 이벤트(클릭, 스크롤 등) 다루기
- 일반 자바스크립트 이벤트 목록과 동일하지만 중간을 대문자로 쓰면 된다.
- onclick => onClick
- onsubmit => onSubmit

```
function handleClick(event){
  console.log("클릭했습니다")
}

<button onClick={handleClick}>제출</button>
```

## 26. 지금까지 배운 개념 정리 2(상태, 리스트, 폼, 로컬스토리지)

> 상태

- 컴포넌트 안에서 자유롭게 변경할 값이 필요할 때

- useState함수로 상태를 추가할 수 있다.
- const[상태명, 상태변경함수명] = React.useState(초기값)
- 컴포넌트 안에서 만들 수 있다.

```
const[counter, setCounter] = React.useState(1)

function 카운터증가(){
  setCounter(counter+1); //(참고)setCounter(prev=> prev+1)로도 가능!
}
return <button onClick={카운터증가}>카운터는 {counter}</button>
```

> 리스트

- 배열로 반복되는 UI 그리기
- 웹 사이트를 만들 때 정말 많이 쓴다.
- 배열에서 map을 돌면서 리액트 UI를 반환한다.

```
const favorites =["이미지1", "이미지2", "이미지3"]
<ul>
  {favorites.map(image => <img src={image}></img>)}
</ul>
```

> 폼

- 사용자 입력 다루기
- 사용자 입력값을 직접 다루기 위해 value를 상태로 관리한다.

```
const[value, setValue] = React.useState("초기값이에요")

function onValueChange(e){
  setValue(e.target.value);
}

<form onSubmit={handleSubmit}>
  <input value={value} onChange={onValueChange}/>
  <button type="submit">제출</button>
</form>
```

> 로컬스토리지

- 리액트 문법x, 브라우저 기능 o
- 브라우저에 데이터 저장하기
- 간단한 데이터 저장이 필요할 땐 localStorage를 쓰세요.
- 일반 브라우저와 다르게 webkit관련 브라우저는 7일까지 저장가능(애플 사파리)

```
localStorage.setItem("이름", "유림");
localStorage.getItem("이름") //유림
```

## 27. 실제 고양이 데이터 받아오기 - fetch, Open API

> 서버 개발자가 있다면 API를 만들어서 이 주소로 호출을 하면 이미지 url을 보내주겠다고 하겠지만 현재 서버 개발자가 없기 때문에 오픈 API를 활용

- https://github.com/public-apis/public-apis => 다양한 오픈API있음
- Animal -> cataas 를 고양이 짤방 만드는 API로 사용

* 고양이 API는 서버로 요청하는 API를 의미한다.
* fetch API는 자바스크립트로 호출할 수 있는 API를 의미한다.

> fetch 사용하기

- https://developer.mozilla.org/ko/docs/Web/API/Fetch_API/Using_Fetch
- 위 사이트에서 fetch사용하기 코드를 가져와서 url을 바꿔주면 고양이 이미지 주소를 Json 형태로 가져올 수 있다.

```
fetch('https://cataas.com/cat?json=true')
  .then((response) => response.json())
  .then((data) => console.log(data));
```

- 위 코드를 콘솔창에 입력하면 아래와 같이 url결과 주소를 얻을 수 있다.

```
{id: '60da12c802e5cf001caa36cc', created_at: '2021-06-28T18:19:51.958Z', tags: Array(1), url: '/cat/60da12c802e5cf001caa36cc'}
```

> fetch를 깊게 공부하려면 primise와 비동기 처리에 대해 알면 좋다.

- promise 이해하기 : https://joshua1988.github.io/web-development/javascript/promise-for-beginners/

- 비동기 이해하기 : https://joshua1988.github.io/web-development/javascript/javascript-asynchronous-operation/

## 28. 고양이 데이터 내 앱에 연동하기

> async await 문법

- await 상위에는 async를 꼭 사용해야한다.
- async, await 문법 글 : https://joshua1988.github.io/web-development/javascript/js-async-await/
- async, await 무료 강의 : https://www.inflearn.com/course/vue-js/lecture/17061?tab=curriculum&volume=1.00

* 어싱크 어웨이트 자바스크립트 비동기 처리 패턴의 최신 문법이다.
* primise와 Callback에서 주는 단점들을 해결하고 자바스크립트의 비동기적 사고 방식에서 벗어나 동기적으로 코드를 작성할 수 있게 도와준다.
* 기본 문법

```
async function fetchData(){
  await getUserList();
}
```

> mainCat의 사진이 api에 연동되어 고양이 랜덤 사진 안에 내가 입려간 단어가 그려지게 하기

- async, await, fetch를 사용해서 api에 있는 url주소를 가져와서 내가 원하는 text값과 조합하여 최종으로 원하는 url로 만들어준다.

```
const fetchCat = async (text) => {
  const OPEN_API_DOMAIN = "https://cataas.com";
  const response = await fetch(`${OPEN_API_DOMAIN}/cat/says/${text}?json=true`);
  const responseJson = await response.json();
  return `${OPEN_API_DOMAIN}/${responseJson.url}`;
};
```

- updateMainCat 함수에서 고양이 메인 사진을 관리해줌. 여기에 새로운 newCat이라는 변수를 만들어서 위에서 만든 fetch함수에 내가 원하는 text를 연결해준다.
  ` const newCat = await fetchCat(value);`

- From 컴포넌트에서 updateMainCat함수와 input value값을 둘다 사용하고 있기 때문에, updateMainCat(value) 함수에 사용자가 입력한 input value를 파라미터로 넘겨준다.

- value값을 받은 updateMainCat(value)함수에서 value가 fetchcat함수에 전달되어 원하는 url주소값을 얻을 수 있다. setMainCat(newCat)으로 상태값이 변경된 고양이 이미지가 MainCard컴포넌트에 전달되어 보여진다.

```
  async function updateMainCat(value) {
          const newCat = await fetchCat(value);

          setMainCat(newCat);
          const nextCounter = counter + 1;
          setCounter(nextCounter);
          jsonLocalStorage.setItem("counter", nextCounter);
        }
```

## 29. 컴포넌트 생성시 고양이 데이터 받아오기 useEffect

> 메인화면에 있는 첫 고양이 사진이 지정 변수로 설정되어있는데 앱 진입시 바로 api콜을 해서 고양이 메인 사진을 동적으로 바꿔주는 작업해보기

- 첫 고양이 사진을 만들어주는 setInitialCat() 함수를 생성한다.
- await와 fetch를 사용하기 때문에 async 함수로 감싸줘야 한다.

```
          async function setInitialCat() {
          const newCat = await fetchCat("First Cat");
          setMainCat(newCat);
        }
```

- app 컴포넌트에서 setInitiaCat() 함수를 실행시키면 고양이 사진이 한개만 나오는게 아니고 계속해서 이미지 주소가 생성된다.

- 위의 상황을 방지하기 위해 useEffect()를 사용해 준다.

```
        React.useEffect(() => {
          setInitialCat();
        }, []);
```

- 고양이 사진 CAT1이 잠깐 떳다가 새로운 사진으로 한번 생성되는 것을 확인할 수 있다.

## 30. useEffect의 정체

- React 컴포넌트 안에 있는 코드는 기본적으로 UI가 새로 업데이트 될때마다 계속 불린다.
- 계속 불리는 것을 방지하고 어떤 상태가 업데이트 될때만 불리도록 제한하기 위해서는 useEffect의 두번쨰 인자로 배열을 넘기고, 배열안에 원하는 상태를 넘겨주면 된다.

* 아래 코드는 counter라는 숫자가 변경될 때마다 setInitialCat()함수가 불린다.

```
        React.useEffect(() => {
          setInitialCat();
        }, [counter]);
```

- 상태 변화에 상관없이 맨처음 앱이 생성되었을 때만 호출하고 싶을 때는 빈배열을 넣어주면 된다.

```
        React.useEffect(() => {
          setInitialCat();
        }, []);
```

## 31. 조건부 렌더링(Conditional Rendering)

> 찜한 사진이 없을때는 "사진 위 하트를 눌러 고양이 사진을 저장해봐요!"라는 문구가 보이도록 해보기

- Favorites 컴포넌트에서 porps로 전달되는 favorites의 길이가 0일때, 조건에 맞는 문구를 보여주도록 한다.

```
 function Favorites({ favorites }) {
        if (favorites.length == 0) {
          return <div>사진 위 하트를 눌러 고양이 사진을 저장해봐요!</div>;
        }
        return (
          <ul className="favorites">
            {favorites.map((cat) => (
              <CatItem img={cat} key={cat} />
            ))}
          </ul>
        );
      }
```

> favorites배열(찜버튼 누른 고양이 사진들의 배열) 안에 있는 고양이 사진이 MainCat에 보여질때 하트 버튼이 빨갛게 뜨도록 만들어 주기

- 배열에 includes 사용하기
- 배열안에 값이 있으면 true, 아니면 false를 반환해준다.
  `[1,2,3].includes(1)`

* App컴포넌트 안에 이미 좋아요 눌렀다는 새로운 변수 alreadyFavorite를 includes를 사용하여 만들어준다.
* mainCat이미지가 favorites 배열안에 포함되어 있다면 true, 아니면 false 반환

```
const alreadyFavorite = favorites.includes(mainCat);
```

- 삼항 연산자 사용하기
- MainCard 컴포넌트로 아까 만든 alreadyFavorite변수를 props로 넘겨준다.
- heartIcon이라는 새로운 변수를 삼항 연산자로 만들어준다.
- alreadyFavorite가 true값이면 빨간 하트를, false라면 하얀 하트를 보여준다.

```
 const MainCard = ({ img, onHeartClick, alreadyFavorite }) => {
        const heartIcon = alreadyFavorite ? "💖" : "🤍";
        return (
          <div className="main-card">
            <img src={img} alt="고양이" width="400" />
            <button onClick={onHeartClick}>{heartIcon}</button>
          </div>
        );
      };
```

## 31. 퀴즈 풀이

> counter가 null이면 "n번째"를 삭제하고 "고양이 가라사대"만 보여주기

- 내가 만든 코드는 title을 두번쓰고 있어서 별로 좋지 않은 것 같다.

```
const counterTitle =
          counter === null ? (
            <Title>고양이 가라사대</Title>
          ) : (
            <Title>{counter}번째 고양이 가라사대</Title>
          );

        return (
          <div>
            {counterTitle}
            <Form updateMainCat={updateMainCat} />
            <MainCard
              img={mainCat}
              onHeartClick={handleHeartClick}
              alreadyFavorite={alreadyFavorite}
            />
            <Favorites favorites={favorites} />
          </div>
        );
```

- 유림님이 만든 코드는 n번째만 바꿔주어서 가독성이 좋다.

```
        const counterTitle = counter === null ? "" : counter + "번째 ";

        return (
          <div>
            <Title>{counterTitle}고양이 가라사대</Title>
            <Form updateMainCat={updateMainCat} />
            <MainCard
              img={mainCat}
              onHeartClick={handleHeartClick}
              alreadyFavorite={alreadyFavorite}
            />
            <Favorites favorites={favorites} />
          </div>
        );
```

## 33. setState 더 알아보기 - 함수, 지연초기화

1. useState()에 함수 생성하여 초기값 한번만 나오도록 해줌

> app 컴포넌트 안에 있는 함수들은 UI가 초기화될 때마다 새로 실행되기 때문에, jsonLocalStorage에 접근하는 부분이 계속 실행되면서 무거워진다.

> 이를 해결하기 위해 jsonLocalStorage가 처음 접속했을 때 한번만 실행되기 위해 useState의 초기값을 값이 아닌 함수로 전달해준다.

- 기존에 값으로 전달해서 문제있는 코드

```
    const [counter, setCounter] = React.useState(
          jsonLocalStorage.getItem("counter")
        );
```

- 화살표 함수로 전달해서 문제 해결한 코드

```
        const [counter, setCounter] = React.useState(() => {
          return jsonLocalStorage.getItem("counter");
        });
```

2. setState()에 값이 아닌 함수를 만들어서 미스매치 현상을 제거

> 생성 버튼을 여러번 눌러도 counter 값이 빠르게 올라가지 않는 현상은 useState의 액션을 처리할때, coutner와 setCounter가 바라보는 위치가 달라서 생기는 미스매치 현상이다.

> 이를 해결하기 위해서 useState의 setCounter를 함수로 넘겨준다.

- 문제가 있었던 이전 코드

```
          const newCat = await fetchCat(value);

          setMainCat(newCat);
          const nextCounter = counter + 1;
          setCounter(nextCounter);
          jsonLocalStorage.setItem("counter", nextCounter);
        }
```

- 화살표 함수로 전달해서 문제를 해결해준 코드
- prev를 통해서 이전 값을 받아와서 setCounter를 함수로 처리해준다.

```
        async function updateMainCat(value) {
          const newCat = await fetchCat(value);

          setMainCat(newCat);
          setCounter((prev) => {
            const nextCounter = prev + 1;
            jsonLocalStorage.setItem("counter", nextCounter);
            return nextCounter;
          });
        }
```

## 34. create-react-app 실무 개발환경 만들기

> 실제 유저들에게 공개하기 전에 무엇을 더 해야할까요?

1. 프로덕션 버전 리액트 라이브러리 사용 = 개발용 경고 등이 불포함되어 용량 작다.
2. 바벨 떼기 = 브라우저에서 매번 바벨로 JS로 통역하는게 아니고 이미 통역된 JS를 올린다.

> 위 문제 해결을 위해 create-reat-app사용

- 리액트 초기 개발에 필요한 모든 것을 자동으로 해줘요

1. 간단한 앱 껍데기
2. 리액트 라이브러리 셋업(개발용/ 프로덕션용)
3. 웹팩(WepPack) 셋업
   - 라이브 서버
   - 저장할때마다 JSX -> JS
   - 웹팩 소개 문서 : https://joshua1988.github.io/webpack-guide/webpack/what-is-webpack.html
   - 웹팩 강의 : https://www.inflearn.com/course/%ED%94%84%EB%9F%B0%ED%8A%B8%EC%97%94%EB%93%9C-%EC%9B%B9%ED%8C%A9?inst=747606f7&utm_source=blog&utm_medium=githubio&utm_campaign=captianpangyo&utm_term=banner
4. 테스트 셋업
5. 빌드 셋업
   - JS로 변환, 코드 용량 최소화, 프로덕션 라이브러리 설정 등

- 사용방법 공식 문서 : https://ko.reactjs.org/docs/create-a-new-react-app.html
- node.js 설치 되어있어야 한다. (확인방법 : 터미널에 node -v )

```
npx create-react-app my-app
cd my-app
npm start
```

- my-app 부분은 직접 원하는 파일명으로 적어준다.

```
npx create-react-app cat-jjal-maker-cra
cd cat-jjal-maker-cra
npm start
```

## 35. create-react-app 폴더 구조 뜯어보기 2

> cat-jjal-maker-cra -> src -> README.md

- cra로 만들어진 프로젝트에 대한 설명이 들어있음.
- build, start 등등

> cat-jjal-maker-cra -> src -> package.json

- cra가 어떤 라이브러리를 사용하고 있는지, 어떤 명령어를 통해 무엇을 할 수 있는지에 대해 나와있는 파일.

> ..App.js

- npm start 했을때 처음 화면 띄워지는 곳
- import, export로 외부로 파일 들여오고 외부로 파일 내보낸다.
  > ..index.js
- documnet.getElementById('root')라는 곳에 나의 app 컴포넌트를 그려준다는 내용이 담겨있다.
- root는 public의 index.html에 들어있다.

> npm 소개
> https://joshua1988.github.io/webpack-guide/build/node-npm.html

> npm과 node.js 소개 무료 강의
> https://www.inflearn.com/course/%ED%94%84%EB%9F%B0%ED%8A%B8%EC%97%94%EB%93%9C-%EC%9B%B9%ED%8C%A9/lecture/37370?inst=747606f7&tab=curriculum&volume=1.00

> ES+ import 문법
> https://joshua1988.github.io/vue-camp/es6+/modules.html#%E1%84%86%E1%85%A9%E1%84%83%E1%85%B2%E1%86%AF%E1%84%92%E1%85%AA%E1%84%8B%E1%85%B4-%E1%84%91%E1%85%B5%E1%86%AF%E1%84%8B%E1%85%AD%E1%84%89%E1%85%A5%E1%86%BC

## 36. 지금까지 만든 앱 create-react-app으로 옮기기

> 기존에 만든 프로젝트를 babel script 다음부터 render 전까지의 코드를 cat-jjal-maker-cra -> src -> App.js 폴더의 App 코드 부분을 지우고 복사한 코드를 붙여넣는다.

> 원래는 컴포넌트마다 파일을 각각 생성해주는 것이 관례이다.
> 우리는 모든 컴포넌트를 App.js에 때려박았지만, Title 컴포넌트를 분리해보는 연습 해보자

- title 컴포넌트 코드를 잘라내서 src 아래에 components 폴더를 만들고 Title.js 파일을 생성해서 여기에 붙여넣는다.
- App.js에서 쓸수있도록`export default Title;`해준다.
- App.js에서는 `import Title from "./components/Title";`해준다.

## 37. 빌드한 결과물 github pages로 배포하기

> cra에 있는 것은 브라우저로 바로 읽을 수 없어서 build과정이 필요

```cd cat-jjal-maker-cra
  npm run build
```

- 위명령어 실행 후 build 폴더 생성
- jsx가 아닌 브라우저가 이해할 수 있는 자바스크립트 파일이 생성
- 깃헙 페이지스에 jsx가 아닌 빌드 폴더를 올려야 한다.
- 깃헙 페이지스 라이브러리를 다운받아야 한다.
  ` npm install gh-pages`
- 깃헙 페이지스를 통해 빌드 폴더를 깃허브에 올리기 위한 명령어 추가.
- package.json -> script에 `"deploy": "gh-pages -d build"` 명령어를 삽입
- package.json -> 상단에 `"homepage": "https://ejshin2ya.github.io/React_cat-jjal-maker_inflearn"` 깃허브 페이지 주소를 작성(마지막에 /는 삭제)

* 다시 한번 빌드 `npm run build`
* `npm run deploy`

* 깃헙 페이지가 기존에 main을 바라보고 있는것을 깃헙 페이지스를 바라보도록 변경
* github -> settings -> pages -> branch를 gh-pages로 변경 후 save
