```html
<html>
    <script type="text/babel">

        function App() {
            const [index, setIndex] = React.useState("xx")
            const onSelect = (event) => {
                setIndex(event.target.value)
            }
            console.log("render w/",index)
            return (
                    <div>
                        <h1>Super Converter</h1>
                        <select value={index} onChange={onSelect}>
                            <option value="xx">Select your units</option>
                            <option value="0">Minutes & Hours</option>
                            <option value="1">Km & Miles</option>
                        </select>
                        <hr/>
                        {index === "xx" ? "Please select your units" : null}
                        {index === "0" ? <MinutesToHours/> : null}
                        {index === "1" ? <KmToMiles/> : null}
                    </div>
            );
        }
        
        const root = document.getElementById("root");
        ReactDOM.render(
                <App/>
                , root);
    </script>
</html>
```
```javascript
            console.log("render w/",index)
```
`console.log("render w/", index)`가 변환될 때마다 실행되는 이유는, React의 상태(`index`)가 변경될 때마다 컴포넌트가 리렌더링 되기 때문입니다.

React에서 상태가 변경되면, 해당 상태를 사용하는 컴포넌트는 자동으로 리렌더링됩니다. 이 과정에서 `render`가 다시 실행되고, 그 안에 있는 코드가 다시 실행됩니다. 따라서 `console.log("render w/", index)`도 상태가 바뀔 때마다 실행되는 것입니다.

여기서 `setIndex(event.target.value)`가 호출되어 상태(`index`)를 변경하고, 이 변경에 따라 컴포넌트가 리렌더링되면서 `console.log`가 다시 실행되는 것입니다. 

리렌더링의 흐름:
1. 사용자가 `<select>` 요소에서 선택을 바꾸면 `onSelect` 핸들러가 호출되어 상태를 변경 (`setIndex`)합니다.
2. 상태가 변경되면, React는 해당 컴포넌트를 리렌더링합니다.
3. 리렌더링이 발생하면, 컴포넌트 내의 모든 코드가 다시 실행되고, 그 중 `console.log`도 실행됩니다.

이러한 방식은 React에서 정상적인 동작이며, 상태가 변경될 때마다 UI를 업데이트할 수 있도록 합니다.