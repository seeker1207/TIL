# React의 리스트와 Key 

> 2021.08.16 	00:54



Javascript의 리스트처럼 React의 엘리먼트도 배열로 반들어 결과를 저장할수 있다.

```javascript
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li>{number}</li>
);
```



- 하지만 이 경우 리스트의 각 항목에 key를 넣어야 한다는 경고가 표시되는데 각 엘리먼트들을 고유하게 식별할수 있는 문자열을 사용한다. 대부분의 경우 데이터의 ID를 사용.

> 이때, 각 엘리먼트의 ID를 인덱스로 사용하는 것은 안티패턴.
>
> 리액트는 각 컴포넌트의 인스턴스를 key 기반으로 갱신되고 재사용되는데, 
>
> 배열이 재배열 될때 (정렬을 한다거나 등등..) 순서가 바뀌었을때 key또한 바뀌므로 컴포넌트의 state가 엉망이 되고 의도하지 않는 방식으로 작동할 수 있다.
>
> 또한 Math.random 과도 같은 변하는 key를 사용하면 인스턴스가 렌더링될때마다 과도하게 재생성 되어 성능이 나빠지거나 자식컴포넌트의 state가 유실될 수 있기 때문에 이또한 사용헤선 안된다.

- key를 사용하면 최적화에도 좋다.

  ```html
  <ul>
    <li>Duke</li>
    <li>Villanova</li>
  </ul>
  
  <ul>
    <li>Connecticut</li>
    <li>Duke</li>
    <li>Villanova</li>
  </ul>
  ```

리스트의 끝에 추가하는건 상관없지만 맨 앞에 추가를 할때에는 key를 사용하지 않으면 ul의 모든 자식 element들이 렌더링 된다.

- key는 배열이 있는 context에서만 의미가 있다.

  ```javascript
  function ListItem(props) {
    const value = props.value;
    return (
      // 틀렸습니다! 여기에는 key를 지정할 필요가 없습니다.    
      <li key={value.toString()}>      {value}
      </li>
    );
  }
  function NumberList(props) {
    const numbers = props.numbers;
    const listItems = numbers.map((number) =>
      // 맞습니다! 배열 안에 key를 지정해야 합니다.
      <ListItem key={number.toString()} value={number} />
    );
    return (
      <ul>
        {listItems}
      </ul>
    );
  }
  ```

  

- Key는 형제 사이에서만 고유한 값이면 된다.

전역에서 고유할 필요는 없으며, 따라서 두가지의 다른 배열을 만들 때 동일한 key를 사용해도 무방.

