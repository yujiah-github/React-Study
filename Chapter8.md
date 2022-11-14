### Hooks
- 리액트 v16.8에서 새로 도입된 기능으로 함수 컴포넌트에서도 상태 관리를 할 수 있는 useState, 랜더링 이후 작업을 설정하는 useEffect 등의 기능을 제공한다.


### useState
- 가장 기본적인 Hooks 이며, 함수 컴포넌트에서도 가변적인 상태를 지닐 수 있게 해준다.

```javascript
import React, {useState} from 'react';

const [name, setName] = useState(''); //기본 값은 아무것도 없는 상태이므로 null로 설정한다.
const [nickname, setNickName] = useState(''); //기본 값은 아무것도 없는 상태이므로 null로 설정한다.

const onChangeName = (event) => {
    setName(event.target.value); //value의 현재 값을 이벤트로 받음
}

const onChangeNickname = (event) => {
    setName(event.target.value); //value의 현재 값을 이벤트로 받음
}

function Info(){
    return(
        <div>
            <div>
                <input
                    value={name}
                    onChange={onChangeName}
                />
                <input 
                    value={nickName}
                    onChange={onChangeNickname}
                />
            </div>
            <div>
                이름: {name}
            </div>
            <div>
                닉네임: {nickname}
            </div>
        </div>
    );
}
```

### useEffect
- 리액트 컴포넌트가 랜더링 될 때마다 특정 작업을 수행하도록 설정할 수 있는 Hook이다.


#### 마운트 될 때만 실행하고 싶을 때
```javascript
useEffect(() => {
    console.log('마운트 될 때만 실행됩니다.');
},[]);
```

#### 특정 값이 업데이트 될 때 사용하고 싶을 때
```javascript
useEffect(() => {
    console.log('name');
},[name]);
```

- 기본적으로 랜더링되고 난 직후마다 실행되며, 두 번째 파라미터 배열에 무엇을 넣는지에 따라 실행되는 조건이 달라진다.
- 컴포넌트가 언마운트 되기 전이나 업데이트 되기 직전에 어떠한 작업을 수행하고 싶다면 useEffect에서 **뒷정리 함수**를 반환해주어야 한다.

```javascript
useEffect(() => {
    console.log('effect');
    console.log(name);
    return() => {
        //effect 부분이 바뀌고 사라질 때 cleanup이 나타난다.
        console.log('cleanup');
        console.log(name);
    };
},[name] //name이 바뀔 때 마다 업데이트가 실행된다.
```

```javascript
import React, {useState} from 'react';

const [name, setName] = useState(''); //기본 값은 아무것도 없는 상태이므로 null로 설정한다.
const [nickname, setNickName] = useState(''); //기본 값은 아무것도 없는 상태이므로 null로 설정한다.
useEffect(() => {
    console.log('랜더링이 완료되었습니다.');
    console.log([
        name,
        nickname
    ]);
})

const onChangeName = (event) => {
    setName(event.target.value); //value의 현재 값을 이벤트로 받음
}

const onChangeNickname = (event) => {
    setName(event.target.value); //value의 현재 값을 이벤트로 받음
}

function Info(){
    return(
        <div>
            <div>
                <input
                    value={name}
                    onChange={onChangeName}
                />
                <input 
                    value={nickName}
                    onChange={onChangeNickname}
                />
            </div>
            <div>
                이름: {name}
            </div>
            <div>
                닉네임: {nickname}
            </div>
        </div>
    );
}

export default Info;
```

#### info 컴포넌트 가시성 바꾸기

```javascript
import React, {useState} from 'react';
import info from './info';

const [visible, setVisible] = useState(false);

const onClick = (event) => {
    setVisible(!visible);
}

useEffect(() => {
    console.log('effect'); //처음에 실행
    return() => {
        console.log('unmount'); //업데이트 되기 전에 실행
    };
},[visible]); //visible이 바뀔 때 마다 실행

function App(){
    return(
        <div>
            <button
                onClick={onClick}
            >
                {visible ? '숨기기' : '보이기' }
            </button>
            <hr />
            {visible && <Info />}
        </div>
    );
};

export default App;


```
