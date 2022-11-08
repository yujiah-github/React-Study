### 자바스크립트 배열의 map() 함수
- 자바스크립트 배열 객체의 내장 함수인 Map 함수를 사용하여 반복되는 컴포넌트를 렌더링 할 수 있다.
- arr.map(callback, [thisArg])의 형태로 사용한다.

### map 함수 이용하여 컴포넌트 만들기

```javascript
//map 함수 이용 전
import React from 'react';

const IterationSample = () => {
    return(
        <ul>
            <li>눈사람</li>
            <li>얼음</li>
            <li>눈</li>
            <li>바람</li>
        </ul>
    );
};

export default IterationSample;

//map 함수 이용 후

const IterationSample = () => {
    const names = ['눈사람', '얼음', '눈', '바람'];
    const nameList = names.map(name => <li>{name}</li>)
    return(
        <ul>
            <li>{nameList}</li>
        </ul>
    );
};

export default IterationSample;
```

### key 설정
- 리액트에서 key는 컴포넌트 배열을 렌더링 했을 때 어떤 원소에 변동이 있었는지 알아내려고 사용한다.
- Key 값이 있다면 변동을 쉽게 감지할 수 있다.
- Key 값은 언제나 고유해야한다.

```javascript
const IterationSample = () => {
    const names = ['눈사람', '얼음', '눈', '바람'];
    const nameList = names.map((name, index) => <li key={index}>{name}</li>);
    return <ul>{nameList}</ul>;
}

export default IterationSample;
```

### map 응용
- 위에서 다룬 내용들을 토대로 동적인 배열을 렌더링 하는 것을 구현해봄.

```javascript
//초기 상태 설정
import React, {useState} from 'react';

const IterationSample = () => {
    const [names, setNames] = useState([
        {id: 1, text: '눈사람'},
        {id: 2, text: '얼음'},
        {id: 3, text: '눈'},
        {id: 4, text: '바람'},
    ]);

    const [inputText, setInputText] = useState('');
    const [nextId, setNextId] = useState(5); //새로운 항목을 추가할 때 사용할 id

    const namesList = names.map(name => <li key={name.id}>{name.text}</li>);
    return <ul>{nameList}</ul>
}

export default IterationSample;


//데이터 추가 기능
import React, {useState} from 'react';

const IterationSample = () => {
    const [names, setNames] = useState([
        {id: 1, text: '눈사람'},
        {id: 2, text: '얼음'},
        {id: 3, text: '눈'},
        {id: 4, text: '바람'},
    ]);

    const [inputText, setInputText] = useState('');
    const [nextId, setNextId] = useState(5); //새로운 항목을 추가할 때 사용할 id

    const namesList = names.map(name => <li key={name.id}>{name.text}</li>);
    const onChange = (event) =>{
        setInputText(event.target.value);
    }
    return (
        <input value={inputText} onChange={onChange}/>
        <button>추가</button>
        <ul>{nameList}</ul>
    );
}

export default IterationSample;
```
