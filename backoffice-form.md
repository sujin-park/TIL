## 복잡한 백오피스에서 Form의 상태 다루기
> FEConf Korea 에서 김성현님의 복잡한 백오피스에서 Form의 상태 다루기를 보고 정리한 내용입니다.


- React Context API만으로 Form 상태관리 하기
    - React Context Form State로 사용하면 생기는 문제
    - React Context를 조금 더 효율적으로 사용하는 방법
    - React Context + useImperativeHandle
- React Form Library
    - Formik
    - React Hook Form
- 결론


### React Context 로 Form 상태관리를 하려고 했던 이유

- Props drilling
    - Input 들을 포함하여 많은 요소들이 Form 을 하나로 이루고 있다.
    - Form 들을 Component 별로 쪼갤 때 Prop들을 넘겨주는 작업들을 반복적으로 하고 싶지 않았다.
    - 생산성이 굉장히 감소될 것이라고 생각하였다.
- 하나의 Store
    - Form 관련 값들을 모아 둘 수 있고 submit 하는 시점에 값들을 사용할 수 있는 하나의 Stor가 필요하다.
- 순수 React로 충분하다.
    - Redux, Mobx 등과 같은 상태관리 라이브러리를 사용할 수 있었겠지만 순수 React만으로 구현 가능하다고 생각했다.


### Context를 Global Store 로 사용하면 생기는 문제

App.jsx
```jsx

...
export default App() {
    const [formState, dispatch] = React.useReducer(reducer, {
        email: '',
        password: ''
    });

    return (
        <FormContext.Provider value={{ formState, dispatch }}>
            <EmailInput />
            <PasswordInput />
        </FormContext.Provider>
    )
}
```

```jsx
const EmailInput = () => {
    const { formState, dispatch } = useContext(FormContext);
    
    ...
};

const PasswordInput = () => {
    const { formState, dispatch } = useContext(FormContext);
    
    ...
};
```

위와 같이 Global Store 로 사용하게 되면 formState 가 커지면 커질 수록, useContext를 많이 쓰면 쓸 수록, 불필요한 re-render 는 계속 증가한다.


### React Context를 조금 더 효율적으로 사용하는 방법

실제 상태를 포함하고 있는 Context 와 dispatch Context 를 분리하여 관리한다.

독립적인 state를 가지고 업데이트를 debounce 한다.

```jsx
useDebounce(
    () => {
        dispatch({
            type: UPDATE_FORM_VALUE,
            payload: { key: 'email', value: internalValue }
        });
    },
    500,
    [internalValue]
);
```

꼭 필요한 경우에만 state 를 정의하고 관리한다.


```jsx
const handleSubmit = (e) => {
    e.preventDefault();

    const json = {
        email: emailRef.current.value,
        password: passwordRef.current.value ,
        ...formState
    }
};

return (
    <FormContext.Provider value={{ formState, dispatch }}>
        <form onSubmit={handleSubmit}>
            <EmailInput ref={emailRef}/>
            <PasswordInput ref={passwordef}/>
        </form>
    </FormContext.Provider>
)
```

### React Context + useImperativeHandle

각각의 컴포넌트들은 각자의 state 를 각자의 scope 에 가지고 있고, 해당 state를 나중에 가져다가 쓸 수 있는 방법은 없을까?

```useImperativeHandle``` hook을 많이 사용하게 되면 컴포넌트 간의 복잡도가 증가할 수 있으므로 꼭 필요할 때만 사용해야 한다.

```
class Formservice {
    constructor({ onSubmit }) {
        this.store = {};
    }

    createOrGetItemRef = (name) => {
        const newRef = React.createRef();
        _set(store, name, newRef);

        return newRef; 
    }
}
```