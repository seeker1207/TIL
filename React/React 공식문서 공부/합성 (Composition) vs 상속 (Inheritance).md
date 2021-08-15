## 합성 (Composition) vs 상속 (Inheritance)

> React는 상속대신 합성을 사용한다!!



어떤 컴포넌트들은 어떤 자식 엘리먼트들이 들어올지 미리 예상할 수 없는 경우가 있다.

일반적인 '박스' 컨테이너 역할을 하는 컴포넌트들.. 

React에서는 이러한 '박스' 역할을 하는 컴포넌트들을 만들어 재사용할 수 있다. 

이때 상속대신 합성을 이용한다.

```javascript
function FancyBorder(props) {
  return (
    <div className={'FancyBorder FancyBorder-' + props.color}>
      {props.children}    </div>
  );
}
```

```javascript
function WelcomeDialog() {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">        
      	Welcome      
      </h1>      
      <p className="Dialog-message">        
      	Thank you for visiting our spacecraft!      
      </p>    
   </FancyBorder>
  );
}
```

이러한 방식으로 children prop을 사용하여 자식 엘리먼트를 그대로 전달한다.

Fancyborder 를 상속하여 재사용하는 방법을 생각할수도 있지만 React에서는 합성으로, 다시말해 prop의 속성전달로 그것을 해결할수 있다.



> Facebook에서는 수천 개의 React 컴포넌트를 사용하지만, 컴포넌트를 상속 계층 구조로 작성을 권장할만한 사례를 아직 찾지 못했습니다.

