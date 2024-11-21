# Dom 생성 - createElement,  잘 사용하지 않는 방법

해당 방법은 잘 사용하지 않음, 대부분  JSX를 이용하여 DOM을 생성함

```bash
<head>
  <meta charset="UTF-8">
</head>
<html>
  <body>
      <div id="root"></div>
  </body>
  <!--React Js는 어플리케이션이 interactive하도록 만들어주는 library,엔진 같은 역할    -->
  <script src="https://unpkg.com/react@17.0.2/umd/react.production.min.js"></script>
  <!--react-dom은 library 또는 package 모든 element를 HTML body에 둘 수 있도록 해줌, React element를 html에 두는것 -->
  <script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js"></script>
  <script>
      const root = document.getElementById("root");
      const h3 = React.createElement("h3", {onMouseEnter: () => console.log('mouse enter')}, "Hello I'm a h3");
      const btn = React.createElement("button", {
          onClick: () => console.log("I'm clicked"),
          style: {backgroundColor: "tomato"}
      }, "Click me");
      const container = React.createElement("div", null, [h3, btn])
      ReactDOM.render(container, root);
  </script>
</html>
```

```bash
const h3 = React.createElement("h3", {onMouseEnter: () => console.log('mouse enter')}, "Hello I'm a h3");
const btn = React.createElement("button", {onClick: () => console.log("I'm clicked")}, "Click me");
const container = React.createElement("div", null, [h3, btn])
```

`React.createElement` 함수는 React에서 DOM 요소나 React 컴포넌트를 생성할 때 사용하는 함수입니다. 함수에 전달되는 **파라미터의 위치와 의미**는 다음과 같습니다:

### **구문**

```jsx
React.createElement(type, props, ...children);

```

### **파라미터 설명**

1. **`type` (첫 번째 파라미터)**
    - 생성하려는 요소의 타입을 지정합니다.
    - **DOM 요소 이름** 또는 **React 컴포넌트**일 수 있습니다.
    - 예:
        - `"h3"`: HTML `<h3>` 태그를 생성.
        - `MyComponent`: 사용자 정의 React 컴포넌트.
2. **`props` (두 번째 파라미터)**
    - 생성한 요소에 전달할 **속성(properties)**을 정의하는 객체입니다.
    - 이 객체에 DOM 속성, 스타일, 이벤트 핸들러 등을 지정할 수 있습니다.
    - 예:
        
        ```jsx
        {
          id: "example",             // 일반 DOM 속성
          style: { color: "red" },   // 인라인 스타일
          onClick: handleClick       // 이벤트 핸들러
        }
        
        ```
        
    - **특별한 속성**:
        - `key`: React에서 리스트 렌더링 시 각 요소를 고유하게 식별하기 위한 키.
        - `ref`: DOM 요소나 컴포넌트에 대한 참조.
3. **`...children` (세 번째 이후 파라미터)**
    - **자식 요소 또는 내용**을 지정합니다.
    - 여러 개의 자식을 전달하려면 배열 또는 쉼표로 구분하여 전달할 수 있습니다.
    - 문자열, 숫자, React 요소 등 다양한 타입이 가능.
    - 예:
        
        ```jsx
        "Hello, World!"                  // 텍스트 자식
        React.createElement("span")      // React 요소 자식
        [React.createElement("li"), ...] // 자식 배열
        
        ```
        

### **주어진 코드 설명**

```jsx
const h3 = React.createElement(
    "h3",
    { onMouseEnter: () => console.log('mouse enter') },
    "Hello I'm a h3"
);

```

1. **`"h3"`**
    - 첫 번째 파라미터: `<h3>` DOM 요소를 생성.
2. **`{ onMouseEnter: () => console.log('mouse enter') }`**
    - 두 번째 파라미터: 요소에 추가할 속성을 객체로 지정.
        - `onMouseEnter`: 마우스가 요소 위로 올라갈 때 실행될 이벤트 핸들러.
3. **`"Hello I'm a h3"`**
    - 세 번째 파라미터: `<h3>` 요소의 내용(텍스트 노드).

### **결과**

위 코드는 다음과 동일한 JSX로 표현될 수 있습니다:

```jsx
<h3 onMouseEnter={() => console.log('mouse enter')}>
  Hello I'm a h3
</h3>

```

React는 내부적으로 이 JSX를 `React.createElement`를 사용하여 처리합니다.’