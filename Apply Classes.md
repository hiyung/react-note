# Class(html props)

> 클래스로 컴포넌트의 스타일을 제어하는데, 다수의 클래스를 조합하여 스타일을 적용할 필요가 있어서... 방법론을 선택적으로 사용하자

## ✅classNames 라이브러리 사용
```
npm install classnames  or  yarn add classnames
```
```javascript
import classNames from "classnames";

export default function Button({ text, type, style }) {
  const className = classNames('button', type, style);

  return <button className={className}> {text} </button>
}

Button.defaultProps = { //기본값 지정
  type: "",
  stylle: "",
}
```

## ✅파라미터에 기본값을 빈 문자열로 처리
```javascript
export default function Button({ text, type = "", style = "" }) {
  return <button className={`button ${type} ${style}`.trim()}> {text} </button> //trim으로 공백 남지 않도록
}
```

## ✅inline 조건부 렌더링
```javascript
export default function Button({ text, type, style }) {
  return <button className={`button ${type ? type : ""} ${style ? style : ""}`.trim()}> {text} <button> //내부에 조건연산 추가
}
```

## ✅Dynamic Props Object 사용
```javascript
export default function Button(props) {
  const classes = { //!!연산자는 boolean으로 값을 반환 ex: !!undefined || !!null -> false
    button: true,
    [props.type]: !!props.type,
    [props.style]: !!props.style,
  };

  const className = Object.keys(classes).filter((key) => classes[key].join(" ");

  return <button className={className}> {props.text} </button>
}
```

----
#### ‼️총 정리!
__- 가장 간결한 코드? classnames 라이브러리__  
__- 조건 경우의 수가 적으면? inline 조건부 렌더링__  
__- 유연성과 undefined, null 확실히 분리? Dynamic Object (단, 코드가 좀 길다ㅎㅎ)__
