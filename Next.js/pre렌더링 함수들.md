## pre 렌더링하는 방식에는 3가지 방식이 있다.

### SSR (Server-side Rendering)
- getServerSideProps 함수를 통해 페이지를 요청할때마다 반환된 props로 미리 렌더링 하는 방식이다.
- 서버측에서 미리 렌더링하여 클라이언트에게 보내준다.

### SSG (Static-site generation)
- getStaticProps 함수를 이용해 next.js를 빌드 할때 페이지를 미리 HTML로 출력하여 렌더링하는 방식이다.
- 정적 HTML을 생성하기 때문에 미리 생성된 HTML이 다시 사용되며, 쿼리 매개변수같은 요청에 응답할수 없다.

### CSR (Client-side Rendering)
- 클라이언트 측에서 렌더링 하는 방식이다. 주로 useEffect를 이용해 렌더링한다.
- Next.js 에서는 SWR 리액트훅 라이브러리로 데이터를 가져오는 것을 추천한다.

## next.js의 프리렌더링 함수들
- getServerSideProps() : 프론트 서버에서 미리 초기의 페이지를 렌더링해 서브한다. (SSR 방식)
- getStaticProps() : getStaticPaths() 와 같이 사용해야하며 staticPath에서 미리 선언된 값들로 페이지를 미리 생성하여 미리 만들어진 HTML을 서브하는 방식.

## 다이나믹 라우팅
- 기본적으로 pages/[변수이름].js 형식으로 다이나믹 라우팅이 가능하다.
- 위에서 언급된 getStaticPaths에 미리 선언된 값들이 변수이름에 선언된 변수로 들어가서 HTML을 생성한다.
