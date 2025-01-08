# state 관리

> useState 제대로 활용하기...

## setState 의 콜백
```javascript
setState((preState) => {
  return newState
});
```
* setState의 인자값이 이전값과 관련되어 있다면, 새로운 초기값으로 콜백함수 로직을 추가

[예시]
```javascript
function App() {
  const [names, setNames] = useState( ['영희', '철수'] ); //초기값을 배열로 설정
  const [input, setInput] = useState("");

  const handleInput = (e) => {
    setInput(e.target.value);
  }
  const handleUpdate = () => {
    setNames((prevState) => { //setState의 인자에는 초기 배열에 값이 추가된 배열이 되어야하므로 콜백함수 사용
      return [input, ...prevState];
    });
  }

  return (
    <div>
      <input type="text" value={input} onChange={handleInput} />
      <button onClick={handleUpdate}>update</button>
      <p>{names}</p>
    </div>
  )
}
```

## useState 의 콜백
```javascript
useState(() => {
  return heavyWorks(); //heavyWorks는 컴포넌트 밖에서 정의
});
```
* useState로 초기값을 받아올 때 무거운 작업이 필요하면, 인자로 콜백함수를 사용
* setState로 state가 변경되더라도 그 때마다 초기값(=preState)을 불러오는 로직이 매번 실행되지 않도록 방지할 수 있음  
  즉, 컴포넌트 내에서 변경이 발생되는 부분만 Reflow, Repainting (Re-rendering) 되어 렌더 횟수와 범위를 최소화하여 성능 개선에 도움이 될 수 있음

[예시]
```javascript
//초기값을 구하는 함수 (무거운 작업이 동반됨)
const heavyWorks = () => {
  return ['영희', '철수'];
}

function App() {
  const [names, setNames] = useState( heavyWorks() ); //초기값 인자로 함수를 콜백
  const [input, setInput] = useState("");

  const handleInput = (e) => {
    setInput(e.target.value);
  }
  const handleUpdate = () => {
    setNames((prevState) => {
      return [input, ...prevState];
    });
  }

  return (
    <div>
      <input type="text" value={input} onChange={handleInput} />
      <button onClick={handleUpdate}>update</button>
      <p>{names}</p>
    </div>
  )
}
```
