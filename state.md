# state 관리

> 이벤트를 통해 값을 변경하려면 제일 먼저 알아둬야 할 개념...

## ✅useState
### syntax
```javascript
const _mode = useState('Welcome');
const mode = _mode[0]    ---a
const setMode = _mode[1] ---b
// a + b 합치면
const [mode, setMode] = useState('Welcome');
```
* 컴포넌트 내에 있는 지역변수의 값의 변화를 기억하지 못함
* 컴포넌트는 한 번만 렌더링. 값의 변화에 따라 그 값으로 재렌더링을 할 필요가 있음
  
__즉, React의 useState 라는 Hook을 사용하여__  
__컴포넌트 내의 값의 변화를 인지하고 + 값의 변화를 반영한 상태로 재렌더링 되도록 함__  

[예시]  
```javascript
import {useState} from 'react';

export default function Calculation() {
  const [number, setNumber] = useState(1);

  function handleClick() {
    setNumber(number + 1);
  }

  return (
    <div id="exampleUseStateHook">
      <button onClick={handleClick}>Click</button>
      <p>{number}</p>
    </div>
  )
}
```
* number의 초기값을 1로 설정
* number에 1을 더하라는 setNumber 기능을 handleClick 이라는 함수로 정의
* onClick 시 handleClick이 실행되면 useState 훅이 사용되어 Calculation 컴포넌트가 재렌더링되면서  
  number의 초기값은 2가 되고 다시 setNumber 될 준비를 하게 됨
  
---
#### ‼️Hook 이란? __함수형 컴포넌트에 기능을 '건다'는 개념__  
__- 상태관리나 라이프사이클에 따른 작업 처리가 가능__  
__- 컴포넌트 안에서만 호출 가능하며, 항상 컴포넌트의 최상위에서 호출되어야함__
