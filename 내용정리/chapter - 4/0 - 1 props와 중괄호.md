React에서 `{text}`를 바로 사용할 수 있는 이유는 **ES6의 객체 구조 분해 할당** 덕분입니다. 이를 이해하기 위해 아래에서 자세히 설명하겠습니다.

---

### **1. 객체 구조 분해 할당이란?**
**구조 분해 할당**은 객체의 속성을 변수로 쉽게 추출하는 ES6(ECMAScript 2015) 문법입니다. React에서 props는 **객체 형태**로 전달되므로 구조 분해 할당을 사용하여 특정 속성만 추출할 수 있습니다.

#### **일반적인 props 사용 방식:**
```jsx
function Btn(props) {
    return <button>{props.text}</button>;
}
```
- 여기서 `props`는 `Btn` 컴포넌트에 전달된 **모든 props가 포함된 객체**입니다.
- `props.text`를 사용하여 `text` 속성에 접근합니다.

---

### **2. 구조 분해 할당으로 간소화:**
React에서는 함수의 매개변수에서 구조 분해 할당을 바로 적용할 수 있습니다. 이를 통해 특정 props를 간단히 추출할 수 있습니다.

#### **구조 분해 할당 적용:**
```jsx
function Btn({ text }) {
    return <button>{text}</button>;
}
```
- `{ text }`는 `props.text`를 간소화한 형태입니다.
- 컴포넌트에 전달된 props 객체에서 `text` 속성만 추출해 **변수처럼 사용할 수 있도록** 만듭니다.

#### **구조 분해의 동작 원리:**
다음 코드는 React가 내부적으로 처리하는 방식과 유사합니다:
```javascript
const props = { text: "Save Changes", color: "red" };
// 구조 분해 할당
const { text } = props;
// 이제 text는 "Save Changes"라는 값을 가집니다.
```

---

### **3. props.text 대신 {text}를 사용하는 이유**
`{text}`를 사용하는 이유는 **간결하고 명료하기 때문**입니다:
1. **간결성**: `props.text` 대신 `text`만 사용하므로 코드가 더 짧아지고 읽기 쉬워집니다.
2. **명확성**: 필요한 props만 추출해 명확히 사용할 수 있습니다.
3. **중복 제거**: 컴포넌트 내에서 반복적으로 `props.`를 작성하지 않아도 됩니다.

---

### **4. 비교: props.text vs {text}**
| 방식          | 설명                                                                 | 코드 예시                              |
|---------------|----------------------------------------------------------------------|---------------------------------------|
| `props.text`  | props 객체에서 직접 속성에 접근                                      | `function Btn(props) { return <button>{props.text}</button>; }` |
| `{text}`      | 구조 분해 할당으로 props에서 필요한 속성만 추출하여 사용              | `function Btn({ text }) { return <button>{text}</button>; }` |

---

### **5. 더 복잡한 props 예제**
구조 분해 할당은 단일 속성뿐만 아니라, 여러 속성을 동시에 추출하거나 기본값을 설정할 때도 유용합니다.

#### **여러 props 구조 분해:**
```jsx
function Btn({ text, color }) {
    return <button style={{ backgroundColor: color }}>{text}</button>;
}
```

#### **기본값 설정:**
```jsx
function Btn({ text = "Click me", color = "blue" }) {
    return <button style={{ backgroundColor: color }}>{text}</button>;
}
```

---

### **6. 결론**
React에서 `props.text` 대신 `{text}`를 사용하는 이유는 **구조 분해 할당**을 통해 props 객체에서 필요한 속성만 추출하기 때문입니다. 이는 코드의 가독성을 높이고, 불필요한 중복을 제거하며, 명확한 코드를 작성하는 데 도움을 줍니다. 

이 문법 덕분에 React 코드가 더욱 간결하고 직관적이게 됩니다!

---
# 구조분해 할당을 일반 js에서도 사용 가능함
네! React가 아닌 **일반 JavaScript**에서도 **구조 분해 할당**은 사용할 수 있습니다. React에서 구조 분해 할당이 사용되는 이유도 사실 ES6(JavaScript의 ECMAScript 2015 표준)의 기본 기능 덕분입니다.

---

### **1. 일반 JavaScript에서 구조 분해 할당**

#### **객체의 구조 분해 할당**
JavaScript에서 객체를 사용할 때 특정 속성만 추출하려면 구조 분해 할당을 사용할 수 있습니다.

```javascript
const props = { text: "Hello", color: "blue", size: "large" };

// 구조 분해 할당
const { text, color } = props;

console.log(text);  // "Hello"
console.log(color); // "blue"
```
- `props.text` 대신 `text`로 바로 접근할 수 있습니다.
- `props.color`도 `color`로 바로 접근 가능합니다.

---

### **2. 함수에서 구조 분해 할당 사용**

React와 유사하게 **함수의 매개변수**에서도 구조 분해 할당을 사용할 수 있습니다.

#### **일반적인 방식:**
```javascript
function logProps(props) {
    console.log(props.text);
    console.log(props.color);
}

logProps({ text: "Hello", color: "blue" });
```

#### **구조 분해 할당 적용:**
```javascript
function logProps({ text, color }) {
    console.log(text);
    console.log(color);
}

logProps({ text: "Hello", color: "blue" });
```
- 함수 매개변수에서 `{ text, color }`로 구조 분해를 사용하면 `props.text`, `props.color`처럼 객체를 반복적으로 참조하지 않아도 됩니다.

---

### **3. 배열의 구조 분해 할당**
구조 분해 할당은 배열에도 사용할 수 있습니다.

#### **배열에서 값 추출:**
```javascript
const array = [1, 2, 3];

// 구조 분해 할당
const [first, second] = array;

console.log(first);  // 1
console.log(second); // 2
```

#### **React의 useState와 유사한 예:**
React의 `useState`에서 반환된 배열을 구조 분해 할당으로 사용하는 방식도 일반 JavaScript에서 가능합니다.

```javascript
function useState(initialValue) {
    return [initialValue, () => console.log("State updated!")];
}

const [value, setValue] = useState(10);

console.log(value);  // 10
setValue();          // "State updated!"
```

---

### **4. 기본값 설정**
구조 분해 할당은 기본값을 설정할 수도 있습니다. 이 기능은 React 컴포넌트에서도 유용하게 쓰