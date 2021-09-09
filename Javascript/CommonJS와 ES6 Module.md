### CommonJs와 ES6 Module

commonJs의 경우 Node.js에서 쓰는 모듈 시스템이다. ECMA 에 정식으로 모듈 기능이 없었던 시절부터 모듈시스템을 사용하기위해  Node.js에서 자체적으로 활용한 모듈 시스템이다.

현재 Node.js에서는 ES 모듈기능을 자체적으로 지원하고 있다. 또한 웹팩을 통해 간접적으로 Node.js에서 ES6 모듈 문법을 사용하기도 한다.

- CommonJS

  **commonJs**에서는 **module.exports**로 외부로 내보낼 변수나 함수를 정의하고 **require**로 내보낸 리소스를 가져와 쓸수 있다.

  ```javascript
  module.exports = {
  	name: name,
  	age: age
  }
  
  const a = require('./example.js')
  ```

  **module.exports**를 그냥 **exports**로 쓸수도 있다.

  ```javascript
  exports.man = {
  	name: name,
  	age: age
  } 
  ```

  보통 객체 하나만을 export하고 싶은 경우 **module.exports**를 쓰고 여러개의 객체를 따로 export하고 싶은경우 **exports** 를 쓴다.

  exports는 module.exports를 참조하는 변수이고 그렇기 때문에 exports에 다른 값을 할당해버리면 **더이상 모듈로 기능하지 않는다.**

![img](https://media.vlpt.us/images/leobit/post/12d2bb2d-7d89-4981-baf8-fff7b3250240/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7,%202020-10-02%2020-08-33.png)



- ES6 Module

  ES6의 Module기능은 기본적으로 export와 import를 사용하며 기본적으로 strict모드에서 동작한다.

  ```javascript
  export function sayHi(user) {
    alert(`Hello, ${user}!`);
  }
  
  import {sayHi} from './sayHi.js';
  
  alert(sayHi); // 함수
  sayHi('John'); // Hello, John!
  ```

  모듈은 각각의 독립된 자신만의 스코프가 있으며 이는 ES6 모듈도 마찬가지이다. 따라서 다른 모듈에서 해당 모듈의 변수를 사용하려면 import 를 해줘야한다.

  또한 동일한 모듈이 여러 곳에서 사용되더라도 모듈은 최초 호출 시 **단 한번만** 실행된다.

  실행 후 결과는 이 모듈를 가져가려는 모든 모듈에 내보내지게 된다.

  따라서 실행된 모듈은 필요한 곳에 공유되므로 어느 한 모듈에서 import된 외부 객체를 수정하면 

  그 객체를 사용하는 다른 모듈에서도 변경사항을 확인 할 수 있다.

  - export default

    es6 module에는 **export default** 라는 특별한 문법이있다. **export default**를 사용하면 '해당 모듈엔 객체가 하나만 있다.'라는 사실을 명확히 나타낼 수 있다.

    이렇게 default를 통해 내보니면 중괄호 `{}`없이 모듈을 import 할 수 있다.

    ```
    export default class User { // export 옆에 'default'를 추가해보았습니다.
      constructor(name) {
        this.name = name;
      }
    }
    import User from './user.js'; // {User}가 아닌 User로 클래스를 가져왔습니다.
    
    new User('John');
    ```

    

- type="module"이 붙은 스크립트의 특징

  기본적으로 브라우저환경에서 es6 module을 사용한 스크립트를 시행하기 위해선 type 속성으로 'module'을 줘야한다.

  이 렇게 module이 붙은 스크립트의 특징은

  1. 지연실행: 모듈스크립트는 지연 실행되며 다운로드할 때 브라우저의 HTML 처리가 멈추지 않으며, HTML 문서가 다 준비될때까지 대기상태에 있다가 완전히 만들어진 이후에 실행된다. (HTML보다 빨리 불러온 경우에도)

  2. 브라우저 환경에서 import는 상대 혹은 절대 URL 앞에 와야한다.

     Node.js나 번들링 환경에서는 경로가 없어도 해당 모듈을 찾을 수 있는 방법을 알기 때문에 경로가 없는 모듈을 사용할수 있지만 브라우저는 경로없는 모듈을 지원하지 않는다.



참고자료

https://ko.javascript.info/modules-intro 모던 자바스크립트 모듈 소개

https://www.daleseo.com/js-node-es-modules/ Node.js의 ES 모듈 지원

https://www.zerocho.com/category/NodeJS/post/5835b500373b5b0018a81a10 Node.js 모듈 시스템

https://velog.io/@leobit/CommonJS CommonJS
