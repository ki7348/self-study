# React - 리액트 이벤트 핸들링

## 설명

### 이벤트란?

- 사용자가 웹 브라우저에서 DOM 요소들과 상호 작용하는 것
- 버튼에 마우스 커서를 올렸을 때 onmouseover 이벤트를 실행하거나, 클릭하면 onClick 이벤트를 실행해줄 때

### 이벤트 작성시 주의 사항

- 이벤트 이름은 camelCase로 작성
  - HTML의 onclick은 리액트에서 onClick으로 작성해야 합니다.

```js
<button onclick="activateButton()">클릭하세요</button> // HTML
<button onClick={activateButton}>클릭하세요</button> // React
```

- 이벤트에 실행할 함수 형태의 값을 전달
  - 자바스크립트 코드를 전달하지 않고 함수 형태의 값을 전달해야 합니다.
  - 화살표 함수 문법으로 작성하거나 렌더링 부분 외부에 미리 만들어서 작성해야 합니다.
- DOM 요소에만 이벤트를 설정
  - div, button, input 등의 DOM요소에는 이벤트 설정을 할 수 있지만, 직접 만든 컴포넌트에는 이벤트를 자체적으로 설정할 수 업습니다.
  - props를 전달해주는 것에 불과합니다.
- DOM 요소의 기본 동작을 방지하기 위해서는 preventDefault를 명시적으로 호출해야 합니다.
  - HTML에서는 기본 동작을 방지하기 위해 false를 반환합니다.
