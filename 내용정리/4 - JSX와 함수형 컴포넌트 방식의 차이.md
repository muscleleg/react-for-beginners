# JSX와 함수형 컴포넌트 방식의 차이

주어진 두 가지 방식:

1. JSX 방식:
    
    ```jsx
    const Title = (<h3 id='title' onMouseEnter={() => console.log('mouse enter')}>Hello I'm a title</h3>);
    const Button = (<button style={{backgroundColor: "tomato"}} onClick={() => console.log("I'm clicked")}>
        Click me
    </button>);
    const container = React.createElement("div", null, [Title, Button]);
    ReactDOM.render(container, root);
    
    ```
    
2. 함수형 컴포넌트 방식:
    
    ```jsx
    function Title() {
        return <h3 id='title' onMouseEnter={() => console.log('mouse enter')}>Hello I'm a title</h3>;
    }
    const Button = () => (
        <button style={{ backgroundColor: "tomato" }} onClick={() => console.log("I'm clicked")}>
            Click me
        </button>
    );
    const Container = () => (
        <div>
            <Title />
            <Button />
        </div>
    );
    ReactDOM.render(<Container />, root);
    
    ```
    

---

### **비교**

### 1. **작성 방식**

- **JSX 방식**:
    - JSX 요소를 직접 정의하고 `React.createElement`로 컴포넌트를 묶습니다.
    - 컴포넌트 재사용을 위한 구조가 아닌 단순한 UI 정의에 적합합니다.
    - 코드가 길어지거나 복잡한 컴포넌트를 다룰 때는 가독성이 떨어집니다.
- **함수형 컴포넌트 방식**:
    - 각각의 UI 요소를 함수형 컴포넌트로 작성해 구조화합니다.
    - 코드가 모듈화되어 재사용과 유지보수가 용이합니다.
    - 선언형 방식으로, React의 설계 철학과 잘 맞습니다.

### 2. **가독성**

- **JSX 방식**:
    
    ```jsx
    const container = React.createElement("div", null, [Title, Button]);
    
    ```
    
    - 여기서 `React.createElement`를 사용해야 하므로 복잡한 UI 구성에서는 읽기 어렵고 실수를 유발할 가능성이 높습니다.
- **함수형 컴포넌트 방식**:
    
    ```jsx
    const Container = () => (
        <div>
            <Title />
            <Button />
        </div>
    );
    
    ```
    
    - 컴포넌트를 계층적으로 표현하여 의도가 명확하고 가독성이 뛰어납니다.

### 3. **재사용성**

- **JSX 방식**:
    - `Title`과 `Button`은 단순히 변수로 정의되어 있으므로 재사용이 어렵습니다.
    - 만약 동일한 `Title`을 여러 곳에서 사용하려면 동일한 코드를 복사해야 합니다.
- **함수형 컴포넌트 방식**:
    - `Title`과 `Button`이 독립적인 함수형 컴포넌트로 작성되어 어디서든 쉽게 재사용할 수 있습니다.
    - 예:
        
        ```jsx
        <Title />
        <Title />
        
        ```
        

### 4. **유지보수성**

- **JSX 방식**:
    - 특정 요소를 수정하려면 전체 `React.createElement` 호출을 수정해야 하므로 번거로울 수 있습니다.
- **함수형 컴포넌트 방식**:
    - 각각의 컴포넌트를 독립적으로 관리하므로 수정 및 유지보수가 용이합니다.
    - 예: `Button` 컴포넌트의 스타일을 변경하려면 해당 컴포넌트만 수정하면 됩니다.

### 5. **React 철학**

- React는 **컴포넌트 기반 설계**를 중심으로 동작합니다.
- **JSX 방식**은 컴포넌트 기반 설계를 따르지 않으며, React의 설계 철학과는 거리가 있습니다.
- **함수형 컴포넌트 방식**은 컴포넌트를 중심으로 구성되어 React의 철학에 부합합니다.

---

### **결론**

- **JSX 방식**은 간단한 UI를 빠르게 정의하거나 일회성으로 사용할 경우 적합합니다.
- **함수형 컴포넌트 방식**은 구조화, 재사용성, 유지보수성 측면에서 훨씬 뛰어나며, React의 권장 방식입니다.

함수형 컴포넌트 방식이 더 **확장성**과 **일관성**을 제공합니다. React로 작성된 대부분의 프로젝트에서 함수형 컴포넌트를 사용하는 이유이기도 합니다.

---

# 함수형 컴포는트의 재사용 의미

주어진 두 코드 방식의 차이를 비교하겠습니다.

---

### 1. **첫 번째 방식**

```jsx
function Title() {
    return (<h3 id='title' onMouseEnter={() => console.log('mouse enter')}>Hello I'm a title</h3>);
};
const Button = () => (<button style={{backgroundColor: "tomato"}} onClick={() => console.log("I'm clicked")}>
    Click me</button>);
const Container = (
        <div>
            <Title/>
            <Button/>
        </div>
);
ReactDOM.render(Container, root);

```

- **`Container` 정의 방식**:
    - `Container`는 JSX 표현식을 통해 **React element**로 정의되어 있습니다.
    - JSX가 변수(`Container`)에 바로 저장된 형태로, React 컴포넌트가 아닌 단순 React element입니다.
    - `ReactDOM.render`에서 `Container`는 컴포넌트가 아니라 그대로 렌더링됩니다.
- **특징**:
    - `Container`를 컴포넌트로 재사용할 수 없습니다.
    
    [“재사용할 수 없다”의 의미](https://www.notion.so/145c691e5a2b80978904efb5ef0e763e?pvs=21)
    
    - 컴포넌트가 아니라 단순한 JSX 표현식이므로, 상태 관리나 React hooks 등을 사용할 수 없습니다.

---

### 2. **두 번째 방식**

```jsx
function Title() {
    return (<h3 id='title' onMouseEnter={() => console.log('mouse enter')}>Hello I'm a title</h3>);
};
const Button = () => (<button style={{backgroundColor: "tomato"}} onClick={() => console.log("I'm clicked")}>
    Click me</button>);
const Container = () => (
        <div>
            <Title/>
            <Button/>
        </div>
);
ReactDOM.render(<Container/>, root);

```

- **`Container` 정의 방식**:
    - `Container`는 **함수형 컴포넌트**로 정의되어 있습니다.
    - React에서 함수형 컴포넌트는 JSX를 반환하는 함수입니다.
    - `ReactDOM.render`에서 `<Container/>` 형태로 호출되어야 렌더링됩니다.
- **특징**:
    - `Container`는 **재사용 가능한 컴포넌트**로 동작합니다.
    - 상태 관리 (`useState` 등)나 React lifecycle (`useEffect` 등)을 사용할 수 있습니다.
    - 컴포넌트 계층 구조를 설계하거나 동적으로 렌더링할 때 적합합니다.

---

### **차이점 요약**

| **특징** | **첫 번째 방식** | **두 번째 방식** |
| --- | --- | --- |
| **`Container` 정의 방식** | JSX 표현식 (React element) | 함수형 컴포넌트 |
| **호출 방식** | `ReactDOM.render(Container, root)` | `ReactDOM.render(<Container/>, root)` |
| **재사용성** | 재사용 불가 | 재사용 가능 |
| **React 기능 사용 가능 여부** | 상태 관리 (`useState`), lifecycle 불가 | 상태 관리, lifecycle 가능 |
| **용도** | 단순한 UI를 렌더링할 때 | 복잡하거나 동적인 UI를 설계할 때 |

---

### **결론**

- 첫 번째 방식은 간단한 React element로, 컴포넌트 계층 구조를 설계하지 않아도 되는 **단순한 UI**에 적합합니다.
- 두 번째 방식은 **재사용성**과 **확장성**이 뛰어나며, React의 기능을 활용할 수 있는 **권장 방식**입니다.