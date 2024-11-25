`React.memo`는 React에서 **컴포넌트의 리렌더링을 최적화**하기 위해 사용하는 고차 컴포넌트(Higher Order Component)입니다. 특정 조건에서 컴포넌트가 불필요하게 다시 렌더링되는 것을 방지합니다. 

### 역할
`React.memo`는 컴포넌트를 **메모이제이션**(memoization)하여, **props**가 변경되지 않는 한 컴포넌트를 다시 렌더링하지 않습니다.  
이로 인해, 동일한 props를 가진 컴포넌트가 리렌더링되는 것을 방지하고, 성능을 개선합니다.

---

### 코드에서 `React.memo`의 동작
```jsx
const MemorizedBtn = React.memo(Btn);
```
위 코드에서 `React.memo`는 `Btn` 컴포넌트를 감싸고, props가 변경되지 않는 한 `MemorizedBtn` 컴포넌트를 다시 렌더링하지 않습니다.

#### `Btn` 컴포넌트 내부의 `console.log`
```jsx
console.log(text + " was rendered");
```
- **첫 번째 렌더링**:
  - `MemorizedBtn`이 각각 `{text: "Save Changes"}`와 `{text: "Continue"}`라는 props로 렌더링됩니다.
  - 이때, 두 버튼 모두 렌더링되고 콘솔에 `"Save Changes was rendered"`와 `"Continue was rendered"`가 출력됩니다.

- **`changeValue` 함수 실행 후**:
  - 첫 번째 `MemorizedBtn`의 `text`가 `"Revert Changes"`로 변경되므로, 첫 번째 버튼만 다시 렌더링됩니다.
  - 두 번째 `MemorizedBtn`의 `text`는 변경되지 않았기 때문에, 두 번째 버튼은 다시 렌더링되지 않습니다.

---

### 동작 방식
1. `React.memo`는 기본적으로 **shallow comparison**을 통해 props를 비교합니다.
   - 같은 객체나 기본 자료형이면 렌더링을 건너뜁니다.
2. props가 변경되지 않았다면, 컴포넌트를 리렌더링하지 않고 이전 결과를 재사용합니다.

---

### 이점을 활용해야 할 경우
- **부모 컴포넌트의 상태가 변경될 때** 자식 컴포넌트가 불필요하게 리렌더링되는 것을 방지하고 싶을 때.
- **props가 자주 변경되지 않는** 컴포넌트에서 성능 최적화를 하고 싶을 때.

---

### 추가로 사용할 수 있는 기능: `React.memo`의 두 번째 인수
`React.memo`는 비교 로직을 커스터마이즈할 수 있도록 두 번째 인수로 **props 비교 함수**를 받을 수 있습니다.
```jsx
const MemorizedBtn = React.memo(Btn, (prevProps, nextProps) => {
  return prevProps.text === nextProps.text;
});
```
이 함수는 `true`를 반환하면 리렌더링을 건너뛰고, `false`를 반환하면 리렌더링합니다.

---

### 요약
- **`React.memo`는 props가 변경되지 않으면 컴포넌트를 재사용하여 성능을 최적화**합니다.
- 이 기능은 컴포넌트가 큰 경우, 또는 부모 컴포넌트가 자주 리렌더링되는 경우에 특히 유용합니다.

### 언제 React.memo를 사용하는 것이 적절한가?
React.memo는 모든 컴포넌트에 무조건 사용하는 것이 아니라, 다음과 같은 경우에만 사용하는 것이 효과적입니다.

컴포넌트가 정적이고 렌더링 비용이 높은 경우

예: 복잡한 계산, 많은 DOM 업데이트가 포함된 컴포넌트.
정적인 데이터(props)가 자주 변경되지 않는 경우 유용합니다.
부모 컴포넌트의 리렌더링이 자식 컴포넌트에 불필요한 영향을 주는 경우

부모의 상태나 props 변경이 자식 컴포넌트까지 전파되지 않도록 하고 싶을 때.
컴포넌트의 렌더링 횟수를 제한해야 하는 경우

대규모 리스트에서 개별 아이템 컴포넌트를 최적화할 때 React.memo가 효과적입니다.
### React.memo 사용을 피해야 하는 경우
Props가 자주 변경되는 컴포넌트
props가 자주 변경되면, React.memo로 인해 props 비교 비용만 추가되고 성능은 오히려 나빠집니다.

렌더링 비용이 낮은 단순한 컴포넌트 렌더링 비용이 적은 컴포넌트에 React.memo를 사용하는 것은 불필요한 비교 작업을 추가하는 것과 같습니다.

useState나 useReducer로 관리되는 내부 상태가 많은 컴포넌트 내부 상태 업데이트가 많으면 React.memo는 큰 효과가 없습니다.

### 결론
과도한 React.memo 사용은 피해야 합니다. React.memo는 비교 비용이 렌더링 비용보다 클 때 오히려 성능을 저하시킬 수 있습니다.
프로파일링 도구를 사용하여 컴포넌트 리렌더링의 병목현상을 먼저 파악한 후, 필요한 경우에만 React.memo를 적용하세요.
React.memo는 props가 자주 변하지 않는 정적 컴포넌트에서만 성능 최적화 도구로 사용하는 것이 가장 효과적입니다.