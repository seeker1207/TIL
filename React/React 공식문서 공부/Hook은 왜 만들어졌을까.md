## Hook은 왜 만들어졌을까?

- 컴포넌트 사이에서 상태 로직을 재사용하기가 어렵다.

  이전에는 render props나 고차 컴포넌트와 같은 패턴을 통해 이러한 문제를 해결했지만 이런 패턴을 사용하면 컴포넌트를 재구성해야하고 코드의 추적을 어렵게 만든다.

  따라서  Hook을 사용해 상태관련 로직을 추상화하고 독립적인 테스트와 재사용이 가능하게 만든다.

- 복잡한 컴포넌트들은 이해하기 어렵다.

  생명주기 메서드에 자주 관련없는 로직이 섞여 들어간다.

  ```javascript
    componentDidMount() {
      document.title = `You clicked ${this.state.count} times`;
      ChatAPI.subscribeToFriendStatus(
        this.props.friend.id,
        this.handleStatusChange
      );
    }
  
    componentDidUpdate() {
      document.title = `You clicked ${this.state.count} times`;
    }
  
    componentWillUnmount() {
      ChatAPI.unsubscribeFromFriendStatus(
        this.props.friend.id,
        this.handleStatusChange
      );
    }
  ```

  관련없는 로직들이 단일 메서드로 결합하기 떄문에 버그가 쉽게 발성하고 무결성을 너무나 쉽게 해친다.

  따라서 Hook을 통해 서로 비슷한 것을 하는 작은 함수의 묶음으로 컴포넌트를 나누는 방법을 사용할수 있다.

- Class는 사람과 기계를 혼동시킨다.

  JavaScript의 **this** 키워드는 다른언어에서와는 다르게 작동하기 때문에 사용자에게 큰 혼란을 주고 코드의 재상용성과 구성을 매우 어렵게 만든다.

따라서 이러한 문제를 해결하기 위해 Hook은 Class 없이 React 기능들을 사용하는 방법을 제시한다.