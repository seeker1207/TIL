## Ref와  DOM

Ref는 DOM 노드와 React 엘리먼트에 접근하는 방법을 제공한다.

일반적으로 React에서는 props를 전달하여 부모컴포넌트가 자식을 수정하는데 이러한 일반적인 데이터플로우에서 벗어나 직접적으로 자식을 수정해야 할때 Ref를 사용한다.

> Ref를 남용하지는 말자.
>
> 되도록이면 Props로 자식 컴포넌트의 State를 컨트롤하는 방향으로 한다.

- Ref를 사용해야 할 때 
  - 포커스, 텍스트 선택영역, 미디어의 재생을 관리할 때.
  - 애니메이션을 직접적으로 실행시킬때.
  - 서드 파티 DOM 라이브러리를 React와 같이 사용할때

Ref는 **React.createRef()** 를 통해 생성 하고 ref 속성을 통해 React 엘리먼트에 부착시킨다.

```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.myRef = React.createRef();
  }
  render() {
    return <div ref={this.myRef} />;
  }
}
```



그럼으로서 컴포넌트 인스턴스 어느 곳에서도 Ref에 접근가능하게된다.

- Ref에 접근하려면 

  ```javascript
  const node = this.myRef.current;
  ```

  

ref가 엘리먼트에 전달 되었을때, 그 노드를 향한 참조는 ref의 **current** 속성에 담기게 된다.

- HTML 엘리먼트에 쓰엿다면, DOM 엘리먼트를  **current** 값으로 받는다.
- 커스텀 클래스 컴포넌트에 쓰였다면, 마운트된 컴포넌트의 인스턴스를 **current**값으로 받는다.
- **함수 컴포넌트** 는 인스턴스가 없기 때문에 **ref** 속성을 사용할 수 없다.
- **ref** 를 수정하는 작업은 **componentDidMount**, **componentDidUpdate** 생명주기 메서드가 호출되기 전에 이루어진다.

