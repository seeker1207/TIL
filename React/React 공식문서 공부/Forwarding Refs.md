## Forwarding Refs
ref 전달은 부모컴포넌트가 자식중 하나에 ref를 전달하는 기법이다.

즉 Ref 전달하기는 일부 컴포넌트가 수신한 ref를 받아 조금 더 아래로 전달 할 수 있는 옵트인 기능입니다.

```javascript
const FancyButton = React.forwardRef((props, ref) => (  <button ref={ref} className="FancyButton">    {props.children}
  </button>
));

// 이제 DOM 버튼으로 ref를 작접 받을 수 있습니다.
const ref = React.createRef();
<FancyButton ref={ref}>Click me!</FancyButton>;
```

 `FancyButton`은 `React.forwardRef`를 사용하여 전달된 `ref`를 얻고, 그것을 렌더링 되는 DOM `button`으로 전달합니다.

자세한 

1. `React.createRef`를 호출해서 **React ref** 를 생성하고 `ref` 변수에 할당합니다.
2. `ref`를 JSX 속성으로 지정해서 `<FancyButton ref={ref}>`로 전달합니다.
3. React는 이 `ref`를 `forwardRef` 내부의 `(props, ref) => ...` 함수의 두 번째 인자로 전달합니다.
4. 이 `ref`를 JSX 속성으로 지정해서 `<button ref={ref}>`으로 전달합니다.
5. ref가 첨부되면 `ref.current`는 `<button>` DOM 노드를 가리키게 됩니다.

이와 같은 과정으로 부모컴포넌트에서 자식컴포넌트의 DOM 노드를 ref를 활용해 컨트롤할수 있습니다.

- 고차원 컴포넌트에서의 ref 전달

고차원 컴포넌트에서도 부분적으로 유용할수 있는데,

```javascript
function logProps(WrappedComponent) {  class LogProps extends React.Component {
    componentDidUpdate(prevProps) {
      console.log('old props:', prevProps);
      console.log('new props:', this.props);
    }

    render() {
      return <WrappedComponent {...this.props} />;    }
  }

  return LogProps;
}
```

이로한 로깅작업을 하는 래퍼 컴포넌트가 있다고 할시에 ref의 경우는 prop이 아니기때문에 `key`와 마찬가지로 React에서 다르게 처리한다.

따라서 ref를 추가하면 래핑된 컴포넌트가 아니라 가장 바깥족 컨테이너 컴포넌트를 참조하게 된다.

FancyButton 컴포넌트가 아니라 LogProps 컴포넌트에 첨부가 된다.

```javascript
import FancyButton from './FancyButton';

const ref = React.createRef();
// 가져온 FancyButton 컴포넌트는 LogProps HOC입니다.
// 렌더링된 결과가 동일하다고 하더라도,
// ref는 내부 FancyButton 컴포넌트 대신 LogProps를 가리킵니다!
// 이것은 우리가 예를 들어 ref.current.focus()를 호출할 수 없다는 것을 의미합니다.

<FancyButton
  label="Click Me"
  handleClick={handleClick}
  ref={ref}/>;
```

따라서 React.forwardRef 를 이용해 ref를 명시적으로 전달한다. 

```javascript
function logProps(Component) {
  class LogProps extends React.Component {
    componentDidUpdate(prevProps) {
      console.log('old props:', prevProps);
      console.log('new props:', this.props);
    }

    render() {
      const {forwardedRef, ...rest} = this.props;
      // 사용자 정의 prop "forwardedRef"를 ref로 할당합니다.
      return <Component ref={forwardedRef} {...rest} />;    }
  }

  // React.forwardRef에서 제공하는 두 번째 파라미터 "ref"에 주의하십시오.
  // 가령 "forwardedRef"같은 일반 prop으로 LogProps에 전달할 수 있습니다.
  // 그 다음 Component에 연결할 수 있습니다.
  return React.forwardRef((props, ref) => {    return <LogProps {...props} forwardedRef={ref} />;  });}
```



- DevTools에 사용자 정의 이름 표시하기

`React.forwardRef`가 받는 렌더링 합수는 DevTools에 'ForwardRef' 로 나타난다.

함수를 지정하면 ForwardRef(myFunction) 으로 나타난다.

렌더링 함수의 displayName 속성을 임의로 지정해 원하는 속성을 설정할 수 있다.

```javascript
function logProps(Component) {
  class LogProps extends React.Component {
    // ...
  }

  function forwardRef(props, ref) {
    return <LogProps {...props} forwardedRef={ref} />;
  }

  // DevTools에서 이 컴포넌트에 조금 더 유용한 표시 이름을 지정하세요.
  // 예, "ForwardRef(logProps(MyComponent))"
  const name = Component.displayName || Component.name;  forwardRef.displayName = `logProps(${name})`;
  return React.forwardRef(forwardRef);
}
```

