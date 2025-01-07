# Component Props

> 처음 컴포넌트 작업한 뒤, 지속적으로 prop이 추가될 때 변경관리가 용이하도록 하려면 어떤 방법이 좋을지에 대한 고민 끝에 정리하게 된 내용...

## ✅Props 사용법
### 구조 분해 할당
```javascript
function Avatar({ name, imageId }) {
  return (
    <img
      src={`https://example.com/${imageId}.jpg`}
      alg={name}
    />
  );
}
```
### props 객체
```javascript
function Avatar({props}) {
  return (
    <img
      src={`https://example.com/${props.imageId}.jpg`}
      alg={props.name}
    />
  );
}
```
* 가독성을 향상 : 구조 분해 할당 👍  
* 안전·유지보수 : 구조 분해 할당 👍  
* 특정조건에 따라 다르게 적용할 때 : props 객체 👍
---
## ✅Props 확장
### ...rest
```javascript
function Card({ title, desc, ...rest }) {
  const { isBg } = rest;
  const cardStyle = isBg ? { backgroundColor: 'lightblue' } : {};
  return (
    <div style={cardStyle} {...rest}>
      <h1>{title}</h1>
      <p>{desc}</p>
    </div>
  );
}
```
### PropType
```javascript
import PropTypes from 'prop-types';

function Card({ title, desc, isBorder = false }) {
  return (
    <div style={{border ? isBorder ? '1px solid red' : 'none'}}>
      <h1>{title}</h1>
      <p>{desc}</p>
    </div>
  );
}

Card.propTypes = {
  title: PropTypes.string.isRequired,
  desc: PropTypes.string.isRequired,
  isBorder: PropTypes.boolean,
};

//예시
<Card title="Hello" desc="This is description" isBorder={true} />
<Card title="No Border" desc="This is description" />
```
* props가 지속적으로 추가/변경될 가능성이 있다면, ...rest 혹은 PropType 을 적절히 활용할 수 있음  
* rest 에서 특정 prop을 분리하여 사용할 수 있음  
* prop을 es6 문법으로 디폴트 값을 지정해주면, 조건문과 함께 사용하여 쓸 수 있으며,  
  해당 prop이 없을 때에도 컴포넌트가 정상적으로 동작할 수 있도록 보장할 수 있음
