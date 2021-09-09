## Source Map이란? 

보통 자바스크립트가 machine-generated 되는 경우가 있다. 

- 보다 효율적으로 서버로부터 스크립트파일을 전송받기 위해 코드를 압축하는 경우.
- CoffeeScript, TypeScript를 쓰는경우 혹은 Babel로 인해 변환되는 경우.

이 경우에 브라우저에서 에러가 났을시 코드가 변환된 상태이기 때문에 디버깅하기가 어렵다.

이를 쉽게하기 위해서 변환된 코드와 원본 소스코드 사이를 맵핑시켜놓는 파일을 하나 생성 해놓고 변환된 코드가 에러가나면 그 부분에 맵핑된 원본 소스코드를 찾아내어 디버깅하기 쉽게 만든다.



### Source Map의 스펙

Source Map의 스펙은 

https://docs.google.com/document/d/1U1RGAehQwRypUTovF1KRlpiOFze0b-_2gc6fAH0KY0k/edit

구글독스에 있는데 따로 공인된 단체에서 스펙을 만드는건 아닌것으로 보이고 Google의 `Joseph Schorr`란 사람이 만든것으로 되어있다.

```javascript
{
  version : 3,
  file: “out.js”,
  sourceRoot : "",
  sources: ["foo.js", "bar.js"],
  sourcesContent: [null, null],
  names: ["src", "maps", "are", "fun"],
  mappings: "AA,AB;;ABCDE;"
}
```

- version은 양수로 소스맵의 버전을 의미하고 항상 제일먼저 나와야 한다.
- file은 변환된 파일명이다.
- sourceRoot는 옵션값으로 소스 파일을 가져올 경로의 루트를 재조정하는데 사용한다.
- sources는 mappings에서 사용할 원본 소스 파일명의 배열이다.
- sourceContent은 옵션값으로 소스의 내용을 답고 있어야 하면 sources의 파일명으로 파일을 가져오지 못했을 때 사용하는 용도이다. null로 지정하면 반드시 소스피알이 필요하다.
- names는 mappings에서 사용할 심볼 이름이다.
- mappings는 인코딩된 매핑 데이터의 문자열이다.

