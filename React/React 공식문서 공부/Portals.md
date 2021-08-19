## Portals

부모컴포넌트의 DOM 계층 구조 바깥에 있는 DOM 노드로 자식을 렌더링하고 싶을때 사용한다.

```javascript
render() {
  // React는 새로운 div를 생성하지 *않고* `domNode` 안에 자식을 렌더링합니다.
  // `domNode`는 DOM 노드라면 어떠한 것이든 유효하고, 그것은 DOM 내부의 어디에 있든지 상관없습니다.
  return ReactDOM.createPortal(
    this.props.children,
    domNode  );
}
```

전형적으로 사용되는 경우는 부모컴포넌트에 **overflow: hidden** 이나 **z-index** 가 있는경우 또는 시각적으로 '튀어나오도록' 보여야하는 경우(사이드바, 모달창)가 있다.

- Protal을 통한 이벤트 버블링

  portal이 DOM 트리의 어디든 존재할 수 있따 하더라도 일반적인 React 자식처럼 동작합니다.

  따라서 context와 같은기능도 기존과 같게 동작합니다. 

  DOM트리에서의 위치와 상관없이 여전히 React 트리에 존재하기 때문.

  그렇기 때문에 이벤트 버블링도 DOM트리에서는 자식이 아니라고 할지라도 React 트리에서 자식 컴포넌트라면 적용된다.