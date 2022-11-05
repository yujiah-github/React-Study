### 컴포넌트 생성
```javascript
import Component from './Component';
//모듈 불러오기

const MyComponent =() => {
    return <div>나의 새롭고 멋진 컴포넌트</div>
}

export default MyComponent;
//모듈 내보내기
```

### props
- **properties** 를 줄인 표현으로 컴포넌트 속성을 설정할 때 사용하는 요소
- props 값을 지정할 때, 부모 컴포넌트에서 자식 컴포넌트로 이동한다.
- props의 기본 값을 설정할 때는 defaultProps를 사용한다.


```javascript
const MyComponent = props => {
    return <div>안녕하세요, 제 이름은 {props.name}입니다.</div>;
};

MyComponent.defaultProps = {
    name: '기본 이름'
};

export default MyComponent;
```

### 비구조화 할당 문법을 통해 props 내부 값 추출하기

```javascript
const MyComponent = ({name, children}) => {
    //객체에서 값을 추출하는 문법을 비구조화 할당이라고 한다.
    return(
        <div>
        안녕하세요, 제 이름은 {name}입니다. <br />
        children 값은 {children}
        입니다.
        </div>
    )
}

MyComponent.defaultProps = {
    name: '기본 이름'
}

export default MyComponent
```

### propTypes를 통한 props 검증

```javascript
import PropTypes from 'prop-types';

const MyComponent = ({name, children}) => {
    return (...);
}

MyComponent.defaultProps = {
    name: '기본 이름'
};

export default MyComponent
```

### isRequired를 사용하여 필수 propTypes 설정

```javascript
import PropTypes from 'prop-types';

const MyComponent = ({name, favoriteNumber, children}) => {
    return(
        <div>
        안녕하세요, 제 이름은 {name}입니다. <br />
        children 값은 {children}
        입니다.
        <br />
        제가 좋아하는 숫자는 {favoriteNumber} 입니다.
        </div>
    );
}

MyComponent.defaultProps = {
    name: '기본 이름'
};

MyComponent.propTypes = {
    name: PropTypes.string,
    favoriteNumber: PropTypes.number.isRequired
};

export default MyComponent
```

### useState 사용하기

```javascript
import React, {useState} from 'react';

const Say = () => {
    const [message, setMessage] = useState('');
    const onClickEnter = () => setMessage('안녕하세요!');
    const onClickLeave = () => setMessage('안녕히 가세요!');

    return(
        <div>
            <button onClck={onClickEnter}>입장</button>
            <button onClck={onClickLeave}>퇴장</button>
            <h1>{message}</h1>
        </div>
    );
}

export default Say;
```

- useState 함수의 인자에는 상태의 초깃값을 넣어준다.
- useState의 값의 형태는 숫자, 문자열, 객체, 배열 등 다양하다.

### 한 컴포넌트에서 useState 여러 번 사용하기

```javascript
import React, {useState} from 'react';

const Say = () => {
    const [message, setMessage] = useState('');
    const onClickEnter = () => setMessage('안녕하세요!');
    const onClickLeave = () => setMessage('안녕히 가세요!');

    const [color, setColor] = useState('black');

    return(
        <div>
            <button onClick={onClickEnter}>입장</button>
            <button onClick={onClickLeave}>퇴장</button>
            <h1 style={{color}}>{message}</h1>
            <button style={{color: 'red'}} onClick={() => setColor('red')}>
            빨간색
            </button>
        </div>
    );
}


export default Say;
```
