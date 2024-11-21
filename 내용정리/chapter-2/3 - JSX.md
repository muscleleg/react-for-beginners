# JSX

[중괄호 2개의 의미](https://www.notion.so/2-144c691e5a2b800aba77d35181e7fd16?pvs=21)

## JSX

```jsx
const Button = <button style={{backgroundColor: "tomato"}} onClick={() => console.log("I'm clicked")}>Click Me</button>;
```

### **React에서 JSX 변환**

React는 JSX를 **`React.createElement` 함수**로 변환합니다. 수정된 JSX 코드는 다음과 같이 변환됩니다:

```jsx
const Button = React.createElement(
  "button",
  {
    style: { backgroundColor: "tomato" },
    onClick: () => console.log("I'm clicked")
  },
  "Click Me"
);
```

→ JSX를 React.createElement로 변환해주는 것이 Babel

```bash
<!DOCTYPE html>
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
    <!--JSX를 사용하려면 일종의 번역과정이 필요함, JSX를 번역해주는 라이브러리    -->
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <script type="text/babel">
        const root = document.getElementById("root");
        const Title = (<h3 id='title' onMouseEnter={() => console.log('mouse enter')}>Hello I'm a title</h3>);
        const Button = <button style={{backgroundColor: "tomato"}} onClick={() => console.log("I'm clicked")}
        >
            Click me</button>
        const container = React.createElement("div", null, [Title, Button])
        ReactDOM.render(container, root);
    </script>
</html>
```

![https://babeljs.io/](https://prod-files-secure.s3.us-west-2.amazonaws.com/a6577081-5e09-4130-a73f-8bfe38fd58d3/54fc7bdd-78b2-445b-b2e8-ae3909dbbf10/image.png)

https://babeljs.io/