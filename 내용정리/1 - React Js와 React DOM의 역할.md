# 1. React Js와 React DOM의 역할

주어진 두 스크립트는 React와 ReactDOM 라이브러리를 포함하여 React 애플리케이션을 브라우저 환경에서 실행할 수 있도록 설정하는 역할을 합니다. 각각의 역할은 다음과 같습니다:

### 1. **React 라이브러리**

```html
<script src="<https://unpkg.com/react@17.0.2/umd/react.production.min.js>"></script>

```

- **역할**:
    
    React의 핵심 기능을 제공합니다. React는 컴포넌트를 정의하고 상태(state) 및 속성(props)을 관리하는 데 사용됩니다. 이 스크립트는 React 요소(virtual DOM)를 생성하고, 애플리케이션의 논리와 UI 컴포넌트 구조를 정의하는 역할을 담당합니다.
    
- **주요 기능**:
    - React.createElement()로 가상 DOM 요소를 생성.
    - 상태 관리 및 라이프사이클 메서드 지원.
    - 컴포넌트 기반 구조 제공.

### 2. **ReactDOM 라이브러리**

```html
<script src="<https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js>"></script>

```

- **역할**:
    
    ReactDOM은 React 요소를 실제 DOM으로 렌더링(render)하는 역할을 합니다. 브라우저에서 React 애플리케이션을 실행 가능하게 만듭니다.
    
- **주요 기능**:
    - ReactDOM.render()로 React 요소를 HTML DOM에 렌더링.
    - React 요소와 실제 DOM 간의 변경 사항을 동기화.
    - React 애플리케이션과 HTML DOM 간의 상호작용을 가능하게 함.

### 요약

- **React**: 애플리케이션의 논리와 UI를 정의하는 **엔진** 역할.
- **ReactDOM**: React 애플리케이션을 브라우저의 HTML DOM에 연결해주는 **브릿지** 역할.

이 두 스크립트를 함께 사용하면 React 컴포넌트를 생성하고, 그것을 브라우저 화면에 렌더링할 수 있습니다.