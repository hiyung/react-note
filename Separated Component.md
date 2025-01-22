# Separated Component (분리형 컴포넌트)

> Single Component 와 달리 grouping이 필요한 컴포넌트은 제어가 좀 더 까다로움...
> Composable 하게, Headless Component 구현을 위해서 부모 컴포넌트가 자식 컴포넌트를 어떻게 제어하는지...

## ✅데이터의 단방향 흐름
> ↔ vue 에서는 양방향 바인딩이(v-model, emit) 가능하다는 면에서 다름
```javascript
import { useState } from 'react';

//Parent
export default function RadioGroup({
  children, //하위에 올 child 컴포넌트들을 의미
  selectedValue,
  onChange,
  ...props
}) {
  const handleRadio = (newValue) => { //자식의 변화를 부모에게 알릴 수 있는 중개 함수
    onChange(newValue);
  }
  
  return (
    {React.Children.map(() => { //children이 단일 일 수도 있고 배열일 수도 있으므로 map 사용
      if (React.isValidElement(child)) {
        //child의 props을 직접 제어 못하므로 상태 관리를 중앙에서 관리 가능하도록
        //cloneElement로 복제본을 만든 후 제어할 prop을 전달하고 기존의 child의 props과 병합시켜
        //새로 탄생한 복제본을 반환하는 것
        return React.cloneElement(child, {
          checked: child.props.value === selectedValue, //자식에게 줄 prop (부모가 관리)
          onChange: () => handleRadio(child.props.value), //자식에게 줄 prop (부모가 관리)
        });
      }
    })}
  )
}

//Child
export default function Radio({
  value,
  label,
  disabeld,
  checked, //부모가 전달한 prop
  onChagne //부모가 전달한 prop
}) {
  return (
    <label>
      <input value={value} disabled={disabled} checked={checked} onChange={onChange} />
      <span>{label}</span>
    </label>
  )
}

//data
const options = [ //임시 데이터
  {value: 'option1', label: 'option1', disabled: false},
  {value: 'option2', label: 'option2', disabled: false},
  {value: 'option3', label: 'option3', disabled: true},
];

//use
const [selectedOption, setSelectedOption] = useState('option1');
<RadioGroup
  name=""
  selectedValue={selectedOption}
  onChange={handleRadioOnChange} //최종 UI를 업데이트하는 함수
>
  {options.map((option) => (
    <Radio
      key={option.value}
      value={option.value}
      label={option.label}
      disabled={option.disabled}
    />
  ))}
</RadioGroup>
```

#### ‼️총 정리!
__- 부모 컴포넌트는 자식 컴포넌트의 prop을 직접 제어할 수 없어 복제본을 사용(cloneElement)__  
__- 자식의 상태 변화를 부모가 중앙에서 제어하기 위해 onChagne를통해 변경된 값을 전달하는 중개 함수가 필요__  
__- 부모 자기 자신에게 직접 전달된 onChagne와 자식에게 변화를 받아오기 위한 onChange 구별 필요__  
__- Radio, Checkbox, Select 등에서 잘 쓰일 예정__
